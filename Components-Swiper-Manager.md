![managerswiper.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/managerswiper.gif)

## Example of using MDSwiperManager:

```python
import os
from kivy.lang import Builder
from kivy.core.window import Window
from kivy.metrics import dp
from kivy.properties import StringProperty, ObjectProperty
from kivy.uix.boxlayout import BoxLayout
from kivymd.app import MDApp
from kivymd.utils.cropimage import crop_image
from kivymd.uix.card import MDCard
from kivymd.uix.managerswiper import MDSwiperPagination

kv = """
#:import images_path kivymd.images_path


<MyCard>:
    orientation: "vertical"
    size_hint_y: None
    height: dp(300)
    pos_hint: {"top": 1}

    Image:
        source:
            "{}/demos/kitchen_sink/assets/" \
            "guitar-1139397_1280_swiper_crop.png".format(app.directory)
        size_hint: None, None
        size: root.width, dp(250)
        pos_hint: {"top": 1}

    MDLabel:
        theme_text_color: "Custom"
        bold: True
        text_color: app.theme_cls.primary_color
        text: root.text
        size_hint_y: None
        height: dp(60)
        halign: "center"


<ScreenOne@Screen>:
    name: "screen one"
    MyCard:
        text: "Swipe to switch to screen one".upper()


<ScreenTwo@Screen>:
    name: "screen two"
    MyCard:
        text: "Swipe to switch to screen two".upper()


<ScreenThree@Screen>:
    name: "screen three"
    MyCard:
        text: "Swipe to switch to screen three".upper()


<ScreenFour@Screen>:
    name: "screen four"
    MyCard:
        text: "Swipe to switch to screen four".upper()


<ScreenFive@Screen>:
    name: "screen five"
    MyCard:
        text: "Swipe to switch to screen five".upper()


<MySwiperManager>:
    orientation: "vertical"

    canvas:
        Color:
            rgba: 0, 0, 0, .2
        Rectangle:
            pos: self.pos
            size: self.size

    MDToolbar:
        id: toolbar
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        background_palette: "Primary"
        elevation: 10
        left_action_items: [["menu", lambda x: x]]

    BoxLayout:
        padding: dp(10)
        orientation: "vertical"

        MDSwiperManager:
            id: swiper_manager

            ScreenOne:

            ScreenTwo:

            ScreenThree:

            ScreenFour:

            ScreenFive:
"""


class MySwiperManager(BoxLayout):
    pass


class MyCard(MDCard):
    text = StringProperty("")


class MainApp(MDApp):
    swiper_manager = ObjectProperty()

    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Swiper Manager"
        self.theme_cls.primary_palette = "Indigo"
        super().__init__(**kwargs)

    def build(self):
        self.crop_image_for_card()
        Builder.load_string(kv)
        start_screen = MySwiperManager()
        self.swiper_manager = start_screen.ids.swiper_manager
        paginator = MDSwiperPagination()
        paginator.screens = self.swiper_manager.screen_names
        paginator.manager = self.swiper_manager
        self.swiper_manager.paginator = paginator
        start_screen.add_widget(paginator)

        self.root = start_screen

    def crop_image_for_card(self):
        path_to_crop_image = (
            "{}/demos/kitchen_sink/assets/"
            "guitar-1139397_1280_swiper_crop.png".format(self.directory)
        )
        if not os.path.exists(path_to_crop_image):
            crop_image(
                (int(Window.width - dp(10)), int(dp(250))),
                "{}/demos/kitchen_sink/assets/guitar-1139397_1280.png".format(
                    self.directory
                ),
                path_to_crop_image,
            )


if __name__ == "__main__":
    MainApp().run()
```