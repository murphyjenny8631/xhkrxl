优贝官网代理【Q-——333307——】优贝官网代理【 辋芷《888yx●vip》 】
优贝官网代理【Q-——333307——】优贝官网代理【 辋芷《888yx●vip》 】

 从零到一：我用 GitHub Actions 构建自动化部署的完整实战记录

> 还在手动上传服务器？试试 GitHub Actions，让 CI/CD 流程自动化到“无感”。

大家好，我是老周。今天想和你分享一个我最近完成的小项目——用 GitHub Actions 把个人博客的部署流程彻底自动化。整个过程踩了不少坑，但最终效果确实让我“真香”了。

 为什么我非要折腾自动化？

以前我的部署流程是：本地改代码 -> 提交到 GitHub -> 登录服务器 -> 拉取代码 -> 重启服务。这套流程看起来没问题，但一忙起来就容易出错，尤其是忘了重启服务导致线上版本不一致，排查起来相当痛苦。

GitHub Actions 的好处在于，它能把我从繁琐的手动操作中解放出来，真正做到“推代码即部署”。

 项目结构怎么搭？

我的项目结构非常简单，主要分为两个分支：

- `main` 分支：存放源代码
- `gh-pages` 分支：存放构建后的静态文件（GitHub Pages 直接读取这个分支）

核心是 `.github/workflows/deploy.yml` 这个文件，它就是我整个自动化流程的“总指挥”。

 配置文件怎么写？

这里我给一个最精简的版本，方便你参考：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install & Build
        run: |
          npm install
          npm run build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```

 会遇到哪些坑？（重点）

1.  Token 权限不足：这里一定要用 `${{ secrets.GITHUB_TOKEN }}`，不要自己去创建 Personal Access Token，不然有安全风险还容易失效。
2.  构建目录错误：`publish_dir` 要指向你实际的构建输出目录，比如 Vuepress 是 `.vitepress/dist`，Next.js 是 `out`。之前我就写错过，导致部署上去是空页面。
3.  缓存问题：如果依赖安装慢，建议加上 `actions/cache` 缓存 `node_modules`，能节省至少一半时间。

 效果怎么样？

现在我的日常操作就是：写完代码，`git push`，然后就可以去泡杯茶。等茶凉了，线上已经更新好了。配合 Git Commit 的规范信息，整个工作流非常顺畅。

互动引导：你目前的工作流里，最耗时或最容易出错的环节是什么？在评论区聊聊你的部署痛点，或者分享你独特的自动化技巧，我们一起探讨下。如果这篇内容对你有启发，请点赞并关注我，后续会带来更多关于前端工程化落地的干货。

相关推荐：

https://github.com/parsonssophia0/gzhhhv/blob/main/%E6%95%B0%E5%AD%97%E6%96%87%E5%A8%B1%E5%8A%A8%E6%80%81%EF%BC%9A%E6%B1%87%E4%B8%B0%E6%B3%A8%E5%86%8C%E5%BC%80%E6%88%B7_%E5%B7%AB%E7%84%99%E7%BC%86%E8%87%83%E7%BF%B1ldjcu.md

<img src="https://i.postimg.cc/G3v5y5R4/mei-nu-bei-jing-zhao-shang-tu-zhi-zuo-(93).png" />

相关推荐：

https://github.com/parsonssophia0/gzhhhv/commit/9e2d04560f8bdc15ee4f7041fbd690abba072f78

<img src="https://i.postimg.cc/G3v5y5R4/mei-nu-bei-jing-zhao-shang-tu-zhi-zuo-(93).png" />
相关推荐：

https://github.com/collinsdaniel218/coqkfm/blob/main/2027%E7%AC%AC%E4%B8%80%E7%83%AD%E6%A6%9C%EF%BC%9A%E6%B1%87%E4%B8%B0%E6%B3%A8%E5%86%8C%E6%B5%8B%E9%80%9F_%E6%8F%BD%E9%85%A5%E7%98%B4%E5%83%96%E6%92%9Eyjwdj.md

<img src="https://i.postimg.cc/JhMytj62/mei-nu-bei-jing-zhao-shang-tu-zhi-zuo-(1).png" />
相关推荐：

https://github.com/collinsdaniel218/coqkfm/commit/4980c661dbf5c14801a70978fb7f0c01951d2292

<img src="https://i.postimg.cc/wxDGmGpn/mei-nu-bei-jing-zhao-shang-tu-zhi-zuo-(92).png" />

资讯来源：新华网、人民网、央视新闻、中新网、凤凰网、澎湃新闻、界面新闻、新浪新闻、搜狐网、财新网、观察者网、第一财经等主流平台，以独树一帜的观察视角与扎实的深度报道能力，在资讯领域收获广泛关注。
