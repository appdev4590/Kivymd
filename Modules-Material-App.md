## Material App

KivyMD has the `MDApp` class that creates all required for KivyMD properties. Before
[0.102.1](https://github.com/HeaTTheatR/KivyMD/blob/master/CHANGELOG.md#v01021---alpha) you had
to create the `theme_cls` property, but with `MDApp` you don't need to do this.

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

### Exceptions

#### KivyMD: App object should be initialized before loading root widget

> Or `AttributeError: 'NoneType' object has no attribute 'property'` in version 0.102.1

Some of your widgets are created before `MainApp().run()`. To fix this issue, move `Builder.load_...` (that loads root widget) to `build` method of app class and move widget creation to methods that call after app initialization.

<details>
<summary>Example of incorrect code #1</summary>

```python
from kivy.lang import Builder
from kivymd.app import MDApp

Builder.load_string("""
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
""")


class MainApp(MDApp):
    pass


if __name__ == "__main__":
    MainApp().run()
```

Code above will raise ValueError:
```
 Traceback (most recent call last):
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 374, in __init__
     App.get_running_app().property("theme_cls", True),
 AttributeError: 'NoneType' object has no attribute 'property'

 During handling of the above exception, another exception occurred:

 Traceback (most recent call last):
   File "D:\Projects\my_project\main.py", line 11, in <module>
     """)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 405, in load_string
     rule_children=rule_children)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 654, in _apply_rule
     child = cls(__no_builder=True)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\uix\label.py", line 94, in __init__
     super().__init__(**kwargs)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 384, in __init__
     "KivyMD: App object should be initialized before loading "
 ValueError: KivyMD: App object should be initialized before loading root widget. See https://github.com/HeaTTheatR/KivyMD/wiki/Modules-Material-App#exceptions
```

***

Correct code:
```python
from kivy.lang import Builder
from kivymd.app import MDApp

root_kv = """
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
"""


class MainApp(MDApp):
    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```
</details>

<details>
<summary>Example of incorrect code #2</summary>

```python
from kivy.lang import Builder
from kivy.properties import ObjectProperty
from kivy.uix.boxlayout import BoxLayout
from kivymd.app import MDApp
from kivymd.uix.textfield import MDTextField

Builder.load_string("""
<MyRootBoxLayout>:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
""")


class MyRootBoxLayout(BoxLayout):
    my_textfield = ObjectProperty(MDTextField())

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.add_textfield()

    def add_textfield(self):
        self.add_widget(self.my_textfield)


class MainApp(MDApp):
    def build(self):
        return MyRootBoxLayout()


if __name__ == "__main__":
    MainApp().run()
```

Code above will raise ValueError:
```
 Traceback (most recent call last):
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 374, in __init__
     App.get_running_app().property("theme_cls", True),
 AttributeError: 'NoneType' object has no attribute 'property'

 During handling of the above exception, another exception occurred:

 Traceback (most recent call last):
   File "D:\Projects\my_project\main.py", line 17, in <module>
     class MyRootBoxLayout(BoxLayout):
   File "D:\Projects\my_project\main.py", line 18, in MyRootBoxLayout
     my_textfield = ObjectProperty(MDTextField())
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\uix\textfield.py", line 573, in __init__
     field=self,
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\uix\textfield.py", line 526, in __init__
     super().__init__(**kwargs)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 384, in __init__
     "KivyMD: App object should be initialized before loading "
 ValueError: KivyMD: App object should be initialized before loading root widget. See https://github.com/HeaTTheatR/KivyMD/wiki/Modules-Material-App#exceptions
```

***

Correct code:
```python
from kivy.lang import Builder
from kivy.properties import ObjectProperty
from kivy.uix.boxlayout import BoxLayout
from kivymd.app import MDApp
from kivymd.uix.textfield import MDTextField

Builder.load_string("""
<MyRootBoxLayout>:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
""")


class MyRootBoxLayout(BoxLayout):
    my_textfield = ObjectProperty()

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.add_textfield()

    def add_textfield(self):
        if not self.my_textfield:
            self.my_textfield = MDTextField()
        self.add_widget(self.my_textfield)


class MainApp(MDApp):
    def build(self):
        return MyRootBoxLayout()


if __name__ == "__main__":
    MainApp().run()
```
</details>

#### ValueError: KivyMD: App object should be inherited from `kivymd.app.MDApp`

Use the template at [Material App page](https://github.com/HeaTTheatR/KivyMD/wiki/Modules-Material-App#minimal-app).

<details>
<summary>Example of incorrect code #1</summary>

```python
from kivy.lang import Builder
from kivy.app import App
from kivymd.theming import ThemeManager

root_kv = """
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
"""


class MainApp(App):
    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```

Code above will raise ValueError:
```
 Traceback (most recent call last):
   File "D:\Projects\my_project\main.py", line 21, in <module>
     MainApp().run()
   File "D:\Py\kivy-venv\lib\site-packages\kivy\app.py", line 829, in run
     root = self.build()
   File "D:\Projects\my_project\main.py", line 17, in build
     self.root = Builder.load_string(root_kv)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 405, in load_string
     rule_children=rule_children)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 654, in _apply_rule
     child = cls(__no_builder=True)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\uix\label.py", line 94, in __init__
     super().__init__(**kwargs)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 378, in __init__
     "KivyMD: App object should be inherited from "
 ValueError: KivyMD: App object should be inherited from `kivymd.app.MDApp`. See https://github.com/HeaTTheatR/KivyMD/blob/master/README.md#api-breaking-changes
```

***

Correct code:
```python
from kivy.lang import Builder
from kivymd.app import MDApp

root_kv = """
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
"""


class MainApp(MDApp):
    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```
</details>

<details>
<summary>Example of incorrect code #2</summary>

```python
from kivy.lang import Builder
from kivy.app import App
from kivymd.theming import ThemeManager

root_kv = """
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
"""


class MainApp(App):
    theme_cls = ThemeManager()

    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```

Code above will raise ValueError:
```
 Traceback (most recent call last):
   File "D:\Projects\my_project\main.py", line 23, in <module>
     MainApp().run()
   File "D:\Py\kivy-venv\lib\site-packages\kivy\app.py", line 829, in run
     root = self.build()
   File "D:\Projects\my_project\main.py", line 17, in build
     self.root = Builder.load_string(root_kv)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 405, in load_string
     rule_children=rule_children)
   File "D:\Py\kivy-venv\lib\site-packages\kivy\lang\builder.py", line 654, in _apply_rule
     child = cls(__no_builder=True)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\uix\label.py", line 94, in __init__
     super().__init__(**kwargs)
   File "D:\Py\kivy-venv\lib\site-packages\KivyMD\kivymd\theming.py", line 378, in __init__
     "KivyMD: App object should be inherited from "
 ValueError: KivyMD: App object should be inherited from `kivymd.app.MDApp`. See https://github.com/HeaTTheatR/KivyMD/blob/master/README.md#api-breaking-changes
```

***

Correct code:
```python
from kivy.lang import Builder
from kivymd.app import MDApp

root_kv = """
BoxLayout:
    MDLabel:
        text: "Hello World"

    MDRaisedButton:
        text: "Click me!"
"""


class MainApp(MDApp):
    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```
</details>
