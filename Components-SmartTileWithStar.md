![grid.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/grid.gif)

## Example of using MDSmartTile:

```python
from kivy.lang import Builder

from kivymd.app import MDApp

root_kv = """
<MySmartTileWithLabel@SmartTileWithLabel>:
    font_style: "Subhead"


MDBoxLayout:
    orientation: "vertical"

    MDToolbar:
        elevation: 10
        left_action_items: [["menu", lambda x: x]]
        md_bg_color: app.theme_cls.primary_color

    ScreenManager:
        id: manager

        MDScreen:
            name: "one"

            MDRaisedButton:
                pos_hint: {"center_x": .5, "center_y": .55}
                on_release: manager.current = "two"
                text: "Open Grid"

        MDScreen:
            name: "two"

            ScrollView:
                do_scroll_x: False

                MDGridLayout:
                    cols: 2
                    row_default_height: (self.width - self.cols*self.spacing[0]) / self.cols
                    row_force_default: True
                    adaptive_height: True
                    padding: dp(4), dp(4)
                    spacing: dp(4)

                    SmartTileWithStar:
                        stars: 3
                        source: "image-1.png"
                    SmartTileWithStar:
                        stars: 3
                        source: "image-2.png"
                    SmartTileWithLabel:
                        text: "Beautiful\\n[size=12]beautiful-931152_1280.jpg[/size]"
                        source: "beautiful-931152_1280.jpg"
                    SmartTileWithLabel:
                        text: "Robin\\n[size=12]robin-944887_1280.jpg[/size]"
                        source: "robin-944887_1280.jpg"
                    SmartTileWithLabel:
                        text: "Kitten\\n[size=12]kitten-1049129_1280.jpg[/size]"
                        source: "kitten-1049129_1280.jpg"
                    SmartTileWithLabel:
                        text: "Light-Bulb\\n[size=12]light-bulb-1042480_1280.jpg[/size]"
                        source: "light-bulb-1042480_1280.jpg"
                    SmartTileWithLabel:
                        text: "Tangerines\\n[size=12]tangerines-1111529_1280.jpg[/size]"
                        source: "tangerines-1111529_1280.jpg"
"""


class MainApp(MDApp):
    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```