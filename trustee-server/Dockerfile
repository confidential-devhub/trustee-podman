FROM quay.io/redhat-user-workloads/ose-osc-tenant/trustee/trustee:ce52c99ae4be099bc72e93d68bf521ba41ddbbb6

COPY ./kbs-config.toml /etc/kbs-config/kbs-config.toml
COPY ./sgx_default_qcnl.conf /etc/sgx_default_qcnl.conf
COPY ./default.rego /opt/confidential-containers/attestation-service/policies/opa/default.rego
COPY ./reference-values.json /opt/confidential-containers/rvps/reference-values/reference-values.json

RUN mkdir -p /opt/confidential-containers/kbs/repository/default