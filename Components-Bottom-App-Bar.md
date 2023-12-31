![appbar.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/appbar.gif)

## Example of using MDBottomAppBar:

```python
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.app import MDApp

Builder.load_string(
    """
<StyleLabel@MDLabel>:
    adaptive_height: True


<StyleItemCheck@MDBoxLayout>:
    group: ""
    text: ""
    active: False
    adaptive_height: True

    MDCheckbox:
        group: root.group
        active: root.active
        size_hint: None, None
        size: dp(48), dp(48)
        pos_hint: {"center_y": .5}
        on_active: app.callback(root.text, self.active)

    StyleLabel:
        text: root.text
        pos_hint: {"center_y": .5}


<BottomAppBar@Screen>
    name: "bottom app bar"

    MDBoxLayout:
        spacing: dp(10)
        orientation: "vertical"

        MDToolbar:
            title: "Title"
            md_bg_color: app.theme_cls.primary_color
            left_action_items: [["menu", lambda x: x]]

        ScrollView:

            MDGridLayout:
                adaptive_height: True
                cols: 1
                padding: "10dp"
                spacing: "10dp"

                MDSeparator:

                StyleLabel:
                    text: "Notch"

                StyleItemCheck:
                    group: "notch"
                    text: "On"
                    active: True

                StyleItemCheck:
                    group: "notch"
                    text: "Off"

                MDSeparator:

                StyleLabel:
                    text: "Position"

                StyleItemCheck:
                    group: "pos"
                    text: "Attached - Center"
                    active: True

                StyleItemCheck:
                    group: "pos"
                    text: "Attached - End"

                StyleItemCheck:
                    group: "pos"
                    text: "Free - Center"

                StyleItemCheck:
                    group: "pos"
                    text: "Free - End"

        MDBottomAppBar:

            MDToolbar:
                id: toolbar
                title: "Title"
                icon: "git"
                type: "bottom"
                left_action_items: [["menu", lambda x: x]]
"""
)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Bottom App Bar"
        super().__init__(**kwargs)

    def build(self):
        self.root = Factory.BottomAppBar()

    def callback(self, text, value):
        if value and self.root:
            if text == "Off":
                self.root.ids.toolbar.remove_notch()
            elif text == "On":
                self.root.ids.toolbar.set_notch()
            elif text == "Attached - End":
                self.root.ids.toolbar.mode = "end"
            elif text == "Attached - Center":
                self.root.ids.toolbar.mode = "center"
            elif text == "Free - End":
                self.root.ids.toolbar.mode = "free-end"
            elif text == "Free - Center":
                self.root.ids.toolbar.mode = "free-center"


if __name__ == "__main__":
    MainApp().run()
```