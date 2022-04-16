# Certificates

## Setup

```bash
mkdir certs crl csr newcerts private
touch index.txt
echo 1000 > serial
```

## Generate CA key

```bash
openssl genrsa -out private/ca.key.pem 4096
```

## Generate CA cert

```bash
openssl req -config config/openssl.cnf -key private/ca.key.pem -new -x509 -days 1825 -extensions v3_ca -out certs/ca.crt.pem
```

# Server

## Generate Server key

```bash
openssl genrsa -out private/server.key.pem
```

## Generate Server CSR

```bash
openssl req -config config/openssl.cnf -config config/server.cnf -key private/server.key.pem -new -out csr/server.csr.pem
```

## Sign Server CSR and issue cert

```bash
openssl ca -config config/openssl.cnf -extensions server_cert -notext -in csr/server.csr.pem -out certs/server.crt.pem
```