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

Bootstrap cluster:  
```
ansible-playbook -i inventories/ini facts.yml
ansible-playbook -i inventories/ini deployment.yml
ansible-playbook -i inventories/ini ceph.yml --ask-vault-pass -e yes_i_know=yes
```

cluster map:
```


  ┌───provision┼network──────────────────────────────────────────────┐
  │                                                                  │
  │   ┌──ceph┼public───────────────────────────────────────────────┐ │
  │   │                                                            │ │
  │   │  ┌──ceph┼osd────────────────────────────────────────────┐  │ │
  │   │  │                                                      │  │ │
  │   │  │   ┌─osd──┐        ┌─osd──┐         ┌─osd──┐          │  │ │
  │   │  │   │      │        │      │         │      │          │  │ │
  │   │  │   │      │        │      │         │      │          │  │ │
  │   │  │   └──────┘        └──────┘         └──────┘          │  │ │
  │   │  │                                                      │  │ │
  │   │  └──────────────────────────────────────────────────────┘  │ │
  │   │                                                            │ │
  │   │    ┌─mon──┐                       ┌─mon──┐                 │ │
  │   │    │      │                       │      │                 │ │
  │   │    └──────┘                       └──────┘                 │ │
  │   │                  ┌─gateway──┐                              │ │
  │   └──────────────────┤          ├──────────────────────────────┘ │
  │                      │          │                                │
  └──────────────────────┤          ├────────────────────────────────┘
                         └──────────┘

```
