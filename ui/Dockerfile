FROM alpine

RUN apk add py3-pip apache2-utils bash && \
    pip3 install docker flask && \
    mkdir /opt/entrypoint && \
    mkdir -p /opt/confs/site

COPY confs/site/ /opt/confs/site
COPY entrypoint/* /opt/entrypoint/
COPY ui/ /opt/entrypoint/
RUN chmod +x /opt/entrypoint/*.py /opt/entrypoint/*.sh

# Fix CVE-2020-1971
RUN apk add "libcrypto1.1>1.1.1g-r0" "libssl1.1>1.1.1g-r0"

VOLUME /etc/nginx

EXPOSE 5000

WORKDIR /opt/entrypoint
ENV FLASK_APP entrypoint.py
ENTRYPOINT ["/usr/bin/python3", "-m", "flask", "run", "--host=0.0.0.0"]
