FROM maurik/ubuntu_root:latest

LABEL version = "1.0"
LABEL org.lcio.version="v02-07-05"
LABEL ch.cern.root.version="v6.20.05"
LABEL com.ubuntu.version="Ubuntu 20.04 LTS"
LABEL debian_version="bullseye/sid"
LABEL maintainer="maurik@physics.unh.edu"
LABEL description="Minimal install for Hpstr development.\
Includes LCIO, ROOT  and minimal Development Tools and Libraries.\
Runs an ssh-server for easy login and X11 forwarding."

WORKDIR /tmp
RUN git clone https://github.com/iLCSoft/LCIO lcio \
&& cd lcio \
&& git checkout v02-07-05 \
&& mkdir build \
&& cd build \
&& cmake -DBUILD_LCIO_EXAMPLES=OFF -DBUILD_ROOTDICT=ON -DCMAKE_INSTALL_PREFIX=/usr/local .. \
&& make install \
&& cd /tmp && rm -rf lcio
RUN git clone https://github.com/JeffersonLab/hpstr.git \
&& cd hpstr \
&& mkdir build \
&& cd build \
&& cmake -DPYTHON3=on -DLCIO_DIR=/usr/local -DCMAKE_INSTALL_PREFIX=/usr/local .. \
&& make install \
&& cd /tmp && rm -rf hpstr

COPY .bashrc .profile  /home/hps/

CMD ["/usr/sbin/sshd","-D"]
