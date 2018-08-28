# Laravel5.6 Factory 生成测试数据

## 1、生成模型工厂

```PHP
# 创建模型工厂
php artisan make:factory PostFactory

# 配置模型
use Faker\Generator as Faker;

$factory->define(App\Models\User::class, function (Faker $faker) {
    return [
        'username' => $faker->unique()->username,
        'email' => $faker->unique()->safeEmail,
        'mobile' => $faker->unique()->phoneNumber,
        'password' => bcrypt('123456'),
        'nickname' => $faker->unique()->name,
        'reg_ip' => app('request')->ip(),
        'last_login_ip' => app('request')->ip(),
        'remember_token' => str_random(10),
    ];
});
```

## 2、生成数据

```PHP
# 进入命令行
php artisan tinker

# 写入数据 make 生成数据 create 生成并写入到数据库
factory(App\Models\User::class, 5)->create();
```

## 3、生成中文数据

```PHP
# 配置 app.php 添加以下配置项
'faker_locale' => 'zh_CN'
```

