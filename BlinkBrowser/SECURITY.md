# Blink security notes

## Controls enabled

- Safe Browsing is enabled on WebView instances.
- SSL/TLS certificate errors are cancelled; there is deliberately no "continue anyway" code path.
- Mixed content is set to `MIXED_CONTENT_NEVER_ALLOW`.
- `allowFileAccess` and `allowContentAccess` are disabled for page content.
- No `addJavascriptInterface` bridge is exposed to web pages.
- Incognito tabs use a separately named AndroidX WebKit profile when `MULTI_PROFILE` is supported; otherwise Blink refuses to create an incognito tab rather than silently pretending it is private.
- Private URLs are omitted from the saved normal-tab session and local history.

## Threats not solved by these controls

- DDoS attacks against a service require defenses at the service/network edge. This app has no Blink-operated public web server or relay.
- A user visiting explicit `http://` URLs accepts that traffic may be readable or modifiable by a network attacker. HTTPS content's insecure subresources are blocked, but that does not encrypt a page whose main URL is HTTP.
- WebView inherits the installed Android System WebView/Chromium engine. Keep Android and System WebView updated.
- A malicious site may still exploit a browser-engine vulnerability before a patch exists. This is why minimum permissions, regular updates, Safe Browsing, and an external security review matter.
- Browser extensions, a full password manager, certificate pinning, VPN/proxying, anti-fingerprinting, and a remote malware reputation service are not implemented.

## Release checklist

Before calling Blink production-ready: audit dependencies and licenses; enable dependency vulnerability monitoring; inspect the merged manifest; run Android Lint; test current Android versions; verify popup handling, cookies, private-profile cleanup, file uploads, MIME types and duplicate download names; add crash reporting only with consent and privacy review; sign a release build; and commission independent security testing.
