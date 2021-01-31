# Grafana-Veeam

This project provides an automated installation and deployment of the Grafana dashboard for Veeam Enterprise Manager.

## Overview
The project based on various open source components and tools in order to do so. A bash shell script will periodically poll your Veeam data at a regular interval and pushed into an [InfluxDB](https://www.influxdata.com/) time-series database. [Grafana](https://grafana.com/), a data visualization engine for time-series data, is then utilized along with several customized [dashboards](https://github.com/jorgedlcruz/veeam-enterprise_manager-grafana) of [Jorge de la Cruz](https://github.com/jorgedlcruz) to present the data graphically with . All of these components are integrated together using [Docker](https://www.docker.com/).

The only real requirements to utilize this project are a Linux OS and a Docker installation with Docker Compose.

## Getting Started
### Dependencies
You'll need to install [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/). All other dependencies are provided through use of our Docker images.
### Configuration
#### Veeam Info
The only configuration needed is to set Veeam IP or FQDN and credentials within the *"<project_dir\>/.env"* file. 
~~~~
...
VEEAM_IP=<VEEAM_IP>
VEEAM_USER=<VEEAM_USER>
VEEAM_PASS=<VEEAM_PASS>
...
~~~~

### Starting It Up
It's pretty simple: run the docker compose from within the project root directory.

~~~~
$ docker-compose -f docker-compose.yml up -d
~~~~

## Once It's Started
### Accessing the Grafana Dashboards
The dashboards are available at **http://<host\>:3002** using default credentials _admin/admin_. Grafana should be pre-configured for immediate access to your data. Documentation for additional configuration and navigation can be found [here](http://docs.grafana.org/guides/getting_started/).

## Testing
The project can be tested using [Vagrant](https://www.vagrantup.com/docs/installation) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads). 

Clone the repo and change to the project directory.
~~~~
git clone https://github.com/natke889/Grafana-Veeam.git
cd Grafana-Veeam
~~~~

Edit the .env file and set the vcenter info.
~~~~
vi .env
~~~~

Run vagrant up from the project root directory. This will bring up ubuntu with docker installed. 
~~~~
vagrant up
~~~~

Run the docker compose command in order to starting the dockers.
~~~~
$ vagrant ssh -c "cd /vagrant && docker-compose -f docker-compose.yml up -d"
~~~~

Access Grafana at **http://192.168.65.211:3002**. (The IP address can be edit in th Vagrantfile)

## Install on non-internet server
The following stages need to be taken in order to pull the docker images and load them in non-internet access server
~~~~
pull the image on a machine with internet access.

$ docker pull natke889/grafana-veeam-collector:1.0
$ docker pull natke889/grafana-veeam-grafana:1.0
$ docker pull natke889/grafana-veeam-influxdb:1.0

save that image to a .tar files.

$ docker save --output grafana-veeam-collector.tar natke889/grafana-veeam-collector:1.0
$ docker save --output grafana-veeam-grafana.tar natke889/grafana-veeam-grafana:1.0
$ docker save --output grafana-veeam-influxdb.tar natke889/grafana-veeam-influxdb:1.0

copy those files to any machine and load the .tar files to docker with the docker compose command.

$ docker load --output grafana-veeam-collector.tar
$ docker load --output grafana-veeam-grafana.tar
$ docker load --output grafana-veeam-influxdb.tar
~~~~

## Screenshots
*Grafana Dashboard for Veeam Enterprise Manager*
![Grafana Dashboard for Veeam Enterprise Manager](https://i.postimg.cc/8z2bkgsV/5.png)

