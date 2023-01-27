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


openssl req -x509 -sha256 -days 1825 -newkey rsa:2048 -keyout rootCA.key -out rootCA.crt

#### Create client

openssl genrsa -out hellfish.test.key 2048


### Create CSR


openssl req -new -key hellfish.test.key -out hellfish.test.csr


openssl req -newkey rsa:2048 -keyout domain.key -out domain.csr

openssl req -newkey rsa:2048 -nodes -keyout domain.key -out domain.csr

### Sign CSR and create public certificate


openssl x509 -req -in hellfish.test.csr -CA myCA.pem -CAkey myCA.key \
-CAcreateserial -out hellfish.test.crt -days 825 -sha256 -extfile hellfish.test.ext
  

openssl x509 -req -CA rootCA.crt -CAkey rootCA.key -in domain.csr -out domain.crt -days 365 -CAcreateserial -extfile domain.ext


### View Certificate

openssl x509 -text -noout -in domain.crt


