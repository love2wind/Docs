### 1/ 获取网站备案信息，信息从360抓取

```php
<?php   
 // WebSite http://www.jbxue.com  
function miibeian($domain) {   
    $domain = base64_encode ( $domain );   
    $opts = array (   
            'http' => array (   
                    'method' => "GET",   
                    'timeout' => 5    
            )    
    );   
    $context = stream_context_create ( $opts );   
    $url = 'http://webid.360.cn/complaininfo.php?domain=' . $domain;  
    $html = file_get_contents ( $url, false, $context );   
    if (strpos ( $html, '未查询到网站信息' )) {   
        return false;   
    }   
    $flag = '<ul>';   
    $start = strpos ( $html, $flag ) + strlen ( $flag );   
    $info = substr ( $html, $start, strpos ( $html, '</ul>' ) - $start );   

    $info = str_replace ( ' ', '', $info );   
    $info = str_replace ( '<li><strong>网站名称:</strong>', '', $info );   
    $info = str_replace ( '<li><strong>网站首页地址:</strong>', ' ', $info );   
    $info = str_replace ( '<li><strong>主办单位名称:</strong>', ' ', $info );   
    $info = str_replace ( '<li><strong>主办单位性质:</strong>', ' ', $info );   
    $info = str_replace ( '<li><strong>审核时间:</strong>', ' ', $info );   
    $info = str_replace ( '<li><strong>网站备案/许可证号:</strong>', ' ', $info );   
    $info = str_replace ( "\r\n", '', $info );   
    $info = str_replace ( '</li>', '', $info );   
    $info = trim ( $info );   
    $temp = explode ( ' ', $info );   
    return $temp;   
}   
// http://webid.360.cn/complaininfo.php?domain=c3lzeXVuLmNvbQ==  
$result = miibeian ( 'jbxue.com' );   
print_r ( $result ); 
```

### JS代码自动获取ICP备案号

```javascript
<script>document.write('<script src="https://www.yuanxiapi.cn/api/qqbeian/?type=js&url='+window.location.host+'"><\/script>')</script>
<a target="_blank" href="http://beian.miit.gov.cn/state/outPortal/loginPortal.action"><script>if(icp["ICPSerial"]!=null)document.write(icp["ICPSerial"]);</script></a>
```

### 接口版

很多地方填信息都需要填上域名的备案号，每次使用都得： 搜索备案查询-点开链接-输入域名-（有些站点还需要输入验证码）-获取到备案号-复制出来。
这样的方法太过于繁琐，我就尝试搜索了一下域名备案API接口，找到了一些可用的，不过大多都需要注册登录或者付费，所以找到一个免费的接口，改改发布出来。
废话不多，直接上代码：

```php
<?php
$ip = isset($_REQUEST['d'])? $_REQUEST['d'] : '';
if(empty($ip)){
$ip = "4ker.cc";}
$url="http://www.sojson.com/api/beian/$ip";  *//获取API返回值*
$html = file_get_contents($url);  *//赋值为html变量*
$iip=mb_substr($html,22,14,'utf-8'); *//截取字符串*
$iipp=preg_replace('/[(\xc2\xa0)|\s]+/','', $iip);  *//删除字符串中的空格*
echo $iipp;
?>
```

接口原地址: [http://www.sojson.com/api/beian/所查域名](https://cikeblog.com/goto/vld2)
接口来源处: [http://www.sojson.com/api/beian.html](https://cikeblog.com/goto/wyjd)
本来原接口查询是返回JSON值，但是过于繁琐，也过于不方便人眼识别，我就和之前获取IP地址一样，截取了一部分值，使得现在返回值为备案号。
在线使用: [https://d.3s.work/beian.php?d=域名](https://d.3s.work/beian.php?d=)
务必加上?d=所查域名，不然就返回了我的站点，也可以直接修改代码中的域名为个人域名，那么存为页面，需要的时候打开，就可以显示啦。
感谢www.sojson.com所提供的接口，在众多收费接口中，找到一个免费的接口实属不易。

