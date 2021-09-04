![grid.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/grid.gif)

## Example of using MDSmartTile:

```python
import os
from kivy.lang import Builder

from kivymd.app import MDApp
from kivymd.utils.cropimage import crop_image

root_kv = """
<MySmartTileWithLabel@SmartTileWithLabel>:
    mipmap: True
    font_style: "Subhead"


MDBoxLayout:
    orientation: "vertical"

    MDToolbar:
        title: app.title
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
            on_enter:
                app.crop_image_for_tile(tile_1, tile_1.size, \
                "demos/kitchen_sink/assets/beautiful-931152_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_2, tile_2.size, \
                "demos/kitchen_sink/assets/african-lion-951778_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_3, tile_3.size, \
                "demos/kitchen_sink/assets/guitar-1139397_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_4, tile_4.size, \
                "demos/kitchen_sink/assets/robin-944887_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_5, tile_5.size, \
                "demos/kitchen_sink/assets/kitten-1049129_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_6, tile_6.size, \
                "demos/kitchen_sink/assets/light-bulb-1042480_1280_tile_crop.jpg")
                app.crop_image_for_tile(tile_7, tile_7.size, \
                "demos/kitchen_sink/assets/tangerines-1111529_1280_tile_crop.jpg")

            ScrollView:
                do_scroll_x: False

                MDGridLayout:
                    cols: 2
                    row_default_height: (self.width - self.cols*self.spacing[0])/self.cols
                    row_force_default: True
                    adaptive_height: True
                    padding: dp(4), dp(4)
                    spacing: dp(4)

                    SmartTileWithStar:
                        id: tile_2
                        mipmap: True
                        stars: 3
                    SmartTileWithStar:
                        id: tile_3
                        mipmap: True
                        stars: 3
                    SmartTileWithLabel:
                        id: tile_1
                        text:
                            "Beautiful\\n[size=12]beautiful-931152_1280.jpg[/size]"
                    SmartTileWithLabel:
                        id: tile_4
                        text:
                            "Robin\\n[size=12]robin-944887_1280.jpg[/size]"
                    SmartTileWithLabel:
                        id: tile_5
                        text:
                            "Kitten\\n[size=12]kitten-1049129_1280.jpg[/size]"
                    SmartTileWithLabel:
                        id: tile_6
                        text:
                            "Light-Bulb\\n[size=12]light-bulb-1042480_1280.jpg[/size]"
                    SmartTileWithLabel:
                        id: tile_7
                        text:
                            "Tangerines\\n[size=12]tangerines-1111529_1280.jpg[/size]"
"""


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Smart Tile"
        self.theme_cls.primary_palette = "Blue"
        super().__init__(**kwargs)

    def build(self):
        self.root = Builder.load_string(root_kv)

    def crop_image_for_tile(self, instance, size, path_to_crop_image):
        if not os.path.exists(os.path.join(self.directory, path_to_crop_image)):
            size = (int(size[0]), int(size[1]))
            path_to_origin_image = path_to_crop_image.replace("_tile_crop", "")
            crop_image(size, path_to_origin_image, path_to_crop_image)
        instance.source = path_to_crop_image


if __name__ == "__main__":
    MainApp().run()
```