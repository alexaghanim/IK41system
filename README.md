---
- name: PlayBook
  hosts: all
  become: true
  gather_facts: false
  tasks:
  
  - name: Install required system packages
    apt: name={{ item }} state=latest update_cache=yes
    loop: [ 'apt-transport-https', 'ca-certificates', 'curl', 'software-properties-common', 'python-pip', 'virtualenv', 'python3-setuptools']

  - name: Add Docker GPG apt Key
    apt_key:
      url: https://download.docker.com/linux/ubuntu/gpg
      state: present

  - name: Add Docker Repository
    apt_repository:
      repo: deb https://download.docker.com/linux/ubuntu bionic stable
      state: present

  - name: Update apt and install docker-ce
    apt: update_cache=yes name=docker-ce state=latest

  - name: Install Docker Module for Python
    apt:
      name: docker
