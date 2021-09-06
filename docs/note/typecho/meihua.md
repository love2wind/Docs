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



