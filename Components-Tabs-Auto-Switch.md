![auto-switch-tabs.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/kivymddoc/tabs-auto-switch-example.gif)

## Tab auto switch example:

```python

from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.uix.bottomnavigation import MDBottomNavigationItem
from kivymd.uix.menu import MDDropdownMenu
from kivymd.icon_definitions import md_icons


KV = """
<BottomNavigationItem>:

    MDLabel:
        text: root.text
        halign: 'center'


BoxLayout:
    orientation:'vertical'

    MDToolbar:
        id: toolbar
        title: 'Bottom navigation'
        left_action_items: [["dots-vertical", lambda x: app.show_menu()]]

    MDBottomNavigation:
        id: panel
"""


class BottomNavigationItem(MDBottomNavigationItem):
    pass


class Test(MDApp):
    def callback_for_menu_items(self, name_tab):
        self.screen.ids.panel.switch_tab(name_tab)

    def show_menu(self):
        menu_items = [
            {
                "viewclass": "MDMenuItem",
                "text": f"Tab {i}",
                "callback": self.callback_for_menu_items,
            }
            for i in range(3)
        ]
        MDDropdownMenu(items=menu_items, width_mult=3).open(
            self.screen.ids.toolbar.ids.left_actions.children[0]
        )

    def build(self):
        self.screen = Builder.load_string(KV)
        for i, name_icon in enumerate(list(md_icons.keys())[10:13]):
            self.screen.ids.panel.add_widget(
                BottomNavigationItem(
                    name=f"Tab {i}", text=f"Tab {i}", icon=name_icon,
                )
            )
        return self.screen


Test().run()
```