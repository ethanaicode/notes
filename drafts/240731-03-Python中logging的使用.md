# Python 中的 logging 使用案例

可以创建多个日志记录器（`Logger` 实例），每个记录器可以有自己的处理器和配置。这样，你可以在代码中根据需要选择使用哪个日志记录器。

以下是如何实现两个不同的 `Logger` 实例，并在代码中决定使用哪个记录器的示例：

```python
import logging

# 创建第一个日志记录器
logger_a = logging.getLogger('logger_a')
logger_a.setLevel(logging.DEBUG)

# 创建第一个处理器
file_handler_a = logging.FileHandler('file_a.log')
console_handler_a = logging.StreamHandler()

# 创建格式器
formatter_a = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
file_handler_a.setFormatter(formatter_a)
console_handler_a.setFormatter(formatter_a)

# 添加处理器到第一个日志记录器
logger_a.addHandler(file_handler_a)
logger_a.addHandler(console_handler_a)

# 创建第二个日志记录器
logger_b = logging.getLogger('logger_b')
logger_b.setLevel(logging.INFO)

# 创建第二个处理器
file_handler_b = logging.FileHandler('file_b.log')
console_handler_b = logging.StreamHandler()

# 创建格式器
formatter_b = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
file_handler_b.setFormatter(formatter_b)
console_handler_b.setFormatter(formatter_b)

# 添加处理器到第二个日志记录器
logger_b.addHandler(file_handler_b)
logger_b.addHandler(console_handler_b)

# 使用第一个日志记录器
logger_a.debug('This message will go to file_a.log and console for logger_a')

# 使用第二个日志记录器
logger_b.info('This message will go to file_b.log and console for logger_b')
```

在这个示例中：

- `logger_a` 记录器将日志记录到 `file_a.log` 文件和控制台，并设置为 `DEBUG` 级别。
- `logger_b` 记录器将日志记录到 `file_b.log` 文件和控制台，并设置为 `INFO` 级别。

你可以在代码中选择使用 `logger_a` 或 `logger_b`，根据你的需要来决定将日志记录到哪个文件或显示在控制台。
