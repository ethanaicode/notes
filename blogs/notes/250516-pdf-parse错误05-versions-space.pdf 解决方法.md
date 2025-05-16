# pdf-parse 错误 05-versions-space.pdf 解决方法

今天项目中要用到 pdf 识别文本，于是用到了 `pdf-parse` 这个库，结果上来就报错：

```bash
ENOENT: no such file or directory, open './test/data/05-versions-space.pdf'
```

去网上搜了下问题，原来是官方有一段测试代码没有删，真离谱，就是这段：

```bash
//for testing purpose
if (isDebugMode) {

    let PDF_FILE = './test/data/05-versions-space.pdf';
    let dataBuffer = Fs.readFileSync(PDF_FILE);
    Pdf(dataBuffer).then(function(data) {
        Fs.writeFileSync(`${PDF_FILE}.txt`, data.text, {
            encoding: 'utf8',
            flag: 'w'
        });
        debugger;
    }).catch(function(err) {
        debugger;
    });

}
```

解决方法很多，有一种就是去库中把这一段删了，但是为了避免修改依赖库的代码我就没有采用这种方案。

还有一种是导入时引入单独的库：`import pdf from 'pdf-parse/lib/pdf-parse'`

可以解决，但是后面可能还会报别的错误。

最简单的方法就是在项目根目录创建这个文件：`test/data/05-versions-space.pdf`

就可以完美解决了。

但是，我要说但是了，这个库不支持**中文**的识别...猝！

（之后又进行了测试，发现部分中文的 pdf 也能识别出来，比如发票，这可能和 pdf 的格式或者版本有关）

最后使用 `pdfreader` 这个库真正解决了，供参考。
