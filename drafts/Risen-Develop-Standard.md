## Naming

> 驼峰命名（Camel Case）：除第一个单词，其它单词首字母大写
>
> 蛇形命名（Snake Case）：用下划线 \_ 作为单词的分隔符
>
> 串形命名（Kebab Case）：用短横线 - 作为单词的分隔符

**后端方法内变量名：**驼峰命名，如 userLoginCount

**前端参数名：**蛇形命名，如 user_name

**文件命名：** 串形命名，如 risen-document.docx

**文件夹命名：**串形命名，如 Risen-Document

**文件路径：**以“/”开始，如“/public/uploads/filename.jpg”

## Git

- `feat` 增加新的业务功能
- `fix` 修复业务问题/BUG
- `perf` 优化性能
- `style` 更改代码风格, 不影响运行结果
- `refactor` 重构代码
- `revert` 撤销更改
- `test` 测试相关, 不涉及业务代码的更改
- `docs` 文档和注释相关
- `chore` 更新依赖/修改脚手架配置等琐事
- `workflow` 工作流改进
- `ci` 持续集成相关
- `types` 类型定义文件更改
- `wip` 开发中

## MySQL

**全部要求小写加下划线**

主键: id_tablename

外键: tablename_id

字段: field_name

## Doc

**命令及解释的标准**

如果后面有参数，使用`-PARAM`来标注，用空格分割。

以下是一个示例：

- **command**: Command Explain

  `-p` This is a expalin

**符号全部使用英文符号，除了中文段落中间或者末尾的内容**

## Comments

**类的注释**

```php
/**
 * The language file is stored in the lang directory
 *
 * Note: The language file is stored in the lang directory, and the file name is the language name.
 *      all language files will be merged into one array, so the same key will be overwritten.
 */
```

**方法的注释**

```php
/**
 * Get the translation value of the corresponding language

 * @since 1.0
 * @dateTime 2023-11-15
 * @param string $translation   The translation key, like 'success' or 'boolean.true'
 * @param array $params        The parameters to be replaced in the translation
 * @return string
 */
```

**分割线**

```bash
#------------------------
# 分割线
#------------------------
```

一级分割线

```python
# ================================================================
# 分割线
# ================================================================
```

二级分割线

```python
# ----------------------------------------------------------------
# 分割线
# ----------------------------------------------------------------
```

80 个字符，长的分隔符，请用在方法体外，

64 个字符，用在方法体内，方便查看代码

```php
/**
 * --------------------------------------------------------------------------------
 * Reports related @zh-cn: 报告相关，全部强制路由，不再允许使用软路由
 * --------------------------------------------------------------------------------
 */

// --------------------------------------------------------------------------------

// ================================================================
// Code Start
// ----------------------------------------------------------------

// code ...

// ----------------------------------------------------------------
// Code End
// ================================================================
```

## Pics

- **Recents**

收集箱，不知道如何归类，或者不重要的可以扔到这里

（如果是 Inbox 项目，只需要精确到月份即可）

- **Historys**

以前的照片，未归档，搞不清楚了
