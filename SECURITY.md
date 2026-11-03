# Security policy

`uds` is a message-layer codec, not a vehicle authorization system. Its builders can encode requests for security access, ECU reset, routine control and programming operations, but it does not authorize those operations or decide whether a vehicle may safely execute them. Applications must implement their own authentication, transport timeouts, session state and operational safety checks.

## Reporting vulnerabilities

Use GitHub's **Report a vulnerability** / private security advisory flow for this repository if available. Otherwise contact the maintainer privately before publishing a reproducible exploit. Do not include live ECU credentials, personal data, proprietary firmware, production VINs, or customer trace files. A minimal synthetic payload with the affected function, expected behavior and impact is preferred.

## Supported versions

Security fixes target the latest released source in the [Racket Package Catalog](https://pkgs.racket-lang.org/package/uds) and the repository's default branch. Older versions are not guaranteed to receive backports. Review the current catalog checksum and build results when validating a fix; a passing GitHub CI run does not prove that the catalog has picked up the update.
