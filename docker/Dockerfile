from debian:10-slim

ENV WORKDIR /app
ENV TZ=Asia/Shanghai

RUN echo -e "deb https://mirrors.aliyun.com/debian/ bookworm main non-free non-free-firmware contrib\n"\
"deb-src https://mirrors.aliyun.com/debian/ bookworm main non-free non-free-firmware contrib\n"\
"deb https://mirrors.aliyun.com/debian-security/ bookworm-security main\n"\
"deb-src https://mirrors.aliyun.com/debian-security/ bookworm-security main\n"\
"deb https://mirrors.aliyun.com/debian/ bookworm-updates main non-free non-free-firmware contrib\n"\
"deb-src https://mirrors.aliyun.com/debian/ bookworm-updates main non-free non-free-firmware contrib\n"\
"deb https://mirrors.aliyun.com/debian/ bookworm-backports main non-free non-free-firmware contrib\n"\
"deb-src https://mirrors.aliyun.com/debian/ bookworm-backports main non-free non-free-firmware contrib" > /etc/apt/source.list; \
    set -eux; \
    apt -o Acquire::Check-Valid-Until=false update -y; \
    apt install -y --no-install-recommends ca-certificates tzdata procps libcurl4-openssl-dev wget git build-essential libssl-dev libjwt-dev; \
    ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime; \
    echo ${TZ} > /etc/timezone; \
    dpkg-reconfigure --frontend noninteractive tzdata; \
    wget https://boostorg.jfrog.io/artifactory/main/release/1.70.0/source/boost_1_70_0.tar.gz; \
    tar -xzf boost_1_70_0.tar.gz; \
    cd boost_1_70_0; \
    ./bootstrap.sh --prefix=/usr/local; \
    ./b2 install; \
    # rm -rf /var/lib/apt/lists/*; \
    apt autoclean; \
    echo "/usr/local/bin/">>/etc/ld.so.conf; \
    echo "/usr/local/lib/">>/etc/ld.so.conf; \
    /sbin/ldconfig; \
    echo "PS1='\u[\w]\$ '">>/root/.bashrc; \
    echo "alias lg='ls -lh --color=auto'">>/root/.bashrc

WORKDIR $WORKDIR
EXPOSE 8080
CMD ["./ms"]
