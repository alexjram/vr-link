FROM redhat/ubi8

RUN mkdir -p /app
WORKDIR /app
RUN mkdir /app/vrlink
RUN mkdir /app/license
RUN mkdir /app/rti
COPY ./vrLink5.8-linux64-rhe8-20220425.tar.gz /app/vrlink
COPY ./licenseManager5.0-linux64-lsb-20230315.tar.gz /app/license
COPY ./makRti4.6b-linux64-rhe8-20220411.tar.gz /app/rti

RUN cd /app/vrlink/ && tar -xzf ./vrLink5.8-linux64-rhe8-20220425.tar.gz
RUN cd /app/license && tar -xzf ./licenseManager5.0-linux64-lsb-20230315.tar.gz
RUN cd /app/rti/ && tar -xzf ./makRti4.6b-linux64-rhe8-20220411.tar.gz
RUN yum install glibc.i686 -y


RUN cd /app/license/LicenseManager/dongle_drivers && tar -xzf aksusbd-redhat-suse-8.53.tar.gz && \
    cd /app/license/LicenseManager/dongle_drivers/Sentinel_LDK_RedHat_and_SuSE_RPM_Run-time_Installer/ && ls && \
    rpm -i aksusbd-8.53-1.x86_64.rpm && export FLEXID_LIBRARY_PATH=$FLEXID_LIBRARY_PATH:.

RUN cd /app/rti/makRti4.6b && ls

ENV LD_LIBRARY_PATH="/app/rti/makRti4.6b/lib"

RUN yum install gcc gcc-c++ make -y

RUN cd /app/vrlink/vrlink5.8/examples/ && make