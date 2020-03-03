![speeddial.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/kivymddoc/MDFloatingActionButtonSpeedDial.gif)

## Example of using MDFloatingActionButtonSpeedDial:

```python
from kivy.lang import Builder

from kivymd.app import MDApp

KV = '''
Screen:

    MDFloatingActionButtonSpeedDial:
        data: app.data
        rotation_root_button: True
'''


class Example(MDApp):
    data = {
        'language-python': 'Python',
        'language-php': 'PHP',
        'language-cpp': 'C++',
    }

    def build(self):
        return Builder.load_string(KV)


Example().run()
```