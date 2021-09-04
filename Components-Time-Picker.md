![useranimationcard.gif](https://raw.githubusercontent.com/HeaTTheatR/KivyMD-data/master/gallery/kivymddoc/MDTimePicker.png)

## Example of using MDTimePicker:

```python
rom kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.uix.pickers import MDTimePicker

KV = '''
MDFloatLayout:

    MDRaisedButton:
        text: "Open time picker"
        pos_hint: {'center_x': .5, 'center_y': .5}
        on_release: app.show_time_picker()
'''


class Test(MDApp):
    def build(self):
        return Builder.load_string(KV)

    def show_time_picker(self):
        '''Open time picker dialog.'''

        time_dialog = MDTimePicker()
        time_dialog.open()


Test().run()
```