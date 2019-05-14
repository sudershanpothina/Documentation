download file
```
wget https://github.com/containous/traefik/releases/download/v1.7.11/traefik_linux-amd64
```
change traefik.toml
```
################################################################
#
# Configuration sample for Traefik v2
# For Traefik v1: https://github.com/containous/traefik/blob/v1.7/traefik.sample.toml
#
################################################################

################################################################
# Global configuration
################################################################
insecureSkipVerify = true
[global]
  checkNewVersion = true
  sendAnonymousUsage = false
  insecureSkipVerify = true
  debug = true
# Register Certificates in the rootCA.
#
# Optional
# Default: []
#
  rootCAs = [ "/opt/traefik/ucp-ca.pem", "/opt/traefik/ucp-6443.pem" ]
################################################################
# Entrypoints configuration
################################################################

# Entrypoints definition
#
# Optional
# Default:
[entryPoints]
    [entryPoints.http]
    address = ":80"

    [entryPoints.https]
    address = ":443"
      [entryPoints.https.tls]
        [[entryPoints.https.tls.certificates]]
          certFile = "/opt/traefik/ssl.crt"
          keyFile = "/opt/traefik/ssl.key"

     [entryPoints.api]
      address = ":32002"
        [entryPoints.api.tls]
          [[entryPoints.api.tls.certificates]]
            certFile = "/opt/traefik/ssl.crt"
            keyFile = "/opt/traefik/ssl.key"


################################################################
# Traefik logs configuration
################################################################

# Traefik logs
# Enabled by default and log to stdout
#
# Optional
#
[log]

# Log level
#
# Optional
# Default: "ERROR"
#
level = "DEBUG"

# Sets the filepath for the traefik log. If not specified, stdout will be used.
# Intermediate directories are created if necessary.
#
# Optional
# Default: os.Stdout
#
# filePath = "log/traefik.log"

# Format is either "json" or "common".
#
# Optional
# Default: "common"
#
# format = "common"

################################################################
# Access logs configuration
################################################################

# Enable access logs
# By default it will write to stdout and produce logs in the textual
# Common Log Format (CLF), extended with additional fields.
#
# Optional
#
# [accessLog]

# Sets the file path for the access log. If not specified, stdout will be used.
# Intermediate directories are created if necessary.
#
# Optional
# Default: os.Stdout
#
# filePath = "/path/to/log/log.txt"

# Format is either "json" or "common".
#
# Optional
# Default: "common"
#
# format = "common"

################################################################
# API and dashboard configuration
################################################################

# Enable API and dashboard
[api]

  # Name of the related entry point
  #
  # Optional
  # Default: "traefik"
  #
  entryPoint = "api"

  # Enabled Dashboard
  #
  # Optional
  # Default: true
  #
  dashboard = true

################################################################
# Ping configuration
################################################################

# Enable ping
[ping]

  # Name of the related entry point
  #
  # Optional
  # Default: "traefik"
  #
  # entryPoint = "traefik"

[file]
  filename = "backend-file.toml"
  watch = true

# HTTPS certificates
[[tls]]
  entryPoints = ["https"]
  [tls.certificate]
    certFile = "/opt/traefik/ssl.crt"
    keyFile = "/opt/traefik/ssl.key"
```
backend file example
```
insecureSkipVerify = true

[file]

# Backends
[backends]

  [backends.dev]

    [backends.dev.servers]
      [backends.dev.servers.server]
        insecureSkipVerify = true
        url = "https://sonsdkfj" # port is configured in the config file
        weight = 1

    [backends.dev.circuitBreaker]
      expression = "NetworkErrorRatio() > 0.5"

    [backends.dev.loadBalancer]
      method = "drr"
      [backends.dev.loadBalancer.stickiness]
        cookieName = "foobar"


# Frontends
[frontends]
  [frontends.dev]
    entryPoints = ["http", "https"]
    backend = "dev"
    passHostHeader = true
    priority = 42

    [frontends.dev.passTLSClientCert]
        pem = true
        [frontends.dev.passTLSClientCert.infos]
            notBefore = true
            notAfter = true
            [frontends.dev.passTLSClientCert.infos.subject]
                country = true
                domainComponent = true
                province = true
                locality = true
                organization = true
                commonName = true
                serialNumber = true
            [frontends.dev.passTLSClientCert.infos.issuer]
                country = true
                domainComponent = true
                province = true
                locality = true
                organization = true
                commonName = true
                serialNumber = true

    [frontends.dev.whiteList]
      sourceRange = ["subnet range"]
      useXForwardedFor = true

    [frontends.dev.routes]
      [frontends.dev.routes.route0]
        rule = "Host:spothi.skycal.com"
```
run install, can be run multiple times I think
```
./traefik_linux-amd64 --configFile=traefik.toml
```
