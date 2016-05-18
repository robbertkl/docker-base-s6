# robbertkl/base-s6

[![](https://badge.imagelayers.io/robbertkl/base-s6:latest.svg)](https://imagelayers.io/?images=robbertkl/base-s6:latest)

Base image extension with s6-overlay:

* Based on [robbertkl/base](https://github.com/robbertkl/docker-base)
* Uses [s6-overlay](https://github.com/just-containers/s6-overlay)
* Runs `cron` and `rsyslogd` services
* Helper service to output arbitrary logs to `stdout` or `stderr`
* Basic SSL certificate preparation

## Usage

Just extend it in your `Dockerfile` using `FROM`. Example:

```
FROM robbertkl/base-s6

RUN cleaninstall package1 package2 package3
RUN echo /var/log/custom.log >> /etc/services.d/logs/stderr

...
```

## Logging

To have your custom logs show up in `docker logs`, you can append your name to either `/etc/services.d/logs/stdout` or `/etc/services.d/logs/stderr`.

## SSL

As a convention, please copy or mount your SSL files to `/private/ssl` named `cert.pem`, `key.pem` and `ca.pem`. A default (snakeoil) certificate will be provided as a fallback. Create custom (combined) pem bundles from these files in your s6 `run` scripts.

Alternatively, you can mount a Let's Encrypt configuration to `/etc/letsencrypt` and set `LETSENCRYPT_HOST` to the hostname of the certificate to use. Symlinks with the correct names will then be create in `/private/ssl`.

## Authors

* Robbert Klarenbeek, <robbertkl@renbeek.nl>

## License

This repo is published under the [MIT License](http://www.opensource.org/licenses/mit-license.php).
