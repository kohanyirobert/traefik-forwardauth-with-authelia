# About

Example of using Docker, Traefik and Authelia together on `localhost`.

## Notes

Mind the `providers.docker.endpoint` setting in `docker-compose.yml`.
It is set to `tcp://host.docker.internal:2375`, this works for Docker Desktop for Windows after enabling the setting *Expose daemon on `tcp://localhost:2375` without TLS* in the Docker Desktop for Windows GUI.

**Note**: doesn't work with *Docker Toolbox*.

## Requirements

Create certificates for development on `localhost` using [`mkcert`](https://github.com/FiloSottile/mkcert).

`mkcert "docker.localhost" "*.docker.localhost"`

## Using

Run `docker-compose up -d` then navigate to these domains in your browser

* `https://bypass.docker.localhost` - allows accessing `index.html` without login.
* `https://one-factor.docker.localhost` - allows accessing `index.html` after one-factor login.
* `https://two-factor.docker.localhost` - allows accessing `index.html` after two-factor login.

When prompted supply `user` as the user name and `user` again for password.

When trying to login via two-factor authentication an email will be sent by Authelia to the user who tries to login.
This email will be intercepted at `https://smtp.docker.localhost`.

## Readings

Read these
* Authelia [deployment](https://github.com/authelia/authelia/blob/master/docs/deployment-dev.md) and [configuration](https://github.com/authelia/authelia/blob/master/docs/configuration.md).
* Traefik [documentation](https://docs.traefik.io/).

## Generating Passwords

Run this to generate passwords for testing: `docker run --rm -it httpd htpasswd -n <username>`.
