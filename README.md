# Note

Sorry for the name, I'm already in 2024 :-D (probably the stress of presentation :-D ).

There are a few files missing and Wiki is coming in a few days (I must migrate from my test repo to have a clean repo with limited number of commits).
Will be fixed in a few days when I get a good connexion.

# Source
the origin of the project comes from french medium article and the work done iin University of Lausanne
https://github.com/ouidou/monitoring-bootstrap

# WLPC Prague 2023
Demo project Prometheus Grafana

# Install pre-requesite on server / RPi

To re-use this repo, I recommand you to fork the repository
Install Git to get the code : 

`sudo apt install -y git gh`

install Docker :
https://docs.docker.com/engine/install/

Install on RPi :
https://docs.docker.com/engine/install/raspberry-pi-os/

Install Docker-compose :
`sudo apt install docker-compose`

To manage our server, based on docker container, it's a good option to install Portainer.
It offers a GUI to see the container, logs, ports used then stop, start, restart.

`sudo docker volume create portainer_data`

`sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

You may have now a webpage on your server to manager your docker environnement :

[https://IP_OF_YOUR_SERVER:9443](https://IP_OF_YOUR_SERVER:9443)

More info on the installation / if you use differente OS :
[https://docs.portainer.io/start/install-ce](https://docs.portainer.io/start/install-ce/server/docker)

# Clone this repo

Start by forking the repo on your Github account (you can then tweak it, make it private, ...).

`gh repo clone Martoni74/WLANProPrague`

# Repo structure

The main file of the project is the file "docker-compose.yml".
It contains all the container to run, witch ports they use, the external "disk" used to store data, ...

The file use passwords stored in the file .env
You can modify that file and keep it secured in a vault or password manager.
(don't upload it to GitHub to avoid hack).

Everytime you run the command "sudo docker-compose up -d", this file is checked :
- if you select a new version, the container is recreated ;
- if you add parameter, the container restart.

Important note, if you modify information in a config file, you must restart the container yourself (via portainer it's easy).

# Configuration

Except node-exporter which run directly with the docker compose info, exporters use config files.

There is a directory for every container to facilitate the modification and understanding.

Every exporter is explained in WiKi so you can modify it for your needs.

# Launch the Stack

When your config files are ready, you can start the stack with the command :

`sudo docker-compose up -d`

Docker will download the images if they are not already there then launch the different containers.

# Next steps

There are a lot of exporters written for different vendors, simply type prometheus exporter + brand.
Sometimes there are old / not working with new software releases but here are a few ressources interesting :

SNMP :
[https://github.com/prometheus/snmp_exporter](https://grafana.com/blog/2022/02/01/an-advanced-guide-to-network-monitoring-with-grafana-and-prometheus/)

Ruckus (used in UNIL) :
https://github.com/ddericco/smartzone_exporter

Cisco :
https://github.com/lwlcom/cisco_exporter

Aruba :
https://pkg.go.dev/github.com/yankiwi/aruba_exporter#section-readme
https://github.com/slashdoom/aruba_exporter

Junos (Mist ?) :
https://github.com/czerwonk/junos_exporter

Arista :
https://github.com/Showmax/arista-eos-exporter

Grafana dashboard :
https://grafana.com/grafana/dashboards/

