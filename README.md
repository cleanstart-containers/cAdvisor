# CleanStart Container for cAdvisor

cAdvisor (Container Advisor) provides container users with resource usage and performance characteristics of running containers. It is a running daemon that collects, aggregates, processes, and exports information about running containers. Specifically, for each container it keeps resource isolation parameters, historical resource usage, histograms of complete historical resource usage and network statistics. This container includes enterprise-grade security hardening and monitoring capabilities optimized for production deployments.

**📌 CleanStart Foundation:** Security-hardened, minimal base OS designed for enterprise containerized environments.

**Image Path:** `ghcr.io/cleanstart-containers/cadvisor`

**Registry:** CleanStart Registry

---

## Overview

cAdvisor (Container Advisor) is a running daemon that collects, aggregates, processes, and exports information about running containers. It provides container users with resource usage and performance characteristics, making it an essential tool for container monitoring and observability in production environments.

---

## Key Features

Core capabilities and strengths of this container:

- Real-time container resource monitoring and metrics collection
- Native Prometheus metrics endpoint integration
- Historical performance data analysis and storage
- Enterprise-grade security with RBAC support
- Resource isolation parameters tracking
- Network statistics collection
- Complete historical resource usage histograms

---

## Common Use Cases

Typical scenarios where this container excels:

- Container resource usage monitoring in production environments
- Performance analysis and capacity planning for containerized applications
- Resource utilization tracking for Kubernetes clusters
- Container metrics collection for observability platforms
- Troubleshooting container performance issues
- Infrastructure monitoring and alerting

---

## Quick Start

### Pull Latest Image

Download the container image from the registry:
```bash
docker pull ghcr.io/cleanstart-containers/cadvisor:latest
docker pull ghcr.io/cleanstart-containers/cadvisor:latest-dev
```

### Basic Run

Run the container with basic configuration:
```bash
docker run -d --name cadvisor \
  -v /:/rootfs:ro \
  -v /var/run:/var/run:ro \
  -v /sys:/sys:ro \
  -v /var/lib/docker/:/var/lib/docker:ro \
  -v /dev/disk/:/dev/disk:ro \
  -p 8080:8080 \
  ghcr.io/cleanstart-containers/cadvisor:latest
```

### Production Deployment

Deploy with production security settings:
```bash
docker run -d --name cadvisor-prod \
  --read-only \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  -v /:/rootfs:ro \
  -v /var/run:/var/run:ro \
  -v /sys:/sys:ro \
  -v /var/lib/docker/:/var/lib/docker:ro \
  -v /dev/disk/:/dev/disk:ro \
  -p 8080:8080 \
  ghcr.io/cleanstart-containers/cadvisor:latest
```

### Volume Mount

Mount required system directories for monitoring:
```bash
docker run -d \
  -v /:/rootfs:ro \
  -v /var/run:/var/run:ro \
  -v /sys:/sys:ro \
  ghcr.io/cleanstart-containers/cadvisor:latest
```

### Port Forwarding

Run with metrics endpoint exposed:
```bash
docker run -d -p 8080:8080 ghcr.io/cleanstart-containers/cadvisor:latest
```

---

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PATH` | `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` | System PATH configuration |
| `CADVISOR_PORT` | `8080` | Port for the cAdvisor metrics endpoint |
| `CADVISOR_STORAGE_DURATION` | `2m0s` | How long to keep data in memory |

---

## Security & Best Practices

### Recommended Security Context
```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  runAsGroup: 1000
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop: ['ALL']
```

### Best Practices

- Use specific image tags for production (avoid latest)
- Configure resource limits: memory and CPU constraints
- Enable read-only root filesystem when possible
- Run containers with non-root user (--user 1000:1000)
- Use --security-opt=no-new-privileges flag
- Regularly update container images for security patches
- Implement proper network segmentation
- Monitor container metrics for anomalies

---

## Architecture Support

CleanStart images support multiple architectures to ensure compatibility across different deployment environments:

- **AMD64**: Intel and AMD x86-64 processors
- **ARM64**: ARM-based processors including Apple Silicon and ARM servers

### Multi-Platform Images
```bash
docker pull --platform linux/amd64 ghcr.io/cleanstart-containers/cadvisor:latest
docker pull --platform linux/arm64 ghcr.io/cleanstart-containers/cadvisor:latest
```

---

## Resources

- **Official Documentation:** https://github.com/google/cadvisor
- **Provenance / SBOM / Signature:** https://images.cleanstart.com/images/cadvisor
- **Docker Hub:** https://hub.docker.com/r/cleanstart/cadvisor
- **CleanStart All Images:** https://images.cleanstart.com/images/cAdvisor/details
- **CleanStart Community Images:** https://hub.docker.com/u/cleanstart

---

## Vulnerability Disclaimer

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

**Security remains a shared responsibility:** CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
