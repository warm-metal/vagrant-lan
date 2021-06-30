# Vagrant LAN

This project helps create virtual machines(vm) in the same LAN. 
Each vm as only one hostonly NIC and it accesses the Internet via the only gateway machine in the same LAN.

The project only works for the VirtualBox provider on either MacOS or Linux host. The guest can be any OS.

## Usage

First of all, you need **VirtualBox** and  **vagrant**.

Then, download or clone this repo to your mac or pc.

Run `vagrant up` in the `gateway` directory to initialize the LAN gateway.
The gateway will be stopped automatically after halting the last machine in the LAN, and also started before the first machine getting up.

You can modify the network configuration in the Vagrantfile.
Variables shown in the table below can be modified to change the network configuration.
Once any variables in the table are changed, make sure they are identical in Vagrantfiles of both gateway and vms.

| Variable | Description |
| --- | --- |
| VM_LAN | The name of virtualbox host network that often is in the form of `vboxnetN`. It is determined by virtualbox while the network creating. Users can create a hostonly network manually, or leave it to vagrant. If vagrant doesn't found the network users specified, it will create a new hostonly network. But the name of the new network might not match the given name. Users must change the given value to the name of the network just created. |
| VM_LAN_IP_PREFIX | The network ID of the LAN which depends on the net mask. It must end with a .(dot). |
| VM_LAN_MASK | The net mask of the LAN |
| VM_LAN_IP | The IP address of the hostonly bridge. It often is the first address of the LAN. |
| VM_LAN_GATEWAY_IP | The IP address of the only gateway machine in the LAN. |
| GATEWAY_MACHINE | The name of the gateway machine. |
| ROOT_RSA | The path to a SSH id that is used to execute IP address allocating approches before machine provisioning. |

Finally, use the Vagrantfile in the `vm` folder to start your machines. Users can modify variables below to change the vm spec.
| Variable | Description |
| --- | --- |
| CLUSTER_NAME | The group name of the machines. All machines created by the same Vagrantfile will be places in the same group. The default group name is the name of the folder where the Vagrantfile is located. |
| NUM_VMS | Number of machines in the same group |
| NUM_CPU_CORES | Number of CPU cores of each vm |
| CAP_MEMORY | Memory spec of each vm in MB |
| BASE_BOX | The name of the vagrant box |
