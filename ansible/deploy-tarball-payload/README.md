# deploy-tarball-payload.yml
This is a simple Ansible playbook which will clean the target nodes before copying and extracting
a tarball along with synchronizing a data folder. In this particular use case, the tarball contained
an app which would be run with the check.sh script. A portion data payload is this checked by this app
based on a hash value provided by the playbook.
## Ansible host data structure
```
deploy-tarball-payload
│   README.md
│   deploy-tarball-paylaod.yml
│   hosts.yml
│   tarball.tar.gz
│
└───data
│   │
│   └───failures
│   │
│   └───sorted
│   │   │   file111
│   │   │   file112
│   │   │   ...
│   │
│   └───staging
│   │   │   file111
│   │   │   file112
│   │   │   ...
```
## Usage
There are two parts to this deployment. As the verification app requires the use of a common data
source, the second portion of the deployment had to be run in a semi-manual mode. The first portion
of the deploy sets up the environment on the target nodes and creates the check.sh script which
has the hash value parameters needed by the verification app to split the payload data. The second
portion requires a manual execution of the check scripts on each of the worker nodes.
```bash
# on ansible host
ansible-playbook ./deploy-tarball-payload.yml -v -i ./hosts.yml

# on worker nodes
./tmp/check.sh
```