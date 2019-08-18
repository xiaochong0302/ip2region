基于 [ip2region](https://github.com/lionsoul2014/ip2region)，单独提取PHP版本，提供 composer 下载使用, [推荐到作者的项目点 Stars 关注](https://github.com/lionsoul2014/ip2region)。

发现一个项目 [atzcl/ip2region
](https://github.com/atzcl/ip2region) 针对 ip2region 做了 composer，但是好久没更新了，所以造个轮子。

--

ip2region - 最自由的ip地址查询库，ip到地区的映射库，提供Binary,B树和纯内存三种查询算法，妈妈再也不用担心我的ip地址定位。

### 1. 99.9%准确率，定时更新：

数据聚合了一些知名ip到地名查询提供商的数据，这些是他们官方的的准确率，经测试着实比纯真啥的准确多了。<br />
每次聚合一下数据需要1-2天，会不定时更新。

### 2. 标准化的数据格式：

每条ip数据段都固定了格式：_城市Id|国家|区域|省份|城市|ISP_

只有中国的数据精确到了城市，其他国家只能定位到国家，后前的选项全部是0，已经包含了全部你能查到的大大小小的国家。
（请忽略前面的城市Id，个人项目需求）

### 3. 体积小：

生成的数据库文件ip2region.db只有1.5M（1.2版本前是3.5M）

### Composer 安装

```
composer require xiaochong0302/ip2region
```

### ip2region 使用
```php

<?php

use Koogua\Ip2Region\Searcher;

$searcher = new Searcher();

$ip = '101.105.35.57';
// 三种算法 binarySearch | btreeSearch | memorySearch
// 这里使用 b-tree 算法；作者原话：任何客户端b-tree都比binary算法快，当然Memory算法固然是最快的！
$ip_info = $searcher->btreeSearch($ip);

echo '<pre>';
print_r($ip_info);

/***************************************************
    Array
    (
        [city_id] => 2163
        [region] => 中国|华南|广东省|深圳市|鹏博士
    )
 ***************************************************/

```
