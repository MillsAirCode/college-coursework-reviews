# CS305-SSL-Server-Application

https://github.com/MillsAirCode/CS305-SSL-Server-Application

## what it was

Built this for CS-305 (Software Security) at SNHU. The assignment was to configure a Spring Boot web server with HTTPS using a self-signed keystore and add a SHA-256 hashing endpoint. The fictional client was "Artemis Financial" — SNHU's simulated company for the whole module. Spring Boot 2.2.4 on Java 8, single endpoint at `/hash` that returns a hardcoded name hashed with SHA-256.

## what holds up

The SSL keystore configuration in `application.properties` is still correct — `key-alias`, `key-store-password`, `key-store`, `key-store-type` are the right properties for a JKS keystore on port 8443. The OWASP dependency-check-maven plugin in `pom.xml` was ahead of its time for a college project. I still think running dependency scans as part of the build is worth doing, even if version 5.3.0 is ancient now.

The `bytesToHex` method with BigInteger and manual zero-padding actually works fine. It's not the prettiest way to hex-encode a byte array, but it's correct and doesn't pull in extra dependencies.

## what I'd refactor

The controller is defined as an inner class inside the main application class. `SslServerController` is declared right after `SslServerApplication` in the same file. I'd split that into its own file immediately. The `@RestController` annotation on a package-private inner class works, but it's confusing and makes the file do two things.

Everything is hardcoded. The name, the static data string, the cipher algorithm — nothing is parameterized. The endpoint takes no query params, no path variables. It just returns the same response every time. At minimum I'd add a `?name=` query parameter so it's actually a useful endpoint.

The response is raw HTML with `</br>` tags stuffed into a String return. Spring Boot can return JSON out of the box with a proper DTO or even a `Map`. Returning HTML from a `@RestController` is a leftover from `@Controller` + `@ResponseBody` days.

The test is just `contextLoads()` — the default Spring Boot test stub. No actual verification that `/hash` returns anything useful. I'd add at least a MockMvc test hitting the endpoint and checking the response contains a 64-character hex string.

The FIXME comment on line 27 is still there. I left the instructor's placeholder comment in the submitted code.

## portfolio take

Archive it. It demonstrates basic HTTPS config and SHA-256 usage, which is what the course asked for, but there's nothing here that shows engineering judgment beyond following a scaffold.
