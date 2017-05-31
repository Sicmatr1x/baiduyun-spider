# Easy To Use

```sql
--
-- 表的结构 `share_file`
--

CREATE TABLE IF NOT EXISTS `share_file` (
  `fid` bigint(20) unsigned NOT NULL,
  `title` varchar(100) NOT NULL,
  `uk` bigint(20) unsigned NOT NULL,
  `shorturl` varchar(15) NOT NULL,
  `isdir` tinyint(1) NOT NULL,
  `size` bigint(20) unsigned NOT NULL COMMENT 'byte',
  `md5` varchar(32) NOT NULL,
  `shareid` varchar(20) NOT NULL,
  `deleted` tinyint(4) NOT NULL DEFAULT '0',
  `d_cnt` int(11) unsigned NOT NULL DEFAULT '0',
  `ext` varchar(10) NOT NULL,
  `create_time` int(11) NOT NULL,
  `file_type` tinyint(4) NOT NULL COMMENT '0:video;1:image;2:document;3:music;4:package;5:software',
  `uid` int(20) NOT NULL,
  `feed_type` varchar(10) NOT NULL DEFAULT 'share',
  `feed_time` int(11) NOT NULL,
  `indexed` tinyint(1) NOT NULL DEFAULT '0'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## 快速查找影片

网盘链接形如：http://pan.baidu.com/share/link?uk=2571445480&shareid=1360521416

```sql
--显示总共爬取分析文件个数
select count(title) as num
from share_file;

--搜索包含指定关键字的项目
select title, size, uk, shareid
from share_file
where title like '%C86%';

--显示所有视频
select title, size, uk, shareid
from share_file
where file_type='0';

--搜索指定大小的视频
select title, size, uk, shareid
from share_file
where file_type='0' and size>2*1024*1024*1024;


--搜索含指定关键字的视频
--例如：
select title, size, uk, shareid
from share_file
where file_type='0' and title like '%十大%';

select title, size, uk, shareid
from share_file
where file_type='0' and title like '%1080P%';

select title, size, uk, shareid
from share_file
where file_type='0' and title like '%BluRay%';
```


```sql
-- --------------------------------------------------------

--
-- 表的结构 `share_users`
--

CREATE TABLE IF NOT EXISTS `share_users` (
  `uid` int(20) NOT NULL,
  `user_name` varchar(50) NOT NULL,
  `uk` bigint(20) unsigned NOT NULL,
  `avatar_url` varchar(200) NOT NULL,
  `intro` text NOT NULL,
  `follow_count` int(11) NOT NULL,
  `fens_count` int(11) NOT NULL,
  `pubshare_count` int(11) NOT NULL,
  `album_count` int(11) NOT NULL,
  `last_visited` int(11) NOT NULL,
  `weight` tinyint(4) NOT NULL,
  `create_time` int(11) NOT NULL,
  `visited_count` int(11) NOT NULL DEFAULT '0',
  `fetched` int(11) NOT NULL DEFAULT '0' COMMENT '爬取到的文件数'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- --------------------------------------------------------

--
-- 表的结构 `spider_list`
--

CREATE TABLE IF NOT EXISTS `spider_list` (
  `sid` bigint(20) NOT NULL,
  `uk` bigint(20) unsigned NOT NULL,
  `file_fetched` int(11) NOT NULL DEFAULT '0',
  `follow_fetched` int(11) NOT NULL DEFAULT '0',
  `follow_done` tinyint(1) NOT NULL DEFAULT '0',
  `file_done` tinyint(1) NOT NULL DEFAULT '0',
  `weight` tinyint(4) NOT NULL DEFAULT '5',
  `uid` bigint(20) NOT NULL DEFAULT '0'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
