### 钥匙管理

内容信任（Content Trust）与镜像标签（tag）直接关联，每个仓库都有一组密钥，发布者可以使用这些密钥对每个镜像进行签名。

一个仓库可以包含未签名和签名的镜像。 它们作为单独的实体存在，因此相同的标签（tag）（例如 `latest`）可以指向不同的内容，具体取决于客户端上是否启用了Docker Content Trust。

镜像信任（Image trust）构建在 4 种不同的密钥上：

- `root` 密钥（_offline_）是一个镜像内容信任（Content Trust）的根基。这是存储在 Yubikey 上的关键，只能在有限的操作中联机
- `targets` 密钥（_online_）对实际文件进行签名，储存在客户端上并在空闲时加密
- `snapshot` 密钥（_online_）对包含集合上所有其它元数据信息的元数据文件进行签名
- `timestamp` 密钥（_online_）定期通过带时间戳的签署声明确保内容的新鲜度

为了方便起见，`snapshot` 和 `timestamp` 可以通过 Notary 服务进行管理。
