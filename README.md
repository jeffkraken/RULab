# Container Security Lab
This lab environment provides a safe and easy way to practice penetration testing and network scanning using Docker containers. Students can scan and interact with two deliberately vulnerable Linux targets from their own Kali Linux VM.
## Lab Overview
#### Container Name: rockylinux-target
OS & Services: Rocky Linux 8
Ports Exposed: 2121 (FTP), 2222 (SSH), 8081 (HTTP)
Description: Multi-service target with misconfigurations (student user, anonymous FTP)

#### Container Name: ubuntu-vuln

OS & Services: Ubuntu 20.04
Ports Exposed: 2122 (FTP), 2223 (SSH), 8082 (HTTP)
Description: Deliberately weak "workstation" with default credentials, anonymous FTP
Students will use their Kali Linux VM (as the host) to run the lab and perform scans using tools like nmap, ftp, hydra, etc.

## Requirements
Kali Linux VM (with Docker and docker-compose installed)
At least 2GB RAM and 2 CPU cores recommended
Internet access for initial Docker image downloads
Lab Setup
Put all the following files together in the same directory:

docker-compose.yml
Dockerfile (for the Rocky Linux target)
Dockerfile.ubuntu-vuln (for the Ubuntu vulnerable workstation)

Open a terminal and change to that directory.
To build and launch the lab environment, use this command (most systems):

sudo docker-compose up --build

If you are using the newer Docker Compose Plugin, use:

sudo docker compose up --build

The first time you run this, Docker will build both custom images and start both containers.

To stop and remove the containers when finished, use:

sudo docker-compose down

or

sudo docker compose down

## Accessing the Targets
From your Kali host, these ports are exposed:

#### RockyLinux (rockylinux-target)

SSH: 2222
HTTP: 8081
FTP: 2121

#### Ubuntu (ubuntu-vuln)

SSH: 2223
HTTP: 8082
FTP: 2122
Examples:

SSH: ssh student@localhost -p 2222 (password: password)
FTP: ftp localhost 2121 (login as anonymous or student)
HTTP: Open  in a web browser

## Example Tasks
Use nmap to scan for open ports and services:

nmap -sV -p 2121,2222,8081,2122,2223,8082 localhost
Brute-force SSH credentials with hydra or similar tools.

Perform web vulnerability testing on the HTTP services.

Test anonymous FTP uploads to both targets.

Enumerate system banners and fingerprint OS/services.

Credentials and Defaults
User: root
Password: toor
Available on: Both targets

User: student
Password: password
Available on: Both targets

FTP Anonymous Access: Any value for password
Maps to: student user's home directory

## Troubleshooting
Use sudo if you get permission errors.
If ports are already in use, either stop other services or change the ports in docker-compose.yml.
Make sure both Dockerfiles are in the directory and named correctly. If containers don’t build, double check file names.
Cleaning Up
To remove all containers and stop the lab, run:

sudo docker-compose down
or

sudo docker compose down
To completely delete built images, use:

docker image rm <imagename>

## Disclaimer
This environment is for educational and ethical security testing only.
Do not use or expose these containers outside a controlled lab environment.

Happy hacking!
