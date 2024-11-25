## KVM

#### KVM管理工具

>1. libvirt
>2. virsh
>3. virt-manager

#### Linux的模式

>1. 用户模式
>
>- 不能直接访问底层硬件
>  - 崩溃可恢复
>
>1. 内核模式
>   - 直接访问底层硬件
>     - 崩溃不可恢复

#### 硬件虚拟化

>1. KVM
>   - 完成内存和CPU的虚拟化
>2. qume
>   - I/O的虚拟化

虚拟网络组网模式

>1. KVM管理工具
>
>   ```shell
>   # libvirt
>   
>   # virsh
>   
>   #virt-manager
>   ```
>
>   
>
>2. Linux的模式
>
>   ```shell
>   # 用户模式
>   
>   # 内核模式
>   ```
>
>   
>
>3. 硬件虚拟化
>
>4. 虚拟网络组网模式
>
>5. 虚拟网桥
>
>6. qemu-kvm
>
>   ```shell
>   -m 设置内存大小 MB
>   -smp 设置CPU个数
>   -hda/drive 设置驱动
>   ```
>
>7. libirt XML配置文件
>
>   ```shell
>   <domain> 域标签
>   <name> 客户机名称
>   <vcpu> vcpu个数
>   <memory> 内存 KB
>   <os>操作系统类型和启动顺序
>   ```
>
>8. VIrsh管理虚拟机
>
>   ```shell
>   # 列出虚拟机列表
>   	virsh list 
>   	virsh list --all
>   	
>   # 创建虚拟机
>   	virsh define $xml	'创建但不启动'
>   	virsh create $xml	'创建并启动虚拟机'
>   	
>   # 启动虚拟机
>   	virsh start $name
>   	
>   # 查看虚拟机信息
>   	virsh dominfo $name
>   	
>   # 恢复暂停虚拟机
>   	virsh resume $name
>   	
>   #修改虚拟机的配置文件
>   	virsh edit $name
>   	
>   # 关闭虚拟机
>   	virsh shutdown $name '正常关闭'
>   	virsh destory $name '强制关闭'
>   	
>   # 重启虚拟机
>   	virsh reboot $name
>   	
>   # 删除虚拟机
>   	virsh undefine $name
>   ```
>
>9. Virsh 管理虚拟网络
>
>   ```shell
>   # 查看虚拟网络列表
>   	virsh net-list --all
>   	
>   # 创建/定义虚拟网络
>   	virsh net-define $xml
>   	
>   # 启动虚拟网络
>   	virsh net-start $name
>   	
>   # 查看虚拟网络基础信息
>   	virsh net-info $name
>   	
>   # 查看虚拟网络配置文件信息 （详细信息）
>   	virsh net-dumpxml $name
>   	
>   # 停止网络
>   	virsh net-destory $name
>   	
>   # 设置网络自启
>   	virsh net-autostart $name
>   	
>   # 删除网络
>   	virsh net-undefine $name
>   
>   ```
>
>10. Virsh管理虚拟存储池
>
>    ```shell
>    # 查看存储池列表
>    	virsh pool-list --all
>    
>    # 定义存储池
>    	virsh pool-define $name
>    
>    # 构造存储池
>    	virsh pool-build $name
>    
>    # 启动存储池
>    	virsh pool-start $name
>    
>    # 查看存储池的基本信息
>    	virsh pool-info $name
>    
>    # 查看存储池的配置文件信息
>    	virsh pool-dumpxml $name
>    
>    # 编辑/修改存储池配置文件
>    	virsh pool-edit $name
>    ```
>
>11. 
>
>