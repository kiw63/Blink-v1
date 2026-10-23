# Blink manual test plan

This is a test plan, not a claim that these tests have already passed.

## Address and navigation

- Open `https://www.google.com` and `http://example.com` from the address field.
- Enter plain words and confirm the selected search engine opens.
- Open a long URL and a URL with query parameters, fragments, ports, and non-English characters.
- Test redirects, back, forward, reload, home, external `mailto:`/`tel:` links, and unsupported custom schemes.
- Tap `target=_blank` links and verify the popup becomes a new Blink tab.

## Tabs and privacy

- Create multiple normal tabs, switch between them, close one and close the final tab.
- Open a private tab. If the installed WebView does not support multi-profile, verify Blink explains that rather than opening a normal tab.
- In private mode, sign in to a test site, check cookies/storage separation from normal mode, close the last private tab, and verify its session data is removed.
- Force-close and relaunch Blink to check normal-session restore and confirm private tabs are not restored.

## Bookmark and history

- Add a bookmark, add the same URL again, open it, share its link, and delete it.
- Visit several URLs, verify the normal history list, remove one item, and clear all history.
- Verify private visits do not enter the local history or saved session.

## Downloads and uploads

- Download a PDF, image, ZIP, and APK from trusted direct links; check progress and Android download notifications.
- Open a completed file, share it as a file attachment, cancel an in-progress download, and remove a failed download from the list.
- Test duplicate filenames, interrupted downloads, expired-login downloads, large files, metered networks, and low-storage conditions.
- Test websites with single-file and multi-file upload inputs.
- Confirm blob-based downloads and protected streaming services report their limitations rather than falsely claiming success.

## Security and resilience

- Confirm invalid HTTPS certificates are rejected with no bypass option.
- Confirm a known-safe HTTPS page with HTTP mixed subresources does not load those insecure subresources.
- Inspect WebView settings to ensure no JavaScript bridge exists and local file access stays disabled.
- Test offline mode, captive portals, DNS failures, process death, rotation, and WebView renderer crashes.
- Run Android Lint, dependency checks, and independent security review before distributing broadly.
