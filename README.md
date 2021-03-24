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
sh install.sh（注：此处需要给install.sh执行权限`chmod +x install.sh`）

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
wcsfs [OPTION...] [bucketname] [mountpoint]  # 注：moutpoint需为本地已存在的路径，工具不会自动创建
例1：wcsfs /mnt    #将用户所有空间挂载到目录/mnt下
例2：wcsfs bucketName1 /mnt2    #将用户的空间bucketName1挂载到目录/mnt2下
```

5、取消挂载

```
umount /mnt
```

6、卸载
```
rpm -e wcsfs-0.6.1-4.x86_64
```

7、调试

- 如挂载出现异常，可在wcsfs.conf.xml配置文件中修改日志级别为debug，并通过-l参数指定日志文件后，在日志中查看异常原因
```
<log>
	<!-- use syslog for error messages -->
	<use_syslog type="boolean">False</use_syslog>
 	<use_color type="boolean">False</use_color>

 	<!-- log level - LOG_err = 0, LOG_msg = 1, LOG_debug =2 -->
 	<level type="int">0</level>
</log>
```

挂载时指定日志文件
`wcsfs -c wcsfs.conf -l wcsfs.log /mnt/wcsfs`
