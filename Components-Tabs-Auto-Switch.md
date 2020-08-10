![auto-switch-tabs.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/kivymddoc/tabs-auto-switch-example.gif)

## Tab auto switch example:

```python
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.theming import ThemableBehavior
from kivymd.uix.behaviors import RectangularElevationBehavior
from kivymd.uix.bottomnavigation import MDBottomNavigationItem
from kivymd.icon_definitions import md_icons
from kivymd.uix.boxlayout import MDBoxLayout
from kivymd.uix.menu import MDDropdownMenu

KV = """
<BottomNavigationItem>

    MDLabel:
        text: root.text
        halign: 'center'


<CustomToolbar>
    size_hint_y: None
    height: self.theme_cls.standard_increment
    padding: "5dp"
    spacing: "12dp"

    MDIconButton:
        id: button
        icon: "menu"
        pos_hint: {"center_y": .5}
        on_release: app.menu.open()

    MDLabel:
        text: "MDBottomNavigation"
        pos_hint: {"center_y": .5}
        size_hint_x: None
        width: self.texture_size[0]
        text_size: None, None
        font_style: 'H6'


BoxLayout:
    orientation: "vertical"

    CustomToolbar:
        id: toolbar

    MDBottomNavigation:
        id: panel
"""


class BottomNavigationItem(MDBottomNavigationItem):
    pass


class CustomToolbar(
    ThemableBehavior, RectangularElevationBehavior, MDBoxLayout,
):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.md_bg_color = self.theme_cls.primary_color


class Test(MDApp):
    def callback(self, instance):
        self.screen.ids.panel.switch_tab(instance.text)

    def create_menu(self, instance):
        menu_items = [{"text": f"Tab {i}"} for i in range(3)]
        return MDDropdownMenu(
            caller=instance, 
            items=menu_items,
            width_mult=5,
            callback=self.callback,
        )

    def build(self):
        self.screen = Builder.load_string(KV)
        self.menu = self.create_menu(self.screen.ids.toolbar.ids.button)

        for i, name_icon in enumerate(list(md_icons.keys())[10:13]):
            self.screen.ids.panel.add_widget(
                BottomNavigationItem(
                    name=f"Tab {i}", text=f"Tab {i}", icon=name_icon,
                )
            )
        return self.screen


Test().run()
```