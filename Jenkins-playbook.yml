---
- name: Install jenkins
  hosts: localhost
  become: yes
  become_user: root

  tasks:
  - name: Update all packages to their latest version
    apt:
      name: "*"
      state: latest

  - name: download jenkins key
    ansible.builtin.get_url:
      url: https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      dest: /usr/share/keyrings/jenkins-keyring.asc
        
  - name: Add Jenkins repo
    ansible.builtin.apt_repository:
      repo: deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/
      state: present
      filename: jenkins.list  

  - name: Update all packages to their latest version
    apt:
      name: "*"
      state: latest

  - name: Install fontconfig
    shell: apt install fontconfig -y    

  - name: Install java
    shell: apt install fontconfig openjdk-17-jre -y  

  - name: Install the Jenkins
    ansible.builtin.apt:
      name: jenkins
      state: present  

  - name: Make sure a service unit is running
    ansible.builtin.systemd:
      state: started
      name: jenkins
      enabled: yes    
