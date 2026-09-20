# 蹲蹲记 🚽

极简黑白风的「上厕所打卡」App —— 记录每次上厕所的时间与全天次数,统计习惯、看月历、看年度总结。

## 功能

- ✅ 点击大圆圈打卡,记录当时时间 + 全天次数
- ✅ 敲木鱼风格:飘字动画 + 合成木鱼音效 + 触觉震动
- ✅ 统计:累计/日均/连续天数/活跃天数
- ✅ 智能分析:总结一天中拉粑粑最频繁的时间段
- ✅ 24 小时分布柱状图
- ✅ 周期对比:本周 vs 上周、本月 vs 上月
- ✅ 打卡月历(可翻月)+ 年度总结(可翻年,12 个月柱状图)
- ✅ 设置:开关音效 / 开关震动、清空数据
- ✅ 数据仅存本地(localStorage),无广告、无联网、隐私安全

## 现在就能运行(3 种方式任选)

**方式 A:直接双击打开**
双击 `index.html`,用浏览器打开即可。数据保存在浏览器本地。

**方式 B:本地服务器(推荐,支持离线安装)**
在本目录下运行一个静态服务器,例如:

```powershell
# PowerShell,进入 dundunji 目录后:
python -m http.server 8080
# 或
npx serve .
```

然后手机/电脑浏览器打开 `http://localhost:8080`。

**方式 C:iPhone 直接安装成 App(PWA,免编译)**
1. 把 `dundunji` 文件夹放到一个能通过 https 访问的地方(比如 GitHub Pages、Vercel、Netlify 等免费静态托管)。
2. iPhone 用 Safari 打开该网址。
3. 点击底部「分享」→「添加到主屏幕」→ 完成。
4. 桌面上会出现「蹲蹲记」图标,点开就是全屏 App,和原生体验几乎一样,无需 Apple 开发者账号。

## 以后要上架 iOS App Store(跨平台编译)

你用的是 Windows、没有 Swift 环境,推荐用 **Capacitor**(把本项目网页打包成原生壳),然后通过云端构建 iOS 包 —— 全程不需要 Mac:

1. 安装 Node.js,然后:
```powershell
npm init -y
npm i @capacitor/core @capacitor/cli
npx cap init "蹲蹲记" "com.dundunji.app" --web-dir=.
npm i @capacitor/ios @capacitor/android
npx cap add android     # Android 可在 Windows 本地直接构建
npx cap add ios         # iOS 工程(在 Windows 上仅生成源码,无法本地编译)
```

2. **iOS 构建(Windows 无 Mac 的两种办法)**:
   - **Ionic Appflow / Capacitor Cloud Build**:云端自动打包 iOS,产出一个 `.ipa`。
   - **GitHub Actions + macOS runner**:把仓库推到 GitHub,用 mac 运行器自动构建 ipa。

3. 打包后用 Xcode / Transporter 上传 App Store Connect(需要 Apple 开发者账号,¥688/年)。

> 提示:如果只是想自己手机上用,走上面的「方式 C PWA」最省事,完全免费、无需编译、无需开发者账号。

## 文件结构

```
dundunji/
├── index.html           # 整个 App(单文件)
├── manifest.json        # PWA 清单
├── sw.js                # Service Worker(离线缓存)
├── icon.svg             # 矢量图标
├── icon-192.png / icon-512.png / apple-touch-icon.png   # 各尺寸图标
└── README.md
```

## 技术说明

- 纯 HTML/CSS/JS,零依赖构建,任何平台浏览器都能跑。
- 图标库 Lucide + 图表 Chart.js + 样式 Tailwind(均通过 CDN 引入)。
- 木鱼音效用 Web Audio API 合成,无需音频文件。
