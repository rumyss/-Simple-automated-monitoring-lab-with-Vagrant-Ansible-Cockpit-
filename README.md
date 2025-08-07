# Simple Monitoring Lab

This project creates a small lab with **two Ubuntu VMs** using Vagrant + libvirt:

- **ansible**: For automation and playbooks
- **client**: The monitored machine

Both are set up with automatic triggers for easier management and demo purposes.

---

## How it works

- **Automatic network detection:**
  The Vagrantfile script finds your subnet and assigns static IPs:
  - ansible: `<subnet>.10` (for example: `192.168.121.10`)
  - client: `<subnet>.225` (for example: `192.168.121.225`)
  > *Note: Actual IPs may change if subnet or DHCP pool is different.*

- **Shared folder:**
  `/vagrant_data` is synced between your host and both VMs for easy playbook/config transfer.

- **Startup triggers:** 
  When you run `vagrant up ansible`, the following happens:
    1. The **client** VM starts automatically.
    2. Then the **ansible** VM starts.
    3. After boot, an Ansible playbook is run to **install Cockpit** (web dashboard) on the client VM.

- **Cockpit Web UI:**
  After everything is up, you can monitor and manage the client VM in real-time via Cockpit:

       https://192.168.121.225:9090

-------------
 
(Login as `vagrant` / `vagrant` by default.)

- **Power off the client:**  
Use Ansible from the ansible VM to shut down the client VM easily with a playbook.

---

## Quick Start Guide

1. **Start the lab:**
 ```sh
 vagrant up ansible 

--------------

 This will start both VMs with correct order and setup.

    Access the ansible VM:

vagrant ssh ansible

(Optional) Shut down the client VM:

ansible-playbook /vagrant_data/close.yml -i /vagrant_data/hosts.ini

Monitor via web UI:
Open your browser and go to
https://192.168.121.225:9090
(Replace IP if your client VM’s IP is different!)

---Rumeysa Kaya---





