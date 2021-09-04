![chips.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/chips.gif)

## Example of using MDChip:

```python
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.toast import toast

kv = """
MDBoxLayout:
    orientation: "vertical"
    spacing: dp(10)

    MDToolbar:
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        left_action_items: [["menu", lambda x: x]]
        background_palette: "Primary"

    ScrollView:

        MDGridLayout:
            padding: dp(10)
            spacing: dp(10)
            cols: 1
            adaptive_height: True

            MDLabel:
                text: "Chips with color: "

            MDSeparator:

            MDStackLayout:
                adaptive_height: True
                spacing: dp(5)

                MDChip:
                    text: "Coffee"
                    color: .4470588235294118, .19607843137254902, 0, 1
                    icon: "coffee"
                    callback: app.callback

                MDChip:
                    text: "Duck"
                    color: .9215686274509803, 0, 0, 1
                    icon: "duck"
                    callback: app.callback

                MDChip:
                    text: "Earth"
                    color: .21176470588235294, .09803921568627451, 1, 1
                    icon: "earth"
                    callback: app.callback

                MDChip:
                    text: "Face"
                    color: .20392156865098, .48235294117606, .43529411764705883, 1
                    icon: "face"
                    callback: app.callback

                MDChip:
                    text: "Facebook"
                    color: .5607843137254902, .48235294164706, .435294117705883, 1
                    icon: "facebook"
                    callback: app.callback

            Widget:
                size_hint_y: None
                height: dp(5)

            MDLabel:
                text: "Chip without icon: "

            MDSeparator:

            MDStackLayout:
                adaptive_height: True
                spacing: dp(5)

                MDChip:
                    text: "Without icon"
                    icon: ""
                    callback: app.callback

            Widget:
                size_hint_y: None
                height: dp(5)

            MDLabel:
                text: "Chips with check: "

            MDSeparator:

            MDStackLayout:
                adaptive_height: True
                spacing: dp(5)

                MDChip:
                    text: "Check"
                    icon: ""
                    check: True
                    callback: app.callback

                MDChip:
                    text: "Check with icon"
                    icon: "city"
                    check: True
                    callback: app.callback
            Widget:
                size_hint_y: None
                height: dp(5)

            MDLabel:
                text: "Choose chip: "

            MDSeparator:

            MDChooseChip:

                MDChip:
                    text: "Earth"
                    icon: "earth"
                    callback: app.callback
                    selected_chip_color: .21176470535294, .098039627451, 1, 1

                MDChip:
                    text: "Face"
                    icon: "face"
                    callback: app.callback
                    selected_chip_color: .21176470535294, .098039627451, 1, 1

                MDChip:
                    text: "Facebook"
                    icon: "facebook"
                    callback: app.callback
                    selected_chip_color: .21176470535294, .098039627451, 1, 1
"""


class MainApp(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.title = "KivyMD Examples - Chip"
        self.theme_cls.primary_palette = "Red"

    def build(self):
        self.root = Builder.load_string(kv)

    def callback(self, instance, value):
        toast(value)


if __name__ == "__main__":
    MainApp().run()
```