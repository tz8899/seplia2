# seplia2
安装docker  这个什么都有 直接用这个代码安装docker

```bash
curl -fsSL https://get.docker.com | sudo sh
```


第二个备份用
测试

## 启动服务

在项目目录中运行以下命令启动服务：

```bash
docker-compose up -d
```

## 查看日志

使用以下命令查看服务日志：

```bash
docker-compose logs -f
```

## 注意事项

- 确保所有服务在同一网络中运行。
- 确保 JWT 秘密文件路径正确，并且两个服务都能访问。
- 检查防火墙设置，确保允许必要的端口。

## Step 6. Checking If Nodes Are Synced
➡️**Execution Node (Geth)**
```
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}' http://localhost:8545
```
* ✅Response if fully synced:
```json
{"jsonrpc":"2.0","id":1,"result":false}
```
* 🚫Response if still syncing:
```json
{"jsonrpc":"2.0","id":1,"result":{"currentBlock":"0x1a2b3c","highestBlock":"0x1a2b4d","startingBlock":"0x0"}}
```
* You'll see an object with `startingBlock`, `currentBlock`, and `highestBlock`, indicating the sync progress.

➡️**Beacon Node (Prysm)**
```bash
curl http://localhost:3500/eth/v1/node/syncing
```
* ✅Response if fully synced:
```json
{"data":{"head_slot":"12345","sync_distance":"0","is_syncing":false}}
```
If `is_syncing` is `false` and `sync_distance` is `0`, the beacon node is fully synced.

* 🚫Response if still syncing:
```json
{"data":{"head_slot":"12345","sync_distance":"100","is_syncing":true}}
```
* If `is_syncing` is `true`, the node is still syncing, and `sync_distance` indicates how many slots behind it is.

---
