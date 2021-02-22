# UptimeStatus
 > 一款基于UptimeRobot API的漂亮的网站监控面板。
## 食用方式
1. 下载或 clone 代码；
2. 第一次下载之后先执行 npm i 安装依赖；
3. 改 src/config.js 中的 apikeys；
4. 执行 npm run build 打包；
5. 把 build 目录下的静态文件随便找个地方扔就完事了。

## 基于 Cloudflare Workers 搭建 UptimeRobot API 代理，以解决官网 API 跨域问题

```
const handleRequest = async ({ request }) => {
  let url = new URL(request.url);
  let response = await fetch('https://api.uptimerobot.com' + url.pathname, request);
  response = new Response(response.body, response);
  response.headers.set('Access-Control-Allow-Origin', '*');
  response.headers.set('Access-Control-Allow-Methods', '*');
  response.headers.set('Access-Control-Allow-Credentials', 'true');
  response.headers.set('Access-Control-Allow-Headers', 'Content-Type,Access-Token');
  response.headers.set('Access-Control-Expose-Headers', '*');
  return response;
}

addEventListener('fetch', (event) => {
  event.respondWith(handleRequest(event));
});
```

* 修改 `config.js` 中的 `ApiDomian` 为你的域名。
