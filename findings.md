# Incident Findings

## Initial Access

The authentication logs showed a failed root login followed shortly afterward by a successful root login from the same external IP address.

This indicated that an unauthorized user likely gained access to the system through SSH using the root account.

## Malicious Activity

A malicious shell script named `update-agent.sh` was identified during system triage.

The script repeatedly contacted an external endpoint using `curl` and immediately executed the downloaded content with `sh`.

The script repeated this behavior every 60 seconds, which was consistent with malicious beaconing or command-and-control activity.

## Remediation

The malicious script was removed, and the deployment user's home directory was restored to its expected structure.

Legitimate scripts and reports were reorganized into their proper directories, unnecessary cache files were removed, and the findings were documented.

## Hardening

SSH key-based authentication was configured and successfully tested using a new Ed25519 key pair.

A recommended security improvement would be to disable password-based SSH login for the root account and require key-based authentication instead.
