# Stage 06 evidence

This folder is reserved for reviewed screenshots from the vulnerable web application and Wazuh archive validation.

Screenshots are pending transfer. Add them only after checking that they do not expose credentials, tokens, private configuration, sensitive host paths or full Docker container identifiers.

Planned evidence:

1. Vulnerable web application running in the browser.
2. Harmless `whoami` request submitted to the application.
3. Matching Docker log or Wazuh archive event.
4. Discover result showing the event collected under agent `007` and indexed in `wazuh-archives-*`.

The current verified result is documented in [Stage 06](../../docs/lessons/lesson-06-threat-hunter-lab-improvements.md).
