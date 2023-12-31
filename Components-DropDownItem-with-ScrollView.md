![MDDropDownItem-with-ScrollView.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/MDDropDownItem-with-ScrollView.gif)

## Example of using MDDropDownItem with ScrollView:

```python
from kivy.properties import ListProperty
from kivy.uix.boxlayout import BoxLayout
from kivy.lang import Builder
from kivymd.app import MDApp
from kivymd.uix.dropdownitem import MDDropDownItem
from kivymd.uix.list import IRightBodyTouch, ThreeLineRightIconListItem

Builder.load_string(
    """
<Item>:
    height: dp(56)
    text: "A button with"
    secondary_text: "a dropdown"
    font_style: "H6"

    ListButtonDropdown:
        items: root.items


<Base>:
    orientation: "vertical"
    spacing: "10dp"

    MDToolbar:
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        elevation: 10
        left_action_items: [["menu", lambda x: x]]

    ScrollView:

        GridLayout:
            id: box
            size_hint_y: None
            height: self.minimum_height
            cols: 1
"""
)


class Base(BoxLayout):
    pass


class Item(ThreeLineRightIconListItem):
    items = ListProperty()


class ListButtonDropdown(IRightBodyTouch, MDDropDownItem):
    pass


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - DropDownItem with ScrollView"
        super().__init__(**kwargs)

    def build(self):
        self.root = Base()

    def on_start(self):
        for i in range(20):
            self.root.ids.box.add_widget(
                Item(items=[str(i + 1), str(i + 2), str(i + 3)])
            )


if __name__ == "__main__":
    MainApp().run()
```