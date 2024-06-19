# sub-web-modify
- 重制[原项目sub-web](https://github.com/CareyWang/sub-web) CSS样式
- 兼容nodejs最新版本（可直接一键部署至Vercel）
- 解决大部分布局细节问题，增加“暗黑模式”， 默认自动切换亮/暗模式（点击“太阳/月亮”图标可手动切换），
- 增加“高级功能”点击显示/隐藏
- 增加近百条远程配置
- 增加从短链接中获取订阅信息并返回至前端界面


## Requirements

你需要安装 [Node](https://nodejs.org/zh-cn/) 与 [Yarn](https://legacy.yarnpkg.com/en/docs/install) 来安装依赖与打包发布。你可以通过以下命令查看是否安装成功。
注：以下步骤为 Ubuntu 下相应命令，其他系统请自行修改。为了方便后来人解决问题，有问题请发 issue。

```shell
node -v
v16.20.0

yarn -v
1.22.19
```

## Install

```shell
yarn install
```

## Usage

```shell
yarn serve
```

## Deploy

发布到线上环境，你需要安装依赖，执行以下打包命令，生成的 dist 目录即为发布目录。如需修改默认后端，请修改 /.env 中 **VUE_APP_SUBCONVERTER_DEFAULT_BACKEND** 配置项。

```shell
yarn build
```

- nginx示例配置

```
server {
    listen 80;
    server_name example.com;

    root /var/www/http/sub-web/dist;
    index index.html index.htm;

    error_page 404 /index.html;

    gzip on; #开启gzip压缩
    gzip_min_length 1k; #设置对数据启用压缩的最少字节数
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6; #设置数据的压缩等级,等级为1-9，压缩比从小到大
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml; #设置需要压缩的数据格式
    gzip_vary on;

    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
```

- caddy2示例配置
```
example.com {
    root * /var/www/sub-web/dist
    file_server

    encode gzip
}
```

## Related

- [tindy2013/subconverter](https://github.com/tindy2013/subconverter)
- [CareyWang/MyUrls](https://github.com/CareyWang/MyUrls)
- [CareyWang/sub-web](https://github.com/CareyWang/sub-web)
- [youshandefeiyang/sub-web-modify](https://github.com/youshandefeiyang/sub-web-modify)
