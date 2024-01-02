# Janus 快速入门

[toc]

## Janus 包含工程

- janus-ui
- janus-admin

### 前端(janus-ui)

- github 地址: https://github.com/GrailStack/janus-ui

```shell
git clone https://github.com/GrailStack/janus-ui.git
```

### 后端(janus-admin)

- github 地址：https://github.com/GrailStack/janus-admin

```shell
git clone https://github.com/GrailStack/janus-admin.git
```

## janus-ui 前端依赖

- node.js
- vue

进入工程：后执行 npm install 命令即可

```shell
npm install
```

## janus-admin 后端依赖

- MySQL(需安装)
- influxDB(计划去除中，目前必需)
- jdk 等

## 依赖组件安装

>  为了能够快速启动，这里仅以 Docker 环境为示例

### MySQL

略

### InfluxDB

- dockerhub 的 influxDB 主页：https://hub.docker.com/_/influxdb

### 工程配置

- 在 janus-admin 工程中，找到 `resource/application.yml` 文件，在 `halo.influxdb` 节点下配置 `influxDB` 相关的配置项。如：url、username、password 等

```yaml
halo:
  influxdb:
    enable: true
    enableOkHttpClient: true
    url: http://localhost:8086 #这里配置你的 influxDB 连接地址
    username: admin #用户名
    password:  #密码
    database: mydb #db
    retention-policy: autogen
    okhttp:
      connectTimeout: 10
```

## 后端启动

![image-20240102090216680](https://sjl-picture.oss-cn-shanghai.aliyuncs.com/img/janus/start-succ.png)

## 前端启动

![image-20240102090445209](https://sjl-picture.oss-cn-shanghai.aliyuncs.com/img/janus/front-end-succ.png)

- 前端登录界面

  ![登录界面](https://sjl-picture.oss-cn-shanghai.aliyuncs.com/img/janus/front-end-login.png)

- 主页

  ![image-20240102091134630](https://sjl-picture.oss-cn-shanghai.aliyuncs.com/img/janus/front-end-homepage.png)

## 其他说明

1. 前端配置了代理，配置文件位于  `janus-ui/vue.config.js` ，所以后端最好使用默认的 8084 端口，如果后端修改了端口，前端代理也要同时修改。
    ```yaml
    devServer: {
        // port: 8080,
        //host: 'janus.com',
        https: false,
        proxy: {
          '/admin': {
            target: 'http://127.0.0.1:8084',
            changeOrigin: true,
          },
        },
      },
    ```

2. 前端默认用户密码。默认用户名：jin.xu，默认密码：123456。
