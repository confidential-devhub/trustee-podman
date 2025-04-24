FROM --platform=linux/amd64 docker.io/library/rust:slim

RUN apt-get update && apt-get install -y curl gpg

RUN curl -fsSL https://download.01.org/intel-sgx/sgx_repo/ubuntu/intel-sgx-deb.key | \
    gpg --dearmor --output /usr/share/keyrings/intel-sgx.gpg && \
    echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/intel-sgx.gpg] https://download.01.org/intel-sgx/sgx_repo/ubuntu jammy main' | \
    tee /etc/apt/sources.list.d/intel-sgx.list

RUN apt-get update && apt-get install -y libtss2-esys-3.0.2-0 libtss2-tctildr0 libsgx-dcap-quote-verify-dev
COPY ./kbs-client /kbs-client
COPY ./kbs /kbs
COPY ./sgx_default_qcnl.conf /etc/sgx_default_qcnl.conf
COPY ./policy.rego /opt/confidential-containers/opa/policy.rego
