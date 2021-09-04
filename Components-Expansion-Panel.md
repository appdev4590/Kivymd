![expansion_panel.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/kivymddoc/expansion-panel.gif)

## Example of using MDExpansionPanel:

```python
from kivy.lang import Builder

from kivymd.uix.boxlayout import MDBoxLayout
from kivymd.app import MDApp
from kivymd import images_path
from kivymd.uix.expansionpanel import MDExpansionPanel, MDExpansionPanelThreeLine

KV = '''
<Content>
    size_hint_y: None
    height: self.minimum_height

    TwoLineIconListItem:
        text: "(050)-123-45-67"
        secondary_text: "Mobile"

        IconLeftWidget:
            icon: 'phone'


MDScreen:

    MDBoxLayout:
        orientation: "vertical"

        MDToolbar:
            title: "Expansion panel"
            elevation: 10

        ScrollView:

            MDGridLayout:
                cols: 1
                adaptive_height: True
                id: box
'''


class Content(MDBoxLayout):
    pass


class Test(MDApp):
    def build(self):
        return Builder.load_string(KV)

    def on_start(self):
        for i in range(10):
            self.root.ids.box.add_widget(
                MDExpansionPanel(
                    icon=f"{images_path}kivymd_logo.png",
                    content=Content(),
                    panel_cls=MDExpansionPanelThreeLine(
                        text="Text",
                        secondary_text="Secondary text",
                        tertiary_text="Tertiary text",
                    )
                )
            )


Test().run()
```