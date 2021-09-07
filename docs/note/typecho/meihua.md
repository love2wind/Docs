## 根据时段显示不同的css样式风格

PHP根据时段白天黑夜显示不同的网站css样式风格。这段PHP代码会自动判断服务器时间从而在不同时段让你的博客显示出不同的样式，前提是你要准备两个CSS，例如我的白天是day.css，晚上就night.css。
这里设定的是白天为凌晨7点到18点，晚上是19点到凌晨6点。

把下面代码放到header.php里引用CSS的地方。

```
<?php    
date_default_timezone_set('PRC'); //设定时区，PRC就是中国 
$hour = date('H');    
if($hour <= 18 && $hour > 6){    
echo '<link rel="stylesheet" type="text/css" media="all" href="day.css">';    
}else{    
echo '<link rel="stylesheet" type="text/css" media="all" href="night.css">';    
}    
?>
```

## Typecho时间格式详解

我们在制作Typecho主题的时候，默认官方提供的日期格式是类似July 8, 2020，这样子的，我们可能需要其他的格式，比如2020-08-08。所以我们只需要找到对应模板中的日期格式就可以。这里简单记录一下，如果以后有需要的话可以使用到。

> 我们看到默认的格式是：('F j, Y')
>
> 我们可以更换的是：('Y-m-d')

这样我们就可以更换成需要的格式。如果我们有需要其他格式的话，可以参考这里：

```php
("F j, Y, g:i a");                   // March 10, 2001, 5:16 pm
("m.d.y");                           // 03.10.01
("j, n, Y");                         // 10, 3, 2001
("Ymd");                             // 20010310
('h-i-s, j-m-y, it is w Day z ');    // 05-16-17, 10-03-01, 1631 1618 6 Fripm01
('\i\t \i\s \t\h\e jS \d\a\y.');     // It is the 10th day.
("D M j G:i:s T Y");                 // Sat Mar 10 15:16:08 MST 2001
('H:m:s \m \i\s\ \m\o\n\t\h');       // 17:03:17 m is month
("H:i:s");                           // 17:16:17
("Y-m-d H:i:s");                     // 2001-03-10 17:16:18 （MySQL DATETIME 
```

