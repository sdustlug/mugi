# mugi  

SDUSTLUG 使用的镜像同步工具

## 依赖

bash、rsync、systemd、jq、sponge

## 文件组织

```
/
├── etc
│   ├── mugi
│   │   └── mugi.conf
│   └── systemd
│       └── system
│           ├── mugi@archlinuxcn.timer
│           ├── mugi@archlinux.timer
│           ├── mugi@.service
│           └── mugi@ubuntu.timer
└── usr
    └── bin
        └── mugi

```

## 配置文件格式

默认的配置文件位于 `/etc/mugi/mugi.conf`, 样例配置可以查看 [mugi.conf](./mugi.conf)

### global

在 `[global]` 一节你可以配置：

1. `mirror` 镜像同步的基础目录，留空时为 /mirror

2. `log` 镜像同步日志文件存放目录，留空时为 _mirror_/log

3. `status` 镜像同步状态文件存放目录，留空时为 _mirror_/status

4. `timeout` rsync 同步时的 timeout 参数，留空时为 30

### 同步配置

配置文件其余各节以同步任务名称命名，如 `[archlinux]` 是同步 archlinux 仓库所用到的配置。你可以配置：

1. `upstream` 同步上游，必填，请添加形如 `rsync://mirrors.sdust.edu.cn/arhclinx` 的 uri

2. `dir` 该仓库存放位置（相对于 _mirror_ 的路径），留空时和同步任务名称相同，此例中即 `archlinux`

3. `bandwith` rsync 同步时的 bandwith 参数，用于限制 I/O 带宽，默认为 0，即不限制。单位为 kbps

## 用户及权限配置

目前同步任务使用了 `mirror` 这个用户，因此请创建该用户并修改相应目录权限 (如 _mirror_ 目录)

或者修改 `mugi@.service`，使用其他用户进行同步任务

_* 此节待补充_

## 安装

### 手动安装

参考[文件组织](##文件组织)

_* 此节待补充_

### archlinux 安装

~~PKGBUILD 在写了在写了~~

_* 此节待补充_

## 使用

编辑配置文件，配置 `[global]` 一节，并配置至少一个同步任务，然后创建相应的 systemd timer 控制定时同步。以同步任务 `[archlinux]` 为例，你需要创建 `mugi@archlinux.timer` 可以参照 [timer 样例](./systemd/mugi@archlinux.timer) 配置时间表。

开始此 timer 并设置开机启动

```shell
# systemctl enable --now mugi@archlinux.timer
```
