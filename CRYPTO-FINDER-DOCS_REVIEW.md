# Documentation Audit: Crypto Finder
**Reviewer:** Andrés Ibarra (Lead Technical Engineer)
**Status:** Verification Pending (Permission Issue)

## 1. Validation Status: Blocked
During the technical audit of the [Crypto Finder Getting Started](https://scanoss.mintlify.app/en/latest/crypto-finder/getting-started/overview) guide, I was unable to fully verify the accuracy of the scanning results and the effectiveness of the documentation.

![crypto-call header](image-3.png)
![crypto-call error](image-4.png)

**Issue Identified:**
The scanning process fails during the ruleset download phase. Specifically, the engine returns a **404 Not Found** error when attempting to fetch the `dca@latest` ruleset.

**Technical Root Cause:**
After performing a manual `curl` diagnostic to the API endpoint:

* **Without API Key:** Returns `401 Unauthorized`.
![API-call wo Key](image-5.png)

* **With Current API Key:** Returns `404 Not Found`.
![API-call w key](image-6.png)

**Conclusion:**
This indicates that the API endpoint is reachable, but the current API Key lacks the necessary permissions or "Premium Dataset" entitlements to access Cryptography resources. 

## 2. Recommendations for the Documentation Team
Once the permission issue is resolved, I suggest adding a **"Pre-flight Access Check"** section to the guide. This would help users identify if their API Key is correctly provisioned for Crypto scanning *before* they attempt to run a large-scale audit, preventing the "resource does not exist" confusion.

---
## UPDATE:

Retried setting again the API URL, because the url referred in the stdio error shows the `/scan`, after trying to curl another endpoint with the same key, it works, so it should have been an error setting up the environment variables.

In this case is not a documentation issue, so from the tool's side it might be good to include a verification of the source url the ruleset is trying to be downloaded to catch the error.