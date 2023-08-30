
# whoami-example

In this repository, we explain how to setup and query HTTP and HTTPS servers provided by the docker image [whoami](https://hub.docker.com/r/containous/whoami).


## Run HTTP Server

Run the HTTP server using the following command

```bash
docker run -d -p 80:80 containous/whoami
```

Curl the server using the following command

```bash
curl http://0.0.0.0:80
```

## Run HTTPS Server

To generate the SSL Certificate and Private Key

```bash
// Generate certificate and private key. Note that since its a self signed certificate, its recommended to specify the host you're exposing as the "Common Name". In our case, it would be 0.0.0.0
openssl req -x509 -newkey rsa:4096 -keyout key_with_password.pem -out cert.pem -days 365

// Remove password protection from private key
openssl rsa -in key_with_password.pem -out key_without_password.pem

// Create a common directory to store certificates
mkdir certs

// Move certificates to that directory
mv *.pem certs

// Convert the certificate and key to a single pem file.
cat cert.pem key_without_password.pem > cert-and-key.pem
```

Run the HTTPS server using the following command

```bash
docker run -d -p 443:443 -v ./certs:/certs containous/whoami --cert /certs/cert.pem --key /certs/key_without_password.pem --port 443
```

Curl the server using the following command

```bash
curl --cacert cert-and-key.pem https://0.0.0.0:443 -v
```

To see what certificate the server is sending, run the following command

```bash
// The below command is interactive. You what to write quit and then press enter to continue
(openssl s_client -showcerts -servername 0.0.0.0 -connect 0.0.0.0:443 > server-cert.pem) && openssl x509 -inform PEM -in server-cert.pem -text -out certdata && rm server-cert.pem
```
