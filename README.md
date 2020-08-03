# node-serves
静态服务器，可以访问多种后缀路径

node-dev 每次修改代码重启服务器
```javascript
yarn global add node-dev
node-dev server.js 8888
```

根据输入的地址，获取请求路径
```javascript
const filePath = path === '/' ? '/index.html' : path;
    let content;
    // 也有可能没有请求的路径
    try {
        content = fs.readFileSync(`./public${filePath}`)
    } catch{
        content = '文件不存在';
        response.statusCode = 404;
    }
```


根据请求路径的后缀，使用哈希据结构设置响应头
```javascript
// 设置响应头类型，得到.的位置，截取filePath后缀，使用哈希表判断
    const index = filePath.indexOf('.');
    const suffix = filePath.substring(index);
    const fileType = {
        '.html': 'text/html',
        '.css': 'text/css',
        '.js': 'text/javascript',
        'png': 'image/png',
        'jpg': 'image/jpg'
    }

    response.setHeader('Content-Type', `${fileType[suffix] || 'text/html'};charset=utf-8`)
```
