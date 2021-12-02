[基于仓库的README](./README1.md)

etherpad-lite: 1.8.16

### 使用前
1. 先看下原版说明书，配置环境这些就不说了；
2. 项目先本地跑起来；

### 过程
0. npm的源要注意下，国内有时候会让你浪费很多时间
```jsunicoderegexp
npm get registry
https://registry.yarnpkg.com/
```
1. 启动服务中 另起窗口安装plugins
```jsunicoderegexp
窗口A:
./bin/run.sh

窗口B:
npm i ep_pluginsname
```
2. __settings.json__ 文件手动把注解删除，看着碍眼，想看说明在 __settings.json.template__
看就行了;
3. 安装插件，都是在根目录底下搞哈~ 以评论插件为例 __ep_comments_page__ 这个安装前提需要 __formidable@v3__ 升级到最新稳定版本(别问问啥，目前我也不清楚)；
```md
 npm i ep_comments_page 

+ ep_comments_page@0.1.79
  updated 1 package and audited 1243 packages in 17.527s

```
3. 第二步完事后，打开本地跑的项目, 地址 __ip:port/admin/plugins__ 插件随便安装完吧，安装后记得看控制台是否已经安装完毕。
这步骤是有问题的，在后台看不到别的插件，只能看到 __ep_comment_page__
4. 所以通过命令行尝试了下，
```md
 npm i ep_headings2
+ ep_headings2@0.2.35
  added 1 package from 3 contributors, removed 1 package and audited 1244 packages in 10.783s


```
5. 再次重启 
```jsunicoderegexp
./bin/run/sh 显示如下
```
```md
[2021-12-02 10:41:54.235] [INFO] server - Starting Etherpad...
[2021-12-02 10:41:54.517] [INFO] plugins - Running npm to get a list of installed plugins...
[2021-12-02 10:41:54.642] [INFO] plugins - npm --version: 6.14.15
[2021-12-02 10:42:07.592] [INFO] plugins - Loading plugin ep_comments_page...
[2021-12-02 10:42:07.593] [INFO] plugins - Loading plugin ep_etherpad-lite...
[2021-12-02 10:42:07.593] [INFO] plugins - Loading plugin ep_headings2...
[2021-12-02 10:42:07.595] [INFO] plugins - Loaded 3 plugins
```
于是，我一口气
```jsunicoderegexp
npm install ep_markdown ep_align ep_font_color ep_webrtc ep_embedded_hyperlinks2


+ ep_align@0.3.42
+ ep_markdown@0.1.41
+ ep_embedded_hyperlinks2@1.2.4
+ ep_webrtc@0.1.91
+ ep_font_color@0.0.52
added 41 packages from 27 contributors and audited 1285 packages in 26.528s

```
于是，我重启了下
```code
./bin/run.sh
[2021-12-02 11:00:02.968] [INFO] server - Starting Etherpad...
[2021-12-02 11:00:03.135] [INFO] plugins - Running npm to get a list of installed plugins...
[2021-12-02 11:00:03.492] [INFO] plugins - npm --version: 6.14.15
[2021-12-02 11:00:14.209] [INFO] plugins - Loading plugin ep_align...
[2021-12-02 11:00:14.209] [INFO] plugins - Loading plugin ep_comments_page...
[2021-12-02 11:00:14.209] [INFO] plugins - Loading plugin ep_embedded_hyperlinks2...
[2021-12-02 11:00:14.209] [INFO] plugins - Loading plugin ep_etherpad-lite...
[2021-12-02 11:00:14.210] [INFO] plugins - Loading plugin ep_font_color...
[2021-12-02 11:00:14.210] [INFO] plugins - Loading plugin ep_headings2...
[2021-12-02 11:00:14.210] [INFO] plugins - Loading plugin ep_markdown...
[2021-12-02 11:00:14.210] [INFO] plugins - Loading plugin ep_webrtc...
[2021-12-02 11:00:14.213] [INFO] plugins - Loaded 8 plugins
```
接着报错来了
```jsunicoderegexp
[2021-12-02 11:03:35.724] [INFO] Minify - Compress JS file ../node_modules/unorm/lib/unorm.js.
[2021-12-02 11:03:40.269] [WARN] client - TypeError: Cannot read property 'getUserMedia' of undefined -- {
  errorId: 'fvQSdjIgOj1g2ZmvjHo6',
  type: 'Unhandled Promise rejection',
  msg: "TypeError: Cannot read property 'getUserMedia' of undefined",
  url: 'http://0.0.0.0:9001/p/%E7%89%9B%E9%80%BC%E5%95%8A',
  source: 'unknown',
  linenumber: -1,
  userAgent: 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.107 Safari/537.36',
  stack: "TypeError: Cannot read property 'getUserMedia' of undefined\n" +
    '    at r (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:13356)\n' +
    '    at eval (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:13716)\n' +
    '    at Array.map (<anonymous>)\n' +
    '    at Object.updateLocalTracks (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:13678)\n' +
    '    at async eval (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:15086)\n' +
    '    at async Object.activate (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:15263)\n' +
    '    at async Object.postAceInit (eval at R (http://0.0.0.0:9001/static/js/require-kernel.js?v=7023e8cc:1:1), <anonymous>:3:10625)'
}

```
看着像是webrtc的， 然后卸载了
```jsunicoderegexp
npm uninstall ep_webrtc


./bin/run

[2021-12-02 11:08:23.826] [INFO] plugins - npm --version: 6.14.15
[2021-12-02 11:08:40.312] [INFO] plugins - Loading plugin ep_align...
[2021-12-02 11:08:40.312] [INFO] plugins - Loading plugin ep_comments_page...
[2021-12-02 11:08:40.313] [INFO] plugins - Loading plugin ep_embedded_hyperlinks2...
[2021-12-02 11:08:40.313] [INFO] plugins - Loading plugin ep_etherpad-lite...
[2021-12-02 11:08:40.313] [INFO] plugins - Loading plugin ep_font_color...
[2021-12-02 11:08:40.313] [INFO] plugins - Loading plugin ep_headings2...
[2021-12-02 11:08:40.313] [INFO] plugins - Loading plugin ep_markdown...
[2021-12-02 11:08:40.326] [INFO] plugins - Loaded 7 plugins

```

6. 插件好好玩 接着稿 重复上述步骤
```jsunicoderegexp
npm i ep_inline_toolbar
+ ep_inline_toolbar@0.2.8
added 1 package from 1 contributor and audited 1302 packages in 31.905s

```


