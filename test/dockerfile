FROM centos:7
MAINTAINER auspbro@gmail.com

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim && \
    yum -y install net-tools && \
    yum clean all

EXPOSE 80

CMD echo $MYPATH
CMD echo "+++++++++ end ++++++++"
CMD /bin/bash
CMD ["ls","-a"]
