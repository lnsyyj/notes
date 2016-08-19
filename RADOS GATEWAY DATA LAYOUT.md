# RADOS GATEWAY DATA LAYOUT数据布局 #

本文只做了ceph官方文档的简单翻译，由于英语水平有限，我也不想误导大家。如有翻译问题或者错误请大家指正，微信yjtcok。

原文在，http://docs.ceph.com/docs/master/radosgw/layout/

**INTRODUCTION（介绍）**

Swift提供一种叫container的东西，我们与术语bucket交替使用。有人可能会说RGW的buckets实现了Swift的containers。

本文不考虑RGW这些结构如何运作，例如使用编码（）和解码（）序列化方法等等。

**CONCEPTUAL VIEW（概念视图）**

虽然RADOS只知道pools和携带xattrs及OMAP【1】的objects，概念上RGW组织其数据分成三种不同类型：metadata 、bucket index 、and data.

> Metadata

我们有元数据的3个sections：user、bucket、bucket.instance

您可以使用下面的命令来检查元数据项：
	radosgw-admin metadata list

	radosgw-admin metadata list bucket
	radosgw-admin metadata list bucket.instance
	radosgw-admin metadata list user

	radosgw-admin metadata get bucket:<bucket>
	radosgw-admin metadata get bucket.instance:<bucket>:<bucket_id>
	radosgw-admin metadata get user:<user> # get or set

	user：保存user information
	bucket：保存bucket name和bucket instance id之间的映射
	bucket.instance：保存bucket instance information【2】
	每个metadata entry被保存在一个单独rados object中，请参见下面
	需要注意的是，当列出一个metadata section，我们做了一个pool上的rados pgls操作。

> Bucket Index

这是一个不同类型的metadata，并分开存放。这个bucket index保存了一个key-value映射，在rados object中。默认情况下每个bucket保存一个单独的rados object，但是它可能因为Hammer版本shard，映射在多个rados objects上。这个映射自身保存在omap中，关联每个rados object。每个omap的key是objects的名字，value保存object的basic metadata —— 当list bucket时，显示metadata。此外，每个omap保存一个header，并且header中保存bucket accounting metadata（objects数量，总size，等）

请注意，我们在bucket index中也保存一些其他信息，它保存在其他关键的namespaces。我们可以保存bucket index log在那，objects version有许多信息，我们保存在其他key中。


> Data

每个rgw object的objects data保存在一个或多个rados objects

**OBJECT LOOKUP PATH（对象查找路径）**

当访问objects，REST APIs携带3个参数：account information（access key in S3 or account name in Swift）、bucket or container name、object name (or key)。目前RGW仅使用account information去找出user ID并access control。只有bucket name 和 object key被用来处理pool中的object 。

user ID在RGW中是一个字符串，通常实际的user name来自user credentials而不是一个哈希或映射标识符。

当访问一个user's data时，用户记录从.users.uid pool中的一个<user_id> object中加载。

在pool .rgw中bucket names被直接表示。为了获取所谓的marker（它作为一个bucket的ID ），bucket记录被加载。

该对象位于pool .rgw.buckets中。object name是<marker>_<key>，例如default.7593.4_image.png，这里的marker是default.7593.4，key是image.png。由于这些连在一起的名称不解析，只向下传递到RADOS，分离器的选择并不重要并且不会引起歧义。出于同样的原因，斜杠允许出现在object names中（keys）。

另外，也可以创建多个data pools，并使不同user的buckets被默认创建在不同的rados pools中，提供必要的扩展。这些layout和pools name被policy设置所控制。【3】

一个RGW object可以包括若干RADOS objects，其中第一个是head（包含metadata），例如manifest、ACLs 、content type 、ETag 和user-defined metadata。这个metadata被存储在xattrs。为了提高效率和原子操作，head还可以包含object data最多512 kilobytes。manifest描述每个object是如何在RADOS objects中布局的。 

**BUCKET AND OBJECT LISTING（bucket和object列表）**

Buckets





**FOOTNOTES（脚注）**
     





**APPENDIX: COMPENDUM（附录）**
     

















