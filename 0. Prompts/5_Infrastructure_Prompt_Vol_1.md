# Instagram — Infrastructure Prompt — Volume 1

# 1. ROLE

You are the **Senior Infrastructure and DevOps Engineering implementation team** responsible for implementing the bounded infrastructure scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* AWS
* cloud networking
* containerized services
* infrastructure as code
* Kubernetes/container orchestration where justified
* managed databases
* Redis
* object storage
* CDN
* secrets management
* IAM
* TLS
* DNS
* environments
* CI/CD
* observability
* autoscaling
* reliability
* disaster recovery foundations
* security
* cost-aware infrastructure
* developer experience
* production operations

Your responsibility is to implement the assigned infrastructure scope completely and coherently inside the repository while preserving compatibility with the application's architecture, contracts, deployment model, and operational requirements.

Do not implement application business logic merely because infrastructure supports it.

Do not create fake infrastructure, placeholder deployment definitions, incomplete manifests presented as production-ready, hardcoded secrets, or configurations that silently assume unavailable cloud resources.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The target platform includes:

* web frontend
* iOS and Android mobile clients
* backend services
* PostgreSQL
* Redis
* event streaming
* background workers
* search
* object storage
* media processing
* CDN
* realtime communication
* notifications
* moderation
* analytics
* observability
* security
* reliability
* disaster recovery
* production deployment

The expected cloud direction is **AWS**, using managed services where they provide appropriate operational value.

The application targets large-scale production usage and must be deployed using infrastructure capable of supporting independently scalable application components.

This prompt is limited to the **core infrastructure foundation, environments, networking, compute orchestration foundation, configuration, IAM, secrets, storage foundations, and deployment prerequisites**.

# 3. CURRENT INFRASTRUCTURE ASSIGNMENT

Implement the infrastructure foundation required for the project.

This volume owns:

* infrastructure-as-code structure
* AWS account/environment model
* development/staging/production separation
* networking
* VPC structure
* subnets
* routing
* security groups
* private/public boundaries
* DNS foundations
* TLS foundations
* IAM
* workload identities
* secrets management
* parameter/configuration management
* container registry
* container image standards
* core compute/orchestration foundation
* object-storage foundation
* CDN foundation prerequisites
* infrastructure tagging
* environment configuration
* foundational CI/CD integration
* infrastructure validation
* drift-aware deployment discipline
* cost and security guardrails

Do not implement complete production scaling, disaster recovery, database operations, Redis operations, event infrastructure, or observability infrastructure beyond the foundational integration needed here when those responsibilities belong to later infrastructure volumes.

# 4. REPOSITORY INSPECTION

Before changing infrastructure, inspect the repository comprehensively.

At minimum inspect:

* repository structure
* backend services
* frontend applications
* mobile application
* worker processes
* Dockerfiles
* Docker Compose configuration
* package-management configuration
* environment files
* environment examples
* infrastructure directories
* existing Terraform/OpenTofu/CDK/CloudFormation files
* CI/CD workflows
* deployment scripts
* application configuration
* API contracts
* database configuration
* Redis configuration
* object-storage configuration
* media-processing configuration
* search configuration
* realtime configuration
* observability configuration
* test infrastructure
* documentation
* architecture artifacts

Identify what infrastructure already exists.

Do not replace working infrastructure simply because another architecture would also be possible.

Treat the repository and authoritative architecture artifacts as the source of truth for currently established services and dependencies.

# 5. TECHNOLOGY BASELINE

Use the infrastructure technology already established in the repository.

The expected cloud baseline is:

* AWS
* Infrastructure as Code
* Docker/container images
* managed AWS services where appropriate
* private networking for internal workloads
* IAM roles instead of long-lived access keys
* Secrets Manager and/or SSM Parameter Store according to secret/config classification
* ECR for container images
* CloudFront and S3 for applicable web/static/media delivery
* Route 53 for DNS where appropriate
* TLS certificates through ACM
* CI/CD through the project's established automation platform

Do not introduce multiple IaC systems unnecessarily.

Do not create cloud resources manually when the project expects reproducible infrastructure-as-code.

# 6. INFRASTRUCTURE-AS-CODE STRUCTURE

Create a maintainable IaC structure.

Separate concerns appropriately for:

* shared/global resources
* networking
* environment configuration
* IAM
* compute
* storage
* edge/CDN
* security
* application deployment
* environment-specific configuration

Use reusable modules/components where they materially improve consistency.

Avoid creating a single enormous infrastructure file containing the entire platform.

Use clear naming and tagging conventions.

# 7. ENVIRONMENT MODEL

Establish explicit infrastructure environments for:

* development
* staging
* production

Where the repository has a local-development environment, integrate it without forcing local developers to provision production infrastructure.

Environment separation must prevent:

* production credentials in development
* development workloads using production databases
* cross-environment secret reuse
* accidental production deployment from development workflows
* shared mutable resources without deliberate justification

Production must have explicitly protected deployment boundaries.

# 8. AWS ACCOUNT / ENVIRONMENT BOUNDARIES

Where the infrastructure model supports multiple AWS accounts, establish clear account responsibilities.

A typical production-grade model may separate:

* development
* staging
* production
* centralized/shared services where required

Do not fabricate AWS account IDs, credentials, organizational units, or live resources.

Where real account access is unavailable, implement the infrastructure definitions and document required external inputs.

# 9. NETWORK ARCHITECTURE

Implement the project VPC/network foundation.

Support appropriate:

* VPC
* availability zones
* public subnets
* private application subnets
* private data subnets where appropriate
* route tables
* internet gateway
* NAT strategy
* security groups
* network ACLs where justified
* VPC endpoints where materially valuable

Internal application services should not require public exposure merely to communicate with each other.

Avoid unnecessary public IP assignment.

# 10. AVAILABILITY ZONES

Design the production network for multi-AZ operation.

Use multiple availability zones for critical production workloads where the selected AWS service supports it.

Ensure that:

* public ingress can tolerate an AZ failure
* application workloads can be distributed across AZs
* critical managed services use multi-AZ capabilities where appropriate
* infrastructure does not accidentally concentrate critical components in one AZ

Do not claim multi-AZ availability for resources that are actually configured as single-AZ.

# 11. INGRESS AND EDGE FOUNDATIONS

Establish secure ingress for web and API workloads.

Use appropriate AWS services such as:

* Route 53
* CloudFront
* Application Load Balancer
* ACM
* WAF where appropriate

The exact topology must follow the application architecture.

Support:

* DNS
* TLS
* certificate management
* HTTP routing
* health checks
* secure transport
* edge termination
* origin protection

Do not expose internal services directly to the public internet when a private architecture is appropriate.

# 12. TLS AND CERTIFICATE MANAGEMENT

Implement certificate management using AWS-managed certificate infrastructure where appropriate.

Support:

* HTTPS
* certificate validation
* automatic renewal through the managed service
* environment-specific domains
* secure redirect behavior where applicable

Do not hardcode certificate contents or private keys into the repository.

# 13. IAM

Implement least-privilege IAM.

Establish roles/policies for:

* CI/CD
* infrastructure deployment
* application workloads
* background workers
* media processors
* storage access
* database-related infrastructure where required
* monitoring integrations
* administrative operations where appropriate

Avoid long-lived AWS access keys inside workloads.

Prefer IAM roles and short-lived credentials.

Do not grant wildcard administrative permissions merely to simplify development.

# 14. WORKLOAD IDENTITY

Ensure services receive only the AWS permissions they actually require.

For example:

* API services should receive only required S3/media permissions
* workers should receive only required queue/storage permissions
* frontend build roles should receive only required deployment permissions
* CI/CD should be separated from runtime workload identities

Document material permission boundaries.

# 15. SECRET MANAGEMENT

Implement secure secret management.

Classify configuration into:

### Public configuration

Safe for client/build exposure where genuinely public.

### Runtime configuration

Required by server workloads but not intended for client exposure.

### Secrets

Credentials, tokens, private keys, database passwords, provider secrets, and similar sensitive values.

Use appropriate AWS services such as:

* Secrets Manager
* SSM Parameter Store

Do not:

* commit secrets
* place secrets into Docker images
* place secrets in frontend bundles
* place secrets in Terraform state without appropriate protection strategy
* hardcode production credentials
* use example secrets that resemble real credentials

# 16. CONFIGURATION MANAGEMENT

Create a clear configuration model across environments.

Support:

* environment-specific configuration
* validation
* typed configuration where application tooling supports it
* secure injection
* clear naming
* versioning
* controlled changes

Document required external configuration inputs.

Do not silently provide fake default production credentials.

# 17. CONTAINER REGISTRY

Implement AWS ECR foundations for application images.

Support repositories appropriate for:

* backend/API services
* workers
* media processing services
* other independently deployable containers defined by the architecture

Configure appropriate:

* image naming
* lifecycle policies
* encryption
* access control
* immutable tagging strategy where appropriate
* image retention

Do not use `latest` as the sole production deployment identifier.

Prefer immutable image digests or versioned image tags.

# 18. CONTAINER IMAGE STANDARDS

Review and standardize Dockerfiles for production deployment.

Ensure:

* deterministic builds
* appropriate base images
* non-root execution where practical
* minimal runtime image
* dependency installation discipline
* health-check compatibility
* no secret embedding
* predictable startup
* correct signal handling
* appropriate logging to stdout/stderr

Do not rewrite application containers unnecessarily if existing Dockerfiles already meet the requirements.

# 19. COMPUTE / ORCHESTRATION FOUNDATION

Implement the core compute foundation appropriate to the project's architecture.

Use the selected AWS orchestration platform, such as:

* ECS/Fargate
* EKS
* another explicitly established AWS compute model

Do not introduce Kubernetes solely because the project is large.

The chosen orchestration layer must support:

* independent service deployment
* health checks
* rolling deployment foundations
* autoscaling hooks
* secret/config injection
* private networking
* service identity
* logging integration

# 20. SERVICE DEPLOYMENT BOUNDARIES

Infrastructure must allow major backend workloads to scale independently where architecture requires it.

Support distinct deployment units for appropriate workload classes such as:

* API
* realtime services
* background workers
* media-processing workers
* scheduled jobs

Do not collapse independently scalable workloads into one deployment solely for convenience.

# 21. HEALTH CHECKS

Configure infrastructure-level health checks based on actual application endpoints.

Support:

* startup considerations
* readiness
* liveness where applicable
* load-balancer health checks
* unhealthy-instance replacement behavior

Do not point health checks at arbitrary static endpoints that do not reflect application readiness.

Do not claim a service is healthy merely because its process started.

# 22. OBJECT STORAGE FOUNDATION

Implement S3 foundations for application-managed object data according to architecture.

Support appropriate buckets or prefixes for:

* user media
* processed media
* static web assets
* other contract-defined object classes

Configure:

* encryption
* private access
* lifecycle policies where appropriate
* versioning where required
* access control
* logging/auditing where appropriate
* cross-origin rules only where required
* public-access blocking by default

Do not make user media buckets public by default.

# 23. MEDIA STORAGE SECURITY

Storage infrastructure must support secure media delivery.

Ensure:

* private objects remain private
* application/client access uses authorized mechanisms
* storage credentials are not exposed
* CDN access is controlled
* direct object access is restricted where appropriate
* temporary signed access can be supported by the application architecture

Do not implement permanent public URLs for private media.

# 24. CDN FOUNDATION

Implement the CDN foundation required by web/static/media delivery.

Where appropriate, configure:

* CloudFront
* origin access controls
* cache behavior
* HTTPS
* compression
* allowed methods
* cache policies
* security headers
* environment-specific distributions where required

Do not cache authenticated/private responses publicly.

Distinguish public static assets from private user content.

# 25. WEB HOSTING FOUNDATION

Where the architecture uses S3/CloudFront for frontend static assets, establish:

* build artifact publishing
* versioned asset handling
* origin configuration
* invalidation strategy only where necessary
* secure bucket access

Do not expose the origin bucket publicly when CloudFront origin access can provide the required protection.

# 26. DNS

Establish environment-aware DNS.

Support:

* production domain
* staging domain
* development domain where appropriate
* API hostnames
* media/CDN hostnames
* verification records needed by managed services

Do not invent domains the user has not supplied.

Where domains are external inputs, use explicit variables/placeholders that do not masquerade as production values.

# 27. NETWORK SECURITY

Implement appropriate security-group boundaries between:

* load balancers
* application services
* workers
* databases
* Redis
* other internal services

Prefer explicit service-to-service access.

Avoid `0.0.0.0/0` ingress except where genuinely required for public endpoints.

Do not expose database or Redis ports publicly.

# 28. INFRASTRUCTURE TAGGING

Implement consistent tags/labels for resources.

At minimum support concepts such as:

* project
* environment
* service
* owner/team
* managed-by
* cost-center where available
* data classification where appropriate

Use naming/tagging consistently enough to support operational search and cost analysis.

# 29. COST GUARDRAILS

Infrastructure must remain commercially realistic.

Establish sensible controls such as:

* lifecycle policies
* log retention defaults
* object-storage lifecycle rules
* development resource sizing
* environment separation
* autoscaling foundations
* resource tagging
* avoidance of unnecessary NAT/egress costs where practical
* controlled non-production resource lifetimes

Do not optimize cost by weakening required production security or reliability.

# 30. CI/CD INFRASTRUCTURE FOUNDATION

Integrate infrastructure and application deployment with the repository's CI/CD system.

The foundation should support:

* code validation
* container build
* image publishing
* infrastructure validation
* environment deployment
* controlled production promotion
* deployment identity through short-lived credentials
* artifact traceability

Do not put long-lived cloud credentials directly into CI configuration.

# 31. DEPLOYMENT SAFETY

Establish protections against accidental production deployments.

Support where appropriate:

* branch/environment restrictions
* manual approval for production
* protected environments
* immutable artifacts
* deployment identity controls
* environment-specific configuration
* auditability

Do not rely solely on developer convention to protect production.

# 32. INFRASTRUCTURE VALIDATION

Infrastructure code must be validated before deployment.

At minimum use applicable checks for:

* syntax
* formatting
* static validation
* security scanning
* dependency scanning
* IaC linting
* policy checks
* plan/diff review
* container scanning

Do not report an infrastructure plan as safe merely because it parsed successfully.

# 33. STATE MANAGEMENT

If using Terraform/OpenTofu or equivalent stateful IaC:

* use remote state where appropriate
* protect state access
* encrypt state at rest
* control state permissions
* support locking where the tool provides it
* avoid placing secrets into state unnecessarily
* document state-management requirements

Do not commit production state files to the repository unless the architecture explicitly requires and protects them.

# 34. LOCAL DEVELOPMENT

Maintain a practical local-development path.

Where appropriate, provide:

* Docker Compose or equivalent
* local service dependencies
* development environment configuration
* local networking
* local object storage emulation only where appropriate
* development database connectivity
* clear startup commands
* local validation

Do not force developers to rely on production AWS resources merely to run the project locally.

# 35. ENVIRONMENT PROMOTION

The infrastructure design should support controlled promotion from:

* development
* staging
* production

Where immutable application artifacts are used, promote the same verified artifact rather than rebuilding arbitrary production variants.

Do not allow environment-specific source changes to undermine artifact traceability.

# 36. SECURITY

Infrastructure security must include:

* least privilege
* private networking
* encrypted storage
* TLS
* secure secret management
* restricted administrative access
* auditability
* dependency/image scanning
* no public databases
* no public Redis
* no hardcoded credentials
* security-group minimization
* secure CI/CD identity

Do not disable security controls to simplify deployment.

# 37. OBSERVABILITY FOUNDATION

Integrate application infrastructure with the project's observability architecture sufficiently to establish:

* centralized logs
* basic infrastructure metrics
* load-balancer metrics
* container/service health
* deployment visibility
* baseline alarms where already defined by the architecture

Do not fully implement the project's complete observability/alerting platform if it belongs to a later infrastructure volume.

Do not log secrets or sensitive application payloads.

# 38. RELIABILITY FOUNDATION

Establish infrastructure foundations for:

* multi-AZ application deployment
* health-based replacement
* safe rolling deployment
* failure isolation
* graceful service replacement
* availability checks
* infrastructure reproducibility

Do not claim disaster recovery is complete in this volume.

# 39. DOCUMENTATION

Update infrastructure documentation covering:

* AWS environment structure
* IaC directory structure
* environment model
* networking
* IAM
* secrets
* container registry
* deployment architecture
* storage
* CDN
* DNS
* local development
* CI/CD
* required external inputs
* deployment prerequisites
* security assumptions
* operational ownership

Document the infrastructure actually implemented.

# 40. OUT OF SCOPE

Do not implement the following beyond minimal integration required by this foundation:

* final PostgreSQL production architecture and operations
* final Redis production architecture
* Kafka/event-streaming infrastructure
* queue infrastructure
* complete media-processing infrastructure
* complete OpenSearch infrastructure
* full observability/alerting platform
* complete disaster recovery
* backup/restore operations
* production-scale load testing
* complete deployment optimization
* unrelated application code
* frontend feature work
* mobile feature work
* moderation business logic

These responsibilities belong to their dedicated planned infrastructure/implementation scopes.

# 41. IMPLEMENTATION DISCIPLINE

Do not:

* commit AWS secrets
* commit provider credentials
* embed production passwords
* create public databases
* create public Redis
* expose private S3 buckets
* use unrestricted security groups unnecessarily
* use mutable production image tags as the sole deployment identity
* create manual-only production infrastructure that cannot be reproduced
* leave required TODO/FIXME placeholders
* create fake Terraform resources
* create invalid Kubernetes/ECS definitions
* disable security scans merely to make CI pass
* claim resources were provisioned when they were not actually provisioned

Where external AWS access is unavailable, implement the IaC and accurately report what could not be deployed or verified.

# 42. TESTING

Add infrastructure-focused validation where supported.

Cover:

* IaC syntax
* IaC static validation
* formatting
* policy/security checks
* container build
* container scan
* environment configuration validation
* CI workflow validation
* deployment manifest validation
* security-group expectations
* secret-injection behavior
* local development startup
* infrastructure module/component tests where applicable

Do not rely exclusively on successful compilation.

# 43. VALIDATION

Before considering the implementation complete:

* run IaC formatting
* run IaC validation
* run security/policy scanning
* build container images
* scan container images where tooling exists
* validate deployment definitions
* validate CI/CD configuration
* verify configuration classification
* inspect IAM policies for excessive permissions
* inspect security groups for excessive exposure
* inspect S3 public-access settings
* inspect secret references
* inspect image-tag strategy
* inspect environment isolation
* verify local development path
* run relevant infrastructure tests
* review planned resource changes

Where AWS credentials or live cloud access are unavailable, do not claim that live deployment succeeded.

# 44. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the infrastructure foundation actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Infrastructure Components

Identify networking, IAM, secrets, registry, compute foundation, storage, CDN, DNS, and CI/CD infrastructure implemented.

## Tests

List infrastructure tests, IaC validation, scans, and configuration checks actually executed.

## Validation

List local, static, container, security, and deployment validation performed.

## External Dependencies

Identify required AWS accounts, domains, certificates, credentials, permissions, or other external inputs that were not available in the execution environment.

## Important Decisions

Document significant infrastructure decisions and tradeoffs.

## Limitations

Document genuine infrastructure limitations.

Do not represent unprovisioned resources as deployed infrastructure.

# 45. DEFINITION OF DONE

This prompt is complete only when:

* infrastructure-as-code structure is established
* development/staging/production environments are defined
* networking is implemented coherently
* multi-AZ foundations exist where appropriate
* public/private network boundaries are correct
* security groups are appropriately restricted
* IAM roles follow least privilege
* secrets/configuration management is established
* ECR foundations exist
* production container standards are applied
* compute/orchestration foundation is implemented
* service deployment boundaries are clear
* health checks are configured
* S3/storage foundations are secure
* CDN foundations are established where required
* DNS/TLS foundations are defined
* CI/CD integrates with infrastructure safely
* production deployment protections exist
* infrastructure validation and security checks exist
* local development remains practical
* documentation reflects actual infrastructure
* no secrets are committed
* no public databases or Redis resources are created
* no required TODO/FIXME placeholders remain
* no fake infrastructure resources remain
* live deployment is never claimed unless verified

# 46. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production infrastructure engineering task.

Do not expand into later infrastructure domains listed as out of scope.

Do not ask the user to choose among infrastructure approaches when the project architecture and repository establish the correct direction.

Make reasonable infrastructure decisions based on the existing architecture, contracts, and AWS production practices.

Where a real AWS account, domain, credential, or external service is required but unavailable, implement everything that can be represented reproducibly in code and report the external dependency accurately.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
