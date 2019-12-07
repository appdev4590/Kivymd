![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/time-picker.gif)

## Example of using MDTimePicker:

```python
from kivy.lang import Builder
from kivy.factory import Factory
from kivy.properties import ObjectProperty
from kivymd.app import MDApp


kv = """
<Pickers@Screen>
    name: "pickers"

    BoxLayout:
        orientation: "vertical"
        spacing: dp(20)
        pos_hint: {"center_x": .5, "center_y": .5}
        size_hint_y: None
        height: self.minimum_height

        MDRaisedButton:
            text: "Open time picker"
            pos_hint: {"center_x": .5}
            on_release: app.show_example_time_picker()

        MDLabel:
            id: time_picker_label
            theme_text_color: "Primary"
            halign: "center"

        BoxLayout:
            size_hint: None, None
            size: self.minimum_size
            pos_hint: {"center_x": .5}

            Label:
                theme_text_color: "Primary"
                text: "Start on previous date"
                size_hint_x: None#, None
                width: self.texture_size[0]
                color: 0, 0, 0, 1

            MDCheckbox:
                id: time_picker_use_previous_time
                size_hint: None, None
                size: dp(48), dp(48)
"""


class MainApp(MDApp):
    previous_time = ObjectProperty()

    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Time Picker"
        super().__init__(**kwargs)

    def build(self):
        Builder.load_string(kv)
        self.root = Factory.Pickers()

    def show_example_time_picker(self):
        from kivymd.uix.picker import MDTimePicker

        time_dialog = MDTimePicker()
        time_dialog.bind(time=self.get_time_picker_date)

        if self.root.ids.time_picker_use_previous_time.active:
            try:
                time_dialog.set_time(self.previous_time)
            except AttributeError:
                pass
        time_dialog.open()

    def get_time_picker_date(self, instance, time):
        self.root.ids.time_picker_label.text = str(time)
        self.previous_time = time


if __name__ == "__main__":
    MainApp().run()
```