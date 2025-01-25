---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Authentication

{% hint style="info" %}
For detailed information about required headers and their format, please see the \[Headers Overview]\(/users/api-documentation/introduction/README.md).
{% endhint %}

## Authentication Methods

There are two ways to authenticate:

1. PlyrID Authentication
   * Requires PlyrID and 2FA token
   * Returns a session JWT valid for 24 hours by default
2. InstantPlayPass Authentication
   * Quick authentication for instant play
   * No registration required

## Common Flows

### Standard Authentication Flow

1. Authenticate using PlyrID or InstantPlayPass
2. Store received sessionJwt
3. Authenticate with sessionJwt for subsequent requests
