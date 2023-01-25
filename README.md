# Configuration

## Setup project

Install requirements and ansible on ubuntu controller:
```bash
sudo apt install python3-venv
git clone git@github.com:legitYosal/ceph-lab.git
cd ceph-lab
git submodule update --init --recursive
python3 -m venv env
source env/bin/activate
pip install -r requirements.txt
ansible-galaxy install -r requirements.yml
```
## Infra

First bootstrap servers and initially configure them.  
```
ansible-playbook -i inventories/ini deployment.yml


# Ceph

