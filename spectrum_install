---
- name: Prepare Spectrum servers
  hosts: spectrum_servers
  become: yes

  tasks:

    - name: Check operating system
      command: cat /etc/redhat-release
      register: os_version

    - name: Display OS version
      debug:
        var: os_version.stdout

    - name: Check available disk space
      command: df -h
      register: disk_space

    - name: Display disk space
      debug:
        var: disk_space.stdout

    - name: Install required packages
      yum:
        name:
          - unzip
          - wget
          - tar
        state: present

    - name: Create Spectrum installation directory
      file:
        path: /opt/spectrum
        state: directory
        mode: '0755'

    - name: Copy installation package
      copy:
        src: SpectrumInstaller.tar.gz
        dest: /opt/spectrum/SpectrumInstaller.tar.gz

    - name: Extract installation package
      unarchive:
        src: /opt/spectrum/SpectrumInstaller.tar.gz
        dest: /opt/spectrum
        remote_src: yes

    - name: Check Spectrum process
      shell: ps -ef | grep -i spectrum | grep -v grep
      register: spectrum_process
      failed_when: false

    - name: Display Spectrum process status
      debug:
        var: spectrum_process.stdout
