# setuptools 可以做什么？如何构建自己的 python 包

`setuptools` 是 Python 的一个库，用于简化包的创建和管理过程。它是 Python 包开发和分发的核心工具之一，提供了一种标准的方法来构建、包装和安装 Python 项目。

### 主要功能

1. **打包和分发**：
   - `setuptools` 允许开发者定义项目的元数据，如名称、版本、作者等。
   - 它可以自动查找项目中的所有模块和子包，便于打包。
   - 支持包含非代码文件，如文档、配置文件等。
2. **依赖管理**：
   - 可以在 `setup.py` 文件中声明项目的依赖，确保在安装时自动安装所需的外部包。
   - 支持版本控制，可以指定依赖的具体版本或版本范围。
3. **扩展支持**：
   - 支持编译和包含扩展模块，即用 C 或 C++ 编写的 Python 模块。
4. **自定义命令**：
   - 允许开发者自定义安装脚本中的命令，例如添加编译文档或运行测试的命令。
5. **轮子支持**：
   - 支持生成和安装 wheel 格式的包（`.whl`），这是一种比传统 egg 格式更快更现代的包格式。

### 常见用法

`setuptools` 通常在 `setup.py` 文件中使用，该文件是项目的安装脚本。下面是一个典型的 `setup.py` 示例：

```python
from setuptools import setup, find_packages

setup(
    name='YourPackageName',
    version='0.1',
    packages=find_packages(),
    install_requires=[
        'numpy',               # 依赖 numpy，不指定版本
        'pandas>=1.0.0',       # 依赖 pandas，版本至少为 1.0.0
    ],
    entry_points={
        'console_scripts': [
            'your_script = your_package.module:function'
        ]
    },
    include_package_data=True,
    package_data={
        '': ['*.txt', '*.rst'],  # 包含所有 .txt 和 .rst 文件
        'your_package': ['data/*.data']  # 包括 your_package/data 目录下的所有 .data 文件
    },
    author='Your Name',
    author_email='your.email@example.com',
    description='A short description of the project.',
    long_description=open('README.md').read(),
    long_description_content_type='text/markdown',
    url='https://github.com/yourusername/yourproject',
)
```

### 安装和使用

`setuptools` 通常已预装在许多 Python 环境中，但也可以通过 pip 显式安装：

```bash
pip install setuptools
```

它是 Python 包开发和分发的基石之一，特别是对于希望将自己的项目分享给更广泛社区的开发者来说是必不可少的工具。