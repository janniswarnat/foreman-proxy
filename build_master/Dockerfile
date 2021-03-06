FROM python:3.7-bullseye
RUN apt-get update
RUN apt-get install -y sqlite3

RUN wget https://deb.theforeman.org/foreman.asc -O /etc/apt/trusted.gpg.d/foreman.asc
RUN echo "deb http://deb.theforeman.org/ bullseye 3.2" > /etc/apt/sources.list.d/foreman.list
RUN echo "deb http://deb.theforeman.org/ plugins 3.2" >> /etc/apt/sources.list.d/foreman.list

RUN apt-get update
RUN apt-get install -y foreman-proxy
RUN apt-get install -y ruby-smart-proxy-salt

RUN addgroup --gid 450 --system salt
RUN adduser --shell /bin/sh --system --disabled-password --ingroup salt salt
RUN mkdir -p /etc/pki /etc/salt/pki /etc/salt/minion.d/ /etc/salt/master.d /etc/salt/proxy.d /var/cache/salt /var/log/salt /var/run/salt
RUN chmod -R 2775 /etc/pki /etc/salt /var/cache/salt /var/log/salt /var/run/salt
RUN chgrp -R salt /etc/pki /etc/salt /var/cache/salt /var/log/salt /var/run/salt

ENTRYPOINT ["/usr/bin/dumb-init"]
CMD ["/usr/local/bin/saltinit"]
ADD saltinit.py /usr/local/bin/saltinit
RUN chmod u+rwx /usr/local/bin/saltinit
EXPOSE 4505 4506 8000 9000
VOLUME /etc/salt/pki/

RUN USE_STATIC_REQUIREMENTS=1 pip3 install --no-cache-dir salt=="3004"
RUN su - salt -c 'salt-run salt.cmd tls.create_self_signed_cert'
