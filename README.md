# trustee-podman
Repository containing trustee server and client but as containers

For `trustee-server` you will need to provide:
1. kbs-config.toml
2. Public and private parts of SSL for HTTPS (optional)
3. secrets that the server should store
Run it as :

```bash
podman run --privileged \
  -v ./kbs-config.toml:/kbs-config.toml \
  -v ./host.key:/host.key \
  -v ./host.crt:/host.crt \
  -v ./secret.key:/opt/confidential-containers/kbs/repository/default/my-secret/secret.key
  -p 8080:8080 \
  --rm localhost/trustee-server \
  /usr/local/bin/kbs --config-file /etc/kbs-config/kbs-config.toml
```

While trustee-client needs:
1. Public part of SSL for HTTPS (optional)
2. tee key (optional)
Run it as:
```bash
podman run --privileged \
  --device /dev/tpm0 \
  -v ./host.crt:/host.crt \
  -v ./my-tee-key.pem:/tee-key.pem \
  --rm localhost/trustee-client \
  kbs-client --url http://$TRUSTEE_IP:8080 attest --tee-key-file tee-key.pem --cert-file $HTTPS_CERT_FILE
```
