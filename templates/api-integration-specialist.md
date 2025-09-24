---
title: "API Integration Specialist"
description: "Integrate third-party APIs with proper error handling and authentication"
category: "template-prompt"
tags: ["api-integration", "third-party", "authentication", "error-handling", "http-client"]
tech_stack: ["any"]
---

# API Integration Specialist

You're skilled at linking third-party APIs with solid error handling and security measures.

## Integration Requirements
- **API Provider**: [INSERT API PROVIDER - Stripe, Twilio, AWS, etc.]
- **API Type**: [INSERT TYPE - REST, GraphQL, SOAP, WebSocket]
- **Programming Language**: [INSERT LANGUAGE]
- **Authentication**: [INSERT AUTH - API Key, OAuth, JWT, Basic Auth]
- **Use Case**: [INSERT PURPOSE - payments, notifications, data sync]
- **Rate Limits**: [INSERT LIMITS - requests per minute/hour]

## API Documentation
[INSERT API ENDPOINT DETAILS, PARAMETERS, AND RESPONSES]

## Output Format

### Client Implementation

```[INSERT LANGUAGE]
// [APIName]Client.js
import axios from 'axios'; // or fetch, or other HTTP client

class [APIName]Client {
  constructor(config) {
    this.baseURL = config.baseURL || '[API_BASE_URL]';
    this.apiKey = config.apiKey;
    this.timeout = config.timeout || 10000;
    this.retryAttempts = config.retryAttempts || 3;
    
    // Create HTTP client instance
    this.client = axios.create({
      baseURL: this.baseURL,
      timeout: this.timeout,
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${this.apiKey}`,
        'User-Agent': '[YOUR_APP_NAME]/1.0'
      }
    });

    // Request interceptor
    this.client.interceptors.request.use(
      (config) => this.handleRequest(config),
      (error) => this.handleRequestError(error)
    );

    // Response interceptor
    this.client.interceptors.response.use(
      (response) => this.handleResponse(response),
      (error) => this.handleResponseError(error)
    );
  }

  // Main API methods
  async [primaryMethod]([parameters]) {
    try {
      const response = await this.client.post('/[endpoint]', {
        [requestPayload]
      });

      return this.formatResponse(response.data);
    } catch (error) {
      throw this.handleAPIError(error);
    }
  }

  async [secondaryMethod]([parameters]) {
    try {
      const response = await this.client.get(`/[endpoint]/${[id]}`);
      return this.formatResponse(response.data);
    } catch (error) {
      throw this.handleAPIError(error);
    }
  }

  // Error handling
  handleAPIError(error) {
    if (error.response) {
      const { status, data } = error.response;

      switch (status) {
        case 400:
          return new APIValidationError(data.message, data);
        case 401:
          return new APIAuthenticationError('Invalid API credentials');
        case 403:
          return new APIAuthorizationError('Insufficient permissions');
        case 429:
          return new APIRateLimitError('Rate limit exceeded', error.response.headers['retry-after']);
        case 500:
          return new APIServerError('Internal server error');
        default:
          return new APIError(`API request failed with status ${status}`, data);
      }
    } else if (error.request) {
      return new APINetworkError('Network error - no response received');
    } else {
      return new APIError('Request configuration error', error.message);
    }
  }

  // Rate limiting with retry logic
  async makeRequestWithRetry(requestFunction, retries = this.retryAttempts) {
    try {
      return await requestFunction();
    } catch (error) {
      if (error instanceof APIRateLimitError && retries > 0) {
        const delay = error.retryAfter * 1000 || 1000;
        await this.sleep(delay);
        return this.makeRequestWithRetry(requestFunction, retries - 1);
      }
      throw error;
    }
  }

  // Utility methods
  sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }

  formatResponse(data) {
    return {
      success: true,
      data: data,
      timestamp: new Date().toISOString()
    };
  }

  handleRequest(config) {
    console.log(`[API Request] ${config.method.toUpperCase()} ${config.url}`);
    return config;
  }

  handleResponse(response) {
    console.log(`[API Response] ${response.status} ${response.config.url}`);
    return response;
  }
}

// Custom error classes
class APIError extends Error {
  constructor(message, details = null) {
    super(message);
    this.name = 'APIError';
    this.details = details;
  }
}

class APIValidationError extends APIError {
  constructor(message, validationErrors) {
    super(message);
    this.name = 'APIValidationError';
    this.validationErrors = validationErrors;
  }
}

class APIAuthenticationError extends APIError {
  constructor(message) {
    super(message);
    this.name = 'APIAuthenticationError';
  }
}

class APIRateLimitError extends APIError {
  constructor(message, retryAfter) {
    super(message);
    this.name = 'APIRateLimitError';
    this.retryAfter = retryAfter;
  }
}

class APINetworkError extends APIError {
  constructor(message) {
    super(message);
    this.name = 'APINetworkError';
  }
}

export default [APIName]Client;
```

### Configuration

```[INSERT LANGUAGE]
// config/[apiName].js
export const [API_NAME]_CONFIG = {
  baseURL: process.env.[API_NAME]_BASE_URL || '[DEFAULT_URL]',
  apiKey: process.env.[API_NAME]_API_KEY,
  timeout: 10000,
  retryAttempts: 3,
  rateLimitPerMinute: [RATE_LIMIT],
  
  development: {
    debug: true,
    logRequests: true
  },
  
  production: {
    debug: false,
    logRequests: false
  }
};
```

### Service Layer

```[INSERT LANGUAGE]
// services/[APIName]Service.js
import [APIName]Client from '../clients/[APIName]Client';
import { [API_NAME]_CONFIG } from '../config/[apiName]';

class [APIName]Service {
  constructor() {
    this.client = new [APIName]Client([API_NAME]_CONFIG);
  }

  async [businessMethod]([businessParameters]) {
    try {
      const apiParams = this.transformToAPIFormat([businessParameters]);
      const result = await this.client.[primaryMethod](apiParams);
      
      return this.transformFromAPIFormat(result);
      
    } catch (error) {
      this.logError(error, '[businessMethod]', [businessParameters]);
      throw new Error(`Failed to [business operation]: ${error.message}`);
    }
  }

  transformToAPIFormat(businessData) {
    return {
      [apiField]: businessData.[businessField],
      // ... other transformations
    };
  }

  transformFromAPIFormat(apiData) {
    return {
      [businessField]: apiData.[apiField],
      // ... other transformations
    };
  }

  logError(error, method, parameters) {
    console.error(`[${[APIName]Service.name}] Error in ${method}:`, {
      error: error.message,
      parameters,
      timestamp: new Date().toISOString()
    });
  }
}

export default [APIName]Service;
```

### Tests

```[INSERT LANGUAGE]
// tests/[APIName]Client.test.js
import [APIName]Client from '../clients/[APIName]Client';
import axios from 'axios';

jest.mock('axios');
const mockedAxios = axios as jest.Mocked<typeof axios>;

describe('[APIName]Client', () => {
  let client;

  beforeEach(() => {
    client = new [APIName]Client({
      apiKey: 'test-api-key',
      baseURL: 'https://api.test.com'
    });
    
    jest.clearAllMocks();
  });

  test('should successfully make API request', async () => {
    const mockResponse = {
      data: { [responseField]: '[responseValue]' },
      status: 200
    };
    
    mockedAxios.create.mockReturnValue({
      post: jest.fn().mockResolvedValue(mockResponse),
      interceptors: {
        request: { use: jest.fn() },
        response: { use: jest.fn() }
      }
    });

    const result = await client.[primaryMethod]([testParameters]);
    
    expect(result.success).toBe(true);
    expect(result.data).toEqual(mockResponse.data);
  });

  test('should handle API errors correctly', async () => {
    const mockError = {
      response: {
        status: 400,
        data: { message: 'Validation error' }
      }
    };
    
    mockedAxios.create.mockReturnValue({
      post: jest.fn().mockRejectedValue(mockError),
      interceptors: {
        request: { use: jest.fn() },
        response: { use: jest.fn() }
      }
    });

    await expect(client.[primaryMethod]([testParameters]))
      .rejects
      .toThrow('Validation error');
  });

  test('should retry on rate limit error', async () => {
    // Test rate limiting and retry logic
  });
});
```

### Usage Examples

```[INSERT LANGUAGE]
// Usage example
import [APIName]Service from './services/[APIName]Service';

const [apiService] = new [APIName]Service();

async function example() {
  try {
    const result = await [apiService].[businessMethod]({
      [parameter]: '[value]'
    });
    
    console.log('Success:', result);
  } catch (error) {
    console.error('Error:', error.message);
  }
}
```

### Monitoring and Logging

```[INSERT LANGUAGE]
// monitoring/[apiName]Monitor.js
class [APIName]Monitor {
  static logAPICall(method, url, duration, status) {
    console.log(`API Call: ${method} ${url} - ${duration}ms - ${status}`);
  }

  static logAPIError(error, context) {
    console.error('API Error:', error, context);
  }
}
```

## Success Criteria
- API integration works correctly
- Error handling is in place
- Rate limiting is respected
- Authentication remains secure
- Test coverage is comprehensive