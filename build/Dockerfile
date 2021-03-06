# SPDX-license-identifier: Apache-2.0
##############################################################################
# Copyright (c) 2018
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Apache License, Version 2.0
# which accompanies this distribution, and is available at
# http://www.apache.org/licenses/LICENSE-2.0
##############################################################################

FROM golang:1.14.1

WORKDIR /go/src/github.com/onap/multicloud-k8s
COPY ./ ./
RUN cd src/orchestrator && make all
RUN cd src/ncm && make all
RUN cd src/dcm && make all
RUN cd src/rsync && make all
RUN cd src/ovnaction && make all
RUN cd src/clm && make all

FROM ubuntu:16.04

WORKDIR /opt/mco
RUN groupadd -r mco && useradd -r -g mco mco
RUN chown mco:mco /opt/mco -R
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/orchestrator/orchestrator ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/ncm/ncm ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/dcm/dcm ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/rsync/rsync ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/ovnaction/ovnaction ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/src/clm/clm ./
COPY --chown=mco --from=0 /go/src/github.com/onap/multicloud-k8s/build/entrypoint ./

USER mco

ENTRYPOINT ["./entrypoint"]

