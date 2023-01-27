### PKI

  Public Key Infraestructure

### OpenSSL

  Create key

  openssl genrsa -out private.key 2048

  Using encryption

  openssl genrsa -aes256 -out private.key

  Extract public key

  openssl rsa -in private.pem -outform PEM -pubout -out public.pem

  Obtain all chain

  certtool -in < chain.pem

#### Create CA key


openssl genrsa -des3 -out myCA.key 2048

#### Create root certificate


openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem


#### Create client

openssl genrsa -out hellfish.test.key 2048


### Create CSR


openssl req -new -key hellfish.test.key -out hellfish.test.csr


### Sign CSR and create public certificate


openssl x509 -req -in hellfish.test.csr -CA myCA.pem -CAkey myCA.key \
-CAcreateserial -out hellfish.test.crt -days 825 -sha256 -extfile hellfish.test.ext
  
