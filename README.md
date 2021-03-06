# SilexAgain
Silexは2018年の6月で残念ながらEOLとなってしまいました。
    
Silexの簡単にサービスプロバイダやイベントを作成できるところが好きだったので、  
使用感を再現するtraitを作ってみました。

## Requirements
`PHP 5.4`以上で動作します。  

## License
MITライセンスとします。

## Installation
```
composer require n0wada/silexagain
```

## Usage
webアプリケーションクラスにSilexAgainTraitを適用することで使用します。  
beforeメソッドやafterメソッドは名前が衝突しないように自分で定義してください。  
  
Slimを使う場合は以下のような感じです。   

```php
<?php
use SilexAgain\SilexAgainTrait;
use SilexAgain\Events;
use Slim\App;
  
class myApp extends App
{
    use SilexAgainTrait;
    
    function before($callback)
    {
        $this->on(Events::BEFORE_EVENT, $callback);
    }
}
 
 
$app = new myApp();
    
$app->register(new YourServiceProvider());
    
$app->before(function () {
     echo "before_event!";
});
    
$app->get("/", function () use ($app) {
    $app->dispatch(Events::BEFORE_EVENT);
});
    
$app->boot()->run();
```



