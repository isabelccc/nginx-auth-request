# Traefik Auth Request Demo

This project demonstrates how to use Traefik to authenticate requests based on HTTP headers.

## Architecture

The setup consists of two services:

1. **Auth**: A Flask service that validates the `x-pretest` header.
2. **Traefik**: Acts as a gateway, using middleware to validate incoming requests.

## How it works

1. The client sends requests to Traefik with or without the `x-pretest` header.
2. Traefik forwards the authentication headers to the auth service.
3. The auth service checks if the `x-pretest` header contains a valid token.
4. If authentication succeeds, Traefik processes the request; otherwise, it returns a 401 error.

## Valid Authentication

A valid request must include the header: `x-pretest: valid-token`

## Running the Demo

```bash
docker-compose up --build
```

## Testing

You can test manually:

```bash
# Valid request
curl -H "x-pretest: valid-token" http://localhost:8080/auth
curl -H "x-pretest: valid-token" http://localhost:8080/health

# Invalid request
curl -i -H "x-pretest: wrong-token" http://localhost:8080/auth
# → should return HTTP/1.1 401 Unauthorized

# Missing header
curl -i http://localhost:8080
# → should return HTTP/1.1 404 Not Found
``` 