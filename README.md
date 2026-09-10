# wPlugin-flipa-SSRF-report
# SSRF in viewer.html

**Title:** [Flipa — PDF Flipbook 0.18.3] Server-Side Request Forgery (SSRF) via pdf parameter in viewer.html

**Vulnerability Type:** Server-Side Request Forgery (CWE-918)

**CVSS 3.1 Vector:** **CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N** **Base Score: 5.3 Medium**

**Description:** The viewer.html file accepts a user-controlled pdf parameter and loads it without sufficient validation or sanitization. This allows unauthenticated attackers to make the server (or browser context) request arbitrary URLs, including internal network addresses.

**Proof of Concept:** Normal request: http://wpflipa.test/wp-content/plugins/flipa-pdf-flipbook/assets/viewer.html?pdf=http://wpflipa.test/wp-content/uploads/...

SSRF test (internal port scanning):

- Open port (e.g. http://127.0.0.1:3306): Instant error "Could not read this PDF: Failed to fetch"

please look the video.

- Closed port (e.g. http://127.0.0.1:3307): Delayed error (1~2 seconds) with same message

please look the video.

This time difference allows **port scanning** on localhost and potentially the internal network. Further attacks may be possible.
