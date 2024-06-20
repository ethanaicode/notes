# 解决 externally-managed-environment 错误，在 python 中使用 pip 安装包时

当我使用 `pip3` 安装依赖包时，总是报错，提示： **error: externally-managed-environment**

```bash
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try brew install
    xyz, where xyz is the package you are trying to
    install.

    If you wish to install a Python library that isn't in Homebrew,
    use a virtual environment:

    python3 -m venv path/to/venv
    source path/to/venv/bin/activate
    python3 -m pip install xyz

    If you wish to install a Python application that isn't in Homebrew,
    it may be easiest to use 'pipx install xyz', which will manage a
    virtual environment for you. You can install pipx with

    brew install pipx

    You may restore the old behavior of pip by passing
    the '--break-system-packages' flag to pip, or by adding
    'break-system-packages = true' to your pip.conf file. The latter
    will permanently disable this error.

    If you disable this error, we STRONGLY recommend that you additionally
    pass the '--user' flag to pip, or set 'user = true' in your pip.conf
    file. Failure to do this can result in a broken Homebrew installation.

    Read more about this behavior here: <https://peps.python.org/pep-0668/>

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.
```

网上了解了下，这是为了避免 Python 安装的模块，破坏了系统中的内容，比如同名的包，就可能会破坏系统中原来存在的包。

所以看返回的错误，也可以找到解决方法，要么创建一个虚拟的环境，要么使用`pipx`，但是实测`pipx`不能解决这个问题，原因是它安装的包仅仅适用于命令行（这个原因非官方说法，是我猜测的）。

所以我们就使用虚拟环境来解决这个问题。

## 解决方法

> 我这里使用的路径为`~/.env`，你可以换成别的，不一定要完全一样

1.

**创建一个虚拟环境的文件夹**

```bash
mkdir ~/.venv
```

2.

**创建虚拟环境的配置**

可以通过命令直接来创建：

```bash
python3 -m venv ~/.venv
```

3.

**激活虚拟环境**

```bash
source ~/.venv/bin/activate
```

4.

**现在你就可以在虚拟环境中安装包了**

```bash
pip3 install <module name>
```

这个时候安装的依赖包就会安装到这个环境中，也就是`~/.env`目录下。

0.

**一些提示**

- 如果你之后想停用这个虚拟环境，只需要关闭命令行工具即可，或者使用这个命令关闭：

  ```bash
  deactivate
  ```

- 激活这个虚拟环境后，你可以看到这个虚拟环境的文件夹名称在你的命令提示符上，类似这样：

  ```bash
  (.venv) ethan@shejibiji.com project_name %
  ```

- 如果你需要在 VSCode 中配置 Python 的虚拟环境，可以参考文章：

  [Python environments in VS Code](https://code.visualstudio.com/docs/python/environments#_types-of-python-environments)

  （命令面板中搜索：`Python: Create Environment`）

## 参考

官方参考：[`venv` — Creation of virtual environments](https://docs.python.org/3/library/venv.html)

文章参考：[Python Virtual Environment Setup on Mac OSX - Easiest Way](https://www.studytonight.com/post/python-virtual-environment-setup-on-mac-osx-easiest-way)
