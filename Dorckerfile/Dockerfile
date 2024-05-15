FROM quay.io/buildah/stable:v1

RUN touch /etc/subgid /etc/subuid \
 && chmod g=u /etc/subgid /etc/subuid /etc/passwd \
 && echo build:10000:65536 > /etc/subuid \
 && echo build:10000:65536 > /etc/subgid \
 && yum install -y git \
    libicu \
    lttng-ust \
 && yum clean all

# Use chroot since the default runc does not work when running rootless
RUN echo "export BUILDAH_ISOLATION=chroot" >> /home/build/.bashrc

# Use VFS since fuse does not work
RUN mkdir -p /home/build/.config/containers \
 && (echo '[storage]';echo 'driver = "vfs"') > /home/build/.config/containers/storage.conf


USER build
WORKDIR /home/build

# Download and extract vsts agent
RUN curl -o vsts-agent-linux-x64-3.236.1.tar.gz -L https://vstsagentpackage.azureedge.net/agent/3.236.1/vsts-agent-linux-x64-3.236.1.tar.gz \
 && tar xzf ./vsts-agent-linux-x64-3.236.1.tar.gz \
 && rm vsts-agent-linux-x64-3.236.1.tar.gz

# Just keep the container running, allowing "oc rsh" access
CMD ["python3", "-m", "http.server"]