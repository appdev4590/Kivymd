![chips.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/tooltips.gif)

## Example of using MDTooltip:

```python
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.uix.button import MDIconButton
from kivymd.uix.tooltip import MDTooltip
from kivymd.icon_definitions import md_icons

KV = """
MDBoxLayout:
    orientation: "vertical"

    MDToolbar:
        title: "MDTooltip"
        elevation: 10

    MDScreen:

        MDBoxLayout:
            id: box
            adaptive_size: True
            padding: "10dp"
            spacing: "10dp"
            pos_hint: {"center_x": .5, "center_y": .9}
"""


class IconButtonTooltips(MDIconButton, MDTooltip):
    pass


class MainApp(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)

    def build(self):
        return Builder.load_string(KV)

    def on_start(self):
        for name_icon in list(md_icons.keys())[10:16]:
            self.root.ids.box.add_widget(
                IconButtonTooltips(
                    icon=name_icon,
                    tooltip_text=name_icon,
                )
            )


MainApp().run()
```

## MDTooltip Behavior on Mobile:

![chips.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/tooltips-on-mobile.gif)

