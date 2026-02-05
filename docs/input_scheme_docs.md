# Input Schema Documentation

This document explains each section of the `input_schema.json` used by **Ai-GRC-Agent**.

-----
## Top-Level Structure

The input configuration is a single JSON object with the following required top-level keys:

- `system`
- `network`
- `security`
- `applications`
- `compliance`
- `intent`

---

### System

Describes the host or environment being analyzed.

#### Fields

- `hostname`: Unique identifier for the system.
- `environment`: Deployment context.
  - `production`, `staging`, `development`, `test`
- `os`: Operating system details.
  - `name`: OS name (e.g., Ubuntu)
  - `version`: OS version
  - `kernel`: Kernel version (optional)
  - `architecture`: CPU architecture (`x86_64`, `arm64`, `aarch64`)
- `hardware` (optional):
  - `cpu_cores`: Number of CPU cores
  - `memory_gb`: Total system memory
  - `storage`: List of storage volumes
    - `mount`: Mount point
    - `type`: `ssd`, `hdd`, or `nvme`
    - `size_gb`: Size in gigabytes
    - `encrypted`: Whether the volume is encrypted

Used to assess baseline security posture, patching expectations, and compliance requirements tied to environment and architecture

-----

### Network

Defines networking exposure and controls.

#### Fields

- `interfaces`: Network interfaces
  - `name`: Interface name
  - `ip_address`: IPv4 address
  - `subnet`: Subnet mask
  - `gateway`: Default gateway (optional)
  - `public_facing`: Whether interface is internet-facing
- `dns_servers`: List of DNS resolvers
- `open_ports`: Exposed ports
  - `port`: Port number
  - `protocol`: `tcp` or `udp`
  - `service`: Service name (optional)
- `firewall` (optional):
  - `default_policy`: `allow` or `deny`
  - `rules`: Explicit firewall rules
    - `port`
    - `source`
    - `action`: `allow` or `deny`

Drives attack-surface analysis, exposure detection, and compliance checks related to network segmentation and access control


------

### Security

Captures security controls and defensive measures.

#### Fields

- `authentication`
  - `password_policy`
    - `min_length`: Minimum password length
    - `complexity_required`: Require letters, numbers, and symbols
    - `rotation_days`: Number of days before password must be changed
  - `mfa_enabled`: Multi-factor authentication enabled
  - `privileged_access_management`: Use of privileged access management tools

- `encryption`
  - `data_at_rest`: Encryption for stored data
  - `data_in_transit`: Encryption for network traffic
  - `tls_versions`: List of allowed TLS versions (e.g., 1.2, 1.3)
  - `weak_protocols_enabled`: List of deprecated or weak protocols still enabled

- `monitoring` (optional)
  - `logging_enabled`: Whether logging is active
  - `log_retention_days`: Number of days logs are retained
  - `ids_enabled`: Intrusion detection system enabled
  - `siem_integrated`: Security Information and Event Management integration

- `patching` (optional)
  - `automatic_updates`: Whether OS and applications auto-update
  - `last_patch_date`: Last date patches were applied
  - `known_unpatched_vulnerabilities`: List of CVEs or known vulnerabilities

Used to identify weak or strong security controls, assess risk, and provide actionable recommendations

------


### Applications

Defines application-layer services running on the system.

#### Fields

- `web_server` (optional)
  - `name`: Application name (e.g., nginx)
  - `version`: Application version
  - `ssl_enabled`: Whether SSL/TLS is enabled
  - `http_to_https_redirect`: Whether HTTP traffic is redirected to HTTPS
  - `cipher_suites`: List of allowed TLS cipher suites

- `database` (optional)
  - `name`: Database name (e.g., MySQL)
  - `version`: Database version
  - `encryption_enabled`: Encryption for stored data
  - `remote_access`: Whether remote access is allowed
  - `backup`
    - `enabled`: Backups enabled
    - `encrypted`: Backups encrypted
    - `retention_days`: Retention period for backups

Provides context for application-specific security and compliance checks

-------

### Compliance

Provides regulatory and organizational context.

#### Fields

- `organization`
  - `industry`: Industry sector (e.g., finance, healthcare)
  - `company_size`: `small`, `medium`, `enterprise`

- `jurisdiction`: List of applicable jurisdictions or regions (e.g., US-Federal, EU)

- `regulations`: List of regulations to evaluate against (e.g., PCI-DSS, HIPAA)

- `data_types`: Types of data processed
  - Examples: `PII`, `PHI`, `financial_records`, `authentication_credentials`

- `audit_history` (optional)
  - `last_audit_date`: Date of the most recent audit
  - `open_findings`: List of unresolved audit findings
    - `id`: Unique finding identifier
    - `severity`: `low`, `medium`, `high`, `critical`
    - `description`: Text describing the finding

Enables mapping of system status to regulatory requirements and highlights compliance gaps.

-----------

### Intent

Controls how the agent processes the input and generates output.

#### Fields

- `analysis_type`: List of requested analyses
  - `security_assessment`
  - `compliance_check`
  - `recommendations`

- `output_detail_level`: Level of detail in output (`low`, `medium`, `high`)

- `regulation_only`: If `true`, the agent returns only applicable regulations without analyzing the system

Determines the workflow path and output scope of the agent.
