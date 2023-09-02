# whoami-consul-example

In this example we register the `whoami` server (http and https) to consul and query using consul as gateway.

## Concepts

### Service Discovery

Discover, track, and monitor the health of services within a network.
Service discovery registers and maintains a recod of services in a catalog.

Can be useful for

- Dynamic IP address and port discovery
- Horizontal Service Scaling
- Reliable service connection ensured by health checks

There are two types of service discovery patterns

1. Client Side Discovery
    1. Consumer queries the service catalog.
    2. Catalog returns all access information (if X instances are present for a service in catalog, it will return all).
    3. Consumer can select which service (among X) it needs to query.
    4. Can also be called client side load balancing.
2. Server Side Discovery
    1. Consumer queries the intermediary service
    2. Intermediary service queries catalog and rout requests to the available service instances

### Service Mesh

Dedicated network layer that provides **secure** service to service communication within and across infrastructure.

Benefits would include

- Service Discovery
- Load Balancing
- Automatic failover
- Traffic Management
- Encryption
- Observability and Traceability
- Authentication and Authorization
- Network Automation

Typically consists of two things

1. Control Plane (Service Discovery)
2. Data Plane
    1. Handles communication between the services (TLS / Load Balancing / Metrics).
    2. Generally a sidecar proxy to deployed to handle data plane communication, and thus limit level of awareness the sevices need to have about the network environment


## Consul

Service Definition: https://developer.hashicorp.com/consul/docs/services/usage/define-services#define-service-defaults

## TODO

- tls: failed to verify certificate: x509: certificate relies on legacy Common Name field, use SANs instead
- Query using consul as gateway
