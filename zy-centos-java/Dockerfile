FROM centos:7.6

MAINTAINER ellios <104082492@qq.com>

# basic settings
ENV TZ=Asia/Shanghai \
    LANG=en_US.UTF-8 

RUN set -x && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime

# basic paths
ENV TOP_HOME=/opt
ENV APP_HOME=${TOP_HOME}/app \
    WWW_ROOT=${TOP_HOME}/www

RUN set -x && chmod a+x root && mkdir -p ${APP_HOME} ${WWW_ROOT}

# basic tools
RUN set -x && yum -y install wget unzip net-tools sysstat lrzsz && yum clean all

# jdk
ENV JAVA_DOWNLOAD_URL="http://download.oracle.com/otn-pub/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jdk-8u201-linux-x64.rpm" \
    JAVA_HOME=/usr/java/latest

RUN set -x \
 && wget -q --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" ${JAVA_DOWNLOAD_URL} -O /tmp/java.rpm \
 && yum -y install /tmp/java.rpm \
 && yum clean all && rm -rf /tmp/*

# sshd
RUN set -x \
 && yum install -y openssh-server openssh-clients \
 && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key \
 && yum clean all

EXPOSE 22 80 8080 8500

CMD ["/usr/sbin/sshd", "-D"]