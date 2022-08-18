建立專案目錄

```sh
$ mkdir psr4-autoload
$ cd psr4-autoload
# 新增 composer.json
$ touch composer.json

# 熟悉參數設定之後可以使用建立 composer.json
$ composer init
```

設計專案結構

```sh
# /psr4-autoload

$ mkdir src
$ mkdir src/Database
$ mkdir src/Game
$ touch src/Database/Adapter.php
$ touch src/Game/Game.php
$ touch src/Game/GameController.php
```

撰寫 php 類別，注意目錄名稱大小寫和命名空間須一致，否則在產 `autoload.php` 的時候 compser 會有錯誤

```php
<?php

namespace App\Database;

class Adapter {
  public function __construct()
  {
    echo "Adapter created";
  }
}
```

其他類別遵循慣例的 `namespace` 和目錄結構規則。組織完類別之後切換到 `composer.json`

```json
{
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

之後開啟指令介面執行

```sh
$ composer dump-autoload -o

# 會產生 vendor 目錄，裡面有 autoload.php
```

完成之後可以在專案目錄下建立一個 `index.php` 來使用這些類別

```php
<?php

use App\Game\Game;

require_once __DIR__.'/vendor/autoload.php';

$game = new Game();
```

- [參考影片](https://www.youtube.com/watch?v=xWgtKALpx9E)
