Ansible module that allows you to define and create a VMWare vsphere guest OS instance which can then be booted to start an automated install.

Here is an example of defining the guest:

    - hosts: 127.0.0.1
      connection: local
      user: username
      sudo: false
      gather_facts: false
      serial: 1
    
      tasks:
    
        - vsphere_guest: > 
            vcenter_hostname='vcenter.host.edu' user='username' password='password' 
            datacenter="Dev_Datacenter" datastore="hit04_sata_datastore04" esxi_hostname="esx15.mgt.host.edu" 
            vm_name="romeotestvm" vm_memory_mb=2048 vm_num_cpus=2 vm_notes="woohoo" guestosid="rhel6_64Guest"
            power_on=yes
            args:
                vm_cdrom:
                    type: "iso"
                    iso_path: "hit04_iso_datastore/path/to/kickstart_boot.iso"
                vm_extra_config:
                    vcpu.hotadd: 'TRUE'
                    mem.hotadd:  'TRUE'            
                vm_disk:                
                    disk1:                     
                        size_gb: 1
                        datastore: "hit04_sata_datastore04"
                        type: "thin"
                    disk2:
                        size_gb: 2
                        datastore: "hit04_sata_datastore05"
                        type: "thin"
                vm_nic:
                    nic1:
                        type: "vmxnet3"
                        network: "dv_172_16_4_0_24"
                        network_type: "dvs"
                    nic2:
                        type: "vmxnet3"
                        network: "dv_128_171_16_0_24"
                        network_type: "dvs"
