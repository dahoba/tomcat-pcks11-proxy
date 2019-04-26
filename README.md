# Tomcat with PKCS11-proxy

Tomcat with PKCS11-proxy enabled; to use web application with SoftHSM or HSM device

This contain

- Tomcat 8.5 jre-8-alpine
- PKCS11-proxy compiled
- stunnel install for secure connection between SoftHSM and this container

## Build

OS with pcks11-proxy installed
```
docker build --rm -t dahoba/tomcat-pcks11-proxy .
```

OS with Sarabun fonts installed. suitable for application that use jasper libary
```
docker build --rm -f "8-alpine-fonts/Dockerfile" -t dahoba/tomcat-pcks11-proxy:8-alpine-fonts .
```