### 容器云

1. #### 基础环境准备

   |     节点IP     |  角色  |   CPU   |  内存  |
   | :------------: | :----: | :-----: | :----: |
   | 192.168.200.20 | Master | 2个以上 | 2G以上 |
   | 192.168.200.13 | Worker | 2个以上 | 2G以上 |

   - 安装Kubeeasy

     ```shell
     # master节点
     
     mount -o loop chinaskills_cloud_paas_v2.0.2.iso /mnt/
     cp -rvf /mnt/* /opt/
     umount /mnt
     mv /opt/kubeeasy /var/bin/kubeeasy
     ```

   - 安装依赖包

     ```shell
     # master节点
     
     kubeeasy install depend \
     --host 192.168.200.20,192.168.200.13 \
     --usesr root \
     --password 000000 \
     --offline-file /opt/dependencies/base-rpms.tar.gz
     ```

   - 配置SSH免密钥

     ```shell
     # master节点
     
     #集群节点的连通性检测
     
     kubeeasy check ssh \
     --host 192.168.200.20,192.168.200.13 \
     --user root \
     --password 000000
     
     #集群节点间的免密钥配置
     
     kubeeasy create ssh-keygen \
     --master 192.168.200.20
     --worker 192.168.200.13
     --user root \
     --password 000000
     ```

2. 部署Kubernetes集群

   ```shell
   # master节点
   
   kubeeasy install kubernetes \
   --master 192.168.200.20 \
   --worker 192.168.200.13 \
   --user root \
   --password 000000 \
   --version 1.22.1 \	
   --offline-file /opt/kubernetes.tar.gz
   
   # 查看集群状态
   
   kubectl cluster-info
   
   # 查看负载情况
   
   kubectl top nodes --use-protocol-buffers
   ```

3. 部署KubeVirt集群

   ```shell
   # master节点
   
   # 安装KubeVirt
   
   kubeeasy add -virt kubevirt
   
   # 查看Pod
   
   kubectl -n kubevirt get pods
   ```

4. 部署Istio

   ```shell
   # master节点
   
   #安装Istio服务网格环境	(该过程有点慢请耐心等待)
   
   kubeeasy add --istio istio
   
   # 查看Pod
   
   kubectl -n istio-system get pods
   
   # 查看Istio版本信息
   
   istioctl version
   ```

5. 部署Harbor仓库

   ```shell
   # master节点
   
   # 安装Harbor仓库
   
   kubeeasy add --registry harbor
   
   # 查看仓库状态
   
   systemctl status harbor
   
   ```

   