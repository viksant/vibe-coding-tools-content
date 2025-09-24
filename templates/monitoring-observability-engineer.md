---
title: "Monitoring & Observability Engineer"
description: "Implement comprehensive monitoring, logging, and observability systems"
category: "template-prompt"
tags: ["monitoring", "observability", "logging", "metrics", "alerting", "debugging"]
tech_stack: ["prometheus", "grafana", "datadog", "newrelic", "elk-stack"]
---

# Monitoring & Observability Engineer

You are a DevOps/SRE expert specializing in comprehensive monitoring and observability solutions.

## Monitoring Requirements
- **System Type**: [INSERT TYPE - web app, microservices, infrastructure, database]
- **Technology Stack**: [INSERT TECH STACK]
- **Monitoring Tools**: [INSERT TOOLS - Prometheus, Grafana, DataDog, New Relic]
- **Scale**: [INSERT SCALE - requests/sec, services, nodes]
- **SLA Requirements**: [INSERT SLA - uptime, response time, error rate]
- **Alert Channels**: [INSERT CHANNELS - email, Slack, PagerDuty, webhook]

## Current System
[INSERT DESCRIPTION OF SYSTEM TO MONITOR]

## Output Format

### Monitoring Strategy

#### Three Pillars of Observability
1. **Metrics**: Quantitative measurements over time
2. **Logs**: Discrete events with context
3. **Traces**: Request flows through distributed systems

#### Key Metrics to Monitor
- **Application Metrics**: Response time, throughput, error rate
- **Infrastructure Metrics**: CPU, memory, disk, network
- **Business Metrics**: User activity, conversions, revenue
- **Security Metrics**: Failed logins, suspicious activity

### Prometheus Configuration

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - alertmanager:9093

scrape_configs:
  # Application metrics
  - job_name: '[APPLICATION_NAME]'
    static_configs:
      - targets: ['[APP_HOST]:[METRICS_PORT]']
    scrape_interval: 10s
    metrics_path: /metrics
    
  # Node exporter for system metrics
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['[NODE_HOST]:9100']
    
  # Database metrics
  - job_name: '[DATABASE_TYPE]-exporter'
    static_configs:
      - targets: ['[DB_HOST]:[EXPORTER_PORT]']

  # Kubernetes metrics (if applicable)
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
```

### Alert Rules

```yaml
# alert_rules.yml
groups:
  - name: application_alerts
    rules:
      # High error rate
      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.1
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value }} errors per second"

      # High response time
      - alert: HighResponseTime
        expr: histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m])) > 0.5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High response time"
          description: "95th percentile response time is {{ $value }}s"

      # Low availability
      - alert: ServiceDown
        expr: up == 0
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "Service is down"
          description: "{{ $labels.instance }} is down"

  - name: infrastructure_alerts
    rules:
      # High CPU usage
      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage"
          description: "CPU usage is {{ $value }}% on {{ $labels.instance }}"

      # High memory usage
      - alert: HighMemoryUsage
        expr: (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100 > 90
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage"
          description: "Memory usage is {{ $value }}% on {{ $labels.instance }}"

      # Low disk space
      - alert: LowDiskSpace
        expr: (1 - (node_filesystem_avail_bytes / node_filesystem_size_bytes)) * 100 > 85
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Low disk space"
          description: "Disk usage is {{ $value }}% on {{ $labels.instance }}"
```

### Application Instrumentation

```javascript
// metrics.js - Express.js application instrumentation
import express from 'express';
import prometheus from 'prom-client';

// Create metrics registry
const register = new prometheus.Registry();

// Default metrics (CPU, memory, etc.)
prometheus.collectDefaultMetrics({ register });

// Custom application metrics
const httpRequestsTotal = new prometheus.Counter({
  name: 'http_requests_total',
  help: 'Total number of HTTP requests',
  labelNames: ['method', 'status', 'route'],
  registers: [register]
});

const httpRequestDuration = new prometheus.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'status', 'route'],
  buckets: [0.1, 0.5, 1, 2, 5, 10],
  registers: [register]
});

const activeConnections = new prometheus.Gauge({
  name: 'active_connections',
  help: 'Number of active connections',
  registers: [register]
});

const databaseQueryDuration = new prometheus.Histogram({
  name: 'database_query_duration_seconds',
  help: 'Duration of database queries in seconds',
  labelNames: ['operation', 'table'],
  buckets: [0.01, 0.05, 0.1, 0.5, 1, 2],
  registers: [register]
});

// Middleware to track metrics
export const metricsMiddleware = (req, res, next) => {
  const start = Date.now();
  
  // Track active connections
  activeConnections.inc();
  
  res.on('finish', () => {
    const duration = (Date.now() - start) / 1000;
    const route = req.route?.path || req.path;
    
    // Record metrics
    httpRequestsTotal
      .labels(req.method, res.statusCode, route)
      .inc();
    
    httpRequestDuration
      .labels(req.method, res.statusCode, route)
      .observe(duration);
    
    activeConnections.dec();
  });
  
  next();
};

// Database query instrumentation
export const instrumentDatabaseQuery = async (operation, table, queryFunction) => {
  const end = databaseQueryDuration.startTimer({ operation, table });
  
  try {
    const result = await queryFunction();
    end();
    return result;
  } catch (error) {
    end();
    throw error;
  }
};

// Metrics endpoint
export const metricsEndpoint = async (req, res) => {
  try {
    res.set('Content-Type', register.contentType);
    res.end(await register.metrics());
  } catch (error) {
    res.status(500).end(error);
  }
};
```

### Structured Logging

```javascript
// logger.js - Structured logging with correlation IDs
import winston from 'winston';
import { v4 as uuidv4 } from 'uuid';

// Create logger instance
const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  defaultMeta: {
    service: process.env.SERVICE_NAME || 'unknown',
    version: process.env.SERVICE_VERSION || '1.0.0',
    environment: process.env.NODE_ENV || 'development'
  },
  transports: [
    // Console output
    new winston.transports.Console({
      format: winston.format.combine(
        winston.format.colorize(),
        winston.format.simple()
      )
    }),
    
    // File output
    new winston.transports.File({
      filename: 'logs/error.log',
      level: 'error'
    }),
    new winston.transports.File({
      filename: 'logs/combined.log'
    })
  ]
});

// Correlation ID middleware
export const correlationIdMiddleware = (req, res, next) => {
  req.correlationId = req.get('X-Correlation-ID') || uuidv4();
  res.set('X-Correlation-ID', req.correlationId);
  next();
};

// Enhanced logging with context
export const createContextLogger = (req) => {
  return {
    info: (message, meta = {}) => logger.info(message, {
      correlationId: req.correlationId,
      userId: req.user?.id,
      sessionId: req.sessionID,
      userAgent: req.get('User-Agent'),
      ip: req.ip,
      method: req.method,
      url: req.originalUrl,
      ...meta
    }),
    
    warn: (message, meta = {}) => logger.warn(message, {
      correlationId: req.correlationId,
      userId: req.user?.id,
      ...meta
    }),
    
    error: (message, error = null, meta = {}) => logger.error(message, {
      correlationId: req.correlationId,
      userId: req.user?.id,
      error: error ? {
        message: error.message,
        stack: error.stack,
        name: error.name
      } : null,
      ...meta
    })
  };
};

// Request logging middleware
export const requestLoggingMiddleware = (req, res, next) => {
  const start = Date.now();
  const logger = createContextLogger(req);
  
  logger.info('Request started', {
    method: req.method,
    url: req.originalUrl,
    userAgent: req.get('User-Agent'),
    ip: req.ip
  });
  
  res.on('finish', () => {
    const duration = Date.now() - start;
    logger.info('Request completed', {
      method: req.method,
      url: req.originalUrl,
      statusCode: res.statusCode,
      duration,
      contentLength: res.get('Content-Length')
    });
  });
  
  req.logger = logger;
  next();
};
```

### Distributed Tracing

```javascript
// tracing.js - OpenTelemetry setup
import { NodeSDK } from '@opentelemetry/sdk-node';
import { getNodeAutoInstrumentations } from '@opentelemetry/auto-instrumentations-node';
import { JaegerExporter } from '@opentelemetry/exporter-jaeger';
import { Resource } from '@opentelemetry/resources';
import { SemanticResourceAttributes } from '@opentelemetry/semantic-conventions';

// Initialize tracing
const jaegerExporter = new JaegerExporter({
  endpoint: process.env.JAEGER_ENDPOINT || 'http://localhost:14268/api/traces',
});

const sdk = new NodeSDK({
  resource: new Resource({
    [SemanticResourceAttributes.SERVICE_NAME]: process.env.SERVICE_NAME || 'unknown-service',
    [SemanticResourceAttributes.SERVICE_VERSION]: process.env.SERVICE_VERSION || '1.0.0',
    [SemanticResourceAttributes.DEPLOYMENT_ENVIRONMENT]: process.env.NODE_ENV || 'development',
  }),
  traceExporter: jaegerExporter,
  instrumentations: [getNodeAutoInstrumentations({
    '@opentelemetry/instrumentation-fs': {
      enabled: false, // Disable file system instrumentation for performance
    },
  })],
});

// Start tracing
sdk.start();

// Custom span creation
import { trace } from '@opentelemetry/api';

export const createSpan = (name, operation) => {
  const tracer = trace.getTracer('custom-operations');
  
  return tracer.startActiveSpan(name, async (span) => {
    try {
      const result = await operation(span);
      span.setStatus({ code: 1 }); // OK
      return result;
    } catch (error) {
      span.setStatus({ code: 2, message: error.message }); // ERROR
      span.recordException(error);
      throw error;
    } finally {
      span.end();
    }
  });
};

// Database operation tracing
export const traceDatabaseOperation = (operation, query) => {
  return createSpan(`db.${operation}`, (span) => {
    span.setAttributes({
      'db.operation': operation,
      'db.statement': query,
    });
    
    return performDatabaseOperation(query);
  });
};
```

### Health Check Implementation

```javascript
// healthCheck.js
import express from 'express';

const router = express.Router();

// Health check dependencies
const dependencies = {
  database: async () => {
    // Check database connectivity
    try {
      await db.query('SELECT 1');
      return { status: 'healthy', responseTime: Date.now() };
    } catch (error) {
      return { status: 'unhealthy', error: error.message };
    }
  },
  
  redis: async () => {
    try {
      await redis.ping();
      return { status: 'healthy' };
    } catch (error) {
      return { status: 'unhealthy', error: error.message };
    }
  },
  
  externalAPI: async () => {
    try {
      const response = await fetch('https://api.external.com/health', {
        timeout: 5000
      });
      return { 
        status: response.ok ? 'healthy' : 'unhealthy',
        statusCode: response.status 
      };
    } catch (error) {
      return { status: 'unhealthy', error: error.message };
    }
  }
};

// Liveness probe - basic service health
router.get('/health/live', (req, res) => {
  res.json({
    status: 'alive',
    timestamp: new Date().toISOString(),
    uptime: process.uptime()
  });
});

// Readiness probe - service ready to handle traffic
router.get('/health/ready', async (req, res) => {
  const checks = {};
  let overallStatus = 'healthy';
  
  for (const [name, checkFunction] of Object.entries(dependencies)) {
    try {
      checks[name] = await checkFunction();
      if (checks[name].status !== 'healthy') {
        overallStatus = 'unhealthy';
      }
    } catch (error) {
      checks[name] = { status: 'unhealthy', error: error.message };
      overallStatus = 'unhealthy';
    }
  }
  
  const statusCode = overallStatus === 'healthy' ? 200 : 503;
  
  res.status(statusCode).json({
    status: overallStatus,
    timestamp: new Date().toISOString(),
    checks
  });
});

// Detailed health endpoint
router.get('/health', async (req, res) => {
  const health = {
    status: 'healthy',
    timestamp: new Date().toISOString(),
    service: {
      name: process.env.SERVICE_NAME,
      version: process.env.SERVICE_VERSION,
      uptime: process.uptime(),
      memory: process.memoryUsage(),
      pid: process.pid
    },
    dependencies: {}
  };
  
  // Check all dependencies
  for (const [name, checkFunction] of Object.entries(dependencies)) {
    try {
      health.dependencies[name] = await checkFunction();
      if (health.dependencies[name].status !== 'healthy') {
        health.status = 'degraded';
      }
    } catch (error) {
      health.dependencies[name] = { status: 'unhealthy', error: error.message };
      health.status = 'unhealthy';
    }
  }
  
  const statusCode = health.status === 'healthy' ? 200 : 
                    health.status === 'degraded' ? 200 : 503;
  
  res.status(statusCode).json(health);
});

export default router;
```

### Grafana Dashboard Configuration

```json
{
  "dashboard": {
    "title": "[APPLICATION_NAME] Dashboard",
    "tags": ["[SERVICE_NAME]", "monitoring"],
    "timezone": "browser",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])",
            "legendFormat": "{{method}} {{status}}"
          }
        ],
        "yAxes": [
          {
            "label": "Requests/sec"
          }
        ]
      },
      {
        "title": "Response Time",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          },
          {
            "expr": "histogram_quantile(0.50, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "50th percentile"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total{status=~\"5..\"}[5m]) / rate(http_requests_total[5m])",
            "legendFormat": "Error Rate"
          }
        ]
      },
      {
        "title": "System Resources",
        "type": "graph",
        "targets": [
          {
            "expr": "100 - (avg(rate(node_cpu_seconds_total{mode=\"idle\"}[5m])) * 100)",
            "legendFormat": "CPU Usage %"
          },
          {
            "expr": "(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100",
            "legendFormat": "Memory Usage %"
          }
        ]
      }
    ]
  }
}
```

### Alertmanager Configuration

```yaml
# alertmanager.yml
global:
  smtp_smarthost: 'localhost:587'
  smtp_from: 'alerts@company.com'

route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
  receiver: 'default'
  routes:
    - match:
        severity: critical
      receiver: 'critical-alerts'
    - match:
        severity: warning
      receiver: 'warning-alerts'

receivers:
  - name: 'default'
    email_configs:
      - to: 'team@company.com'
        subject: 'Alert: {{ .GroupLabels.alertname }}'
        body: |
          {{ range .Alerts }}
          Alert: {{ .Annotations.summary }}
          Description: {{ .Annotations.description }}
          {{ end }}

  - name: 'critical-alerts'
    slack_configs:
      - api_url: 'YOUR_SLACK_WEBHOOK_URL'
        channel: '#alerts-critical'
        title: 'Critical Alert'
        text: '{{ range .Alerts }}{{ .Annotations.summary }}{{ end }}'
    email_configs:
      - to: 'oncall@company.com'
        subject: 'CRITICAL: {{ .GroupLabels.alertname }}'

  - name: 'warning-alerts'
    slack_configs:
      - api_url: 'YOUR_SLACK_WEBHOOK_URL'
        channel: '#alerts-warning'
        title: 'Warning Alert'
        text: '{{ range .Alerts }}{{ .Annotations.summary }}{{ end }}'
```

## Success Criteria
- All critical metrics monitored
- Alerts fire before user impact
- Logs provide actionable insights
- Dashboards show system health
- On-call team can debug quickly