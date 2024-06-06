# el-select 中的值如果为数字，无法正确回显及传参的vue解决方法

最近也是在尝试用`vue`和`element-ui plus`做一些项目。

今天在使用`el-select`组件时，就发现一个问题，在下面的代码中，我希望如果性别为`1`时，就把选项`男`显示出来。

```vue
<el-form-item prop="gender" label="性别">
  <el-select v-model="formData.gender" placeholder="请选择">
    <el-option label="男" value="1" />
    <el-option label="女" value="0" />
  </el-select>
</el-form-item>
```

但结果却是这样：

![Ethan_2024-04-24_16-10-48](https://pic.shejibiji.com/i/2024/04/24/6628bea08b771.jpg)

仔细查看了`element-ui plus`的文档，理论上只要值对上了，此时就应该自动匹配上呀。

分析接口返回的数据，发现返回的是`number`值`1`，而这里匹配的是字符串`1`，所以没匹配上。

### 解决办法

这里可以直接使用动态绑定`:value="1"` ，Value的值类型就是`number`了，修改为下面代码：

```vue
<el-form-item prop="gender" label="性别">
  <el-select v-model="formData.gender" placeholder="请选择">
    <el-option label="男" :value="1" />
    <el-option label="女" :value="0" />
  </el-select>
</el-form-item>
```

问题就被解决了。