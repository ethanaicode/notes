# PyQt 中实现自定义 Tab 并按照加载对应页面内容

最近在写一个界面，有一个 Tab 页切换的功能，看了下 PyQt5 自带的方法，挺好，但是样式不喜欢，需要自己调整，我想想还不如自己写一个，无非就是一个按钮组，点击其中一个按钮，切换到对应内容。

完成这个 Tab 切换按钮组的设计挺简单，但是内容的切换，就有不同的实现了。

### 1. 预加载所有内容，通过显示和隐藏切换

在这种情况下，所有的 Tab 页面在程序启动时就已经创建和加载了。当用户切换 Tab 时，程序只是简单地显示或隐藏相应的内容。这种方法的优点是切换 Tab 时速度快，因为所有内容都已经加载。缺点是可能会增加初始加载时间和内存占用，特别是当 Tab 页面很多或每个页面内容很丰富时。

### 2. 按需加载内容

在这种方法中，Tab 页面的内容只有在用户首次点击该 Tab 时才加载。这可以通过检测 Tab 的切换并动态创建内容来实现。一旦内容被加载，你可以选择将其保留在内存中（便于再次显示时不需要重新加载），或者在它被隐藏时销毁（释放资源，适合内存敏感的应用）。

### 3. 混合方法

你还可以结合上述两种方法：对于核心或常用的 Tab 页面使用预加载，而对于不常用或资源密集的页面使用按需加载。这样可以在提供快速响应和节省资源之间找到平衡。

### 示例代码（按需加载）

这里是一个简单的 PyQt5 示例，演示如何实现按需加载 Tab 页面的内容：

```python
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QVBoxLayout, QPushButton, QStackedWidget, QLabel)

class TabPage(QWidget):
    def __init__(self, text):
        super().__init__()
        layout = QVBoxLayout()
        label = QLabel(text)
        layout.addWidget(label)
        self.setLayout(layout)

class MainWindow(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        layout = QVBoxLayout()
        self.tabs = QStackedWidget(self)

        self.buttons = {
            "Tab 1": QPushButton("Tab 1"),
            "Tab 2": QPushButton("Tab 2"),
            "Tab 3": QPushButton("Tab 3")
        }

        for text, button in self.buttons.items():
            button.clicked.connect(self.onButtonClick)
            layout.addWidget(button)

        layout.addWidget(self.tabs)

        self.setLayout(layout)
        self.setWindowTitle('Custom Tab Example')

    def onButtonClick(self):
        button = self.sender()
        text = button.text()

        # Check if the tab page has already been created
        for i in range(self.tabs.count()):
            if self.tabs.widget(i).windowTitle() == text:
                self.tabs.setCurrentIndex(i)
                return

        # Create a new tab page
        new_tab = TabPage(f"Content of {text}")
        new_tab.setWindowTitle(text)
        self.tabs.addWidget(new_tab)
        self.tabs.setCurrentWidget(new_tab)

app = QApplication(sys.argv)
win = MainWindow()
win.show()
sys.exit(app.exec_())
```

在这个示例中，每次点击按钮时，都会检查相应的 Tab 页面是否已经被创建。如果没有，它将创建一个新的页面，并将其添加到 `QStackedWidget` 中。这样可以确保每个页面只被加载一次，但仅在需要时加载。

### 总结

选择哪种方法取决于应用需求、预期的用户体验和资源管理策略。

对于大多数应用程序，按需加载提供了更好的性能和资源使用效率。
