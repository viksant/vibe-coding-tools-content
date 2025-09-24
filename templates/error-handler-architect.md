---
title: "Error Handler Architect"
description: "Build comprehensive error handling systems with logging and monitoring"
category: "template-prompt"
tags: ["error-handling", "logging", "monitoring", "debugging", "resilience"]
tech_stack: ["any"]
---

# Error Handler Architect

You are an expert at building robust error handling systems with comprehensive logging and monitoring.

## Error Handling Requirements
- **Application Type**: [INSERT TYPE - web app, API, microservice, CLI]
- **Technology Stack**: [INSERT TECH STACK]
- **Error Types**: [INSERT TYPES - validation, network, business logic, system]
- **Logging Level**: [INSERT LEVEL - debug, info, warn, error, fatal]
- **Monitoring**: [INSERT TOOLS - Sentry, DataDog, New Relic, custom]
- **User Experience**: [INSERT UX - graceful degradation, error pages, retry logic]

## Error Context
[INSERT SPECIFIC ERROR SCENARIOS AND REQUIREMENTS]

## Output Format

### Error Handling System

```[INSERT LANGUAGE]
// ErrorHandler.js - Central error handling system

class ErrorHandler {
  constructor(config = {}) {
    this.environment = config.environment || 'development';
    this.logger = config.logger || console;
    this.monitoring = config.monitoring;
    this.errorTypes = new Map();
    
    this.setupErrorTypes();
    this.setupGlobalHandlers();
  }

  setupErrorTypes() {
    // Define error type configurations
    this.errorTypes.set('ValidationError', {
      statusCode: 400,
      level: 'warn',
      userMessage: 'Please check your input and try again',
      shouldLog: true,
      shouldNotify: false
    });

    this.errorTypes.set('AuthenticationError', {
      statusCode: 401,
      level: 'warn',
      userMessage: 'Authentication required',
      shouldLog: true,
      shouldNotify: false
    });

    this.errorTypes.set('AuthorizationError', {
      statusCode: 403,
      level: 'warn',
      userMessage: 'Access denied',
      shouldLog: true,
      shouldNotify: false
    });

    this.errorTypes.set('NotFoundError', {
      statusCode: 404,
      level: 'info',
      userMessage: 'Resource not found',
      shouldLog: false,
      shouldNotify: false
    });

    this.errorTypes.set('BusinessLogicError', {
      statusCode: 422,
      level: 'warn',
      userMessage: 'Operation cannot be completed',
      shouldLog: true,
      shouldNotify: false
    });

    this.errorTypes.set('ExternalServiceError', {
      statusCode: 502,
      level: 'error',
      userMessage: 'Service temporarily unavailable',
      shouldLog: true,
      shouldNotify: true
    });

    this.errorTypes.set('DatabaseError', {
      statusCode: 500,
      level: 'error',
      userMessage: 'Internal server error',
      shouldLog: true,
      shouldNotify: true
    });

    this.errorTypes.set('SystemError', {
      statusCode: 500,
      level: 'fatal',
      userMessage: 'System error occurred',
      shouldLog: true,
      shouldNotify: true
    });
  }

  setupGlobalHandlers() {
    // Handle unhandled promise rejections
    process.on('unhandledRejection', (reason, promise) => {
      this.handleUnhandledRejection(reason, promise);
    });

    // Handle uncaught exceptions
    process.on('uncaughtException', (error) => {
      this.handleUncaughtException(error);
    });
  }

  // Main error handling method
  async handleError(error, context = {}) {
    try {
      const errorInfo = this.analyzeError(error);
      const enrichedContext = this.enrichContext(context, errorInfo);
      
      // Log error if configured
      if (errorInfo.config.shouldLog) {
        await this.logError(error, enrichedContext, errorInfo.config.level);
      }

      // Send to monitoring if configured
      if (errorInfo.config.shouldNotify && this.monitoring) {
        await this.notifyMonitoring(error, enrichedContext);
      }

      // Return formatted error response
      return this.formatErrorResponse(error, errorInfo);

    } catch (handlingError) {
      // Error in error handling - log and return basic error
      console.error('Error in error handling:', handlingError);
      return this.getBasicErrorResponse();
    }
  }

  analyzeError(error) {
    const errorType = error.constructor.name;
    const config = this.errorTypes.get(errorType) || this.errorTypes.get('SystemError');
    
    return {
      type: errorType,
      message: error.message,
      stack: error.stack,
      config: config,
      isOperational: error.isOperational || false
    };
  }

  enrichContext(context, errorInfo) {
    return {
      ...context,
      timestamp: new Date().toISOString(),
      environment: this.environment,
      errorType: errorInfo.type,
      requestId: context.requestId || this.generateRequestId(),
      userId: context.userId,
      sessionId: context.sessionId,
      userAgent: context.userAgent,
      ipAddress: context.ipAddress,
      endpoint: context.endpoint,
      method: context.method,
      parameters: context.parameters
    };
  }

  async logError(error, context, level) {
    const logEntry = {
      level: level,
      message: error.message,
      error: {
        name: error.name,
        message: error.message,
        stack: error.stack,
        code: error.code
      },
      context: context
    };

    // Structured logging
    this.logger[level](logEntry);

    // Additional logging to external services
    if (this.environment === 'production') {
      await this.sendToExternalLogger(logEntry);
    }
  }

  async notifyMonitoring(error, context) {
    if (!this.monitoring) return;

    try {
      await this.monitoring.captureException(error, {
        tags: {
          environment: this.environment,
          errorType: error.constructor.name
        },
        extra: context,
        user: {
          id: context.userId,
          ip_address: context.ipAddress
        }
      });
    } catch (monitoringError) {
      this.logger.error('Failed to send error to monitoring:', monitoringError);
    }
  }

  formatErrorResponse(error, errorInfo) {
    const response = {
      success: false,
      error: {
        type: errorInfo.type,
        message: this.environment === 'production' 
          ? errorInfo.config.userMessage 
          : error.message,
        code: error.code,
        timestamp: new Date().toISOString()
      }
    };

    // Add stack trace in non-production environments
    if (this.environment !== 'production') {
      response.error.stack = error.stack;
    }

    // Add HTTP status code for web responses
    if (errorInfo.config.statusCode) {
      response.statusCode = errorInfo.config.statusCode;
    }

    return response;
  }

  // Specific error handlers
  handleUnhandledRejection(reason, promise) {
    const error = new Error(`Unhandled Promise Rejection: ${reason}`);
    error.isOperational = false;
    
    this.handleError(error, {
      type: 'unhandledRejection',
      promise: promise
    });

    // In production, might want to gracefully shutdown
    if (this.environment === 'production') {
      this.gracefulShutdown();
    }
  }

  handleUncaughtException(error) {
    error.isOperational = false;
    
    this.handleError(error, {
      type: 'uncaughtException'
    });

    // Always exit on uncaught exception
    process.exit(1);
  }

  gracefulShutdown() {
    console.log('Received fatal error. Graceful shutdown...');
    
    // Close server connections
    // Close database connections
    // Finish processing current requests
    
    setTimeout(() => {
      process.exit(1);
    }, 5000);
  }

  generateRequestId() {
    return Math.random().toString(36).substring(2, 15);
  }

  getBasicErrorResponse() {
    return {
      success: false,
      error: {
        type: 'SystemError',
        message: 'An error occurred',
        timestamp: new Date().toISOString()
      },
      statusCode: 500
    };
  }
}

// Custom Error Classes
class ValidationError extends Error {
  constructor(message, field = null) {
    super(message);
    this.name = 'ValidationError';
    this.field = field;
    this.isOperational = true;
  }
}

class AuthenticationError extends Error {
  constructor(message = 'Authentication required') {
    super(message);
    this.name = 'AuthenticationError';
    this.isOperational = true;
  }
}

class AuthorizationError extends Error {
  constructor(message = 'Access denied') {
    super(message);
    this.name = 'AuthorizationError';
    this.isOperational = true;
  }
}

class BusinessLogicError extends Error {
  constructor(message, code = null) {
    super(message);
    this.name = 'BusinessLogicError';
    this.code = code;
    this.isOperational = true;
  }
}

class ExternalServiceError extends Error {
  constructor(message, service = null, originalError = null) {
    super(message);
    this.name = 'ExternalServiceError';
    this.service = service;
    this.originalError = originalError;
    this.isOperational = true;
  }
}

export { 
  ErrorHandler, 
  ValidationError, 
  AuthenticationError, 
  AuthorizationError, 
  BusinessLogicError, 
  ExternalServiceError 
};
```

### Express.js Middleware

```javascript
// errorMiddleware.js
import { ErrorHandler } from './ErrorHandler.js';

const errorHandler = new ErrorHandler({
  environment: process.env.NODE_ENV,
  monitoring: sentry // or other monitoring service
});

export const errorMiddleware = (error, req, res, next) => {
  const context = {
    requestId: req.id,
    userId: req.user?.id,
    sessionId: req.sessionID,
    userAgent: req.get('User-Agent'),
    ipAddress: req.ip,
    endpoint: req.originalUrl,
    method: req.method,
    parameters: { ...req.params, ...req.query, body: req.body }
  };

  errorHandler.handleError(error, context)
    .then(errorResponse => {
      res.status(errorResponse.statusCode || 500).json(errorResponse);
    })
    .catch(handlingError => {
      console.error('Error in error middleware:', handlingError);
      res.status(500).json({
        success: false,
        error: {
          message: 'Internal server error',
          type: 'SystemError'
        }
      });
    });
};

// Async error handler wrapper
export const asyncHandler = (fn) => {
  return (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
};
```

### Retry Logic

```javascript
// RetryHandler.js
class RetryHandler {
  constructor(config = {}) {
    this.maxAttempts = config.maxAttempts || 3;
    this.initialDelay = config.initialDelay || 1000;
    this.maxDelay = config.maxDelay || 10000;
    this.backoffFactor = config.backoffFactor || 2;
  }

  async executeWithRetry(operation, context = {}) {
    let lastError;
    
    for (let attempt = 1; attempt <= this.maxAttempts; attempt++) {
      try {
        return await operation();
      } catch (error) {
        lastError = error;
        
        if (!this.shouldRetry(error, attempt)) {
          throw error;
        }

        const delay = this.calculateDelay(attempt);
        console.log(`Attempt ${attempt} failed, retrying in ${delay}ms:`, error.message);
        
        await this.sleep(delay);
      }
    }

    throw lastError;
  }

  shouldRetry(error, attempt) {
    // Don't retry if max attempts reached
    if (attempt >= this.maxAttempts) return false;
    
    // Don't retry client errors (4xx)
    if (error.statusCode >= 400 && error.statusCode < 500) return false;
    
    // Don't retry business logic errors
    if (error instanceof BusinessLogicError) return false;
    
    // Retry network errors, timeouts, and server errors
    return true;
  }

  calculateDelay(attempt) {
    const delay = this.initialDelay * Math.pow(this.backoffFactor, attempt - 1);
    return Math.min(delay, this.maxDelay);
  }

  sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
}

export default RetryHandler;
```

### Circuit Breaker

```javascript
// CircuitBreaker.js
class CircuitBreaker {
  constructor(config = {}) {
    this.failureThreshold = config.failureThreshold || 5;
    this.recoveryTimeout = config.recoveryTimeout || 60000;
    this.state = 'CLOSED'; // CLOSED, OPEN, HALF_OPEN
    this.failureCount = 0;
    this.lastFailureTime = null;
    this.successCount = 0;
  }

  async execute(operation) {
    if (this.state === 'OPEN') {
      if (this.shouldAttemptReset()) {
        this.state = 'HALF_OPEN';
        this.successCount = 0;
      } else {
        throw new Error('Circuit breaker is OPEN');
      }
    }

    try {
      const result = await operation();
      this.onSuccess();
      return result;
    } catch (error) {
      this.onFailure();
      throw error;
    }
  }

  onSuccess() {
    this.failureCount = 0;
    
    if (this.state === 'HALF_OPEN') {
      this.successCount++;
      if (this.successCount >= this.failureThreshold) {
        this.state = 'CLOSED';
      }
    }
  }

  onFailure() {
    this.failureCount++;
    this.lastFailureTime = Date.now();
    
    if (this.failureCount >= this.failureThreshold) {
      this.state = 'OPEN';
    }
  }

  shouldAttemptReset() {
    return Date.now() - this.lastFailureTime >= this.recoveryTimeout;
  }
}

export default CircuitBreaker;
```

### Usage Examples

```javascript
// Usage in application
import { ErrorHandler, ValidationError } from './ErrorHandler.js';
import RetryHandler from './RetryHandler.js';

const errorHandler = new ErrorHandler();
const retryHandler = new RetryHandler();

// Business logic with error handling
async function processUserData(userData) {
  try {
    // Validation
    if (!userData.email) {
      throw new ValidationError('Email is required', 'email');
    }

    // External service call with retry
    const result = await retryHandler.executeWithRetry(async () => {
      return await externalAPI.processUser(userData);
    });

    return result;

  } catch (error) {
    const errorResponse = await errorHandler.handleError(error, {
      operation: 'processUserData',
      userData: userData
    });
    
    throw errorResponse;
  }
}
```

## Success Criteria
- All error types properly categorized
- Comprehensive logging implemented
- Monitoring integration working
- Graceful error recovery
- User-friendly error messages