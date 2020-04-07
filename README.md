# 空间挂载工具wcsfs使用指南

---

空间挂载工具通过将网宿对象存储空间挂载到Linux文件系统。可通过操作本地文件的方式操作对象存储中的文件

## 主要功能
wcsfs是基于s3fs,fuse搭建。通过将本地的文件操作映射为S3请求，实现文件管理功能

 - 支持本地文件和网宿对象存储文件的双向同步
 - 大文件支持分片上传
 - 工具只支持Linux环境使用

## 下载地址
[wcsfs下载](http://wcsd.chinanetcenter.com/tool/wcsfs-0.6.1-8-centos-x86-64.zip)

## 安装及使用
以centos为例

1、下载并解压安装包后得到

```
install.sh
Readme.md
wcsfs-0.6.1-4.x86_64.rpm

```

2、进入安装包路径后执行install命令，安装成功后通过`wcsfs --help`查看是否安装成功

```
sh install.sh

```

3、配置账号信息

- 工具安装后会生成一个配置文件/usr/local/etc/wcsfs/wcsfs.conf.xml.def，重命名为/usr/local/etc/wcsfs/wcsfs.conf.xml
- 编辑以下信息

```
<endpoint type="string">S3 EndPoint</endpoint>
<xmlnsurl type="string">http://wcs.chinanetcenter.com/document</xmlnsurl>
<access_key_id type="string">USER's AK</access_key_id>
<secret_access_key type="string">USER' SK</secret_access_key>

```

4、运行

```
wcsfs [OPTION...] [bucketname] [mountpoint]
例1：wcsfs /mnt    #将用户所有空间挂载到目录/mnt下
例2：wcsfs bucketName1 /mnt2    #将用户的空间bucketName1挂载到目录/mnt2下
```
