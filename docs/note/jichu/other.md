## 常用正则表达式

#### 文本匹配提取URL链接

```
var targetText = '教书先生博客：blog.oioweb.cn';
var re = /((https?|ftp|file):\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?/gi;
// 使用全局匹配:
var matches = targetText.match(re);
document.write(matches);
```

#### 过滤文本行所有换行

```
    var str = "教书先生博客\nblog.oioweb.cn";
    var getArr = str.split("\n");
    var strreverse = "";
    for (var i = 0; i < getArr.length; i++) {
        strreverse = strreverse + getArr[i].replace(/[\r\n]/g, "");
    }
    console.log(strreverse);
```

#### 去掉文本中所有空格

```
    var str = " Wel come\n" +
        "Wel come\n" +
        " 教书先生";
    var getArr = str.split("\n");
    var strreverse = "";
    for (var i = 0; i < getArr.length; i++) {
        strreverse = strreverse + getArr[i].replace(/[ ]/g, "") + "\n";
    }
    console.log(strreverse);
```

## 2021最新官方IP地址查询接口

#### 网易云接口

http://ip.ws.126.net/ipquery?ip=[IP地址]

#### 搜狐接口

http://pv.sohu.com/cityjson?ie=utf-8

#### 爱奇艺接口

http://ip.geo.iqiyi.com/cityjson?format=json&ip=[IP地址]

#### ip-api

http://ip-api.com/json/[IP地址]?lang=zh-CN

#### 太平洋电脑网接口

http://whois.pconline.com.cn/ipJson.jsp?ip=[IP地址]&json=true

#### 腾讯接口

https://apis.map.qq.com/ws/location/v1/ip?output=jsonp&key=KUQBZ-FYDCU-YMVVN-2DDW5-7WDYE-5JBJR&ip=[IP地址]&callback=jQuery18301852690032249129_1600324416562&_=1600324417180

## PHP函数大全·持续更新

[PHP函数大全·持续更新 - 教书先生博客 (oioweb.cn)](https://blog.oioweb.cn/54.html)

#### 邮箱验证

```
function is_valid_email($email) {
    if (preg_match('/^[\w\-\.]+@[\w\-\.]+(\.\w+)+$/', $email)) {
        return true;
    } else {
        return false;
    }
}
```

OR

```
function check_email($email)
{
    $result = trim($email);
    if (filter_var($result, FILTER_VALIDATE_EMAIL)) {
        return true;
    } else {
        return false;
    }
}
```

#### 301跳转

```
function redirect($url) {
    header('location:'.$url, false, 301);
    exit;
}
```

#### 获取客户端IP

```
function real_ip($type = 0)
{
    $ip = $_SERVER['REMOTE_ADDR'];
    if ($type <= 0 && isset($_SERVER['HTTP_X_FORWARDED_FOR']) && preg_match_all('#\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}#s', $_SERVER['HTTP_X_FORWARDED_FOR'], $matches)) {
        foreach ($matches[0] as $xip) {
            if (filter_var($xip, FILTER_VALIDATE_IP, FILTER_FLAG_IPV4 | FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
                $ip = $xip;
                break;
            }
        }
    } elseif ($type <= 0 && isset($_SERVER['HTTP_CLIENT_IP']) && filter_var($_SERVER['HTTP_CLIENT_IP'], FILTER_VALIDATE_IP, FILTER_FLAG_IPV4 | FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
        $ip = $_SERVER['HTTP_CLIENT_IP'];
    } elseif ($type <= 1 && isset($_SERVER['HTTP_CF_CONNECTING_IP']) && filter_var($_SERVER['HTTP_CF_CONNECTING_IP'], FILTER_VALIDATE_IP, FILTER_FLAG_IPV4 | FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
        $ip = $_SERVER['HTTP_CF_CONNECTING_IP'];
    } elseif ($type <= 1 && isset($_SERVER['HTTP_X_REAL_IP']) && filter_var($_SERVER['HTTP_X_REAL_IP'], FILTER_VALIDATE_IP, FILTER_FLAG_IPV4 | FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
        $ip = $_SERVER['HTTP_X_REAL_IP'];
    }
    return $ip;
}
```

> X_FORWARDED_FOR：之前的获取真实IP方式，极易被伪造IP
> X_REAL_IP：在网站使用CDN的情况下选择此项，在不使用CDN的情况下也会被伪造
> REMOTE_ADDR：直接获取真实请求IP，无法被伪造，但可能获取到的是CDN节点IP

#### 取中间文本

```
function getSubstr($str, $leftStr, $rightStr)
{
    $left = strpos($str, $leftStr);
    $right = strpos($str, $rightStr, $left);
    if ($left < 0) return '';
    if ($right > 0) {
        return substr($str, $left + strlen($leftStr), $right - $left - strlen($leftStr));
    } else {
        return substr($str, $left + strlen($leftStr));
    }
}
```

#### 是否HTTPS访问

```
function is_https()
{
    if (isset($_SERVER['SERVER_PORT']) && $_SERVER['SERVER_PORT'] == 443) {
        return true;
    } elseif (isset($_SERVER['HTTPS']) && (strtolower($_SERVER['HTTPS']) == 'on' || $server['HTTPS'] == '1')) {
        return true;
    } elseif (isset($_SERVER['HTTP_X_CLIENT_SCHEME']) && $_SERVER['HTTP_X_CLIENT_SCHEME'] == 'https') {
        return true;
    } elseif (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https') {
        return true;
    } elseif (isset($_SERVER['REQUEST_SCHEME']) && $_SERVER['REQUEST_SCHEME'] == 'https') {
        return true;
    } elseif (isset($_SERVER['HTTP_EWS_CUSTOME_SCHEME']) && $_SERVER['HTTP_EWS_CUSTOME_SCHEME'] == 'https') {
        return true;
    }
    return false;
}
```

#### 随机IP

```
function randIp()
{
    return mt_rand(0, 255) . '.' . mt_rand(0, 255) . '.' . mt_rand(0, 255) . '.' . mt_rand(0, 255);
}
```

#### 毫秒时间戳

```
function msectime() {
    list($msec, $sec) = explode(' ', microtime());
    return (float)sprintf('%.0f', (floatval($msec) + floatval($sec)) * 1000);
}
```

#### 获取重定向地址

```
function getrealurl($url){
    @$header = get_headers($url,1);
    if (strpos($header[0],'301') || strpos($header[0],'302')) {
        if(is_array($header['Location'])) {
            return $header['Location'][count($header['Location'])-1];
        }else{
            return $header['Location'];
        }
    }else {
        return $url;
    }
}
```

#### jsonp转数组

```
function jsonp_decode($jsonp, $assoc = false)
{
    $jsonp = trim($jsonp);
    if (isset($jsonp[0]) && $jsonp[0] !== '[' && $jsonp[0] !== '{') {
        $begin = strpos($jsonp, '(');
        if (false !== $begin) {
            $end = strrpos($jsonp, ')');
            if (false !== $end) {
                $jsonp = substr($jsonp, $begin + 1, $end - $begin - 1);
            }
        }
    }
    return json_decode($jsonp, $assoc);
}
```

#### 秒数转换详细时间

```
/**
 * 将秒数转换为剩余详细时间！
 */
function Sec2Time($time)
{
    if (is_numeric($time)) {
        $value = array(
            "years" => 0, "days" => 0, "hours" => 0,
            "minutes" => 0, "seconds" => 0,
        );
        if ($time >= 31556926) {
            $value["years"] = floor($time / 31556926);
            $time = ($time % 31556926);
        }
        if ($time >= 86400) {
            $value["days"] = floor($time / 86400);
            $time = ($time % 86400);
        }
        if ($time >= 3600) {
            $value["hours"] = floor($time / 3600);
            $time = ($time % 3600);
        }
        if ($time >= 60) {
            $value["minutes"] = floor($time / 60);
            $time = ($time % 60);
        }
        $value["seconds"] = floor($time);

        $t = ($value["years"] >= 1 ? $value["years"] . "年" : '') . ($value["days"] >= 1 ? $value["days"] . "天" : '') . ($value["hours"] >= 1 ? $value["hours"] . "小时" : '') . ($value["minutes"] >= 1 ? $value["minutes"] . "分" : '') . ($value["seconds"] >= 1 ? $value["seconds"] . "秒" : '');
        return (!empty($t) ? $t : '0秒');
    } else {
        return (bool) FALSE;
    }
}
```

#### 时间相差秒数

```
/**
 * @param $startdate 开始时间
 * @param int $enddate 结束时间
 * 返回两者之间相差多少秒
 */
function TimeLag($startdate, $enddate = -1)
{
    global $date;
    $enddate = ($enddate == -1 ? $date : $enddate);
    $time = strtotime($enddate) - strtotime($startdate); //和结束时间的时间戳
    $text = '';
    $dater = floor(($time) / 86400);
    if ($dater > 0) {
        $time = $time - ($dater * 86400);
        $text .= $dater . '天';
    }
    $hour = floor(($time) / 3600);
    if ($hour > 0) {
        $time = $time - ($hour * 3600);
        $text .= $hour . '小时';
    }
    $minute = floor(($time) / 60);
    $time = $time - ($minute * 60);
    if ($minute > 0) {
        $text .= $minute . '分钟';
    }
    $second = floor(($time) % 60);
    if ($second > 0) {
        $text .= $second . '秒';
    }

    return $text;
}
```

#### 生成唯一token参数

```
/**
 * @param $vals 混淆函数
 * 生成唯一token参数！
 */
function TokenCreate($vals = '1')
{
    $key = mt_rand();
    $hash = hash_hmac("sha1", $vals . mt_rand() . time(), $key, true);
    return str_replace(['=', '_', '-'], '', strtr(base64_encode($hash), '+/', '-_'));
}
```

#### 获取第一天最后一天

```
/*
 * 获取某个月第一天/最后一天代码
 */
function getthemonth($date)
{
    $firstday = date('Y-m-01', strtotime($date));
    $lastday = date('Y-m-d', strtotime("$firstday +1 month -1 day"));
    return array($firstday, $lastday);
}
```