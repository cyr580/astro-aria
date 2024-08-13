---
title: Reader web
description: ''
date: 'Fri Aug 19 2022 16:33:21 GMT+0800 (中国标准时间)'
dateFormatted: 'Fri Aug 19 2022 16:33:21 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![图片](https://github.com/cyr580/blog-comment/blob/main/IMG_1681.JPG?raw=true)


## 本地书仓

在 `storage/localStore` 中可以集中存放管理本地书籍，开启访问权限的用户可以在 `页面-浏览书仓` 中选择批量导入到自己的书架进行阅读。

## 自定义样式

页面还会加载应用目录下的 `reader-assets/reader.css` 这个CSS样式文件，在这个文件中可以自定义页面样式。

> 自定义样式可能需要配合 `!important` 来设定属性


## 接口服务配置

```
    reader    :
      app    :
        storagePath    :     storage       #     数据存储目录    
        showUI    :     false              #     是否显示UI    
        debug    :     false               #     是否调试模式    
        packaged    :     false            #     是否打包为客户端    
        secure    :     false              #     是否需要登录鉴权，开启后将支持多用户模式    
        inviteCode    :     ”    “                 #     注册邀请码，为空时则开放注册，否则注册时需要输入邀请码    
        secureKey    :     ”    “                  #     管理密码，开启鉴权时，前端管理用户空间的管理密码    
        proxy    :     false               #     是否使用代理    
        proxyType    :     ”    HTTP    “              #     代理类型    
        proxyHost    :     ”    “                  #     代理 Host    
        proxyPort    :     ”    “                  #     代理 port    
        proxyUsername    :     ”    “              #     代理鉴权 用户名    
        proxyPassword    :     ”    “              #     代理鉴权 密码    
        cacheChapterContent    :     false     #     是否缓存章节内容    
        userLimit    :     50                  #     用户上限，最大 50    
        userBookLimit    :     200             #     用户书籍上限，默认最大 200    

      server    :
        port    :     8080                     #     监听端口    
        webUrl    :     http://localhost:${reader.server.port}        #     web链接    

```

## WebDAV同步配置

 1. 首先需要在阅读App里面配置 `WebDAV备份`
    
    服务器地址： `http://IP:端口/reader3/webdav/`
    
    如果开启了 `reader.app.secure` 选项，那么使用网页注册的用户名和密码登录，否则使用用户名 `default` 和 密码 `123456` 登录
    
    
 2. 然后在阅读App里面点击备份
    
    
 3. 在网页里面查看WebDAV文件，确认是否备份成功
    
    
 4. 备份成功之后
    
    
     * 服务器会自动同步书籍阅读进度(暂不支持章节内阅读位置，也不会自动同步书架信息变更)
       
       
     * 可以直接选择阅读App的备份文件进行恢复，这样会直接覆盖书源和书架信息
       
       
     * 可以备份当前书源和书架信息到WebDAV，但是必须要先备份成功
       
       
     * 需要通过恢复备份文件来同步书籍和书源信息
       
       
    
    
 5. PS: 本地书源的书籍同步后无法打开，除非换源
    
    

## 客户端

### Windows / MacOS / Linux

从 [releases](https://github.com/hectorqin/reader/releases) 下载对应平台安装包安装即可，需要安装java10以上环境

MacOS 版 `storage` 默认是 `用户目录/.reader/storage`，其它版本 `storage` 默认是 `程序目录/storage`

#### 配置文件

`storage/windowConfig.json`

包含图形界面和接口服务的相关配置，JSON格式，修改后，程序重启才会生效

> 请仔细检查配置内容，不支持注释，此处注释只是为了方便理解

```

        ”showUI“    :     true    ,                    // 是否显示UI界面，默认为显示    
        ”debug“    :     false    ,                    // 是否调试模式，默认为否    
        ”positionX“    :     0.0    ,                  // 窗口位置 横坐标    
        ”positionY“    :     0.0    ,                  // 窗口位置 纵坐标    
        ”width“    :     1280.0    ,                   // 窗口大小 宽度    
        ”height“    :     800.0    ,                   // 窗口大小 高度    
        ”rememberSize“    :     true    ,              // 改变窗口大小时，是否记住窗口大小，默认记住    
        ”rememberPosition“    :     false    ,         // 移动窗口时，是否记住窗口位置，默认不记住    
        ”setWindowPosition“    :     false    ,        // 启动时是否设置窗口位置，默认不设置，窗口默认居中    
        ”setWindowSize“    :     true    ,             // 启动时是否设置窗口大小，默认按照配置文件进行设置    
        ”serverConfig“    : {                    // 接口服务配置，此处配置会被 `serverPort|showUI|debug` 等覆盖    
            ”reader.app.secure“    :     false    ,      // 是否需要登录鉴权，开启后将支持多用户模式    
            ”reader.app.inviteCode“    :     ”    “    ,      // 注册邀请码，为空时则开放注册，否则注册时需要输入邀请码。仅多用户模式下有效    
            ”reader.app.secureKey“    :     ”    “    ,      // 管理密码，开启鉴权时，前端管理用户空间的管理密码。仅多用户模式下有效    
```
            
            
### 手机端

使用docker版本或者服务器版本，访问web页面

可以添加为桌面应用

### 服务器版

从 [releases](https://github.com/hectorqin/reader/releases) 下载 `reader-$version.jar` 运行即可，需要安装java10以上环境

```
    #     创建目录    
mkdir reader3
    cd     reader3

    #     下载 jar    
wget     ”    xxxx    “    

    #     安装jdk10以上环境...    

    #     运行    

    #     自用版    
java -jar reader-    $version    .jar

    #     多用户版    
java -jar reader-    $version    .jar --reader.app.secure=true --reader.app.secureKey=管理密码 --reader.app.inviteCode=注册邀请码

    #     web端 http://localhost:8080/    
    #     接口地址 http://localhost:8080/reader3/
```

### Docker版

```
    #     自行编译    
    #     docker build -t reader:latest .    

    #     使用环境变量覆盖服务配置，环境变量采用大写字母，不允许使用.-符号，采用下划线“_”取代点“.”  减号“-”直接删除    

    #     docker run -d --restart=always --name=reader -e ”SPRING_PROFILES_ACTIVE=prod“ -v $(pwd)/logs:/logs -v $(pwd)/storage:/storage -p 8080:8080 reader:latest    

    #     跨平台镜像    

    #     新建构建器    
    #     docker buildx create --use --name mybuilder    
    #     启动构建器    
    #     docker buildx inspect mybuilder --bootstrap    
    #     查看构建器及其所支持的cpu架构    
    #     docker buildx ls    
    #     构建跨平台镜像    
    #     docker buildx build -t reader:latest --platform=linux/arm,linux/arm64,linux/amd64 . --push    

    #     使用预编译的镜像    

    #     自用版(建议修改映射端口)    
docker run -d --restart=always --name=reader -e     ”    SPRING_PROFILES_ACTIVE=prod    “     -v     $(    pwd    )    /logs:/logs -v     $(    pwd    )    /storage:/storage -p 8080:8080 hectorqin/reader

    #     多用户版(建议修改映射端口)    
docker run -d --restart=always --name=reader -v     $(    pwd    )    /logs:/logs -v     $(    pwd    )    /storage:/storage -p 8080:8080 hectorqin/reader java -jar /app/bin/reader.jar --spring.profiles.active=prod --reader.app.secure=true --reader.app.secureKey=管理密码 --reader.app.inviteCode=注册邀请码

    #     多用户版 使用环境变量(建议修改映射端口)    
docker run -d --restart=always --name=reader -e     ”    SPRING_PROFILES_ACTIVE=prod    “     -e     ”    READER_APP_SECURE=true    “     -e     ”    READER_APP_SECUREKEY=管理密码    “     -e     ”    READER_APP_INVITECODE=注册邀请码    “     -v     $(    pwd    )    /logs:/logs -v     $(    pwd    )    /storage:/storage -p 8080:8080 hectorqin/reader

    #     更新docker镜像    
    #     docker pull hectorqin/reader    

    #    :后面的端口修改为映射端口    
    #     web端 http://localhost:8080/    
    #     接口地址 http://localhost:8080/reader3/    

    #     通过watchtower手动更新    
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --cleanup --run-once reader
```

### Docker-Compose版(推荐)

```
    #    安装docker-compose    
    #    Debian/Ubuntu    
apt install docker-compose -y
    #    CentOS    
curl -L     ”    https://github.com/docker/compose/releases/download/1.29.2/docker-compose-    $(    uname -s    )    -    $(    uname -m    )    “     -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version

    #     下载项目里的 docker-compose.yaml    
wget https://raw.githubusercontent.com/hectorqin/reader/master/docker-compose.yaml
    #     根据 docker-compose.yaml 里面的注释编辑所需配置    
    #     启动 docker-compose    
docker-compose up -d

    #     停止 docker-compose    
docker-compose stop

    #     查看实时日志    
docker logs -f reader

    #     手动更新    
docker-compose pull     &&     docker-compose up -d
```

## Nginx反向代理

```
    # 此文件放入 conf.d目录下,一般可用 touch /etc/nginx/conf.d/reader.conf 创建    
    server     {
        listen         80    ;
        server_name     域名;
        #开启ssl解除注释    
        #不使用宝塔获取证书脚本  https://github.com/Misaka-blog/acme-1key    
        #listen 443 ssl;    
        #ssl_certificate 证书.cer;    
        #ssl_certificate_key 证书.key;    
        #ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;    
        #ssl_ciphers EECDH+CHACHA20:EECDH+CHACHA20-draft:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;    
        #ssl_prefer_server_ciphers on;    
        #ssl_session_cache shared:SSL:10m;    
        #ssl_session_timeout 10m;    
        #if ($server_port !~ 443){    
        #    rewrite ^(/.*)$ https://$host$1 permanent;    
        #}    
        #error_page 497  https://$host$request_uri;    

        gzip     on    ;     #开启gzip压缩    
        gzip_min_length         1k    ;     #设置对数据启用压缩的最少字节数    
        gzip_buffers         4         16k    ;
        gzip_http_version         1.0    ;
        gzip_comp_level         6    ;     #设置数据的压缩等级,等级为1-9，压缩比从小到大    
        gzip_types     text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml;     #设置需要压缩的数据格式    
        gzip_vary     on    ;

        client_max_body_size           50m    ;     #允许上传50MB文件,上传本地书籍需要修改此项大小.如nginx主配置文件已添加,删除此行并修改主配置即可    

        location         /     {
            proxy_pass      http://127.0.0.1:4396;     #端口自行修改为映射端口    
            proxy_http_version         1.1    ;
            proxy_cache_bypass         $http_upgrade    ;
            proxy_set_header     Upgrade               $http_upgrade    ;
            proxy_set_header     Connection            ”upgrade“    ;
            proxy_set_header     Host                  $host    ;
            proxy_set_header     X-Real-IP             $remote_addr    ;
            proxy_set_header     X-Forwarded-For       $proxy_add_x_forwarded_for    ;
            proxy_set_header     X-Forwarded-Proto     $scheme    ;
            proxy_set_header     X-Forwarded-Host      $host    ;
            proxy_set_header     X-Forwarded-Port      $server_port    ;
    }
}
```

