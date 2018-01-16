## Composer 常用命令

**1、安装 Laravel**

`composer create-project --prefer-dist laravel/laravel 5.xx user-project`

**2、.env 文件操作**

- 生成 APP_KEY：`php artisan key:generate`
- 缓存 .env 配置：`php artisan config:cache`

**3、维护模式**

- 开启：`php artisan down`
- 关闭：`php artisan up`

**4、文件创建**

- 创建中间件：`php artisan make:middleware UserAuth`
- 创建请求：`php artisan make:request UserRequest`
- 创建模型：`php artisan make:model UserModel`
- 创建控制器：`php artisan make:controller UserContorller`

**5、数据迁移和填充**

- 生成迁移数据库表：`php artisan make:migration create_user_table`
- 运行数据迁移：`php artisan migrate`
- 回滚迁移：`php artisan migrate:rollback`
- 生成 Seeder：`php artisan make:seeder UserTableSeeder`
- 运行所有 Seeder：`php artisan db:seed`
- 运行单一 Seeder：`php artisan db:seed --class UserTableSeeder`

**6、autoload 操作**

- 重新加载：`composer dump-autoload`

**7、事件**

- 生成事件和监听器：`php artisan event:generate`