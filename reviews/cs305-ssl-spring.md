# CS-305 SSL Server (Spring Boot)

Spring Boot 2.2.4 on Java 8. Self-signed HTTPS keystore, one endpoint at `/hash` that returns a hardcoded name hashed with SHA-256. "Artemis Financial" was the fictional client. The OWASP dependency-check-maven plugin in the POM was actually ahead of its time for a student project.

The SSL config in `application.properties` is still correct. The `bytesToHex` method with BigInteger works fine.

The controller is an inner class inside the main application class. Everything is hardcoded - no query params, no dynamic input, same response every time. Returns raw HTML with `</br>` tags from a `@RestController`. The only test is the default `contextLoads()` stub. There's a FIXME comment from the instructor still in the code.

**Archive.** Demonstrates "I can configure HTTPS" and not much else.
