# 专注花园 focusgarden

两个单文件的专注计时应用，可以直接双击打开，也可以装到桌面当应用用。

| 应用 | 文件 | 单轮时长 | 每天上限 |
|---|---|---|---|
| 快乐番茄 | `happy-tomato.html` | 25 分钟 | 15 格 |
| 一刻花开 | `quarterbloom.html` | 15 分钟 | 15 朵 |

数据都存在浏览器本机（localStorage），两个应用各记各的，互不影响。

## 目录

```
focusgarden/
├── index.html                    入口页
├── happy-tomato.html             快乐番茄
├── quarterbloom.html             一刻花开
├── manifest-tomato.webmanifest   番茄的应用清单
├── manifest-bloom.webmanifest    花开的应用清单
├── sw.js                         service worker（离线缓存）
└── icons/                        图标，180 / 192 / 512 三档
```

## 部署

1. 在 GitHub 新建仓库 `focusgarden`，公开
2. 把本目录所有文件推到 `main` 分支
3. 仓库 Settings → Pages → Source 选 `Deploy from a branch`，分支 `main`、目录 `/ (root)`
4. 等一分钟，访问 `https://<用户名>.github.io/focusgarden/`

手机上打开后，用浏览器菜单里的「安装应用」或「添加到主屏幕」，两个应用会各自生成一个图标。

## 改了内容之后

`sw.js` 用的是「缓存优先 + 后台更新」：打开页面先用缓存，同时后台拉新版本，**下次打开就是新的**，一般不用手动处理。

只有在想强制让所有设备立刻换新时，才需要把 `sw.js` 里的

```js
const CACHE = 'focusgarden-v1';
```

改成 `v2`、`v3`……数字一变，旧缓存会在下次打开时整个清掉。

## 注意

- 页面里存的是本机数据，换设备、换浏览器都不会同步
- 清理浏览器数据会把记录一起清掉，建议定期用页面里的「导出 JSON」备份
- 从桌面版（双击打开）迁移到网页版，用「导出 JSON」→「导入 JSON」，两边是不同的域名，不会自动同步
