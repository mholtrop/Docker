FROM maurik/ubuntu_dev_python2:latest
LABEL version = "1.0"
LABEL ch.cern.geant4.version="10.2.3.v0.3"
LABEL org.apache.xerces.version="3.2.3"

WORKDIR /tmp
RUN curl https://downloads.apache.org//xerces/c/3/sources/xerces-c-3.2.3.tar.gz --output xerces.tar.gz \
&& tar xzf xerces.tar.gz  \
&& cd xerces-c-3.2.3 \
&& mkdir build \
&& cd build \
&& cmake .. \
&& make install \
&& cd /tmp && rm -rf xerces*

RUN curl http://geant4-data.web.cern.ch/geant4-data/releases/geant4.10.06.p01.tar.gz --output geant4.10.06.p01.tar.gz \
&& tar xzf geant4.10.06.p01.tar.gz \
&& mkdir build \
&& cd build \
&& cmake cmake -DGEANT4_INSTALL_DATA=ON -DGEANT4_USE_GDML=ON -DGEANT4_USE_OPENGL_X11=ON ../geant4.10.06.p01 \
&& make install \
&& cd /tmp && rm -rf geant*

COPY .bashrc .profile  /home/hps/

CMD ["/usr/sbin/sshd","-D"]
