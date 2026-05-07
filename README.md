# pyipatool
苹果商店搜索下载历史版本工具

> 参考 [majd/ipatool](https://github.com/majd/ipatool) 项目，使用 Python 重新实现。

## 功能
- Apple ID 认证登录
- 搜索 iOS 应用
- 查看应用历史版本
- 下载指定版本的 IPA 文件
- 通过 Bundle ID 查询应用信息

## 安装
### 通过 pip 安装
```bash
pip install pyipatool
```

## 配置
复制配置文件示例并根据需要修改：
```bash
cp data/config.json.example data/config.json
```

配置文件说明：
- `auth`: Apple ID 认证信息
- `paths`: 存储路径设置
- `urls`: API 接口地址
- `download`: 下载设置
- `http`: HTTP 请求设置

## 用法

### 1. 认证相关命令

#### 登录 Apple ID
```bash
pyipatool auth login -e your_email@example.com -p your_password
```

#### 撤销凭证
```bash
pyipatool auth revoke
```

#### 查看当前登录信息
```bash
pyipatool auth info
```

### 2. 搜索应用
```bash
pyipatool search "微信" --limit 10
```

### 3. 列出应用版本
通过 App ID 列出版本：
```bash
pyipatool list-versions -i 123456789
```

通过 Bundle ID 列出版本：
```bash
pyipatool list-versions -b com.tencent.xin
```

### 4. 下载应用
下载最新版本：
```bash
pyipatool download -b com.tencent.xin --output ./downloads
```

下载指定版本：
```bash
pyipatool download -b com.tencent.xin --version-id 123456789 --output ./downloads
```

### 5. 查询应用信息
```bash
pyipatool lookup -b com.tencent.xin
```

## 更新说明
- **v1.0.0** (2026-01-07): 为 lookup、search、listversion、download 命令添加对于 5002 错误的重试机制
- **v1.0.1** (2026-01-07): 发布pyipatool的pypi包
- **V1.0.5** (2026-01-07): 修复路径依赖bug,默认配置文件在python安装包目录下
- **V1.0.6** (2026-01-08): 更新支持import方式调用api
- **V1.0.7** (2026-01-08): 更新get-version-metadata接口用于反查list-versions查询结果的版本id
- **V1.0.8** (2026-05-07): 改用 bag 接口动态获取认证端点，登录前先请求 init.itunes.apple.com/bag.xml 获取 authenticateAccount 地址，并增加最多4次重试逻辑（支持302重定向跟随及首次无效凭证重试）