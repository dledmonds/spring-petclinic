# Security Issues
Note that this fork of Pet Clinic has some security issues deliberately created for the purpose of discovery by SAST scan tools, do not use!

## Issues

## Cryptography
- src/main/java/org/springframework/samples/petclinic/owner/OwnerController.java:170, Risky/broken algorithm. ECB mode and NoPadding in use.
- src/main/java/org/springframework/samples/petclinic/owner/OwnerController.java:171, Hardcoded key.
- See recommended setup at https://www.veracode.com/blog/research/encryption-and-decryption-java-cryptography

## Log Forging
- src/main/java/org/springframework/samples/petclinic/owner/OwnerController.java:179, Log entry based on user input, very unlikely attack vector as the encrypted value is output

## Open Redirect
- src/main/java/org/springframework/samples/petclinic/owner/OwnerController.java:185, new method that redirects to a URL passed in as a GET param

### XSS
- src/main/resources/templates/owners/ownerDetails.html:15, use of th:utext is an XSS risk, use th:text to automatically html encode
- src/main/java/org/springframework/samples/petclinic/owner/OwnerController.java:159, new method that defaults to text/html content-type, so XSS risk.

### General
- When the application is started (eg. `mvn spring-boot:run`) the h2 database console is exposed via http://localhost:8080/h2-console - why is this not discovered as a flaw?
