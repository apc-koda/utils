FROM centos:7
MAINTAINER "you" <your@email.here>
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;\
yum update -y; yum -y install epel-release glibc-common openssh-clients openssh-server git wget sudo which; yum clean all;\
systemctl enable sshd.service;\
useradd sysadmin;\
install -o sysadmin -g sysadmin -m 0700 -d /home/sysadmin/.ssh;\
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDC5/ASKyLsX0eSrSpT0eqkALtLhqx/2L1LQX0W37Iix1n6HPI78hjTAQ13Q2DFBofUbuNITVHab6FWcssdwSuWtK8zM+hTn6MjXuIwvraz9RCZYAGkUkDYQ9aqZAgbIdtqjh9uPSveK9gLfkXn4kCgxEHpOz38Axug9V3j5QiKvcySI9H2GglJfBW1a7HLYNDL5Jm20ds1AtcvTk9Gur2V4NAPME6BjmrgspZuoCbkxJ+YI8BMaHS39zB4PP112KAyCfAYSIwS7CebCSGixWsarEIHhx6V5RjEmFQIyXlpR9wDIw+v9zznw5nlxkG5ENVIu6+Xr6j3MdJHv7YTOs/j" > /home/sysadmin/.ssh/authorized_keys;\
chmod 600 /home/sysadmin/.ssh/authorized_keys;\
chown sysadmin:sysadmin /home/sysadmin/.ssh/authorized_keys;\
echo "sysadmin        ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/sysadmin;\
sed -i  "s/account    required     pam_nologin.so/#account    required     pam_nologin.so/" /etc/pam.d/sshd;\
rm -rf /run/nologin
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime
EXPOSE 22 80 443
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
