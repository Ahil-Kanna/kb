---
description: Doc to deploy nested ESX using ansible
---

# Nested ESX

Install the following in Linux

{% tabs %}
{% tab title="centos-py2" %}
```bash
yum install python-pip -y
pip install ansible
ansible-playbook -i input_spec.yml deploy.yml
```
{% endtab %}

{% tab title="centos-py3" %}
```
yum install python3-pip -y
pip3 install ansible
ansible-playbook -i input_spec.yml deploy.yml
```
{% endtab %}
{% endtabs %}

{% file src="../.gitbook/assets/deploy.yml" caption="deploy.yml" %}

{% code title="input\_spec.yml" %}
```yaml
# This has to be a valid yaml, json is also allowed
all:
  vars:
    # Todo: Update iso file
    esxiIsoPath: http://build-squid.eng.vmware.com/build/mts/release/bora-15843807/publish/VMware-VMvisor-Installer-7.0.0-15843807.x86_64.iso
  children:
    base_esxi:
      hosts:
        # info: name of esx - need not match dns or ip
        # info: need esx details, uses vim25 api's to deploy vm
        physical_esx1:
          # info: ip/dns
          ansible_host: '<ESX_IP>'
          ansible_user: 'root'
          ansible_password: '<PASSWORD>'
          datastore: '<DATASTORE>'
          # info: iso cannot be copied incase of vsan datastore, so need to have a non vsan disk for iso copy
          iso_ds: '<DATASTORE>'

    nested_esx:
      vars:
        ansible_user: root
        ansible_password: Skoda1!
        dns: 192.168.101.5
        # info: Can be any number of portgroups
        networks: ['<PORTGRP>', '<PORTGRP>']
      children:
        mgmt_esxi:
          hosts:
            # info: name of vm, good to change it to something else
            Mgmt-esxmb1:
              ansible_host: 192.168.101.101
              fqdn: esxmb1.cloud.vmw
            Mgmt-esxmb2:
              ansible_host: 192.168.101.102
              fqdn: esxmb2.cloud.vmw
            Mgmt-esxmb3:
              ansible_host: 192.168.101.103
              fqdn: esxmb3.cloud.vmw
            Mgmt-esxmb4:
              ansible_host: 192.168.101.104
              fqdn: esxmb4.cloud.vmw
          vars:
            gateway: 192.168.101.1
            vlan: 100

```
{% endcode %}



### References:

* Deploy ESX on VSAN - [https://www.virtuallyghetto.com/2013/11/how-to-run-nested-esxi-on-top-of-vsan.html](https://www.virtuallyghetto.com/2013/11/how-to-run-nested-esxi-on-top-of-vsan.html)
* [https://www.virtuallyghetto.com/nested-virtualization](https://www.virtuallyghetto.com/nested-virtualization)

