# dockerd-blockscout
使用 Docker 镜像快速搭建 [BlockScout](https://github.com/blockscout/blockscout) 以太坊区块浏览器服务。基础镜像 [luchenqun/blockscout](https://hub.docker.com/r/luchenqun/blockscout) 使用 [BlockScout](https://github.com/luchenqun/blockscout) 最新 `master` 分支进行自动编译。

## 准备工作
1. 安装 docker 以及 docker-compose 容器编排工具
3. 自建一个 `geth` 全节点，需要开放 `http` 和 `ws` 接口，并且允许 `net,debug,eth,web3,txpool` 等模块。示例：
```bash
geth --datadir ./data --gcmode archive --networkid 1 --nodiscover --http --http.vhosts="*" --http.corsdomain "*" --http.addr 0.0.0.0 --http.port 40000 --http.api "eth,net,web3,personal,admin,miner,txpool,debug" --ws --ws.addr 0.0.0.0 --ws.port 40000 --ws.api "eth,net,web3,personal,admin,miner,txpool,debug" --ws.origins '*' --verbosity 3 --unlock "0" --password ./pwd --allow-insecure-unlock --mine --miner.threads 1
```

## 修改配置
根据自己的情况修改 `.env`。也可以添加 BlockScout 支持的[环境变量](https://docs.blockscout.com/for-developers/information-and-settings/env-variables)。


## 启动blockscout
```bash
docker-compose up -d blockscout
```
执行完成之后浏览器访问 `http://localhost:4000` 进行查看。

## 删除blockscout
```bash
docker-compose down && rm -rf postgres-data
```