# Contributing to uds

Thank you for helping improve the Racket ISO 14229 message codec.

## Scope and compatibility

This package represents ISO 14229-1 application payloads; it does not operate a CAN interface, manage an ISO-TP session, implement ECU-specific SecurityAccess algorithms, or enforce P2/P2* timeouts. Avoid expanding the public API with transport- or ECU-specific assumptions. Changes to existing return values, exceptions, record layouts, or exports require a compatibility explanation.

## Reproducing checks

Use a current stable Racket release. In a clean checkout:

```sh
raco pkg install --auto --link "$(pwd)"
raco test -p uds
racket uds/examples/quickstart.rkt
raco setup --check-pkg-deps -l uds
```

The CI workflow runs the equivalent checks on Linux, macOS, and Windows. The official Racket package builder also performs a clean package install, a Scribble build, and a separate `raco test --drdr --package uds` pass. A passing local checkout alone does not verify the published catalog checksum or build-server status.

## Protocol change checklist

1. Identify the exact ISO 14229-1 edition or public interoperability reference and distinguish mandatory behavior from OEM-specific behavior. Do not add copyrighted standard text to the repository.
2. Add positive, negative, truncated, oversized and out-of-range byte-vector tests where applicable. Use explicit byte literals; assert the full encoded payload, not just its length.
3. Test round trips only alongside independent golden vectors, so an encoder and decoder cannot validate one another's identical mistake.
4. Update the Scribble API reference for new exports, contracts, byte ordering, units, exceptions and limitations. Update README and `uds/examples/quickstart.rkt` only if the public workflow changes.
5. Review interoperability with the separately published `isotp` and `obd2` packages for changes in shared assumptions or module paths.
6. Keep generated files out of commits. In particular, `uds/doc/` and `compiled/` are build outputs. The source of the public manual is `uds/scribblings/uds.scrbl`.

## Pull requests

Keep changes focused. Explain behavior and compatibility, link the relevant issue if any, and include a reproducing test for bug fixes. Do not commit vehicle traces, secrets, ECU seed-key material, or confidential OEM specifications. Report security-sensitive issues privately as described in [SECURITY.md](SECURITY.md).
