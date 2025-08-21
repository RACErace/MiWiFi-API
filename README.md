# 小米路由器 API 参考文档

## 获取路由器初始化信息

请求 URL：`http://192.168.31.1/cgi-bin/luci/api/xqsystem/init_info`

请求方法：`GET`

认证方式：`无`

请求示例：

```bash
curl "http://192.168.31.1/cgi-bin/luci/api/xqsystem/init_info"
```

响应示例：
```json
{
  "code": 0,
  "isSupportMesh": 1,
  "secAcc": 1,
  "inited": 1,
  "connect": 0,
  "routerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "child_router": "0",
  "mesh_nodes": [],
  "hardware": "RD08",
  "support160M": 1,
  "miioVer": "2",
  "isRedmi": 0,
  "romversion":"1.1.26",
  "countrycode": "CN",
  "imei": "",
  "modules": {
    "replacement_assistant": "1"
  },
  "id": "xxxxx/xxxxxxxxx",
  "routername": "xxx",
  "showPrivacy": 0,
  "displayName": "Xiaomi路由器BE6500 Pro",
  "miioDid": "xxxxxxxxx",
  "moduleVersion": "",
  "maccel": "1",
  "model": "xiaomi.router.rd08",
  "wifi_ap": 1,
  "bound": 0,
  "newEncryptMode": 1,
  "language": "zh_cn"
}
```

响应参数：

参数 | 参数说明 | 参数类型 | 值
-- | -- | -- | --
`code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0`
`isSupportMesh` | 是否支持 Mesh 网络<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1`
`secAcc` | 是否启用安全访问<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1`
`inited` | 路由器是否已初始化<ul><li>`0`：未初始化</li><li>`1`：已初始化</li></ul> | `int` | `1`
`connect` | 路由器是否已连接到互联网<ul><li>`0`：未连接</li><li>`1`：已连接</li></ul> | `int` | `0`
`routerId` | 路由器唯一标识符 | `str` | `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
`child_router` | 是否为子路由器<ul><li>`0`：不是</li><li>`1`：是</li></ul> | `int` | `0`
`mesh_nodes` | Mesh 网络节点列表 | `list` | `[]`
`hardware` | 路由器硬件型号 | `str` | `RD08`
`support160M` | 是否支持 160MHz 频宽<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1`
`miioVer` | miIO 协议版本 | `str` | `2`
`isRedmi` | 是否为 Redmi 路由器<ul><li>`0`：不是</li><li>`1`：是</li></ul> | `int` | `0`
`romversion` | 路由器固件版本 | `str` | `1.1.26`
`countrycode` | 路由器所在国家代码 | `str` | `CN`
`imei` | 路由器 IMEI 号 | `str` |
`modules` | 路由器支持的功能模块 | `obj` |
`replacement_assistant` | 是否支持更换助手功能<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1`
`id` | 路由器设备 ID | `str` | `xxxxx/xxxxxxxxx`
`routername` | 路由器名称 | `str` | `xxx`
`showPrivacy` | 是否显示隐私政策<ul><li>`0`：不显示</li><li>`1`：显示</li></ul> | `int` | `0`
`displayName` | 路由器显示名称 | `str` | `Xiaomi路由器BE6500 Pro`
`miioDid` | miIO 设备 ID | `str` | `xxxxxxxxx`
`moduleVersion` | 路由器模块版本 | `str` |
`maccel` | 是否启用 MAC 加速<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1`
`model` | 路由器型号 | `str` | `xiaomi.router.rd08`
`wifi_ap` | 是否启用 Wi-Fi 热点<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1`
`bound` | 路由器是否已绑定到小米账号<ul><li>`0`：未绑定</li><li>`1`：已绑定</li></ul> | `int` | `0`
`newEncryptMode` | 是否启用新加密模式<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1`
`language` | 路由器语言设置 | `str` | `zh_cn`

---

## 登录路由器

请求 URL：`http://192.168.31.1/cgi-bin/luci/api/xqsystem/login`

请求方法：`POST`

认证方式：`无`

请求参数：
参数 | 参数说明 | 参数类型 | 默认值
-- | -- | -- | --
`username` | 登录用户名，必填固定为`admin`。 | `str` | `admin`
`password` | 通过`oldPwd()`加密后的登录密码，必填。 | `str` |
`logtype` | 登录类型，必填。 | `int` | `2`
`nonce` | 登录随机数，必填通过`nonceCreat()`获取。 | `str` |

请求示例：

```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/api/xqsystem/login" \
  --data-urlencode "username=admin" \
  --data-urlencode "password=<oldPwd>" \
  --data-urlencode "logtype=2" \
  --data-urlencode "nonce=<nonce>"
```

响应示例：

```json
{
  "url": "/cgi-bin/luci/;stok=e244da90292d265d9cf2e36f433d9457/web/home",
  "token": "e244da90292d265d9cf2e36f433d9457",
  "code": 0
}
```

响应参数：

参数 | 参数说明 | 参数类型 | 值
-- | -- | -- | --
`url` | 登录成功后跳转的 URL | `str` | `/cgi-bin/luci/;stok=e244da90292d265d9cf2e36f433d9457/web/home`
`token` | 登录成功后返回的 Token，用于后续接口认证。 | `str` | `e244da90292d265d9cf2e36f433d9457`
`code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0`

备注

获取`key`和`deviceId`

```js
async function getKeyAndDeviceId() {
  const res = await fetch('http://192.168.31.1/cgi-bin/luci/web', {
    method: 'GET',
  });
  const html = await res.text();
  const keyMatch = html.match(/key:\s*'([^']+)'/);
  const deviceIdMatch = html.match(/deviceId\s*=\s*'([^']+)'/);
  return {
    key: keyMatch?.[1] ?? '',
    deviceId: deviceIdMatch?.[1] ?? '',
  };
}
```

获取加密后的密码

```js
function oldPwd(pwd, key) {
  if(newEncryptMode == 1){
    return CryptoJS.SHA256(this.nonce + CryptoJS.SHA256(pwd + key).toString()).toString();
  }else{
    return CryptoJS.SHA1(this.nonce + CryptoJS.SHA1(pwd + key).toString()).toString();
  }
}
```

获取登录随机数

```js
function createNonce() {
  var type = 0;
  var deviceId = 'xx:xx:xx:xx:xx:xx';
  var time = Math.floor(new Date().getTime() / 1000);
  var random = Math.floor(Math.random() * 10000);
  return [type, deviceId, time, random].join('_');
}
```

---
