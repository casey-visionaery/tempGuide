# tempGuide

# Setup Commands for MIC-711ON for Ubuntu 20.04 LTS

## Prep & Install Dependencies

### nvidia-container-toolkit & Docker

[Source](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

```
curl https://get.docker.com | sh \
  && sudo systemctl --now enable docker
```

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
      && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
      && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
            sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
            sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

```


```
sudo apt update
```

```
sudo apt upgrade
```

```
sudo apt-get install -y nvidia-container-toolkit
```

```
sudo nvidia-ctk runtime configure --runtime=docker
```

```
sudo systemctl restart docker
```

```
sudo apt install wget
```

## Install Mosquitto-client
```
sudo apt install mosquitto-clients
```

## Install Docker Compose
Download from https://github.com/docker/compose/releases the binary that matches your OS and architecture
Check OS with command:
```
uname -s
```
e.g output Linux

Check Architecture
```
uname -m
```
e.g output aarch64

If you are connected over SSH then Download this exec in your host, rename it, then copy it to the remote machine and make it runnable as an executable:
On Host:
```
sudo mv ./docker-compose-linux-aarch64 /usr/local/bin/docker-compose
```
```
sudo chmod +x /usr/local/bin/docker-compose
```
Check docker-compose is executable
```
docker-compose --version
```
e.g. output Docker Compose version v2.21.0

### ADD Set so docker doesn't need sudo


## Pull the docker image from registry
```
sudo docker login leak.app.noema.tech:444
```
Insert credentials
- User: twin.eagle
- Pwd: shotheov

```
sudo docker pull leak.app.noema.tech:444/leak_app_mic:latest
```

## Install Cockpit & Cockpit-Navigator

### Cockpit
[Source](https://cockpit-project.org/running#ubuntu)
```
sudo apt install -t focal-backports cockpit
```

### Cockpit Navigator 
[Source](https://github.com/45Drives/cockpit-navigator/blob/main/README.md)
```
wget https://github.com/45Drives/cockpit-navigator/releases/download/v0.5.10/cockpit-navigator_0.5.10-1focal_all.deb
```

```
sudo apt install ./cockpit-navigator_0.5.10-1focal_all.deb
```


## Installing Node Red in Docker 



## Install Hanwha Wave VMS
- Make sure you are in the Home dir for the MIC-711ON 
```
cd /home/mic-711on/
```
- Create a dir named **wave** to store all files for VMS
```
mkdir wave
```
- Move to the wave dir
```
cd wave
```

- Navigate to the [Hanwha Wave Downloads Page](http://beta.networkoptix.com/beta-builds/hanwha/index.html)
- Under the **Releases** section, scroll to the bottom of the most recent releases **Release Notes**
- Select the **ARM** Sub-Section
- Copy the link for the most recent  the **ARM64 (Nvidia Jetson, Qualcomm) - Server installer**

```
wget <link of latest jetson ARM64 Server installer>
```
- Look inside the dir to note the name of the installer file that you just downloaded
```
ll
```
- Install Wave
```
sudo apt-get install ./<name of downloaded installer>.deb
```




# Other Tools
   
## Install Jtop 
```
sudo apt update
```

```
sudo apt install python3-pip
```

```
sudo pip3 install -U jetson-stats
```

```
sudo reboot
```	
	

# Software v1

## Installed on OS using apt and systemctl
1. Cockpit w/ Cockpit-Navigator
2. Hanwha Wave VMS

# Installed on Docker
1. Leak Detection App
2. Mosquitto MQTT Broker
3. Node-Red


# Software v2 Idea

## Installed on OS using apt and systemctl
1. Cockpit w/ Cockpit-Navigator


# Installed on Docker
1. Leak Detection App
1. Flare App
1. Mosquitto MQTT Broker (Internal)
1. Mosquitto MQTT Broker (External)
1. Node-Red (Internal Integrations)
1. Node-Red (External User Integration)
1. Hanwha Wave VMS
1. Portainer
1. Reverse Proxy (?? Which one and How)
1. InfluxDB
1. Cronograf
1. Grafana
