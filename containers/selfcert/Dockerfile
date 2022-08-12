FROM alpine:latest

WORKDIR /certs

RUN apk update && apk add openssl

CMD openssl req -x509 -newkey rsa:4096 -sha256 -days 365 -nodes \
  -keyout me.key \
  -out me.crt \
  -subj "/CN=${DOMAIN}" \
  -addext "subjectAltName=DNS:${DOMAIN}" \
  -addext "extendedKeyUsage=serverAuth"
