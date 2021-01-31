FROM ubuntu:20.04

RUN apt-get update && apt-get install -y cron curl jq

# Add backup script
COPY ./veeam_enterprisemanager.sh /app/
RUN chmod +x /app/veeam_enterprisemanager.sh

# Configure the cron
# Copy file to the cron.d directory
COPY ./veeam-cron /etc/cron.d/veeam-cron

# Give execution rights on the cron job
RUN chmod 0644 /etc/cron.d/veeam-cron

# Apply cron job
RUN crontab /etc/cron.d/veeam-cron

# Create the log file to be able to run tail
RUN touch /var/log/veeam_enterprisemanager.log

VOLUME /var/log/

# Start the cron
CMD cron && tail -f /var/log/veeam_enterprisemanager.log