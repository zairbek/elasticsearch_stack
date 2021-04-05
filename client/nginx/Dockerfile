FROM nginx

COPY nginx.conf /etc/nginx/nginx.conf

RUN curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.12.0-amd64.deb \
    && dpkg -i filebeat-7.12.0-amd64.deb


#RUN filebeat modules enable nginx

COPY filebeat.yml /etc/filebeat/filebeat.yml
COPY nginx.yml /etc/filebeat/modules.d/nginx.yml

RUN filebeat setup \
    && service filebeat start


COPY startup.sh /opt/startup.sh
RUN sed -i 's/\r//g' /opt/startup.sh
CMD ["/bin/bash", "/opt/startup.sh"]