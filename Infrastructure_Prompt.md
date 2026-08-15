Using the approved Architecture Blueprint — Volume 1, the approved Architecture Blueprint — Volume 2, the approved Backend implementation plan, the approved Frontend implementation plan, and the Master Prompt above.

Begin Infrastructure, DevOps, Cloud, Observability, Security Operations, CI/CD, testing infrastructure, and deployment implementation.

Do NOT redesign the approved application architecture.

Do NOT redesign service boundaries, database models, API contracts, event contracts, authentication architecture, authorization architecture, or frontend architecture unless a critical infrastructure requirement makes a correction necessary.

If an approved architectural decision must be changed, explicitly document:

1. The original decision.
2. The reason it cannot safely operate in production.
3. The proposed replacement.
4. The impact on Backend, Frontend, Mobile, Security, and Operations.

Assume all architecture, backend contracts, frontend contracts, and application boundaries have been approved.

Implement infrastructure incrementally according to the Master Prompt milestone strategy.

────────────────────────────────────────

MISSION

Build a production-ready, globally scalable, secure, observable, automated cloud infrastructure platform for the Enterprise Instagram-Style Social Platform.

The infrastructure must support:

• Consumer Web Application

• Consumer Mobile Application backend services

• Creator Studio

• Business Dashboard

• Advertising Manager

• Administration Dashboard

• Moderation Dashboard

• API Gateway

• Authentication Services

• User and Profile Services

• Social Graph Services

• Post Services

• Feed Services

• Recommendation Services

• Media Services

• Image Processing Workers

• Video Processing Workers

• Story Services

• Reels Services

• Messaging Services

• Notification Services

• Search Services

• Creator Services

• Business Services

• Commerce Services

• Advertising Services

• Analytics Services

• Moderation Services

• Trust & Safety Services

• Audit Services

• Feature Flag Services

• Developer Platform Services

• Kafka or Redpanda

• Redis

• PostgreSQL

• Elasticsearch or OpenSearch

• Object Storage

• CDN

• Background Workers

• Monitoring

• Logging

• Distributed Tracing

• Security Operations

• Disaster Recovery

Design for:

• 1B+ registered users

• 300M+ daily active users

• Billions of feed requests

• Billions of media objects

• Global multi-region traffic

• Active-active deployment where appropriate

• High availability

• Horizontal autoscaling

• Zero-downtime deployments

• Failure isolation

• Disaster recovery

• Long-term operational maintainability

────────────────────────────────────────

PRIMARY INFRASTRUCTURE STACK

Containerization

• Docker

Container Orchestration

• Kubernetes

Package Management

• Helm

Infrastructure as Code

• Terraform

CI/CD

• GitHub Actions

Cloud Architecture

• AWS-compatible architecture

Compute

• Kubernetes worker nodes

• Managed node groups where appropriate

Database

• PostgreSQL

Cache

• Redis

Event Streaming

• Kafka or Redpanda

Background Processing

• BullMQ workers

Search

• Elasticsearch or OpenSearch

Object Storage

• AWS S3-compatible storage

CDN

• CloudFront-compatible CDN

Secrets

• HashiCorp Vault or approved managed secret integration

Observability

• Prometheus

• Grafana

• Loki

• Tempo

• OpenTelemetry

Security

• IAM

• Network Policies

• RBAC

• Secret Rotation

• Image Scanning

• Dependency Scanning

• Infrastructure Scanning

• Policy Enforcement

────────────────────────────────────────

INFRASTRUCTURE PRINCIPLES

Strictly follow:

• Infrastructure as Code

• Immutable infrastructure where practical

• Declarative configuration

• Environment isolation

• Least privilege

• Defense in depth

• Zero-trust networking principles

• Horizontal scalability

• High availability

• Failure isolation

• Idempotent infrastructure changes

• Automated deployments

• Automated rollback capability

• Observability by default

• Secure defaults

• Cost awareness

• Disaster recovery readiness

• Reproducible environments

Do not rely on undocumented manual production configuration.

────────────────────────────────────────

ENVIRONMENTS

Generate complete infrastructure architecture for:

• Local Development

• Development

• Staging

• Production

Support environment-specific:

• Configuration

• Secrets

• Domains

• Databases

• Redis instances

• Kafka clusters

• Search clusters

• Object storage buckets

• CDN distributions

• Monitoring configuration

• Resource limits

• Scaling rules

Production must be isolated from lower environments.

────────────────────────────────────────

MONOREPO INFRASTRUCTURE STRUCTURE

Generate and maintain an infrastructure structure containing:

• Docker configurations

• Docker Compose configurations

• Kubernetes base manifests

• Helm charts

• Environment values

• Terraform modules

• Terraform environments

• CI workflows

• CD workflows

• Security workflows

• Database migration workflows

• Monitoring configurations

• Logging configurations

• Tracing configurations

• Alerting rules

• Runbooks

• Backup configurations

• Disaster recovery configurations

• Operational scripts

────────────────────────────────────────

DOCKER

Generate production-ready Docker configurations for:

• API Gateway

• Every backend service

• Background workers

• Media processing workers

• Recommendation workers

• Search indexing workers

• Analytics workers

• Frontend web applications

Use:

• Multi-stage builds

• Minimal production images

• Non-root users

• Dependency caching

• Build reproducibility

• Health checks where appropriate

• Environment-based configuration

• No embedded secrets

• Secure defaults

Generate development-specific Docker configurations where necessary without weakening production images.

────────────────────────────────────────

LOCAL DEVELOPMENT

Generate a complete local development environment using Docker Compose.

Support local development for:

• PostgreSQL

• Redis

• Kafka or Redpanda

• Elasticsearch or OpenSearch

• Object storage emulator where appropriate

• Mail testing service where appropriate

• Backend services

• Workers

• Frontend applications where appropriate

Include:

• Persistent development volumes

• Health checks

• Service dependencies

• Startup ordering

• Environment variables

• Local network configuration

• Development observability where practical

Do not require cloud infrastructure for ordinary local development.

────────────────────────────────────────

KUBERNETES

Generate production-ready Kubernetes architecture.

Include:

• Namespaces

• Deployments

• StatefulSets where appropriate

• Services

• ConfigMaps

• Secrets references

• ServiceAccounts

• Roles

• RoleBindings

• HorizontalPodAutoscalers

• PodDisruptionBudgets

• Resource requests

• Resource limits

• Startup probes

• Readiness probes

• Liveness probes

• Ingress configuration

• NetworkPolicies

• Affinity rules where appropriate

• Anti-affinity rules for high availability

• Topology spread constraints

• Priority classes where appropriate

• Graceful termination

• Rolling updates

• Zero-downtime deployment configuration

────────────────────────────────────────

KUBERNETES SERVICE TOPOLOGY

Design workload separation for:

Critical Services

• API Gateway

• Authentication

• Authorization

• User

• Profile

• Social Graph

• Feed

• Messaging

• Notification

High-CPU Services

• Image Processing

• Video Processing

• Recommendation Processing

• Analytics Processing

High-Memory Services

• Search components where self-managed

• Recommendation workloads where applicable

Stateful Components

• PostgreSQL where self-managed

• Redis where self-managed

• Kafka or Redpanda where self-managed

• Elasticsearch or OpenSearch where self-managed

Prefer managed infrastructure for critical stateful production services when it provides stronger operational reliability, but maintain provider abstraction where possible.

────────────────────────────────────────

HELM

Generate:

• Base charts

• Reusable service chart patterns

• Shared templates

• Environment-specific values

• Production values

• Staging values

• Development values

• Secrets integration

• Resource configuration

• Autoscaling configuration

• Ingress configuration

• Pod security configuration

Do not duplicate identical Kubernetes configuration unnecessarily.

────────────────────────────────────────

TERRAFORM

Generate production-ready Terraform architecture.

Create reusable modules for:

• Networking

• VPC

• Public subnets

• Private subnets

• Routing

• NAT

• Security groups

• Kubernetes cluster

• Node groups

• IAM roles

• Object storage

• CDN

• PostgreSQL

• Redis

• Kafka or Redpanda

• Search

• Load balancing

• DNS

• Certificates

• Secrets integration

• Monitoring infrastructure

• Backup infrastructure

• Disaster recovery infrastructure

Generate separate environment configurations for:

• Development

• Staging

• Production

Use remote Terraform state with:

• State locking

• Encryption

• Environment isolation

• Access controls

Never hardcode cloud credentials.

────────────────────────────────────────

NETWORK ARCHITECTURE

Generate a secure network topology.

Include:

• Multi-AZ design

• Public subnets

• Private application subnets

• Private data subnets

• NAT architecture

• Internet gateways

• Internal service communication

• Load balancers

• Ingress controllers

• API edge layer

• CDN integration

• Firewall boundaries

• Security groups

• Kubernetes network policies

• Private database access

• Private cache access

• Private event-streaming access

• Bastionless administration where practical

Design using defense in depth.

────────────────────────────────────────

GLOBAL DEPLOYMENT

Design infrastructure for multi-region expansion.

Include:

• Primary region

• Secondary region

• Regional Kubernetes clusters

• Global traffic routing

• Health-based failover

• CDN edge distribution

• Regional API endpoints

• Database replication strategy

• Cross-region backups

• Object replication

• Event replication strategy

• Regional isolation

• Controlled failover

Clearly distinguish:

• Active-active workloads

• Active-passive workloads

• Single-writer domains

• Multi-region eventually consistent domains

Do not assume every stateful workload can safely operate active-active without explicit conflict-resolution design.

────────────────────────────────────────

DATABASE INFRASTRUCTURE

Generate production-ready PostgreSQL infrastructure supporting:

• Primary instances

• Read replicas

• Automated backups

• Point-in-time recovery

• Encryption at rest

• Encryption in transit

• Private networking

• Connection pooling

• Monitoring

• Slow query analysis

• Migration workflow

• Maintenance strategy

• Capacity planning

• Disaster recovery

• Cross-region backup strategy

• Restore testing

Coordinate infrastructure with the approved Prisma migration architecture.

Never run destructive migrations automatically without explicit safeguards.

────────────────────────────────────────

REDIS INFRASTRUCTURE

Generate Redis architecture for:

• Caching

• Sessions

• Rate limiting

• Distributed locks

• Feed caching

• Recommendation caching

• Presence

• Socket.IO scaling

• Feature flags

• Idempotency keys

Implement:

• High availability

• Failover

• Encryption

• Authentication

• Private networking

• Monitoring

• Memory limits

• Eviction policies

• Backup strategy where required

• Cache failure behavior

────────────────────────────────────────

EVENT STREAMING

Generate Kafka or Redpanda infrastructure supporting:

• Topic provisioning

• Partition strategy

• Replication

• Retention policies

• Consumer groups

• Dead-letter topics

• Retry topics

• Schema and event-version compatibility strategy

• ACLs

• Encryption

• Monitoring

• Capacity planning

• Broker failure recovery

• Cross-region replication strategy where required

Do not configure transactional and analytics topics with identical retention assumptions.

────────────────────────────────────────

BACKGROUND WORKERS

Deploy independent worker workloads for:

• Image processing

• Video processing

• Thumbnail generation

• Media cleanup

• Story expiration

• Scheduled publishing

• Notification delivery

• Search indexing

• Feed maintenance

• Analytics aggregation

• Recommendation generation

• Trending calculations

• Data retention

• Cache invalidation

• Retry processing

• Dead-letter recovery

Configure:

• Independent autoscaling

• Queue-based scaling where appropriate

• Resource isolation

• Retry policies

• Concurrency limits

• Graceful shutdown

• Poison-message handling

• Worker health metrics

────────────────────────────────────────

MEDIA INFRASTRUCTURE

Generate infrastructure for:

• Object storage

• Separate bucket boundaries where appropriate

• Upload buckets

• Processed media

• Thumbnails

• Temporary media

• Quarantine media

• Archived media

• Lifecycle policies

• Object versioning where required

• Encryption

• Signed URL architecture

• Upload size enforcement

• CDN integration

• Cache invalidation

• Cross-region replication where required

• Malware scanning pipeline integration

Do not expose storage buckets directly unless explicitly required.

────────────────────────────────────────

VIDEO INFRASTRUCTURE

Design infrastructure for:

• FFmpeg processing workers

• CPU-intensive workloads

• Optional GPU readiness

• Transcoding queues

• Temporary storage

• Processing isolation

• Autoscaling

• Resource limits

• Timeout handling

• Retry handling

• Failed-job recovery

• Output publishing

• Thumbnail generation

• Future adaptive bitrate streaming

────────────────────────────────────────

SEARCH INFRASTRUCTURE

Generate Elasticsearch or OpenSearch infrastructure supporting:

• High availability

• Index lifecycle management

• Hot and warm data strategies where appropriate

• Snapshots

• Index monitoring

• Access control

• Encryption

• Private networking

• Capacity scaling

• Recovery procedures

• Reindexing strategy

• Zero-downtime index migrations

────────────────────────────────────────

CDN AND EDGE ARCHITECTURE

Generate:

• CDN distributions

• Media caching

• Static asset caching

• Cache policies

• Origin access controls

• Signed URL or signed cookie support where required

• HTTPS enforcement

• Compression

• Cache invalidation

• Origin failover where appropriate

• DDoS protection integration

────────────────────────────────────────

CI

Generate GitHub Actions workflows for:

• Dependency installation

• Linting

• Type checking

• Unit tests

• Integration tests

• Contract tests

• Build verification

• Docker image building

• Container scanning

• Dependency vulnerability scanning

• Secret scanning

• Infrastructure validation

• Terraform formatting

• Terraform validation

• Helm validation

• Kubernetes manifest validation

• Migration validation

• License checks where appropriate

Use caching safely.

Do not expose secrets in logs.

────────────────────────────────────────

CD

Generate deployment pipelines supporting:

• Development deployment

• Staging deployment

• Production deployment

• Environment approval gates

• Artifact promotion

• Immutable image tags

• Deployment verification

• Health verification

• Smoke tests

• Automatic rollback where safe

• Manual rollback capability

• Database migration coordination

• Progressive delivery readiness

• Canary deployment readiness

• Blue-green deployment readiness

Do not couple deployment success solely to process startup.

Verify application readiness.

────────────────────────────────────────

DATABASE MIGRATION PIPELINE

Generate safe migration workflows.

Include:

• Migration validation

• Compatibility checks

• Expand-and-contract migration strategy

• Backup verification

• Migration locking

• Deployment ordering

• Rollback planning

• Production approval requirements

• Post-migration health checks

Never assume every schema migration is safely reversible.

────────────────────────────────────────

SECRETS MANAGEMENT

Integrate HashiCorp Vault or the approved secrets architecture.

Support:

• Application secrets

• Database credentials

• API credentials

• OAuth secrets

• Signing keys

• Encryption keys

• Third-party service credentials

Implement:

• Secret injection

• Access policies

• Least privilege

• Secret rotation

• Audit logging

• Environment isolation

Never commit secrets.

Never place production secrets inside:

• Docker images

• Git repositories

• Helm values files

• Terraform source code

────────────────────────────────────────

SECURITY INFRASTRUCTURE

Implement:

• IAM least privilege

• Kubernetes RBAC

• Pod security controls

• Network policies

• Private data services

• TLS

• Encryption at rest

• Encryption in transit

• Container scanning

• Dependency scanning

• Secret scanning

• Infrastructure security scanning

• Admission policy readiness

• Image provenance where supported

• Audit logging

• DDoS protection integration

• Web Application Firewall readiness

• Security incident logging

────────────────────────────────────────

OBSERVABILITY

Implement a complete observability platform.

Metrics:

• Prometheus

• Application metrics

• Infrastructure metrics

• Kubernetes metrics

• Database metrics

• Redis metrics

• Kafka metrics

• Queue metrics

• Search metrics

• Media processing metrics

• Business metrics

Visualization:

• Grafana dashboards

Logging:

• Structured application logs

• Centralized collection

• Loki

Tracing:

• OpenTelemetry

• Tempo

Implement correlation between:

• HTTP requests

• API Gateway requests

• Kafka events

• Queue jobs

• Background workers

• WebSocket connections

• Database operations where appropriate

────────────────────────────────────────

MONITORING

Generate dashboards for:

Platform Health

• Availability

• Error rates

• Latency

• Saturation

API Gateway

• Request volume

• Error rate

• Latency

• Rate limiting

Authentication

• Login success

• Login failures

• Token refresh failures

Feed

• Feed latency

• Cache hit rate

• Candidate generation

• Ranking latency

Media

• Upload success

• Processing latency

• Processing failures

• Queue depth

Messaging

• Connected users

• WebSocket connections

• Delivery latency

• Failed delivery

Notifications

• Queue depth

• Delivery success

• Provider failures

Database

• Connections

• Query latency

• Replication lag

• CPU

• Memory

Redis

• Memory

• Hit rate

• Evictions

Kafka

• Consumer lag

• Throughput

• Broker health

Search

• Query latency

• Indexing failures

• Cluster health

Business Metrics

• Active users

• Posts created

• Videos processed

• Feed requests

• Engagement events

────────────────────────────────────────

ALERTING

Generate alert rules for:

• Service unavailable

• High error rate

• High latency

• Pod crash loops

• Deployment failures

• Database failures

• Replication lag

• Low disk capacity

• Redis memory pressure

• Kafka consumer lag

• Queue backlog

• Search cluster failure

• Media processing failures

• Security events

• Backup failures

• Certificate expiration

Use severity levels:

• Critical

• High

• Warning

• Informational

Include alert routing and escalation architecture.

Avoid alerting on every transient failure.

────────────────────────────────────────

LOGGING

Implement centralized structured logging.

Every log event should support:

• Timestamp

• Severity

• Service name

• Environment

• Request ID

• Correlation ID

• Trace ID

• User ID where privacy rules allow

• Error metadata

Do not log:

• Passwords

• Access tokens

• Refresh tokens

• Secret values

• Sensitive authentication material

• Unnecessary personal data

────────────────────────────────────────

BACKUPS

Generate backup strategies for:

• PostgreSQL

• Object storage

• Search data where required

• Configuration

• Critical infrastructure state

Include:

• Backup frequency

• Retention

• Encryption

• Geographic separation

• Restore testing

• Recovery documentation

────────────────────────────────────────

DISASTER RECOVERY

Generate complete disaster recovery architecture.

Define:

• Recovery Point Objective

• Recovery Time Objective

• Regional failure strategy

• Database recovery

• Kubernetes recovery

• Object storage recovery

• Kafka recovery

• Redis recovery strategy

• Search recovery

• DNS recovery

• CDN recovery

• Infrastructure recreation

• Communication procedures

Generate disaster recovery runbooks.

Test recovery assumptions instead of treating backups as proof of recoverability.

────────────────────────────────────────

CAPACITY PLANNING

Generate capacity planning architecture for:

• API traffic

• WebSocket connections

• Feed generation

• Media uploads

• Video processing

• Background queues

• Database growth

• Redis memory

• Kafka throughput

• Search indexing

• CDN bandwidth

Define scaling signals and capacity thresholds.

────────────────────────────────────────

COST MANAGEMENT

Implement cost-awareness architecture.

Include:

• Resource tagging

• Environment budgets

• Storage lifecycle optimization

• Autoscaling

• Spot or interruptible workload readiness where appropriate

• Reserved capacity readiness

• Cost anomaly monitoring

• High-cost service visibility

Do not sacrifice critical production reliability purely for cost reduction.

────────────────────────────────────────

OPERATIONAL RUNBOOKS

Generate runbooks for:

• Service outage

• Database outage

• Redis outage

• Kafka outage

• Search outage

• Media processing backlog

• Failed deployment

• Failed migration

• Rollback

• Regional outage

• Security incident

• Certificate failure

• Backup failure

• High latency

• Queue overload

• Excessive error rate

────────────────────────────────────────

TESTING INFRASTRUCTURE

Generate infrastructure supporting:

• Unit test execution

• Integration testing

• Contract testing

• End-to-end testing

• Performance testing

• Load testing

• Stress testing

• Failure testing

• Chaos engineering readiness

• Security testing

• Dependency testing

• Infrastructure testing

Use isolated test environments where required.

────────────────────────────────────────

PROJECT INDEX

Maintain throughout implementation:

Current Milestone

Generated Infrastructure Files

Completed Docker Components

Completed Kubernetes Components

Completed Helm Charts

Completed Terraform Modules

Completed CI/CD Workflows

Completed Monitoring Components

Completed Security Components

Completed Backup Components

Completed Disaster Recovery Components

Remaining Work

Dependencies

Next File

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

• "implement similarly"

• "left as an exercise"

• "for brevity"

• "remaining code omitted"

Every generated file must integrate with the previously approved architecture and generated implementation.

Do not regenerate unchanged files.

Only modify files when required.

────────────────────────────────────────

STOP CONDITIONS

Generate the infrastructure incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

At the end of every milestone:

• Verify infrastructure consistency.

• Validate integration with the application architecture.

• Update the project index.

• List completed infrastructure components.

• List completed Docker components.

• List completed Kubernetes components.

• List completed Terraform modules.

• List completed CI/CD workflows.

• List completed observability components.

• Identify the exact next file or logical implementation unit.

STOP and wait for approval before generating the next milestone.
