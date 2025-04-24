# trustee-podman
Repository containing trustee server and client but as containers

trustee-server container contains server as well as the client side
utility. You will need to provide:
1. kbs-config.toml
2. Public and private parts of SSL for HTTPS
Run it as :
```bash
podman run --privileged \
-v ./kbs-config.toml:/kbs-config.toml \
-v ./host.key:/host.key \
-v ./host.crt:/host.crt \
-p 8080:8080 \
--rm localhost/trustee-server \
/kbs --config-file /kbs-config.toml
```

While trustee-client needs:
1. Public part of SSL for HTTPS
Run it as:
```bash
podman run -it --network=host --privileged \
--device /dev/tpm0 \
-v ./host.crt:/host.crt \
--rm localhost/trustee-client \
/kbs-client --url https://<server_ip>:8080 --cert-file /host.crt attest
```
