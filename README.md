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

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `isSupportMesh` | 是否支持 Mesh 网络<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1` |
| `secAcc` | 是否启用安全访问<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1` |
| `inited` | 路由器是否已初始化<ul><li>`0`：未初始化</li><li>`1`：已初始化</li></ul> | `int` | `1` |
| `connect` | 路由器是否已连接到互联网<ul><li>`0`：未连接</li><li>`1`：已连接</li></ul> | `int` | `0` |
| `routerId` | 路由器唯一标识符 | `str` | `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| `child_router` | 是否为子路由器<ul><li>`0`：不是</li><li>`1`：是</li></ul> | `int` | `0` |
| `mesh_nodes` | Mesh 网络节点列表 | `list` | `[]` |
| `hardware` | 路由器硬件型号 | `str` | `RD08` |
| `support160M` | 是否支持 160MHz 频宽<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1` |
| `miioVer` | miIO 协议版本 | `str` | `2` |
| `isRedmi` | 是否为 Redmi 路由器<ul><li>`0`：不是</li><li>`1`：是</li></ul> | `int` | `0` |
| `romversion` | 路由器固件版本 | `str` | `1.1.26` |
| `countrycode` | 路由器所在国家代码 | `str` | `CN` |
| `imei` | 路由器 IMEI 号 | `str` |  |
| `modules` | 路由器支持的功能模块 | `obj` |  |
| `replacement_assistant` | 是否支持更换助手功能<ul><li>`0`：不支持</li><li>`1`：支持</li></ul> | `int` | `1` |
| `id` | 路由器设备 ID | `str` | `xxxxx/xxxxxxxxx` |
| `routername` | 路由器名称 | `str` | `xxx` |
| `showPrivacy` | 是否显示隐私政策<ul><li>`0`：不显示</li><li>`1`：显示</li></ul> | `int` | `0` |
| `displayName` | 路由器显示名称 | `str` | `Xiaomi路由器BE6500 Pro` |
| `miioDid` | miIO 设备 ID | `str` | `xxxxxxxxx` |
| `moduleVersion` | 路由器模块版本 | `str` |  |
| `maccel` | 是否启用 MAC 加速<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1` |
| `model` | 路由器型号 | `str` | `xiaomi.router.rd08` |
| `wifi_ap` | 是否启用 Wi-Fi 热点<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1` |
| `bound` | 路由器是否已绑定到小米账号<ul><li>`0`：未绑定</li><li>`1`：已绑定</li></ul> | `int` | `0` |
| `newEncryptMode` | 是否启用新加密模式<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `1` |
| `language` | 路由器语言设置 | `str` | `zh_cn` |

---

## 登录路由器

请求 URL：`http://192.168.31.1/cgi-bin/luci/api/xqsystem/login`

请求方法：`POST`

认证方式：`无`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `username` | 登录用户名，必填固定为`admin`。 | `str` | `admin` |
| `password` | 通过`oldPwd()`加密后的登录密码，必填。 | `str` |  |
| `logtype` | 登录类型，必填。 | `int` | `2` |
| `nonce` | 登录随机数，必填通过`nonceCreat()`获取。 | `str` |   ||

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

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `url` | 登录成功后跳转的 URL | `str` | `/cgi-bin/luci/;stok=e244da90292d265d9cf2e36f433d9457/web/home` |
| `token` | 登录成功后返回的 Token，用于后续接口认证。 | `str` | `e244da90292d265d9cf2e36f433d9457` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

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

获取登录随机数| 
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

## 重启路由器

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/reboot`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `client` | 操作平台<ul><li>`web`</li></ul> | `str` |  |


请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/reboot" \
  --data-urlencode "client=web"
```

响应示例：
```json
{
  "lanIp": [
    {
      "mask": "255.255.255.0",
      "ip": "192.168.31.1"
    }
  ],
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `lanIp` | 当前 LAN 配置 | `obj` |  |
| `mask` | 子网掩码 | `srt` |`255.255.255.0` |
| `ip` | 路由器 IP 地址 | `srt` | `192.168.31.1` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 关闭路由器（无效）

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/shutdown`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/shutdown"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 恢复出厂设置（未测试）

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/reset`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `format` | 响应格式<ul><li>`0`</li><li>`1`</li></ul> | `int` |  |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/reset" \
  --data-urlencode "format=0"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取路由器语言

请求 URL：`http://192.186.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/get_languages`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/get_languages"
```

响应示例：
```json
{
  "list": [
    {
      "lang": "zh_cn",
      "name": "简体中文"
    },
    {
      "lang": "zh_hk",
      "name": "香港繁體"
    },
   {
      "lang": "zh_tw",
      "name": "台湾繁體"
    }
  ],
  "lang": "zh_cn",
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `list` | 支持的语言列表 | `list` | `[{lang: "zh_cn", name: "简体中文"}, ...]` |
| `lang` | 当前语言设置 | `str` | `zh_cn` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置路由器语言

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_language`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：
| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `language` | 语言代码，必填。<ul><li>`zh_cn`：简体中文</li><li>`zh_hk`：香港繁體</li><li>`zh_tw`：台湾繁體</li></ul> | `str` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_language" \
  --data-urlencode "language=zh_cn"
```
响应示例：
```json
{
  "code": 0
}
```

响应参数：
| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取路由器系统信息

请求 URL：`http://192.168.31.1//cgi-bin/luci/;stok={token}/api/misystem/messages`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/messages"
```

响应示例：
```json
{
  "messages": [],
  "count": 0,
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `messages` | 系统消息列表 | `list` | `[]` |
| `count` | 消息数量 | `int` | `0` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取路由器名称

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/router_name`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/router_name"
```

响应示例：
```json
{
  "locale": "xxx",
  "name": "xxx",
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `locale` | 路由器位置 | `str` | `xxx` |
| `name` | 路由器名称 | `str` | `xxx` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置路由器名称

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/set_router_name`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `name` | 路由器名称，必填。 | `str` |  |
| `locale` | 路由器位置，必填。 | `str` |  |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/set_router_name" \
  --data-urlencode "name=<routername>" \
  --data-urlencode "locale=<locale>"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取路由器 IP 冲突信息

请求 URL：`http://192.168.31.1//cgi-bin/luci/;stok={token}/api/misystem/r_ip_conflict`

请求方法：`POST`

认证方式：`Token` | `stok`

请求示例：
```bash
curl -X POST "http://192.168.31.1//cgi-bin/luci/;stok={token}/api/misystem/r_ip_conflict"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取Wi-Fi热点信息

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/wifi_detail_all`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/wifi_detail_all"
```

响应示例：
```json
{
  "bsd": 1,
  "info": [
    {
      "ifname": "wl1",
      "channelInfo": {
        "bandwidth": "0",
        "bandList": [
          "20",
          "40"
        ],
        "channel": 1
      },
      "encryption": "psk2",
      "wifimode": "11ax",
      "bandwidth": "0",
      "kickthreshold": "0",
      "status": "1",
      "mode": "Master",
      "bsd": "1",
      "ssid": "xxx",
      "weakthreshold": "0",
      "device": "wifi0.network1",
      "ax": "1",
      "hidden": "0",
      "password": "xxxxxxxx",
      "weakenable": "0",
      "ssid_len_limit": "28",
      "channel": "0",
      "txpwr": "max",
      "txbf": "3",
      "available_channels": [
        {
          "c": 0,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 1,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 2,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 3,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 4,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 5,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 6,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 7,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 8,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 9,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 10,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 11,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 12,
          "b": [
            "20",
            "40"
          ]
        },
        {
          "c": 13,
          "b": [
            "20",
            "40"
          ]
        }
      ],
      "signal": -91
    },
    {
      "ifname": "wl0",
      "channelInfo": {
        "bandwidth": "0",
        "bandList": [
          "20",
          "40",
          "80",
          "160"
        ],
        "channel": 40
      },
      "encryption": "psk2",
      "wifimode": "11ax",
      "bandwidth": "0",
      "kickthreshold": "0",
      "status": "1",
      "mode": "Master",
      "bsd": "1",
      "ssid": "xxx",
      "weakthreshold": "0",
      "device": "wifi1.network1",
      "ax": "1",
      "hidden": "0",
      "password": "xxxxxxxx",
      "weakenable": "0",
      "ssid_len_limit": "31",
      "channel": "0",
      "txpwr": "max",
      "txbf": "3",
      "available_channels": [
        {
          "c": 0,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 36,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 40,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 44,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 48,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 52,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 56,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 60,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 64,
          "b": [
            "20",
            "40",
            "80",
            "160"
          ]
        },
        {
          "c": 149,
          "b": [
            "20",
            "40",
            "80"
          ]
        },
        {
          "c": 153,
          "b": [
            "20",
            "40",
            "80"
          ]
        },
        {
          "c": 157,
          "b": [
            "20",
            "40",
            "80"
          ]
        },
        {
          "c": 161,
          "b": [
              "20",
              "40",
              "80"
          ]
        },
        {
          "c": 165,
          "b": [
            "20"
          ]
        }
      ],
      "signal": -94
    }
  ],
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `bsd` | 是否启用 Wi-Fi 热点<ul><li>`1`：启用</li><li>`0`：未启用</li></ul> | `int` | `1` |
| `info` | Wi-Fi 热点信息列表 | `list` | `[{ifname: "wl1", channelInfo: {...}, encryption: "psk2", ...}, ...]` |
| `ifname` | 接口名称 | `str` | `wl1` |
| `channelInfo` | 频道信息 | `obj` |  |
| `bandwidth` | 频宽<ul><li>`0`：自动</li><li>`20`：20MHz</li><li>`40`：40MHz</li><li>`80`：80MHz</li><li>`160`：160MHz</li></ul> | `str` | `0` |
| `bandList` | 支持的频宽列表 | `list` | `["20", "40"]` |
| `channel` | 当前频道 | `int` | `1` |
| `encryption` | 加密方式<ul><li>`none`：无加密</li><li>`wep`：WEP</li><li>`psk2`：WPA2-PSK</li></ul> | `str` | `psk2` |
| `wifimode` | Wi-Fi 模式<ul><li>`11ax`：Wi-Fi 6</li><li>`11ac`：Wi-Fi 5</li><li>`11n`：Wi-Fi 4</li></ul> | `str` | `11ax` |
| `kickthreshold` | 踢出阈值 | `str` | `0` |
| `status` | 热点状态<ul><li>`1`：启用</li><li>`0`：未启用</li></ul> | `str` | `1` |
| `mode` | 热点模式<ul><li>`Master`：主模式</li><li>`Slave`：从模式</li></ul> | `str` | `Master` |
| `bsd` | 是否启用广播服务<ul><li>`1`：启用</li><li>`0`：未启用</li></ul> | `str` | `1` |
| `ssid` | 热点 SSID | `str` | `xxx` |
| `weakthreshold` | 弱信号阈值 | `str` | `0` |
| `device` | 设备标识 | `str` | `wifi0.network1` |
| `ax` | 是否支持 Wi-Fi 6<ul><li>`1`：支持</li><li>`0`：不支持</li></ul> | `str` | `1` |
| `hidden` | 是否隐藏 SSID<ul><li>`1`：隐藏</li><li>`0`：不隐藏</li></ul> | `str` | `0` |
| `password` | Wi-Fi 密码 | `str` | `xxxxxxxx` |
| `weakenable` | 是否启用弱信号增强<ul><li>`1`：启用</li><li>`0`：未启用</li></ul> | `str` | `0` |
| `ssid_len_limit` | SSID 长度限制 | `str` | `28` |
| `channel` | 频道设置<ul><li>`0`：自动</li><li>`1-13`：手动设置</li></ul> | `str` | `0` |
| `txpwr` | 发射功率<ul><li>`max`：最大</li><li>`min`：最小</li></ul> | `str` | `max` |
| `txbf` | MIMO 技术支持<ul><li>`0`：不支持</li><li>`1`：支持</li><li>`2`：2x2 MIMO</li><li>`3`：3x3 MIMO</li></ul> | `str` | `3` |
| `available_channels` | 可用频道列表 | `list` | `[{c: 0, b: ["20", "40"]}, ...]` |
| `c` | 频道号 | `int` | `0` |
| `b` | 支持的频宽列表 | `list` | `["20", "40"]` |
| `signal` | 信号强度（dBm） | `int` | `-91` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取网络拓扑图

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/topo_graph`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/topo_graph"
```

响应示例：
```json
{
    "show": 0,
    "graph": {
        "ssid": "xxx",
        "color": 100,
        "ip": "192.168.31.1",
        "locale": "xx",
        "name": "xxx",
        "channel": "release",
        "hardware": "RD08",
        "mode": 0,
        "renumber": 0,
        "onlines": "6"
    },
    "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `show` | 是否显示拓扑图<ul><li>`0`：不显示</li><li>`1`：显示</li></ul> | `int` | `0` |
| `graph` | 拓扑图信息 | `obj` |  |
| `ssid` | Wi-Fi SSID | `str` | `xxx` |
| `color` | 拓扑图颜色 | `int` | `100` |
| `ip` | 路由器 IP 地址 | `str` | `192.168.31.1` |
| `locale` | 路由器位置 | `str` | `xx` |
| `name` | 路由器名称 | `str` | `xxx` |
| `channel` | 频道信息 | `str` | `release` |
| `hardware` | 路由器硬件型号 | `str` | `RD08` |
| `mode` | 拓扑图模式<ul><li>`0`：默认</li><li>`1`：高级</li></ul> | `int` | `0` |
| `renumber` | 是否重新编号<ul><li>`0`：不重新编号</li><li>`1`：重新编号</li></ul> | `int` | `0` |
| `onlines` | 在线设备数量 | `str` | `6` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 添加Mesh节点

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/add_mesh_node`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `mac` | Mesh 节点 MAC 地址，必填。 | `str` |
| `local` | Mesh 节点位置，必填。 | `str` |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/add_mesh_node" \
  --data-urlencode "mac=<mac>" \
  --data-urlencode "local=<local>"
```

响应示例：
```json
{
  "code": 0,
  "status": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `status` | 添加状态<ul><li>`0`：添加成功</li><li>`1`：正在连接mesh节点</li><li>`2`：正在同步Mesh网络配置</li><li>`3`：正在扩展Mesh网络</li><li>`4`：失败</li></ul> | `int` | `0` |

---

## 获取添加子节点状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_addnode_status`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `mac` | Mesh 节点 MAC 地址，必填。 | `str` |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_addnode_status" \
  --data-urlencode "mac=<mac>"
```

响应示例：
```json
{
  "code": 0,
  "status": 0
  
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `status` | 添加状态<ul><li>`0`：添加成功</li><li>`1`：正在连接mesh节点</li><li>`2`：正在同步Mesh网络配置</li><li>`3`：正在扩展Mesh网络</li><li>`4`：失败</li></ul> | `int` | `0` |

---

## 获取可添加的Mesh子节点

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/scan_mesh_node`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/scan_mesh_node"
```

响应示例：
```json
{
  "list": [],
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `list` | 可添加的 Mesh 子节点列表 | `list` | `[]` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 路由器带宽测试

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/bandwidth_test`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `new` | 开始新的带宽测试，固定为`1` | `int` | `1` |
| `history` | 获取历史测试结果，固定为`1` | `int` | `1` |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/bandwidth_test" \
  --data-urlencode "history=1"
```

响应示例：
```json
{
  "manual": 0,
  "bandwidth2": 49.17,
  "code": 0,
  "upload": 6293.76,
  "download": 257172.48,
  "bandwidth": 2009.16
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `manual` | 是否手动测试<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `bandwidth2` | 上传带宽（Mbps） | `float` | `49.17` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `upload` | 上传速度（KB/s） | `float` | `6293.76` |
| `download` | 下载速度（KB/s） | `float` | `257172.48` |
| `bandwidth` | 下载带宽（Mbps） | `float` | `2009.16` |

---

## 手工设置外网带宽

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/set_band`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `manual` | 是否手动设置带宽，固定为`1` | `int` | `1` |
| `upload` | 上传带宽，必填，单位 Mbps。 | `int` |  |
| `download` | 下载带宽，必填，单位 Mbps。 | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/set_band" \
  --data-urlencode "manual=1" \
  --data-urlencode "upload=50" \
  --data-urlencode "download=200"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取多WAN状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetdetect/nettb2`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetdetect/nettb2"
```

响应示例：
```json
{
  "info": [
    {
      "wantype": "eth",
      "disabled": 0,
      "name": "wan",
      "error": 0,
      "wanname": "WAN1"
    },
    {
      "wantype": "eth",
      "disabled": 1,
      "name": "wan_2",
      "error": 1,
      "wanname": "WAN2"
    }
  ],
  "on": 0,
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `info` | 外网信息列表 | `list` | `[{wantype: "eth", disabled: 0, name: "wan", ...}, ...]` |
| `wantype` | 外网类型<ul><li>`eth`：有线</li><li>`pppoe`：PPPoE</li><li>`dhcp`：动态 IP</li><li>`static`：静态 IP</li></ul> | `str` | `eth` |
| `disabled` | 是否禁用<ul><li>`0`：未禁用</li><li>`1`：已禁用</li></ul> | `int` | `0` |
| `name` | 外网接口名称 | `str` | `wan` |
| `error` | 是否有错误<ul><li>`0`：无错误</li><li>`1`：有错误</li></ul> | `int` | `0` |
| `wanname` | 外网名称 | `str` | `WAN1` |
| `on` | 是否启开启多wan<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取多WAN配置信息

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/get_ps_service`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `service` | 服务名称，必填。<ul><li>`multiwan`：多WAN</li></ul> | `str` | `multiwan` |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/get_ps_service" \
  --data-urlencode "service=multiwan"
```

响应示例：
```json
{
  "multiwan": {
    "enable": 0,
    "policy": {
      "bandwidth_wan1": "0",
      "currwan": "wan",
      "weight1": "1",
      "bandwidth_wan2": "0",
      "mode": 0,
      "weight2": "1"
    },
    "port_map": [
      {
        "name": "WAN1",
        "port": "1"
      },
      {
        "name": "WAN2",
        "port": "-1"
      }
    ]
  },
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `multiwan` | 多WAN信息 | `obj` |  |
| `enable` | 是否启用多WAN<ul><li>`0`：未启用</li><li>`1`：已启用</li></ul> | `int` | `0` |
| `policy` | 多WAN策略信息 | `obj` |  |
| `bandwidth_wan1` | WAN1 带宽，单位 Mbps | `str` | `0` |
| `currwan` | 当前使用的外网接口名称 | `str` | `wan` |
| `weight1` | WAN1 权重 | `str` | `1` |
| `bandwidth_wan2` | WAN2 带宽，单位 Mbps | `str` | `0` |
| `mode` | 多WAN模式<ul><li>`0`：负载均衡</li><li>`1`：主备模式</li></ul> | `int` | `0` |
| `weight2` | WAN2 权重 | `str` | `1` |
| `port_map` | 端口映射信息列表 | `list` | `[{name: "WAN1", port: "1"}, ...]` |
| `name` | 外网名称 | `str` | `WAN1` |
| `port` | 物理端口号<ul><li>`1`：LAN1</li><li>`2`：LAN2</li><li>`3`：LAN3</li><li>`4`：LAN4</li><li>`-1`：未映射</li></ul> | `str` | `1` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取设备列表

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/devicelist`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `mlo` | 是否开启MLO<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/devicelist" \
  --data-urlencode "mlo=1"
```

响应示例：
```json
{
  "mac": "XX:XX:XX:XX:XX:XX",
  "list": [
    {
      "mac": "XX:XX:XX:XX:XX:XX",
      "oname": "xxxx-xxx-xxx",
      "isap": 0,
      "pctlv2": 0,
      "parent": "XX:XX:XX:XX:XX:XX",
      "authority": {
        "wan": 1
      },
      "push": 0,
      "online": 1,
      "name": "xxxx-xxx-xxx",
      "times": 0,
      "ip": [
        {
          "downspeed": "67",
          "online": "661",
          "active": 1,
          "upspeed": "94",
          "ip": "192.168.31.12"
        }
      ],
      "statistics": {
        "downspeed": "67",
        "online": "661",
        "upspeed": "94"
      },
      "icon": "",
      "type": 1
    }
  ],
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `mac` | 路由器 MAC 地址 | `str` | `XX:XX:XX:XX:XX:XX` |
| `list` | 设备列表 | `list` | `[{mac: "XX:XX:XX:XX:XX:XX", oname: "xxxx-xxx-xxx", ...}, ...]` |
| `mac` | 设备 MAC 地址 | `str` | `XX:XX:XX:XX:XX:XX` |
| `oname` | 设备原始名称 | `str` | `xxxx-xxx-xxx` |
| `isap` | 是否为AP<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `pctlv2` | 家长控制版本 | `int` | `0` |
| `parent` | 家长控制父设备 MAC 地址 | `str` | `XX:XX:XX:XX:XX:XX` |
| `authority` | 设备权限信息 | `obj` |  |
| `wan` | 是否允许访问外网<ul><li>`0`：不允许</li><li>`1`：允许</li></ul> | `int` | `1` |
| `push` | 是否允许推送通知<ul><li>`0`：不允许</li><li>`1`：允许</li></ul> | `int` | `0` |
| `online` | 设备在线状态<ul><li>`0`：离线</li><li>`1`：在线</li></ul> | `int` | `1` |
| `name` | 设备名称 | `str` | `xxxx-xxx-xxx` |
| `times` | 设备连接次数 | `int` | `0` |
| `ip` | 设备 IP 地址列表 | `list` | `[{downspeed: "67", online: "661", ...}, ...]` |
| `downspeed` | 当前下载速度，单位 Kbps | `str` | `67` |
| `online` | 在线时长，单位 秒 | `str` | `661` |
| `active` | 是否为活跃 IP<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `upspeed` | 当前上传速度，单位 Kbps | `str` | `94` |
| `ip` | 设备 IP 地址 | `str` | `192.168.31.12` |
| `statistics` | 设备流量统计信息 | `obj` |  |
| `downspeed` | 当前下载速度，单位 Kbps | `str` | `67` |
| `online` | 在线时长，单位 秒 | `str` | `661` |
| `upspeed` | 当前上传速度，单位 Kbps | `str` | `94` |
| `icon` | 设备图标 URL | `str` |  |
| `type` | 连接方式<ul><li>`0`: 有线</li><li>`1`: 2.4G wifi</li><li>`2`: 5G wifi</li><li>`3`: guest wifi</li></ul> | `int` | `1` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 禁止设备上网

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_mac_filter`

请求方法：`GET`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `mac` | 设备 MAC 地址，必填。 | `str` |  |
| `wan` | 是否禁止设备访问外网，必填。<ul><li>`0`：禁止</li><li>`1`：允许</li></ul> | `int` |  |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_mac_filter" \
  --data-urlencode "mac:<mac>" \
  --data-urlencode "wan:0"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取路由器状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/status`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/status"
```

响应示例：
```json
{
  "dev": [
    {
      "mac": "XX:XX:XX:XX:XX:XX",
      "maxdownloadspeed": "65044762",
      "isap": 0,
      "upload": "4532221195",
      "upspeed": "75782",
      "downspeed": "1476517",
      "online": "32917",
      "devname": "xxxx-xxx-xxx",
      "maxuploadspeed": "12499260",
      "download": "3735522348"
    }
  ],
  "code": 0,
  "mem": {
    "usage": 0.43,
    "total": "256MB",
    "hz": "1333MHz",
    "type": "DDR3"
  },
  "temperature": 0,
  "count": {
    "all_without_mash": 10,
    "online": 4,
    "all": 10,
    "online_without_mash": 4
  },
  "hardware": {
    "mac": "XX:XX:XX:XX:XX:XX",
    "platform": "RD08",
    "version": "1.1.26",
    "channel": "release",
    "ispName": "",
    "sn": "XXXXX/XXXXXXXXX",
    "DisplayRomVer": "1.1.26",
    "displayName": "Xiaomi路由器BE6500 Pro"
  },
  "upTime": "64117.27",
  "cpu": {
    "core": 4,
    "hz": "1000MHz",
    "load": 0
  },
  "wan": {
    "downspeed": "1476561",
    "maxdownloadspeed": "65045487",
    "devname": "nil",
    "upload": "5562483924",
    "upspeed": "75800",
    "maxuploadspeed": "12600163",
    "download": "8912571853"
  }
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `dev` | 连接设备列表 | `list` | `[{mac: "XX:XX:XX:XX:XX:XX", maxdownloadspeed: "65044762", ...}, ...]` |
| `mac` | 设备 MAC 地址 | `str` | `XX:XX:XX:XX:XX:XX` |
| `maxdownloadspeed` | 设备最大下载速度，单位 bps | `str` | `65044762` |
| `isap` | 是否为AP<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `upload` | 设备上传总流量，单位 Byte | `str` | `4532221195` |
| `upspeed` | 设备当前上传速度，单位 bps | `str` | `75782` |
| `downspeed` | 设备当前下载速度，单位 bps | `str` | `1476517` |
| `online` | 设备在线时长，单位 秒 | `str` | `32917` |
| `devname` | 设备名称 | `str` | `xxxx-xxx-xxx` |
| `maxuploadspeed` | 设备最大上传速度，单位 bps | `str` | `12499260` |
| `download` | 设备下载总流量，单位 Byte | `str` | `3735522348` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `mem` | 内存信息 | `obj` |  |
| `usage` | 内存使用率 | `float` | `0.43` |
| `total` | 内存总量 | `str` | `256MB` |
| `hz` | 内存频率 | `str` | `1333MHz` |
| `type` | 内存类型 | `str` | `DDR3` |
| `temperature` | 路由器温度，单位 摄氏度 | `int` | `0` |
| `count` | 设备统计信息 | `obj` |  |
| `all_without_mash` | 非Mesh设备总数 | `int` | `10` |
| `online` | 在线设备总数 | `int` | `4` |
| `all` | 设备总数 | `int` | `10` |
| `online_without_mash` | 非Mesh在线设备总数 | `int` | `4` |
| `hardware` | 硬件信息 | `obj` |  |
| `mac` | 路由器 MAC 地址 | `str` | `XX:XX:XX:XX:XX:XX` |
| `platform` | 路由器硬件型号<ul><li>`R1D`：小米路由器</li><li>`R2D`：小米路由器2</li><li>`R3D`：小米路由器HD</li><li>`R1CM`：小米路由器MINI</li><li>`R1CL`：小米路由器青春版</li><li>`R3`：小米路由器3</li><li>`R3L`：小米路由器3C</li><li>`R3P`：小米路由器3 Pro</li><li>`R3A`：小米路由器3A</li><li>`R3G`：小米路由器3G</li><li>`R4`：小米路由器4</li><li>`R4C`：小米路由器4Q</li><li>`R4CM`：小米路由器4C</li><li>`D01`：小米路由器Mesh</li><li>`R4AC`：小米路由器4A</li><li>`R4A`：小米路由器4 v2</li><li>`R3Gv2`：小米路由器3G</li><li>`R2600`：小米路由器2600</li><li>`R2100`：小米路由器AC2100</li><li>`R1500`：小米路由器1500</li><li>`R3600`：小米AIoT路由器 AX3600</li><li>`R1800`：小米AIoT路由器 AX1800</li><li>`RA72`：小米路由器 AX6000</li><li>`RA80`：小米路由器 AX3000</li><li>`RA81`：Redmi路由器 AX3000</li><li>`RB08`：Xiaomi HomeWiFi</li><li>`RC01`：Xiaomi万兆路由器</li><li>`RC06`：Xiaomi路由器BE7000</li><li>`RD02`：Redmi路由器 AX3000</li><li>`RD08`：Xiaomi路由器BE6500 Pro</li></ul> | `str` | `RD08` |
| `version` | 路由器固件版本 | `str` | `1.1.26` |
| `channel` | 路由器固件渠道<ul><li>`current`：内测版</li><li>`release`：稳定版</li><li>`stable`：开发版</li></ul> | `str` | `release` |
| `ispName` | 运营商名称 | `str` |  |`" "` |
| `sn` | 路由器序列号 | `str` | `XXXXX/XXXXXXXXX` |
| `DisplayRomVer` | 显示的固件版本 | `str` | `1.1.26` |
| `displayName` | 路由器显示名称 | `str` | `Xiaomi路由器BE6500 Pro` |
| `upTime` | 路由器运行时间，单位 秒 | `str` | `64117.27` |
| `cpu` | CPU 信息 | `obj` |  |
| `core` | CPU 核心数 | `int` | `4` |
| `hz` | CPU 频率 | `str` | `1000MHz` |
| `load` | CPU 负载百分比 | `int` | `0` |
| `wan` | 外网信息 | `obj` |  |
| `downspeed` | 外网当前下载速度，单位 bps | `str` | `1476561` |
| `maxdownloadspeed` | 外网最大下载速度，单位 bps | `str` | `65045487` |
| `devname` | 外网接口名称 | `str` | `nil` |
| `upload` | 外网上传总流量，单位 Byte | `str` | `5562483924` |
| `upspeed` | 外网当前上传速度，单位 bps | `str` | `75800` |
| `maxuploadspeed` | 外网最大上传速度，单位 bps | `str` | `12600163` |
| `download` | 外网下载总流量，单位 Byte | `str` | `8912571853` |

---

## 检查PPPoE拨号状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/pppoe_status`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/pppoe_status"
```

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `wan_name` | 外网接口名称，必填。<ul><li>`WAN1`：WAN1</li><li>`WAN2`：WAN2</li></ul> | `str` |  |

请求示例：
```bash
curl -G "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/pppoe_status" \
  --data-urlencode "wan_name=WAN1"
```

响应示例：
```json
{
  "proto": "dhcp",
  "dns": [
    "192.168.1.1"
  ],
  "code": 0,
  "status": 2,
  "gw": "192.168.1.1",
  "ip": {
    "mask": "255.255.255.0",
    "address": "192.168.1.78"
  }
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `proto` | 外网连接类型<ul><li>`pppoe`：PPPoE</li><li>`dhcp`：DHCP</li><li>`static`：静态IP</li></ul> | `str` | `dhcp` |
| `dns` | 外网 DNS 服务器列表 | `list` | `["192 .168.1.1"]` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `status` | PPPoE 拨号状态<ul><li>`1`: 正在拨号</li><li>`2`: 拨号成功</li><li>`3`: 拨号失败</li><li>`4`: 已断开</li></ul> | `int` | `2` |
| `gw` | 外网网关地址 | `str` | `192.168.1.1` |
| `ip` | 外网 IP 信息 | `obj` |  |
| `mask` | 外网子网掩码 | `str` | `255.255.255.0` |
| `address` | 外网 IP 地址 | `str` | `192.168.1.78` |

---

## 检查wan口连接状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_wan_status`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_wan_status"
```

响应示例：
```json
{
  "ipv6": {
    "code": 0,
    "wan6_info": {
      "ip6addr": [
        "240e:398:4cac:ca30:92fb:5dff:fe3a:70a6/128"
      ],
      "ifname": "eth0.1",
      "dns": [
        "fe80::1"
      ],
      "up": true,
      "lan_ip6addr": [
        [
          "240e:398:4cac:ca32::1/64"
        ]
      ],
      "ip6gw": "fe80::1",
      "lan_ip6prefix": [
        "240e:398:4cac:ca32::"
      ],
      "ipv6_mode": "native"
    }
  },
  "code": 0,
  "ipv4": {
    "proto": "dhcp",
    "dns": [
      "192.168.1.1"
    ],
    "code": 0,
    "status": 2,
    "gw": "192.168.1.1",
    "ip": {
      "mask": "255.255.255.0",
      "address": "192.168.1.78"
    }
  }
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `ipv6` | IPv6 信息 | `obj` |  |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |
| `wan6_info` | IPv6 外网信息 | `obj` |  |
| `ip6addr` | IPv6 外网地址列表 | `list` | `["240e:398:4cac:ca30:92fb:5dff:fe3a:70a6/128"]` |
| `ifname` | IPv6 外网接口名称 | `str` | `eth0.1` |
| `dns` | IPv6 外网 DNS 服务器列表 | `list` | `["fe80::1"]` |
| `up` | IPv6 外网连接状态<ul><li>`true`：已连接</li><li>`false`：未连接</li></ul> | `bool` | `true` |
| `lan_ip6addr` | IPv6 内网地址列表 | `list` | `[["240e:398:4cac:ca32::1/64"]]` |
| `ip6gw` | IPv6 外网网关地址 | `str` | `fe80::1` |
| `lan_ip6prefix` | IPv6 内网前缀列表 | `list` | `["240e:398:4cac:ca32::"]` |
| `ipv6_mode` | IPv6 连接模式<ul><li>`native`：自动配置</li><li>`dhcpv6`：DHCPv6</li><li>`pppoev6`：PPPoEv6</li><li>`static`：static</li><li>`passthrough`: Passthrough</li><li>`6to4`: Tunnel 6t04</li><li>`6rd`: Tunnel 6rd</li><li>`6in4`: Tunnel 6in4</li></ul> | `str` | `native` |
| `ipv4` | IPv4 信息 | `obj` |  |
| `proto` | IPv4 外网连接类型<ul><li>`pppoe`：PPPoE</li><li>`dhcp`：DHCP</li><li>`static`：静态IP</li></ul> | `str` | `dhcp` |
| `dns` | IPv4 外网 DNS 服务器列表 | `list` | `["192.168.1.1"]` |
| `status` | PPPoE 拨号状态<ul><li>`1`: 正在拨号</li><li>`2`: 拨号成功</li><li>`3`: 拨号失败</li><li>`4`: 已断开</li></ul> | `int` | `2` |
| `gw` | IPv4 外网网关地址 | `str` | `192 .168.1.1` |
| `ip` | IPv4 外网 IP 信息 | `obj` |  |
| `mask` | IPv4 外网子网掩码 | `str` | `255.255.255.0` |
| `address` | IPv4 外网 IP 地址 | `str` | `192.168.1.78` |

---

## 自动测速

请求 URL：`http://192.268.31.1/cgi-bin/luci/;stok={token}/api/misystem/active`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/misystem/active"
```

响应示例：
```json
{
  "code": 0,
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取MLO状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_hostap_mlo`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_hostap_mlo"
```

响应示例：
```json
{
  "mlo_enable": 1,
  "mlo_support": 1,
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `mlo_enable` | MLO 是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `mlo_support` | 设备是否支持 MLO<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置MLO状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_hostap_mlo`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `mlo_enable` | MLO 是否启用，必填。<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_hostap_mlo" \
  --data-urlencode "mlo_enable=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置WiFi状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_all_wifi`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `bsd` | 是否启用Wi-Fi多频合一<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `on1` | 2.4G WiFi 是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `ssid1` | 2.4G WiFi 名称，必填。 | `str` | `Xiaomi_XXXX` |
| `encryption1` | 2.4G WiFi 加密方式<ul><li>`none`：无密码</li><li>`wep`：WEP</li><li>`psk`：WPA-PSK</li><li>`psk2`：WPA2-PSK</li><li>`psk-mixed`：WPA/WPA2-PSK 混合</li></ul> | `str` | `psk2` |
| `channel1` | 2.4G WiFi 信道<ul><li>`0`：自动</li><li>`1`-`13`：指定信道</li></ul> | `int` | `0` |
| `bandwidth1` | 2.4G WiFi 信道宽度<ul><li>`0`：自动</li><li>`20`：20MHz</li><li>`40`：40MHz</li></ul> | `int` | `0` |
| `hidden1` | 2.4G WiFi 是否隐藏 SSID<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `txpwr1` | 2.4G WiFi 发射功率<ul><li>`min`：节能</li><li>`mid`：标准</li><li>`max`：穿墙</li></ul> | `str` | `max` |
| `pwd1` | 2.4G WiFi 密码，WEP 加密时为 5 或 13 位 ASCII 字符，WPA/WPA2 加密时为 8-63 位 ASCII 字符，必填。 | `str` | `password` |
| `on2` | 5G WiFi 是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `ssid2` | 5G WiFi 名称，必填。 | `str` | `Xiaomi_XXXX` |
| `encryption2` | 5G WiFi 加密方式<ul><li>`none`：无密码</li><li>`wep`：WEP</li><li>`psk`：WPA-PSK</li><li>`psk2`：WPA2-PSK</li><li>`psk-mixed`：WPA/WPA2-PSK 混合</li></ul> | `str` | `psk2` |
| `channel2` | 5G WiFi 信道<ul><li>`0`：自动</li><li>`36`、`40`、`44`、`48`：低频段</li><li>`52`、`56`、`60`、`64`：DFS 频段</li><li>`100`、`104`、`108`、`112`、`116`、`120`、`124`、`128`、`132`、`136`、`140`：DFS 频段</li><li>`149`、`153`、`157`、`161`、`165`：高频段</li></ul> | `int` | `0` |
| `bandwidth2` | 5G WiFi 信道宽度<ul><li>`0`：自动</li><li>`20`：20MHz</li><li>`40`：40MHz</li><li>`80`：80MHz</li><li>`160`：160MHz（仅部分型号支持）</li></ul> | `int` | `0` |
| `hidden2` | 5G WiFi 是否隐藏 SSID<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `txpwr2` | 5G WiFi 发射功率<ul><li>`min`：节能</li><li>`mid`：标准</li><li>`max`：穿墙</li></ul> | `str` | `max` |
| `pwd2` | 5G WiFi 密码，WEP 加密时为 5 或 13 位 ASCII 字符，WPA/WPA2 加密时为 8-63 位 ASCII 字符，必填。 | `str` | `password` |
| `on3` | Guest WiFi 是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `ssid3` | Guest WiFi 名称，必填。 | `str` | `Xiaomi_XXXX_Guest` |
| `encryption3` | Guest WiFi 加密方式<ul><li>`none`：无密码</li><li>`wep`：WEP</li><li>`psk`：WPA-PSK</li><li>`psk2`：WPA2-PSK</li><li>`psk-mixed`：WPA/WPA2-PSK 混合</li></ul> | `str` | `psk2` |
| `channel3` | Guest WiFi 信道，固定为 `0`（自动）。 | `int` | `0` |
| `bandwidth3` | Guest WiFi 信道宽度，固定为 `0`（自动）。 | `int` | `0` |
| `hidden3` | Guest WiFi 是否隐藏 SSID<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `txpwr3` | Guest WiFi 发射功率，固定为 `max`（最大）。 | `str` | `max` |
| `pwd3` | Guest WiFi 密码，WEP 加密时为 5 或 13 位 ASCII 字符，WPA/WPA2 加密时为 8-63 位 ASCII 字符，必填。 | `str` | `password` |
| `isDFS` | 是否启用 DFS 信道<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_all_wifi" \
  --data-urlencode "bsd=0" \
  --data-urlencode "on1=1" \
  --data-urlencode "ssid1=Xiaomi_XXXX" \
  --data-urlencode "encryption1=psk2" \
  --data-urlencode "channel1=0" \
  --data-urlencode "bandwidth1=0" \
  --data-urlencode "hidden1=0" \
  --data-urlencode "txpwr1=max" \
  --data-urlencode "pwd1=password" \
  --data-urlencode "on2=1" \
  --data-urlencode "ssid2=Xiaomi_XXXX" \
  --data-urlencode "encryption2=psk2" \
  --data-urlencode "channel2=0" \
  --data-urlencode "bandwidth2=0" \
  --data-urlencode "hidden2=0" \
  --data-urlencode "txpwr2=max" \
  --data-urlencode "pwd2=password" \
  --data-urlencode "on3=1" \
  --data-urlencode "ssid3=Xiaomi_XXXX_Guest" \
  --data-urlencode "encryption3=psk2" \
  --data-urlencode "hidden3=0" \
  --data-urlencode "pwd3=password" \
  --data-urlencode "isDFS=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取畅快连状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_miotrelay_switch`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_miotrelay_switch"
```

响应示例：
```json
{
  "enabled":1,
  "code":0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `enabled` | 畅快连是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `1` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取静默模式状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_wifi_silence`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_wifi_silence"
```

响应示例：
```json
{
  "on": 0,
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `on` | 静默模式是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` | `0` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置Wi-Fi6状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_ax`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `ax` | Wi-Fi6 是否启用<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |
| `isDFS` | 是否启用 DFS 信道<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_ax" \
  --data-urlencode "ax=1" \
  --data-urlencode "isDFS=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置MU-MIMO状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_txbf`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `txbf` | MU-MIMO 是否启用<ul><li>`0`：否</li><li>`1`：是</li><li>`3`：自动</li></ul> | `int` |  |
| `isDFS` | 是否启用 DFS 信道<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_txbf" \
  --data-urlencode "txbf=3" \
  --data-urlencode "isDFS=1"
```

响应示例：
```json
{
  "cac_time":0,
  "code":0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `cac_time` | DFS 信道切换等待时间，单位 秒 | `int` | `0` |
| `code` | 状态代码<ul><li>`0`：成功</li></li> | `int` | `0` |

---

## 设置畅快连状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/miotrelay_switch`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `on` | 畅快连是否启用，必填。<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/miotrelay_switch" \
  --data-urlencode "on=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取国家代码

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/country_code`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/country_code"
```

响应示例：
```json
{
  "current": "CN",
  "list": [
    {
      "name": "中国大陆",
      "code": "CN"
    }
],
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `current` | 当前国家代码 | `str` | `CN` |
| `list` | 支持的国家列表 | `list` | `[{"name": "中国大陆", "code": "CN"}, ...]` |
| `name` | 国家名称 | `str` | `中国大陆` |
| `code` | 国家代码 | `str` | `CN` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置国家代码

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_country_code`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `country` | 国家代码，必填。 | `str` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqsystem/set_country_code" \
  --data-urlencode "country=CN"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 获取TWT节能模式状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_twt`

请求方法：`GET`

认证方式：`Token` | `stok`

请求示例：
```bash
curl "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/get_twt"
```

响应示例：
```json
{
  "status": "0",
  "code": 0
}
```

响应参数：
| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `status` | TWT节能模式状态<ul><li>`0`：否</li><li>`1`：是</li></ul> | `str` | `0` |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置TWT节能模式状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_twt`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `on` | TWT节能模式是否启用，必填。<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_twt" \
  --data-urlencode "on=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---

## 设置静默模式状态

请求 URL：`http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_silence`

请求方法：`POST`

认证方式：`Token` | `stok`

请求参数：

| 参数 | 参数说明 | 参数类型 | 默认值 |
| --- | --- | --- | --- |
| `on` | 静默模式是否启用，必填。<ul><li>`0`：否</li><li>`1`：是</li></ul> | `int` |  |

请求示例：
```bash
curl -X POST "http://192.168.31.1/cgi-bin/luci/;stok={token}/api/xqnetwork/set_wifi_silence" \
  --data-urlencode "on=1"
```

响应示例：
```json
{
  "code": 0
}
```

响应参数：

| 参数 | 参数说明 | 参数类型 | 值 |
| --- | --- | --- | --- |
| `code` | 状态代码<ul><li>`0`：成功</li></ul> | `int` | `0` |

---