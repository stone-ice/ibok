# ibok
php+swoole，简单的聊天室，直播

## install composer 安装
`composer require tianrang/ibok:dev-master`

## usage 使用
* 自动加载 `require './vendor/autoload.php'`

* 配置参数，并实例化 `tianrang\ibok\Start` 类，具体配置参考`src/config.php`

* cli模式运行服务端脚本

* 在浏览器访问客户端脚本


## example 例子：
* composer.json 同级目录下，创建文件 do.php

```php

## composer 自动加载
require './vendor/autoload.php';

## 项目初始化配置
$config = [
	'host' => '192.168.10.20'
	];

## 初始化项目实例
$bootstrap = tianrang\ibok\Start::init($config);

## 判断脚本运行模式
$type = $_GET['type'] ?? 'server';

## cli模式运行服务端脚本
if ($type === 'server') {
	preg_match("/cli/i", php_sapi_name()) === 0 && die('必须用CLI模式运行！');
	$bootstrap->serverRun();
}

## fcgi模式运行客户端脚本
if ($type === 'client') {
	$bootstrap->clientRun();
}

```
* linux 上运行 `do.php`
![聊天服务器](https://static.ishappy.cn/images/server.webchat.png)

* 浏览器访问 `http://XXX.com/do.php?type=client`
![聊天客户端](https://static.ishappy.cn/images/client.webchat.png)
