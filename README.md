# php-excel


## 安装

```
composer require cck/php-excel
```

引入

```
use cck\excel\Excel;
```

## Demo

```
// [名称, 字段名, 类型, 类型规则]
$header = [
    ['ID', 'id', 'text'],
    ['手机号码', 'mobile'], // 规则不填默认text
    ['openid', 'fans.openid', 'text'],
    ['昵称', 'fans.nickname', 'text'],
    ['关注/扫描', 'type', 'selectd', [1 => '关注', 2 => '扫描']],
    ['性别', 'sex', 'function', function($model){
        return $model['sex'] == 1 ? '男' : '女';
    }],
    ['创建时间', 'created_at', 'date', 'Y-m-d'],
];

$list = [
    [
        'id' => 1,
        'type' => 1,
        'mobile' => '18888888888',
        'fans' => [
            'openid' => '123',
            'nickname' => '昵称',
        ],
        'sex' => 1,
        'create_at' => time(),
    ]
];
```

### 导出

```
// 简单使用
return Excel::exportData($list, $header);

// 定制 默认导出xlsx 支持 : xlsx/xls/html/csv， 支持写入绝对路径
return Excel::exportData($list, $header, '测试', 'xlsx', '/www/data/');

// 另外一种导出csv方式
return Excel::exportCsvData($list, $header);

```

### 导入

```
/**
 * 导入
 *
 * @param $filePath 文件路径
 * @param int $startRow 开始行数 默认 1
 * @return array|bool|mixed
 */
$data = Excel::import($filePath, $startRow);
```

### FORK
[jianyan74/php-excel](https://github.com/jianyan74/php-excel)

