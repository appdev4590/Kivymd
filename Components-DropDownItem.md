![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/dropdownitem.gif)

## Example of using MDDropDownItem:

```python
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.uix.menu import MDDropdownMenu

KV = """
#:import toast kivymd.toast.toast


Screen:

    MDToolbar:
        pos_hint: {"top": 1}
        title: "MDDropDownItem"

    MDDropDownItem:
        id: dropdown_item
        text: "Item 0"
        pos_hint: {'center_x': 0.5, 'center_y': 0.6}
        dropdown_bg: [1, 1, 1, 1]
        on_release: app.menu.open()

    MDRaisedButton:
        pos_hint: {'center_x': 0.5, 'center_y': 0.3}
        text: 'Chek Item'
        on_release: toast(dropdown_item.current_item)
"""


class Test(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.screen = Builder.load_string(KV)
        menu_items = [{"icon": "git", "text": f"Item {i}"} for i in range(5)]
        self.menu = MDDropdownMenu(
            caller=self.screen.ids.dropdown_item,
            items=menu_items,
            position="center",
            callback=self.set_item,
            width_mult=4,
        )

    def set_item(self, instance):
        self.screen.ids.dropdown_item.set_item(instance.text)

    def build(self):
        return self.screen


Test().run()
```