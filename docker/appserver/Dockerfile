FROM ubuntu:16.04


###############################################
# ENV 
###############################################
ENV FRAPPE_USER=frappe \
    MYSQL_PASSWORD=12345678 \
    ADMIN_PASSWORD=12345678 \
    DEBIAN_FRONTEND=noninteractive

###############################################
# Basic Ubuntu and tools (git, Python, etc)
###############################################
RUN echo 'APT::Install-Recommends 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'APT::Install-Suggests 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && apt-get update \
 && apt-get install -y wget nano git ca-certificates sudo cron python python3 python3-pip python-setuptools python3-setuptools fontconfig \
 && pip3 install --upgrade pip


###############################################
# Redis
###############################################
#pre-reqs
RUN apt-get install -y build-essential tcl8.5
#install redis
RUN wget http://download.redis.io/redis-stable.tar.gz \
 && tar xvzf redis-stable.tar.gz \
 && cd redis-stable \
 && make \
 && sudo make install \
 && cd utils \
 && sudo ./install_server.sh
#cleanup
RUN rm redis-stable.tar.gz

###############################################
# WKHTMLtoPDF with patched QT (required for pdf generation)
###############################################
#pre-reqs
RUN apt-get install -y build-essential xorg libssl-dev libxrender-dev wget gdebi
#download & install
# RUN wget http://downloads.sourceforge.net/project/wkhtmltopdf/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
RUN gdebi --n wkhtmltox_0.12.5-1.xenial_amd64.deb
#cleanup
RUN rm wkhtmltox_0.12.5-1.xenial_amd64.deb

###############################################
#cleanup
###############################################
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


###############################################
#Frappe Bench
###############################################
#create the user
RUN useradd $FRAPPE_USER \
 && mkdir /home/$FRAPPE_USER \
 && chown -R $FRAPPE_USER.$FRAPPE_USER /home/$FRAPPE_USER \
 && usermod -aG sudo $FRAPPE_USER
#change user to $FRAPPE_USER
USER $FRAPPE_USER
WORKDIR /home/$FRAPPE_USER
#install bench from pip
RUN pip install frappe-bench
# alternative, for dev environments:
# #clone and install bench
# RUN git clone https://github.com/frappe/bench ~/.bench \
#  && pip3 install --user -e ~/.bench
#configure ENVs
ENV PATH="/home/frappe/.local/bin:${PATH}"
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

#erpnext
RUN bench init erpnext
#todo: continue from here


CMD ["/bin/bash"]
