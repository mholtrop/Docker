FROM maurik/ubuntu_dev:latest
LABEL version = "1.1"
LABEL ch.cern.root.version="v6.20.05"

WORKDIR /tmp
RUN git clone http://root.cern.ch/git/root.git \
&& cd root \
&& git checkout v6-20-00-patches \
&& mkdir /tmp/root/cbuild \
&& cd /tmp/root/cbuild \
&& cmake -DALL=ON .. \
&& make install \
&& cd ../.. && rm -rf root
# Note: make -j 6 does not reliably build root in a Docker. Single thread build does.

COPY .bashrc .profile  /home/hps/

CMD ["/usr/sbin/sshd","-D"]
