## 测试环境节点描述

ipfs测试网，目前运行了4个节点，分别是：

> yihen@10.0.1.106:onchain
>
> yihen@10.0.1.107:onchain
>
> yihen@10.0.1.108:onchain
>
> yihen@10.0.1.128:onchain

```
其中 1.106、1.107、1.108这3个节点是运行节点；
1.128这个节点除了负责运行ipfs之外，还兼任ipfs编译部署的任务；
```



## 如何将本地ipfs节点，加入测试网？

1. 将下面内容保存至~/.ipfs/swarm.key文件中

   ```
   /key/swarm/psk/1.0.0/
   /base16/
   4929057a75acb32f200c67afc7b984daa2fa91122e9ed603943ec91268a5944a
   ```

2. 删除~/.ipfs/config中默认的bootstrap值，命令如下：

   ```
   ./ipfs bootstrap rm all
   ```

3. 增加测试网中的一个或多个节点作为启动连接节点，命令如下：

   ```
   ./ipfs bootstrap add /ip4/10.0.1.128/tcp/4001/ipfs/QmbN2Xd5scdQm1WMqrVkE2ad2dbjRMFKnnP2BX2yfhuave
   ```

4. 启动本地节点，命令如下：

   ```
   ./ipfs daemon &
   ```

5. 检验是否已经加入测试网络，命令如下：

   ```
   ./ipfs swarm peers
   ```

   

## 更新go-ipfs后，如何重新部署？

1. 登录ipfs测试环境部署机(10.0.1.128)，git pull更新代码至测试部署机；
2. cd $GO_IPFS_DIR & make build
3. 切换到$GO_IPFS_DIR/cmd/ipfs/ipfs目录下，执行ipfs-deploy命令，将编译好的ipfs可执行文件，分发至106 107 108三台机器；（4个节点的ipfs的运行目录都是在HOME/workspace/ipfs/bin/ipfs）
4. 重启 各个部署节点的 ipfs daemon；