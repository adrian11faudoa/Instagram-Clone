# Instagram — Infrastructure Prompt — Volume 2

# 1. ROLE

You are the **Senior Infrastructure and DevOps Engineering implementation team** responsible for implementing the bounded infrastructure scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* AWS
* Amazon Aurora PostgreSQL
* Amazon ElastiCache for Redis
* Amazon MSK/Kafka
* SQS and background-job infrastructure
* OpenSearch
* S3 and media-processing infrastructure
* secure networking
* encryption and key management
* autoscaling
* high availability
* infrastructure-as-code
* observability integration
* disaster-aware architecture
* performance and cost engineering

Your responsibility is to implement the assigned infrastructure scope completely and coherently inside the repository while preserving compatibility with the application's architecture and authoritative contracts.

Do not implement application business logic merely because infrastructure supports it.

Do not create fake infrastructure, placeholder resources, incomplete production configurations, hardcoded credentials, or infrastructure definitions that falsely imply external resources have been provisioned.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The platform includes:

* web frontend
* iOS and Android mobile applications
* backend APIs
* realtime communication
* PostgreSQL
* Redis
* Kafka/event streaming
* queues and background jobs
* OpenSearch
* object storage
* media processing
* CDN
* notifications
* moderation
* analytics
* observability
* reliability
* disaster recovery

The target infrastructure is AWS-based and designed for substantial production scale.

This prompt is limited to the **stateful data, caching, event-streaming, queue, search, and media-processing infrastructure foundations** required by the application.

# 3. CURRENT INFRASTRUCTURE ASSIGNMENT

Implement production infrastructure for:

* PostgreSQL
* PostgreSQL high availability foundations
* PostgreSQL backups and encryption
* Redis
* Redis high-availability foundations
* Kafka/event streaming
* SQS queues where appropriate
* dead-letter queues
* queue security
* worker infrastructure integration
* OpenSearch
* search security
* search networking
* media-processing infrastructure
* storage-processing integration
* encryption and KMS integration
* application-to-data access boundaries
* infrastructure-level data retention/lifecycle controls
* environment-specific data infrastructure
* data service observability foundations
* scaling foundations

This volume must remain infrastructure-focused.

Do not implement application repositories, SQL business logic, Kafka consumers/producers, search indexing logic, or media-processing business algorithms that belong to application implementation prompts.

# 4. REPOSITORY INSPECTION

Before modifying infrastructure, inspect:

* architecture documentation
* database contracts
* existing database configuration
* migrations
* ORM/query-layer configuration
* Redis usage
* cache contracts
* event contracts
* Kafka topic definitions
* queue definitions
* worker services
* search contracts
* OpenSearch integration
* media-processing services
* S3 configuration
* Dockerfiles
* worker deployment definitions
* environment configuration
* Terraform/OpenTofu/CDK/CloudFormation modules
* IAM policies
* networking
* security groups
* CI/CD
* observability configuration
* documentation

Identify existing assumptions around:

* PostgreSQL topology
* connection pooling
* Redis usage
* Kafka topics
* queue semantics
* OpenSearch indices
* object-storage paths
* media-processing workloads
* retention requirements
* data classification

Do not replace existing working infrastructure without a clear engineering reason.

# 5. TECHNOLOGY BASELINE

Use the project's established AWS architecture.

Expected services include:

* Amazon Aurora PostgreSQL or another already established managed PostgreSQL service
* Amazon ElastiCache for Redis
* Amazon MSK for Kafka where Kafka is part of the architecture
* Amazon SQS
* Amazon OpenSearch Service
* Amazon S3
* AWS KMS
* private VPC networking
* IAM roles
* Infrastructure as Code

Use managed services where they reduce operational burden without violating application requirements.

Do not introduce self-managed databases or clusters merely to increase infrastructure complexity.

# 6. DATABASE ARCHITECTURE

Implement the infrastructure foundation for the project's PostgreSQL database.

Support:

* production database cluster
* multi-AZ configuration where applicable
* private subnets
* encryption at rest
* TLS in transit
* security groups
* controlled ingress
* parameter configuration
* automated backup foundation
* monitoring integration
* failover capability
* environment separation

The database must not be publicly accessible.

Do not expose PostgreSQL directly to the internet.

# 7. DATABASE TOPOLOGY

The infrastructure must support application workloads according to the architecture's read/write requirements.

Where appropriate, provide:

* writer endpoint
* reader endpoint
* replicas
* failover target
* controlled connection endpoints

Do not create read replicas merely for theoretical scale if no workload or architecture requires them.

Where replicas are required, ensure application services can distinguish authoritative writes from read traffic.

# 8. DATABASE ENCRYPTION

Configure:

* encryption at rest
* KMS key integration where appropriate
* encrypted automated backups
* encrypted snapshots
* secure transport

Database credentials must be stored through the project's secrets architecture.

Do not place database passwords in:

* source control
* Dockerfiles
* infrastructure constants
* CI logs
* public environment files

# 9. DATABASE BACKUPS

Establish production backup foundations.

Support:

* automated backups
* appropriate retention
* point-in-time recovery capability where supported
* encrypted snapshots
* environment-specific retention
* backup observability

Do not claim backup recoverability without testing restore procedures in the appropriate later operational scope.

# 10. DATABASE CONNECTION MANAGEMENT

Infrastructure must support application connection behavior at scale.

Account for:

* connection limits
* service count
* worker count
* autoscaling
* connection pooling
* failover
* read replicas

Where appropriate, integrate RDS Proxy or equivalent managed connection pooling.

Do not solve connection pressure merely by increasing the database's maximum connection count without considering the resulting resource impact.

# 11. DATABASE NETWORK SECURITY

Restrict database access to explicitly authorized application and worker security groups.

Support:

* private subnets
* restricted ingress
* no public IP
* controlled egress
* TLS
* security-group segmentation

Do not allow unrestricted access from the VPC merely because the services are considered "internal."

# 12. REDIS ARCHITECTURE

Implement the Redis infrastructure foundation.

Use Amazon ElastiCache or the already established managed Redis platform.

Support:

* private networking
* encryption at rest
* encryption in transit
* authentication/access control
* high availability
* controlled failover
* subnet groups
* security groups
* environment isolation
* monitoring

Do not expose Redis publicly.

# 13. REDIS TOPOLOGY

Configure Redis according to actual application responsibilities.

Account for uses such as:

* cache
* session support where defined
* rate limiting
* ephemeral state
* realtime coordination
* distributed locks where explicitly defined

Do not assume Redis is the authoritative persistence layer for durable application data.

The PostgreSQL/event systems remain authoritative according to their respective contracts.

# 14. REDIS RESILIENCE

Where production architecture requires it, configure:

* replicas
* automatic failover
* Multi-AZ
* parameter groups
* maintenance behavior
* controlled upgrades

Document which Redis data is reconstructable and which state requires stronger durability guarantees.

Do not claim persistence requirements that contradict the architecture.

# 15. KAFKA / EVENT STREAMING

Implement the infrastructure foundation for project-wide event streaming.

Use Amazon MSK where Kafka is the established technology.

Support:

* private brokers
* multiple availability zones
* encryption in transit
* encryption at rest
* authentication
* authorization
* security groups
* broker monitoring
* environment isolation
* topic management foundation

Do not create public Kafka brokers.

# 16. KAFKA TOPIC MANAGEMENT

Create infrastructure-level support for the authoritative event taxonomy.

Topics should correspond to the established event contracts.

Examples may include domains such as:

* account events
* social-graph events
* content events
* engagement events
* media events
* feed events
* messaging events
* notification events
* moderation events
* analytics events

Do not invent new business events solely within infrastructure code.

Do not embed application business semantics into Terraform/OpenTofu modules unless the infrastructure itself requires them.

# 17. KAFKA SECURITY

Secure the event-streaming layer using:

* private networking
* encryption
* authenticated clients
* least-privilege access
* environment isolation
* restricted security groups

Application services must receive only the Kafka permissions they require.

Avoid broad wildcard topic permissions.

# 18. KAFKA RETENTION

Configure retention according to established event contracts and operational requirements.

Consider:

* event replay requirements
* consumer recovery
* storage cost
* compliance/data-lifecycle requirements
* analytics consumption
* failure recovery

Do not retain sensitive events indefinitely by default.

Do not delete events so aggressively that supported consumers cannot recover from outages.

# 19. QUEUE INFRASTRUCTURE

Implement SQS-based queue infrastructure where the architecture calls for durable asynchronous processing.

Support queues for appropriate worker workloads such as:

* media processing
* notifications
* moderation processing
* analytics ingestion
* search indexing
* other contract-defined asynchronous jobs

Use queue names and semantics aligned with the project's architecture.

Do not create a queue for every minor function without an architectural need.

# 20. DEAD-LETTER QUEUES

Every production-critical queue that can fail repeatedly should have an appropriate dead-letter strategy.

Support:

* DLQ
* redrive configuration
* retry limits
* visibility timeout
* retention
* monitoring
* alerting hooks where observability infrastructure supports them

Do not allow poison messages to retry forever.

# 21. QUEUE SECURITY

Secure queues using:

* encryption
* IAM access policies
* least privilege
* private service access where appropriate
* environment isolation

Workers must only consume queues they are authorized to process.

Producers must only send to permitted queues.

# 22. QUEUE SCALING FOUNDATIONS

Configure queue infrastructure to support workload-driven worker scaling.

Where architecture supports it, expose:

* queue depth metrics
* oldest-message age
* processing latency signals
* concurrency controls
* autoscaling signals

Do not implement worker autoscaling based only on CPU if queue backlog is the primary workload signal.

# 23. OPENSEARCH INFRASTRUCTURE

Implement the OpenSearch foundation required by discovery/search.

Support:

* private VPC deployment
* encryption at rest
* encryption in transit
* access control
* security groups
* appropriate node topology
* environment isolation
* domain configuration
* monitoring
* controlled endpoint access

Do not expose the OpenSearch endpoint publicly unless the architecture explicitly requires and secures public access.

# 24. OPENSEARCH CAPACITY

Provide a capacity model appropriate to expected workloads.

Consider:

* index count
* shard sizing
* replica count
* document volume
* query volume
* indexing throughput
* storage growth
* recovery requirements

Do not over-shard indices merely because high scale is anticipated.

Use capacity assumptions from the architecture artifacts.

# 25. SEARCH INDEX LIFECYCLE

Infrastructure should support safe:

* index creation
* versioned index migration
* alias-based cutover where applicable
* retention
* snapshot capability
* controlled reindex operations

Do not embed search ranking or application query logic in infrastructure configuration.

# 26. OPENSEARCH SECURITY

Implement:

* IAM or established authentication
* encryption
* private network access
* least-privilege access
* environment isolation
* restricted security groups

Search infrastructure must not become a path around application authorization.

# 27. MEDIA-PROCESSING INFRASTRUCTURE

Implement infrastructure foundations for asynchronous media processing.

Support:

* worker compute
* S3 integration
* processing queues
* temporary processing storage where required
* IAM roles
* CPU/memory sizing
* autoscaling hooks
* failure handling
* logging
* monitoring

The media-processing service must be able to consume authorized jobs and write only to permitted storage locations.

# 28. MEDIA PROCESSING ISOLATION

Separate processing workloads from request-serving workloads where appropriate.

Media-processing workers should have:

* dedicated scaling boundaries
* restricted network permissions
* restricted S3 permissions
* dedicated queue access
* independent failure handling

Do not allow expensive video-processing work to exhaust API-service resources.

# 29. MEDIA WORKER RESOURCE MANAGEMENT

Infrastructure must account for media workloads with materially different resource characteristics.

Support resource profiles appropriate for:

* image processing
* thumbnail generation
* video transcoding
* preview generation
* metadata extraction

Where workloads differ substantially, permit separate worker pools.

Do not run heavy video transcoding under the same resource constraints as lightweight API workers.

# 30. KMS AND ENCRYPTION

Use AWS KMS where the architecture requires customer-managed encryption keys.

Consider:

* database
* Redis
* Kafka
* S3
* queues
* OpenSearch
* secrets

Implement appropriate:

* key policies
* rotation strategy
* service permissions
* environment isolation

Do not create unnecessarily many encryption keys when a coherent key architecture is more operationally appropriate.

# 31. DATA LIFECYCLE

Implement infrastructure-level lifecycle policies where applicable for:

* S3 objects
* logs
* backups
* snapshots
* queue messages
* search storage
* event retention

Lifecycle policies must align with application data-retention contracts.

Do not delete user data through infrastructure lifecycle rules merely because it appears unused.

# 32. DATA CLASSIFICATION

Reflect application data classification in infrastructure decisions.

Distinguish appropriately between:

* public assets
* authenticated/private media
* sensitive user data
* operational logs
* analytics data
* moderation data
* credentials/secrets

Use stronger access restrictions for sensitive datasets.

# 33. DISASTER-RELATED FOUNDATIONS

This volume should establish the underlying infrastructure capabilities required for later disaster-recovery work.

Support where appropriate:

* database snapshots
* automated backups
* Kafka recovery capabilities
* OpenSearch snapshot foundations
* S3 versioning where required
* infrastructure reproducibility
* environment recreation

Do not claim that full disaster recovery is complete.

# 34. OBSERVABILITY FOUNDATIONS

Ensure the data infrastructure exposes useful operational metrics for later observability work.

Examples include:

### PostgreSQL

* CPU
* memory
* connections
* storage
* replication state
* latency
* I/O

### Redis

* memory utilization
* cache pressure
* connections
* replication
* evictions
* latency

### Kafka

* broker health
* throughput
* consumer lag
* storage
* partition health

### SQS

* queue depth
* oldest message age
* DLQ depth

### OpenSearch

* cluster health
* storage
* JVM/memory pressure
* indexing rate
* query latency

Do not implement the complete alerting strategy here if it belongs to the later observability scope.

# 35. PERFORMANCE AND SCALE

Infrastructure sizing must reflect the project's scale targets.

Consider:

* high API request volume
* large social graph
* high write rates
* feed fan-out
* media-heavy workloads
* large event volumes
* search growth
* high Redis access rates
* message workloads
* notification bursts

Do not size every service for theoretical maximum traffic at all times.

Use autoscaling and managed-service scaling capabilities where appropriate.

# 36. COST MANAGEMENT

Maintain commercially realistic infrastructure economics.

Account for:

* database instance sizing
* Redis node sizing
* Kafka broker/storage cost
* OpenSearch capacity
* NAT costs
* data transfer
* S3 storage
* CloudFront delivery
* media-processing compute
* queue throughput

Where appropriate:

* use lifecycle policies
* use autoscaling
* right-size non-production
* avoid unnecessary replicas
* avoid excessive log retention
* avoid excessive Kafka/OpenSearch capacity

Do not reduce required production redundancy solely to lower cost.

# 37. INFRASTRUCTURE TESTING

Add infrastructure-focused tests and validation for:

* database configuration
* Redis configuration
* Kafka configuration
* SQS/DLQ configuration
* OpenSearch configuration
* KMS policies
* IAM permissions
* storage lifecycle
* media-worker deployment definitions
* network isolation
* environment separation

Validate security assumptions through static policy checks where tooling exists.

# 38. CI/CD INTEGRATION

Integrate data-infrastructure deployment into the project's deployment pipeline.

Support:

* plan/preview
* validation
* security scanning
* controlled apply/deployment
* environment-specific variables
* artifact/version traceability
* protected production deployment

Do not allow application deployments to silently mutate data infrastructure without an explicit infrastructure change.

# 39. OUT OF SCOPE

Do not implement:

* application SQL queries
* database repositories
* ORM/business logic
* Redis cache code
* Kafka producer/consumer business logic
* application queue handlers
* OpenSearch query/ranking logic
* media transcoding algorithms
* full observability/alerting platform
* complete disaster recovery procedures
* load/performance testing at production scale
* unrelated frontend/mobile functionality

Those responsibilities belong to application or later infrastructure scopes.

# 40. DOCUMENTATION

Update infrastructure documentation covering:

* PostgreSQL topology
* backups
* connection architecture
* Redis topology
* Kafka topology
* queue/DLQ design
* OpenSearch topology
* media-processing worker infrastructure
* KMS/encryption
* data lifecycle
* security boundaries
* scaling assumptions
* operational prerequisites
* external AWS requirements

Document actual infrastructure configuration.

# 41. IMPLEMENTATION DISCIPLINE

Do not:

* expose PostgreSQL
* expose Redis
* expose Kafka
* expose OpenSearch unnecessarily
* use broad IAM permissions
* commit credentials
* hardcode database passwords
* store secrets in image layers
* create public S3 access for private media
* use infinite queue retries
* create unbounded Kafka retention
* create arbitrary indexes/shards without capacity justification
* create fake managed-service resources
* leave TODO/FIXME placeholders for required infrastructure
* claim successful provisioning without verification

Where live AWS access is unavailable, implement reproducible infrastructure definitions and accurately report deployment limitations.

# 42. VALIDATION

Before considering the implementation complete:

* run IaC formatting
* run IaC validation
* run security/policy scans
* validate PostgreSQL configuration
* inspect database network access
* inspect encryption configuration
* inspect backup configuration
* inspect Redis network/access controls
* inspect Redis encryption
* inspect Kafka security
* inspect Kafka topology
* inspect queue/DLQ policies
* inspect OpenSearch access/security
* inspect media-worker resource configuration
* inspect KMS policies
* inspect lifecycle policies
* inspect IAM permissions
* validate deployment definitions
* run relevant infrastructure tests
* inspect cost-sensitive configuration
* verify environment isolation

Do not claim live resource health unless actual cloud resources were inspected.

# 43. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the database, Redis, Kafka, queue, OpenSearch, media-processing, KMS, and data-lifecycle infrastructure actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Infrastructure Components

Identify the concrete managed services, modules, policies, security groups, and deployment definitions added or changed.

## Tests

List infrastructure tests, IaC validation, security scans, and policy checks actually executed.

## Validation

List local, static, security, configuration, and live-cloud validation actually performed.

## External Dependencies

Identify required AWS accounts, permissions, domains, services, credentials, or provider capabilities not available during execution.

## Important Decisions

Document significant infrastructure decisions and tradeoffs.

## Limitations

Document genuine limitations.

Do not represent unverified infrastructure as provisioned or healthy.

# 44. DEFINITION OF DONE

This prompt is complete only when:

* PostgreSQL infrastructure is production-oriented and private
* high-availability/failover foundations are configured
* backup/encryption foundations exist
* database connection architecture is addressed
* Redis infrastructure is private and secured
* Redis resilience foundations are configured
* Kafka/MSK infrastructure is secured and multi-AZ where appropriate
* queue infrastructure and DLQs are implemented where required
* queue security and retry behavior are defined
* OpenSearch infrastructure is private and secured
* search capacity foundations reflect architecture assumptions
* media-processing worker infrastructure is isolated and scalable
* KMS/encryption integration is established
* lifecycle policies respect application retention requirements
* infrastructure metrics are exposed for later observability
* environment isolation is preserved
* IAM remains least privilege
* no secrets are committed
* no public data services are exposed unnecessarily
* no fake infrastructure resources remain
* no required TODO/FIXME placeholders remain
* documentation reflects actual infrastructure
* live infrastructure is never claimed as healthy unless actually verified

# 45. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production infrastructure engineering task.

Do not expand into the later infrastructure responsibilities or application domains listed as out of scope.

Do not ask the user to choose among infrastructure approaches when the architecture and repository establish the appropriate direction.

Make reasonable AWS infrastructure decisions based on the project's architecture, scale targets, data contracts, and operational requirements.

Where real cloud access or external credentials are unavailable, implement everything that can be represented reproducibly in infrastructure code and report the limitation accurately.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
