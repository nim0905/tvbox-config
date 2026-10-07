# tvbox-config · 影视源配置仓库

影视盒子（FongMi 电视端）的**在线源仓库**。这里存放 4 套完整可用的本地库，
电视/盒子添加一个网址就能直接使用，**不需要手动导入文件、不需要解压**。

---

## 一、怎么用（电视端）

1. 电视上打开影视盒子 → 首页点 **配置**
2. 点 **＋** 新建，把下面任一地址粘进去，起个名字，确定
3. 自动下载并切换，首页内容立刻变成该库的站点列表

| 库 | 配置地址（直接复制） | 内容 |
|---|---|---|
| **饭太硬** | `https://raw.githubusercontent.com/nim0905/tvbox-config/main/fantaihard/api.json` | 49 站点 · 8 条直播 |
| **肥猫** | `https://raw.githubusercontent.com/nim0905/tvbox-config/main/feimao/api.json` | 39 站点 · 2 条直播 |
| **欧歌** | `https://raw.githubusercontent.com/nim0905/tvbox-config/main/ouge/api.json` | 122 站点 · 2 条直播（jar 最多） |
| **天微** | `https://raw.githubusercontent.com/nim0905/tvbox-config/main/tianwei/api.json` | 84 站点 · 6 条直播 |

> **国内直连打不开 raw.githubusercontent.com 时**，在地址前面加加速前缀，例如：
> `https://ghproxy.net/` + 上面的完整地址
> `https://ghfast.top/` + 上面的完整地址

---

## 二、为什么这样放就能用

每套库是一个**完整文件夹**，不只是配置文件：

```
fantaihard/
├── api.json      配置主文件（站点 + 直播 + 规则）
├── spider.jar    插件引擎（api 里的 csp_XXX 由它实现）
├── api/          drpy 运行时与依赖脚本
├── js/           站点专用脚本
└── lives/        直播源清单
```

播放器加载 `api.json` 时，会自动把里面写着的 `./spider.jar`、`./lib/xxx.js`
按**配置网址所在目录**换算成绝对地址去下载。所以只要 jar 和脚本跟 api.json
放在一起，整套就能跑起来 —— 这就是「一个网址搞定」的原理。

---

## 三、机器可读清单

`index.json` 列出了全部库的地址与统计信息，程序（比如源汇转换器）可以直接读它：

```json
{
  "count": 4,
  "libraries": [
    { "slug": "fantaihard", "name": "饭太硬",
      "config": "https://.../fantaihard/api.json",
      "sites": 49, "lives": 8 }
  ]
}
```

---

## 四、如何维护（网页操作，不用命令行）

### 换掉某个库的文件
1. 打开仓库 → 进入对应文件夹（如 `fantaihard/`）
2. 点右上角 **Add file → Upload files**
3. 把新文件拖进去（同名会覆盖）→ 底部点 **Commit changes**

### 新增一个库
1. 仓库首页 **Add file → Create new file**
2. 文件名输入 `新库名/api.json`（斜杠会自动建文件夹）
3. 把内容粘进去 → **Commit changes**
4. 再用 **Upload files** 把该库的 jar、脚本传进同一个文件夹
5. 最后更新根目录 `index.json` 加上这一条

### 看历史 / 回滚
- 仓库首页点 **commits**（提交历史）可看每次改动
- 想回到某个旧版本：找到那次提交 → 点文件 → **History** → 选旧版本 → 复制内容覆盖回来

---

## 五、给转换器用（本机批量）

用「源汇转换器」的 **本地库打包** 功能：
1. 选择含有若干库文件夹的**上一级目录**
2. 工具自动识别每个库，逐个打包成 `库名.zip` + 汇总 `index.json`
3. 把产物解压后按上面的目录结构传进本仓库即可

---

## 六、配套资料

- **影视盒子 2.0 APK** 已内置本仓库的 4 个库，装完即用，无需手动配置
- 完整的图文操作手册（装机 / 换源 / 维护仓库 / 账号安全 / 问题排查）
  见交付包里的 **《影视盒子2.0_联动维护手册》**

### 安全提醒

- 本仓库的更新**只需在网页操作**，日常维护不需要 token
- 如你有过 GitHub token，请在 <https://github.com/settings/tokens> 定期检查并删除不用的
- 密码与 token 属于敏感信息，请勿发送给他人或粘贴在聊天中

---

*本仓库由「影视盒子」项目维护，配置内容来自公开分享，仅供学习交流。*
