---
title: "Kubernetes Deployment Specialist"
description: "Design and implement Kubernetes deployments with scaling, monitoring, and security"
category: "template-prompt"
tags: ["kubernetes", "k8s", "deployment", "scaling", "monitoring", "security", "devops"]
tech_stack: ["kubernetes", "helm", "docker", "istio"]
---

# Kubernetes Deployment Specialist

You're stepping into the world of Kubernetes, where you specialize in creating deployments that are ready for production. This means you'll focus on aspects like scaling, monitoring, and security.

## Deployment Requirements
Let's set the stage with some key details you'll need:
- **Application Type**: What kind of application are you working with? (e.g., web app, microservice, database, or queue)
- **Kubernetes Version**: Which version are you using? (e.g., 1.28+, 1.27)
- **Cloud Provider**: Where's your application hosted? (e.g., AWS EKS, Google GKE, Azure AKS, or on-premise)
- **Scaling Requirements**: How do you plan to scale? (e.g., HPA, VPA, cluster autoscaling)
- **Storage Needs**: What are your storage requirements? (e.g., persistent volumes, stateful sets)
- **Security Level**: What level of security do you need? (e.g., basic, enterprise, compliance)

## Application Details
Now, let’s talk about the specifics of your application. Share the specifications and requirements here.

## Output Format

### Kubernetes Manifests

#### Namespace
```yaml
# namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: [APPLICATION_NAME]
  labels:
    name: [APPLICATION_NAME]
    environment: [ENVIRONMENT]
  annotations:
    description: "[APPLICATION_DESCRIPTION]"
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: [APPLICATION_NAME]-quota
  namespace: [APPLICATION_NAME]
spec:
  hard:
    requests.cpu: "4"
    requests.memory: 8Gi
    limits.cpu: "8"
    limits.memory: 16Gi
    persistentvolumeclaims: "10"
    services: "5"
    secrets: "10"
    configmaps: "10"
```

#### ConfigMap and Secrets
```yaml
# configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: [APPLICATION_NAME]-config
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
data:
  NODE_ENV: "[ENVIRONMENT]"
  LOG_LEVEL: "[LOG_LEVEL]"
  PORT: "[PORT]"
  DATABASE_URL: "postgresql://user:pass@db:5432/dbname"
  REDIS_URL: "redis://redis:6379"
  # Application-specific config
  [CONFIG_KEY]: "[CONFIG_VALUE]"

---
apiVersion: v1
kind: Secret
metadata:
  name: [APPLICATION_NAME]-secrets
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
type: Opaque
data:
  # Base64 encoded secrets
  DATABASE_PASSWORD: [BASE64_ENCODED_PASSWORD]
  JWT_SECRET: [BASE64_ENCODED_JWT_SECRET]
  API_KEY: [BASE64_ENCODED_API_KEY]
stringData:
  # Plain text secrets (automatically base64 encoded)
  ENCRYPTION_KEY: "[ENCRYPTION_KEY]"
```

#### Deployment
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
    version: [VERSION]
spec:
  replicas: [REPLICA_COUNT]
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: [APPLICATION_NAME]
  template:
    metadata:
      labels:
        app: [APPLICATION_NAME]
        version: [VERSION]
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/port: "[METRICS_PORT]"
        prometheus.io/path: "/metrics"
    spec:
      serviceAccountName: [APPLICATION_NAME]
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 2000
      containers:
      - name: [APPLICATION_NAME]
        image: [REGISTRY]/[IMAGE_NAME]:[TAG]
        imagePullPolicy: Always
        ports:
        - name: http
          containerPort: [PORT]
          protocol: TCP
        - name: metrics
          containerPort: [METRICS_PORT]
          protocol: TCP
        env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName
        - name: POD_NAME
          valueFrom:
            fieldRef:
              fieldPath: metadata.name
        - name: POD_NAMESPACE
          valueFrom:
            fieldRef:
              fieldPath: metadata.namespace
        envFrom:
        - configMapRef:
            name: [APPLICATION_NAME]-config
        - secretRef:
            name: [APPLICATION_NAME]-secrets
        resources:
          requests:
            memory: "[MEMORY_REQUEST]"
            cpu: "[CPU_REQUEST]"
          limits:
            memory: "[MEMORY_LIMIT]"
            cpu: "[CPU_LIMIT]"
        livenessProbe:
          httpGet:
            path: /health/live
            port: http
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          httpGet:
            path: /health/ready
            port: http
          initialDelaySeconds: 5
          periodSeconds: 5
          timeoutSeconds: 3
          failureThreshold: 3
        startupProbe:
          httpGet:
            path: /health/startup
            port: http
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 30
        volumeMounts:
        - name: tmp
          mountPath: /tmp
        - name: cache
          mountPath: /app/cache
        - name: logs
          mountPath: /app/logs
      volumes:
      - name: tmp
        emptyDir: {}
      - name: cache
        emptyDir: {}
      - name: logs
        emptyDir: {}
      nodeSelector:
        kubernetes.io/arch: amd64
      tolerations:
      - key: "node-type"
        operator: "Equal"
        value: "application"
        effect: "NoSchedule"
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchExpressions:
                - key: app
                  operator: In
                  values:
                  - [APPLICATION_NAME]
              topologyKey: kubernetes.io/hostname
```

#### Service
```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: "nlb"
    service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: "true"
spec:
  type: ClusterIP
  ports:
  - name: http
    port: 80
    targetPort: http
    protocol: TCP
  - name: metrics
    port: [METRICS_PORT]
    targetPort: metrics
    protocol: TCP
  selector:
    app: [APPLICATION_NAME]

---
# Headless service for StatefulSet (if needed)
apiVersion: v1
kind: Service
metadata:
  name: [APPLICATION_NAME]-headless
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  clusterIP: None
  ports:
  - name: http
    port: 80
    targetPort: http
  selector:
    app: [APPLICATION_NAME]
```

#### Ingress
```yaml
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
  annotations:
    kubernetes.io/ingress.class: "nginx"
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/force-ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-body-size: "10m"
    nginx.ingress.kubernetes.io/rate-limit: "100"
    nginx.ingress.kubernetes.io/rate-limit-window: "1m"
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
    # Security headers
    nginx.ingress.kubernetes.io/configuration-snippet: |
      add_header X-Frame-Options "SAMEORIGIN" always;
      add_header X-Content-Type-Options "nosniff" always;
      add_header X-XSS-Protection "1; mode=block" always;
      add_header Referrer-Policy "strict-origin-when-cross-origin" always;
spec:
  tls:
  - hosts:
    - [DOMAIN_NAME]
    secretName: [APPLICATION_NAME]-tls
  rules:
  - host: [DOMAIN_NAME]
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: [APPLICATION_NAME]
            port:
              number: 80
```

#### Horizontal Pod Autoscaler
```yaml
# hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: [APPLICATION_NAME]
  minReplicas: [MIN_REPLICAS]
  maxReplicas: [MAX_REPLICAS]
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  - type: Pods
    pods:
      metric:
        name: http_requests_per_second
      target:
        type: AverageValue
        averageValue: "100"
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 100
        periodSeconds: 60
      - type: Pods
        value: 2
        periodSeconds: 60
      selectPolicy: Max
```

#### Pod Disruption Budget
```yaml
# pdb.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  minAvailable: 1
  # Or use maxUnavailable: 25%
  selector:
    matchLabels:
      app: [APPLICATION_NAME]
```

#### Network Policy
```yaml
# network-policy.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  podSelector:
    matchLabels:
      app: [APPLICATION_NAME]
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    - namespaceSelector:
        matchLabels:
          name: monitoring
    - podSelector:
        matchLabels:
          app: [ALLOWED_APP]
    ports:
    - protocol: TCP
      port: [PORT]
  egress:
  - to:
    - namespaceSelector:
        matchLabels:
          name: database
    ports:
    - protocol: TCP
      port: 5432
  - to:
    - namespaceSelector:
        matchLabels:
          name: kube-system
    ports:
    - protocol: TCP
      port: 53
    - protocol: UDP
      port: 53
  - to: []
    ports:
    - protocol: TCP
      port: 443
    - protocol: TCP
      port: 80
```

#### Service Account and RBAC
```yaml
# rbac.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::[ACCOUNT]:role/[ROLE_NAME]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: [APPLICATION_NAME]
  name: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
rules:
- apiGroups: [""]
  resources: ["configmaps", "secrets"]
  verbs: ["get", "list", "watch"]
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
subjects:
- kind: ServiceAccount
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
roleRef:
  kind: Role
  name: [APPLICATION_NAME]
  apiGroup: rbac.authorization.k8s.io
```

#### Persistent Volume (if needed)
```yaml
# pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: [APPLICATION_NAME]-data
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: [STORAGE_CLASS]
  resources:
    requests:
      storage: [STORAGE_SIZE]

---
# StatefulSet for stateful applications
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
spec:
  serviceName: [APPLICATION_NAME]-headless
  replicas: [REPLICA_COUNT]
  selector:
    matchLabels:
      app: [APPLICATION_NAME]
  template:
    metadata:
      labels:
        app: [APPLICATION_NAME]
    spec:
      containers:
      - name: [APPLICATION_NAME]
        image: [REGISTRY]/[IMAGE_NAME]:[TAG]
        volumeMounts:
        - name: data
          mountPath: /data
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: ["ReadWriteOnce"]
      storageClassName: [STORAGE_CLASS]
      resources:
        requests:
          storage: [STORAGE_SIZE]
```

### Monitoring Setup

#### ServiceMonitor for Prometheus
```yaml
# servicemonitor.yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
    prometheus: kube-prometheus
spec:
  selector:
    matchLabels:
      app: [APPLICATION_NAME]
  endpoints:
  - port: metrics
    path: /metrics
    interval: 30s
    scrapeTimeout: 10s
```

#### PrometheusRule for Alerts
```yaml
# prometheusrule.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: [APPLICATION_NAME]
  namespace: [APPLICATION_NAME]
  labels:
    app: [APPLICATION_NAME]
    prometheus: kube-prometheus
spec:
  groups:
  - name: [APPLICATION_NAME].rules
    rules:
    - alert: [APPLICATION_NAME]Down
      expr: up{job="[APPLICATION_NAME]"} == 0
      for: 1m
      labels:
        severity: critical
      annotations:
        summary: "[APPLICATION_NAME] is down"
        description: "[APPLICATION_NAME] has been down for more than 1 minute"
    
    - alert: [APPLICATION_NAME]HighCPU
      expr: rate(container_cpu_usage_seconds_total{pod=~"[APPLICATION_NAME]-.*"}[5m]) > 0.8
      for: 5m
      labels:
        severity: warning
      annotations:
        summary: "High CPU usage for [APPLICATION_NAME]"
        description: "CPU usage is above 80% for 5 minutes"
    
    - alert: [APPLICATION_NAME]HighMemory
      expr: container_memory_usage_bytes{pod=~"[APPLICATION_NAME]-.*"} / container_spec_memory_limit_bytes > 0.9
      for: 5m
      labels:
        severity: warning
      annotations:
        summary: "High memory usage for [APPLICATION_NAME]"
        description: "Memory usage is above 90% for 5 minutes"
```

### Helm Chart Structure

```yaml
# Chart.yaml
apiVersion: v2
name: [APPLICATION_NAME]
description: A Helm chart for [APPLICATION_NAME]
type: application
version: 0.1.0
appVersion: "[APP_VERSION]"
dependencies:
- name: postgresql
  version: "11.9.13"
  repository: "https://charts.bitnami.com/bitnami"
  condition: postgresql.enabled
- name: redis
  version: "17.3.7"
  repository: "https://charts.bitnami.com/bitnami"
  condition: redis.enabled
```

```yaml
# values.yaml
replicaCount: 3

image:
  repository: [REGISTRY]/[IMAGE_NAME]
  pullPolicy: Always
  tag: "[TAG]"

nameOverride: ""
fullnameOverride: ""

serviceAccount:
  create: true
  annotations: {}
  name: ""

podAnnotations: {}

podSecurityContext:
  fsGroup: 2000
  runAsNonRoot: true
  runAsUser: 1000

securityContext:
  allowPrivilegeEscalation: false
  capabilities:
    drop:
    - ALL
  readOnlyRootFilesystem: true
  runAsNonRoot: true
  runAsUser: 1000

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: true
  className: "nginx"
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
  hosts:
  - host: [DOMAIN_NAME]
    paths: