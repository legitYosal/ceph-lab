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
ansible-playbook -i inventories/ini deployment.yml --ask-vault-pass
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

## Cheat sheet
Usefull ceph commands:
```bash
ceph osd df | sort -nk 17 # sort osd usage details based on  %USE
ceph osd df | grep -v 1.000 # get all osds wich are not reweighted to 1.000
ceph osd reweight osd.ID NEW_WEIGHT # reweight osd in crush with id ID to weigth NEW_WEIGHT
```
