![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/dropdownmenu.gif)

## Example of using MDDropdownMenu:

```python
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.uix.menu import MDDropdownMenu, RightContent
from kivymd.theming import ThemableBehavior
from kivymd.uix.behaviors import RectangularElevationBehavior
from kivymd.uix.boxlayout import MDBoxLayout

KV = """
<RightContentCls>
    disabled: True

    MDIconButton:
        icon: root.icon
        user_font_size: "16sp"
        pos_hint: {"center_y": .5}

    MDLabel:
        text: root.text
        font_style: "Caption"
        size_hint_x: None
        width: self.texture_size[0]
        text_size: None, None


<CustomToolbar>:
    size_hint_y: None
    height: self.theme_cls.standard_increment
    padding: "5dp"
    spacing: "12dp"

    MDIconButton:
        id: button_1
        icon: "menu"
        pos_hint: {"center_y": .5}
        on_release: app.menu_1.open()

    MDLabel:
        text: "MDDropdownMenu"
        pos_hint: {"center_y": .5}
        size_hint_x: None
        width: self.texture_size[0]
        text_size: None, None
        font_style: 'H6'

    Widget:

    MDIconButton:
        id: button_2
        icon: "dots-vertical"
        pos_hint: {"center_y": .5}
        on_release: app.menu_2.open()


Screen:

    CustomToolbar:
        id: toolbar
        elevation: 10
        pos_hint: {"top": 1}
"""


class RightContentCls(RightContent):
    pass


class CustomToolbar(
    ThemableBehavior, RectangularElevationBehavior, MDBoxLayout,
):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.md_bg_color = self.theme_cls.primary_color


class Test(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.screen = Builder.load_string(KV)
        self.menu_1 = self.create_menu(
            "Button menu", self.screen.ids.toolbar.ids.button_1
        )
        self.menu_2 = self.create_menu(
            "Button dots", self.screen.ids.toolbar.ids.button_2
        )

    def create_menu(self, text, instance):
        menu_items = [
            {
                "right_content_cls": RightContentCls(
                    text=f"R+{i}", icon="apple-keyboard-command",
                ),
                "icon": "git",
                "text": text,
            }
            for i in range(5)
        ]
        return MDDropdownMenu(caller=instance, items=menu_items, width_mult=5)

    def build(self):
        return self.screen


Test().run()
```