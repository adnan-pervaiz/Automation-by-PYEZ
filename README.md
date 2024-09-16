# Automation-by-PYEZ

Configuration File Automation through PYEZ

PYEZ

• Allows to manage Junos devices

• Not tied to Junos version or to Junos product.

• A Juniper package for Python

• A package is a collection of Python modules

• Provides classes and methods


A Python framework


• Provides code that is useful for larger applications.

• Used by Ansible

• Has been tested with Python 2.6 and 2.7.

• Not supported with Python 3.x 


NETCONF PROTOCOL


• PyEZ uses Netconf.

• You need to enable Netconf on your devices.

• Netconf is a Protocol to manipulate configuration of network devices
• IETF standard (RFCs)

• Implemented by most vendors

• TCP transport, SSH encryption, XML encoding

• Uses RPC (remote procedure call) over SSH

• Client/server communication (the server is the network device)

• Server default port must be 830 and (RFC 6241 and 6242)


To enable the NETCONF service on the default port (830) on your devices

lab@ex4200-1# set system services netconf ssh
lab@ex4200-1# commit

In order to enable NETCONF using another port, use this junos command

lab@ex4200-1# set system services netconf ssh port port-number

You might want to create another user on your devices for PyEZ (to trace PyEZ activities)

CORNENTERCITE VTOE FDAECVTICSES, WITH PYEZ

Let’s execute this python program (print_facts.py).It prints the hostname and junos version for a list of devices defined into the program :

python facts/print_facts.py
the device ex4200-2 is a EX4200-24T running 12.3R11.2
The device ex4200-1 is a EX4200-24T running 12.2R2.4
the device ex4200-3 is a EX4200-24T running 12.3R11.2
the device ex4200-4 is a EX4200-24T running 12.3R11.2

It also write the output here
more my_devices_inventory.txt


IMPORT THE CLASS DEVICE

Import the class Device from the package PyEZ.
• The class Device is defined in the module device (device.py) in the package jnpr.junos.
• The class Device provides methods:
• For connecting to devices
• For retrieving facts (such as software number, …) from the devices



from jnpr.junos import Device
# Verify that the Device class has been loaded




INSTANTIATE THE CLASS DEVICE

Instantiate the class Device by declaring a variable (a_device) and calling the class Device passing arguments (your device credentials). This assigns the returned value (the newly created object) to the variable a_device. Example for qfx5100-3


a_device=Device (host="10.19.10.103", user="pytraining", password="Poclab123")

The object a_device is an instance of the class Device

>>> type (a_device)
<class 'jnpr.junos.device.Device'>
>>> a_device
Device(10.19.10.103)


 from pprint import pprint as pp
 
  pp (a_device.facts)
  
{'2RE': False,

'HOME': '/var/home/remote',

'RE0': {'last_reboot_reason': '0x2:watchdog ',

'mastership_state': 'master',

'model': 'EX4200-24T, 8 POE',

'status': 'OK',

'up_time': '4 days, 3 minutes, 'domain': 'poc-nl.jnpr.net', 45 seconds'},

'fqdn': 'ex4200-1.poc-nl.jnpr.net',

'hostname': 'ex4200-1',

'ifd_style': 'SWITCH',

'master': 'RE0',

'model': 'EX4200-24T',

'personality': 'SWITCH',

'serialnumber': 'BM0210118154',

'switch_style': 'VLAN',
''vvcc__cmaodpae'b:l e'':E nTabrluee,d',
'version': '12.2R2.4',
'version_RE0': '12.2R2.4',
'version_info': junos.version_info(major=(12, 2), type=R, minor=2, build=4)}

 Select some device facts

>>> a_device.facts["hostname"]
>>> 
'ex4200-1'

>>> a_device.facts["version"]
>>>
>>> 
'12.2R2.4'

>>> a_device.facts["version"]=="14.1R1.2"
False


DEMO JINJA2 AND YAML AND PYEZ

pytraining@py-automation-master:~$ python configuration_builder/configuration_builder_2.py

Start configuration building

generate config file for device qfx5100-10 : conf_file_run_phase_qfx5100-10.conf

generate config file for device qfx5100-6 : conf_file_run_phase_qfx5100-6.conf

generate config file for device qfx5100-8 : conf_file_run_phase_qfx5100-8.conf

done
