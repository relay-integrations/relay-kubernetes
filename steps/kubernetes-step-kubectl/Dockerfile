FROM alpine:3
RUN set -eux ; \
    mkdir -p /tmp/ni && \
    cd /tmp/ni && \
    wget https://packages.nebula.puppet.net/sdk/ni/v1/ni-v1-linux-amd64.tar.xz && \
    wget https://packages.nebula.puppet.net/sdk/ni/v1/ni-v1-linux-amd64.tar.xz.sha256 && \
    echo "$( cat ni-v1-linux-amd64.tar.xz.sha256 )  ni-v1-linux-amd64.tar.xz" | sha256sum -c - && \
    tar -xvJf ni-v1-linux-amd64.tar.xz && \
    mv ni-v1*-linux-amd64 /usr/local/bin/ni && \
    cd - && \
    rm -fr /tmp/ni
RUN apk --no-cache add bash ca-certificates curl git jq openssh && update-ca-certificates
RUN ["/bin/bash", "-c", "set -eux\nmkdir -p /tmp/kubectl \u0026\u0026 \\\n  cd /tmp/kubectl \u0026\u0026 \\\n  curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.16/bin/linux/amd64/kubectl \u0026\u0026 \\\n  echo \"$( curl -sL https://storage.googleapis.com/kubernetes-release/release/v1.18.16/bin/linux/amd64/kubectl.sha256 )  kubectl\" | sha256sum -c - \u0026\u0026 \\\n  chmod +x kubectl \u0026\u0026 \\\n  mv kubectl /usr/local/bin/kubectl \u0026\u0026 \\\n  cd - \u0026\u0026 \\\n  rm -fr /tmp/kubectl\n"]
COPY "./step.sh" "/nebula/step-kubectl.sh"
ENTRYPOINT []
CMD ["/bin/bash", "/nebula/step-kubectl.sh"]

LABEL "org.opencontainers.image.title"="kubectl"
LABEL "org.opencontainers.image.description"="The Kubectl step task allows general kubectl use and can take kubectl commands."
LABEL "com.puppet.nebula.sdk.version"="v1"
