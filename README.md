CAS Overlay Template
============================

Generic CAS maven war overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS maven war overlays. The CAS services management overlay is available [here](https://github.com/Jasig/cas-services-management-overlay).

# Versions
```xml
<cas.version>4.2.2</cas.version>
```

# Requirements
* JDK 1.7+

# Configuration

The `etc` directory contains the configuration files that need to be copied to `/etc/cas`.

Current files are:

* `cas.properties`
* `log4j2.xml`

# Build

```bash
mvnw clean package
```

or

```bash
mvnw.bat clean package
```

# Deployment

## Embedded Jetty

Create a Java keystore at `/etc/cas/jetty/thekeystore` with the password `123456`.
```bash
sudo keytool -genkey -alias thekeystore -keyalg RSA -validity 365 -keystore thekeystore.keystore
sudo keytool -export -alias thekeystore -file thekeystore.crt
```

Import your CAS server certificate inside this keystore.
```bash
sudo keytool -import -file thekeystore.crt -keystore $JAVA_HOME/jre/lib/security/cacerts -alias thekeystore
```

```bash
mvnw jetty:run-forked
```

CAS will be available at:

* `http://cas.server.name:8080/cas`
* `https://cas.server.name:8443/cas`

## External
Deploy resultant `target/cas.war` to a Servlet container of choice.
