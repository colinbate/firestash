---
"@firestash/api": patch
---

Advertise tarball URLs on the origin the package metadata is requested from, the way public registries do. npm publishes `dist.tarball` with an `http://` scheme and the host the publisher had configured, and the registry used to serve that value back unchanged, so installers were sent to `http://` URLs (and relied on a redirect to reach the registry over HTTPS). The stored path is kept; only the scheme and host are replaced on read, so existing packages are fixed too and the registry can move domains.
