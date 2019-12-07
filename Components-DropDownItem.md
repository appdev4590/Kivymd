![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/dropdownitem.gif)

## Example of using MDDropDownItem:

```python
from kivy.lang import Builder
from kivy.factory import Factory
from kivymd.app import MDApp

Builder.load_string(
    """
#:import toast kivymd.toast.toast


<MyRoot@BoxLayout>
    orientation: "vertical"

    MDToolbar:
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        elevation: 10
        left_action_items: [["menu", lambda x: x]]

    FloatLayout:

        MDDropDownItem:
            id: dropdown_item
            pos_hint: {"center_x": 0.5, "center_y": 0.6}
            items: app.items
            dropdown_bg: [1, 1, 1, 1]

        MDRaisedButton:
            pos_hint: {"center_x": 0.5, "center_y": 0.3}
            text: "Chek Item"
            on_release: toast(dropdown_item.current_item)
"""
)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - DropDownItem"
        self.theme_cls.primary_palette = "BlueGray"
        super().__init__(**kwargs)

    def build(self):
        self.items = [f"Item {i}" for i in range(50)]
        self.root = Factory.MyRoot()


if __name__ == "__main__":
    MainApp().run()
```