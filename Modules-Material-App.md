## Material App

KivyMD has the `MDApp` class with the necessary properties. Before 0.102.1 you
had to create the `theme_cls` property, but with `MDApp` you don't need to do
this.

### Minimal app

Example of minimal app using `MDApp`.

```python
from kivy.lang import Builder
from kivymd.app import MDApp

root_kv = """
BoxLayout:
    MDRaisedButton:
        text: "Click me!"
        on_release: print("Hi!")
"""


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "My Material Application"
        super().__init__(**kwargs)

    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```

### Changing Theme Manager properties

If you want to change theme style, primary colors or other properties of
`ThemeManager`, you can do this in `__init__` method.

```python
from kivy.lang import Builder
from kivymd.app import MDApp

root_kv = """
BoxLayout:
    MDRaisedButton:
        text: "Click me!"
        on_release: print("Hi!")
"""


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "My Material Application"
        self.theme_cls.theme_style = "Dark"
        self.theme_cls.primary_palette = "DeepPurple"
        super().__init__(**kwargs)

    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```

### Accessing app

KivyMD's `MDApp` is a simple Kivy's `App`. You can access your app object with
`App.get_running_app()` in Python code and `app` in KV code.


```python
from kivy.lang import Builder
from kivy.app import App
from kivymd.app import MDApp
from kivymd.uix.chip import MDChip

root_kv = """
BoxLayout:
    MDRaisedButton:
        text: app.title
        on_release: app.title = "Abcd"
    
    MyWidget:
"""


class MyWidget(MDChip):
    def __init__(self, **kwargs):
        self.label = App.get_running_app().title
        super().__init__(**kwargs)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "My Material Application"
        super().__init__(**kwargs)

    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```
