---
  - hosts: SEUGRUPO
    remote_user: SEULOGIN
    become: yes
    tasks:
      - name: cria uma VM ubuntu no vSphere
        vsphere_guest:
          vcenter_hostname: vcenter.dominio
          username: root 
          password: P@ssw0rd
          validate_certs: no
          guest: maquina de teste
          state: powered_off
          vm_extra_config:
            notes: Este e um exemplo de servidor web de producao
          vm_disk:
            disk1:
              size_gb: 10
              type: thin
              datastore: datastore1
          vm_nic:
            nic1:
              type: vmxnet3
              network: VM Network
              network_type: standard
          vm_hardware:
            memory_mb: 512
            num_cpus: 1
            osid: ubuntu64Guest
            scsi: paravirtual
          esxi:
            datacenter: datacenter1
            hostname: vmware-esxi.dominio
