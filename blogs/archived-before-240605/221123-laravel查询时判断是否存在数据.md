# laravel查询时判断是否存在数据

#### 1.Laravel Eloquent模型

> Eloquent 返回的所有结果集都是 Illuminate\Database\Eloquent\Collection 对象的实例，包括通过 get 方法检索或通过访问关联关系获取到的结果。 Eloquent 的集合对象继承了 Laravel 的 Base Collection，因此它自然也继承了数十种能优雅地处理 Eloquent 模型底层数组的方法。因此要判断数据存在，直接用内置方法即可。

```php
// 1.使用内置方法 isEmpty()
$userItems = User::where('sex', '=', '1')->get();
if ($userItems->isEmpty()) {

}

// 2.使用内置方法 count() 检查有没有记录
if (User::where('email', '=', $email)->count() > 0) {
   // 有记录
}

// 3.使用内置方法 exists() 建议使用该方法
$userItems = User::where('sex', '=', '1')->get();
if ($userItems->exists()) {
   // 有记录
}

// 4.使用内置方法 first()
$user = User::where('email', '=', $email)->first();
if ($user === null) {
   // 没记录
}
```

#### 2.数据库：查询构造器

> 直接使用is_null()或empty()判段结果集是否为空。

```php
$users = DB::table('users')->where('id', $id)->get();
// 方法1
if($users){
    // 有记录
}
// 方法2
if(is_null($users)){
    // 没记录
}
// 方法3
if(empty($users)){
    // 没记录
}
```