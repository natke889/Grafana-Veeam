FROM ubuntu:20.04

RUN apt-get update && apt-get install -y cron curl jq

# Create the log file to be able to run tail
RUN touch /var/log/veeam_enterprisemanager.log

VOLUME /var/log/

# Start the cron
CMD crontab /etc/cron.d/veeam-cron && cron && tail -f /var/log/veeam_enterprisemanager.log