## Framework TODO

- Model 错误处理，应该是直接抛出错误，而不是返回字符串（或者考虑做一个开关）

- Request方法里面对get请求的处理，会把参数逗号给编码掉了

- Model处理where那里，如果就是想查null或者空，处理的不是很好

- HttpRequest isHaveFile 有问题（如果传过来的参数是数组就容易异常了）

- DB-->JOIN

- RedisDB 增加插件验证

  ```php
  // check if the redis extension is loaded
  if (!extension_loaded('redis')) {
      throw new Exception('Redis extension not loaded');
  }
  ```

  

- optimization Model class(beginTransaction 启动事务，已上线未测试（测试出了问题，如果link()时，更换了连接数据，实例将被清空，事务被中断，而导致不会被正确提交。）

- 新增或者更新时没有对空值(NULL)做处理

## Start

We will utilize our proprietary PHP framework to finalize the development of API interfaces.

Here, we will provide some usage guidelines for the framework to enhance its effectiveness in completing the development process.

## Config

`app.php` is important!

## Lib

### Core

#### Routes

this is not an object, so you can just make direct operations to the class. Here's the Hello World:

```php
Router::get('/', function() {
  echo 'Hello world!';
});
```

also supports lambda URIs, such as:

```php
Router::get('/(:any)', function($slug) {
  echo 'The slug is: ' . $slug;
});
```

you can make Router run a custom error callback, like:

```php
Router::error(function() {
  echo '404 :: Not Found';
});
```

In addition, soft routing is also supported, and the default call is similar to this:

```php
Router::any('/api/something', 'app\Controller\Api\SomethingController@index');
```

Simple Example:

```php
Router::any('/hello', 'app\Controller\IndexController@hello');
Router::map(['get','post'],'/hello', 'app\Controller\IndexController@hello');
Router::get('/hello/(:all)', 'app\Controller\IndexController@hello');
```

// When multiple routes are matched, only the first execution will be executed

*Router*::haltOnMatch();

#### Model

##### Table Names

By default, if `userModel` is defined, the table name is `user`.

If your model's corresponding database table does not fit this convention, you may manually specify the model's table name by defining a `tablename` property on the model：

```php
<?php

namespace app\Model;

use libs\Core\Model;

class UserModel extends Model
{
    protected static $tablename = 'users';
}
```

##### Database Connections

By default, all Eloquent models will use the default database connection that is configured for your application. If you would like to specify a different connection that should be used when interacting with a particular model, you should define a `$connection` property on the model:

```php
<?php

namespace app\Model;

use libs\Core\Model;

class UserModel extends Model
{
    protected static $connection = 'mysql';
}
```

Then you can directly call the following method statically, for example:

```php
$repeat_check = UserModel::get(['username' => $data['username'], 'email' => $data['email']]);
```

##### Available static methods

::get(array $where, array $field = [])

::getAll(array $where, array $field = [])

::all(array $where, array $field = [])

::insertAll(array $data)

::insert(array $data)

::update(array $data, array $where)

::updateAll(array $data)

::updateOrInsert(array $where, array $data)

::save(array $where, array $data)

::delete(array $where)

::deleteAll()

::truncate()

::count(array $where = [])

::sum($field, array $where = [])

::exists(array $where)

::first(array $where, array $field = [])

::last(array $where, array $field = [])

::paginate(int $page, int $perPage, array $where = [], array $field = [])

::lastInsertId()

::sql(array $where)

::query(string $sql)

::execute(string $sql array $bind = [])

::beginTransaction()

::commit()

::rollback()

::getFields()

::getPrimaryKey()

::getTable()

::getTableInfo()

::getTableStatus()

::getTables()

::getDatabases()

::tablename()

#### Request

write more

#### Registry

which is a design pattern used to store and access shared data or resources throughout an application.

##### set($key, $value)

##### get($key)

#### Config

##### get($key, $default = null)

##### set($key, $value)

##### has($key)

##### all()

#### Foundations

##### version()

#### Validator

##### Introduction

a simple validator that includes some convenient validation rules that you may apply to data.

Currently, only manual creation of validator instances is supported.

This is a simple use case to validate data by passing in data, rules and messages. When the validation fails, it will return a set of error messages, otherwise it will pass normally.

```php
// normalController.php

$data = [
            'age' => '1899',
            'name' => 'Your name'
];
$rules = [
    'age' => ['digits_between:1,3'],
    'name' => ['required']
];
$validator = new \libs\Core\Validator($data, $rules);
$resultValidated = $validator->validate();
if ($resultValidated !== true) {
    throw new Exception("Validation failed: " . $resultValidated);
}
```

When creating a new validator instances, it supports three parameters, similar to this:

`Validator(array $data, array $rules, array $messages = [])`

**$data**: The data to be verified, only supports one-dimensional arrays.

**$rules**: Define validation rules for each field.

**$messages**: Sometimes you may wish to specify a custom error message only for a specific attribute. You may do so using "dot" notation. Specify the attribute's name first, followed by the rule:

```php
$messages = [
    'email.required' => 'We need to know your email address!',
];
```

##### validate()

Execute the validator and return true if the verification passes. If the verification fails, a series of error verification messages will be returned. The following is the message reference after the verification fails:

```php
$return = [
  	'filedA' => 'error messages here', 
  	'filedB' => 'error messages here'
];
```

Note that when a field has multiple validation rules, if one rule fails to validate, other rules will not continue to be validated.

##### setFields(array $value)

Support setting the fields that need to be verified, and you can pass in different fields according to the needs of the scene.

Like this: `setFields(['name', 'email']);`

Will only validate the 'name' and 'email' fields.

##### Available Validation Rules

Below is a list of all available validation rules and their function:

We also provide a recommended message, you can use it by replace the fieldname, or you can completely customize your message (in brackets).

The symbol ":" is followed by recommended parameters, you can modify it.

###### required

The field under validation must be present in the input data and not empty. A field is "empty" if it meets one of the following criteria:

- The value is `null`.
- The value is an empty string.
- The value is an empty array or empty `Countable` object.
- The value is an uploaded file with no path.

######  min:value

The field under validation must have a minimum *value*. 

######  max:value

The field under validation must be less than or equal to a maximum *value*. 

###### numeric

The field under validation must be [numeric](https://www.php.net/manual/en/function.is-numeric.php).

###### double

The field under validation must be double

###### date:format,...

The field under validation must match one of the given *formats*. 

This validation rule supports all formats supported by PHP's [DateTime](https://www.php.net/manual/en/class.datetime.php) class.

###### time

The field under validation must be formatted as an time.

support format like: 000:00:00.000000 and 000:00

###### email

The field under validation must be formatted as an email address. 

###### phone

###### integer

The field under validation must be an integer.

###### decimal(:digit)

can be used to judge the decimal precision, the default number of decimal places is 2

###### float

The field under validation must be an float.

###### boolean

The field under validation must be able to be cast as a boolean. Accepted input are `true`, `false`, `1`, `0`, `"1"`, and `"0"`.

###### array

The field under validation must be a PHP `array`.

###### alpha

The field under validation must be entirely Unicode alphabetic characters contained in [`\p{L}`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=[%3AL%3A]&g=&i=) and [`\p{M}`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=[%3AM%3A]&g=&i=).

###### alphanumeric

The field under validation must be entirely Unicode alpha-numeric characters contained in [`\p{L}`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=[%3AL%3A]&g=&i=), [`\p{M}`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=[%3AM%3A]&g=&i=), and [`\p{N}`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=[%3AN%3A]&g=&i=).

###### same:field

The given *field* must match the field under validation.

###### different:field

The field under validation must have a different value than *field*.

###### url

he field under validation must be a valid URL.

###### ip

The field under validation must be an IP address.

###### in:foo,bar,...

The field under validation must be included in the given list of values. 

(The filedname field value is invalid.)

###### not_in:foo,bar,...

The field under validation must not be included in the given list of values. 

###### uppercase

The field under validation must contain uppercase character.

###### lowercase

The field under validation must contain lowercase character.

###### symbol

The field under validation must contain special character.

###### regex:pattern

The field under validation must match the given regular expression.

###### digits_between:min,max

The integer validation must have a length between the given *min* and *max*.

##### Alias

The verification rule name supports alias, you can enter number or num, both represent the verification rule numeric, the following is the list of verification rule alias:

**numeric**: number, num

**symbol**: specialcharacter

### Db

#### DB

Support database connection and chain query.

```php
$getAll = \App\Lib\DB::link()->table('logs')->where('id', '=', 1)->field('id', 'user_id')->limit(1, 100)->order("id ASC")->get();
```

##### link()

We need to open a database connection with link first.

Then you can use the following methods to perform database data operations.

##### parameter option operation

->table()

->field()

->fieldsSafe()

->join()

->limit()

->order()

->where()

##### query data operation

->select()

->getAll()

->get()

->first()

->getOne()

->find()

->count()

->sum($field)

->exists()

->paginate(int $page, int $perPage)

->lastId()

->last()

->getConfig()

->getFields()

->getPrimaryKey()

->getTable()

->getTableStatus()

->getTables()

->getDatabases()

->getTableInfo()

##### perform data manipulation

->insert()

->insertAll(array $vars)

->update()

->updateAll(array $vars)

->delete()

->deleteAll()

->truncate()

##### native statement query

->query()

->queryOne()

->execute()

##### Debug

->getSql()

->dd()

### Factory

### Helper

#### Generate

> Generate::functionName()

##### generateRandomString

> generateRandomString($length = 10, $includeLetters = true, $includeSymbols = true): string

@Description generate random string

@cn-zh 生成随机字符串

##### generateNonUniqueNumber

> generateNonUniqueNumber(int $digits): string

@Description generate random number

@cn-zh 生成随机数字

##### generateToken

> generateToken(int $length = 32): string

@Description generate token

@cn-zh 生成token

#### Lang(Localization)

>  Lang::functionName()

##### get()

> get($translation)

##### set()

> set($translation, $value)

## Helper

### dd()

The `dd` function dumps the given variables and ends execution of the script:

```php
dd($value);
 
dd($value1, $value2, $value3, ...);
```

If you do not want to halt the execution of your script, use the [`dump`](https://laravel.com/docs/10.x/helpers#method-dump) function instead.

### dump()

### config()

The `config` function gets the value of a configuration variable. The configuration values may be accessed using "dot" syntax, which includes the name of the file and the option you wish to access. A default value may be specified and is returned if the configuration option does not exist:

```php
$value = config('app.displayErrors', $default);
```

If you only pass a string without the "dot" syntax, the parameters in the app file will be read.

### env()

The `env` function gets the value of a configuration variable. 

Mainly used in development environment. In the configuration file app.config, to control whether to read the configuration in .env first.

### lang()

> lang(string $translation, string $language = 'en')

Get the translation of the given string.

### value()

> value($value, ...$args)

The `value` function return the default value of the given value.

If it is a closure function, the result of the closure function will be returned.

### createFolder()

create a folder by safe.

### generateNonUniqueNumber()

generate a unique number:

```php
$ranNumber = generateNonUniqueNumber($digitalLong);
```

## Src

### Rjwt

#### setBlacklist()

```php
    /**
     * @Description set blacklist
     * @DateTime 2023-04-23
     * @param array $blacklisted_jtis
     * @return void
     */
```

#### encode()

```php
    /**
     * @Description Generate jwt, an array will be generated by default, including access_token, refresh_token, expire_time
     * @zh-CN 生成jwt，默认生成一个数组，包含access_token、refresh_token、expire_time
     * @DateTime 2023-04-23
     * @param array $data
     * @param string $secret_key
     * @param int $exp
     * @param bool $refresh_switch
     * @param string $refresh_key
     * @param int $refreshExpireTime
     * @return void
     */
```

#### decode()

```php
    /**
     * @Description Decode the token generated by jwt, Not recommended, please use the verifyToken method
     * @zh-cn: 解码jwt生成的token，不推荐，请使用verifyToken方法
     * @DateTime 2023-04-23
     * @param string $token
     * @param string $key
     * @param string $alg
     * @return array
     */
```

#### verifyToken()

```php
     /**
     * @Description Verify the token generated by jwt and return the valid content
     * @zh-cn: 验证jwt生成的token并返回有效内容
     * @DateTime 2023-04-23
     * @param string $token
     * @param string $key
     * @param string $alg
     * @return array
     */
```

#### verifyRefreshToken()

```php
    /**
     * @Description Verify the refresh token generated by jwt and return the valid content
     * @zh-cn: 验证jwt生成的refresh token并返回有效内容
     * @DateTime 2023-04-23
     * @param string $token
     * @param string $refresh_key
     * @param string $alg
     * @return void
     */
```

### Remail

> Base on phpmailer

### RPDF

> Base on fpdf

