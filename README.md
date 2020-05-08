# monroe-experiment-core
MONROE as a package (MaaP).

The 5Genesis fork (this repo) contains tested snapshots aka Releases of the [Monroe develop repo](https://github.com/MONROE-PROJECT/monroe-experiment-core). 

## Rationale
The rationale behind this repo/package is to allow monroe (with minimal dependencys) to be installed on a fresh Debian installation.

## Howto install a MonroeVN (quick version)
1. Install a fresh debian stretch (with defaults)
2. (as root):  ```apt install -y curl && curl -fsSL https://raw.githubusercontent.com/5genesis/monroe-experiment-core/ReleaseA/get-monroe-release-a.sh -o get-monroe-release-a.sh && sh get-monroe-release-a.sh```

## How to install (long version)
### 1. Install a fresh debian stretch (with defaults)
### 2. Install docker
* ```curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh```
### 3. Install monroe-experiment-core
#### 3.1 Install monroe-experiment-core from [apt-repo](https://github.com/MONROE-PROJECT/apt-repo/) (default)
* ```apt install apt-transport-https curl```
* ```echo 'deb [trusted=yes] https://raw.githubusercontent.com/MONROE-PROJECT/apt-repo/master stretch main' > /etc/apt/sources.list.d/monroe.list```
* ```apt update && apt install monroe-experiment-core-rela```
#### 3.2 Install monroe-experiment-core from source
* Get circle and table-allocator-* deb packages (build or get from a running monroe node)
* ```apt install ./circle_1.1.2-deb8u3_all.deb ./table-allocator-client_0.1.2-deb8u-20170831x1107-65b66b_amd64.deb ./table-allocator-server_0.1.2-deb8u-20170831x1107-65b66b_amd64.deb jq ssh libuv1 libjson-c3 libjq1 libonig4 dnsutils ./monroe-experiment-core_*_amd64.deb```
### 4. Install scheduler
Needed if want to schedule (ie run/control) experiments from a external station.
For a publically available node the API key needs to be changed!
#### 4.1 Install TAP/Rest API scheduler from apt-repo
* ```apt install monroe-tap-agent-rela```
#### 4.2 Install TAP/Rest API scheduler from [source](https://github.com/5genesis/monroe-experiment-core/blob/master/schedulers/tap-agent/)
* See: https://github.com/5genesis/monroe-experiment-core/tree/ReleaseA/schedulers/tap-agent

## Howto Build (need to have docker,bash and internet connection)
1. clone this repo
2. cd monroe-experiment-core
3. ./build.sh core .
4. ./build.sh schedulers/tap-agent .

## Run a experiment and check so it works
1.	To deploy and start an experiment, eg: 
    *	`curl --insecure -H 'x-api-key: $3cr3t_Pa$$w0rd!' -d '{ "script": "monroe/ping:5genesis-rela"}' -H "Content-Type: application/json" -X POST https://<URL>:8080/api/v1.0/experiment/test1/start`
2.	To stop and retrieve the results (as a zip file), eg: 
    * `curl --insecure -H 'x-api-key: $3cr3t_Pa$$w0rd!' -X POST https://<URL>:8080/api/v1.0/experiment/test1/stop -o test1.zip`
