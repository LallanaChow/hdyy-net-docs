- 在锐捷网络设备上，基于MAC地址的VLAN划分可以通过配置MAC VLAN功能来实现，允许用户在不同的物理端口上灵活接入网络。
## MAC VLAN的概述
- MAC VLAN是基于用户设备的MAC地址进行VLAN划分的一种方法。其主要优点在于用户可以在不同的交换机或端口之间移动，而无需重新配置VLAN。这种灵活性特别适合于动态变化的网络环境，如大型企业或会议室等场所 


- 配置步骤
1. 创建VLAN：在锐捷设备上，首先需要创建所需的VLAN。例如，创建VLAN 100和VLAN 200，分别用于不同的部门或用户组 
```bash
vlan 100
name 部门A
exit
vlan 200
name 部门B
exit
```
2. 配置接口：将与用户设备相连的接口配置为允许VLAN报文通过，并设置为MAC VLAN模式。确保接口的类型设置为Hybrid或Trunk，以支持多种VLAN 
```bash
interface GigabitEthernet 0/1
port link-type hybrid
port hybrid pvid vlan 100
mac-vlan enable
exit
```

3. 绑定MAC地址与VLAN：将用户设备的MAC地址与相应的VLAN进行绑定。这样，当设备接入网络时，系统会根据其MAC地址自动将其分配到对应的VLAN中 
```bash
mac-vlan mac-address 54bf.6450.dd10 vlan 100
mac-vlan mac-address 54bf.6450.dd20 vlan 200
```

4. 验证配置：使用命令检查MAC VLAN的配置是否生效。可以通过show mac-vlan interface命令查看接口的MAC VLAN信息，确保只有同一VLAN中的设备可以互相通信 
```bash
show mac-vlan interface
```
