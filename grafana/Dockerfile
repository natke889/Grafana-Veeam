FROM grafana/grafana:7.3.5

COPY ./dashboards /etc/dashboards
COPY ./provisioning /etc/grafana/provisioning
COPY ./grafana.ini /etc/grafana/grafana.ini

ENTRYPOINT ["/run.sh"]