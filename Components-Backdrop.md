![backdrop.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/backdrop.gif)

## Example of using MDBackdrop:

```python
from kivy.lang import Builder
from kivy.properties import StringProperty, BooleanProperty

from kivymd.uix.boxlayout import MDBoxLayout
from kivymd.uix.screen import MDScreen
from kivymd.app import MDApp
from kivymd.theming import ThemableBehavior

# Your layouts.
Builder.load_string(
    """
#:import NoTransition kivy.uix.screenmanager.NoTransition
#:import Window kivy.core.window.Window
#:import IconLeftWidget kivymd.uix.list.IconLeftWidget


<ItemBackdropFrontLayer@TwoLineAvatarListItem>
    icon: "android"

    IconLeftWidget:
        icon: root.icon


<ItemBackdropBackLayer>
    adaptive_height: True
    spacing: "10dp"
    md_bg_color:
        root.theme_cls.primary_dark \
        if root.selected_item \
        else root.theme_cls.primary_color

    MDIconButton:
        icon: root.icon
        theme_text_color: "Custom"
        text_color: (1, 1, 1, .5) if not root.selected_item else (1, 1, 1, 1)

    MDLabel:
        text: root.text
        color: (1, 1, 1, .5) if not root.selected_item else (1, 1, 1, 1)


<ItemBackdropBackLayerOfSecondScreen@BoxLayout>
    size_hint_y: None
    height: "40dp"
    spacing: "25dp"
    text: ""

    MDCheckbox:
        size_hint: None, None
        size: "30dp", "30dp"
        active: False or self.active
        pos_hint: {"center_y": .5}
        selected_color: 1, 1, 1, 1

    MDLabel:
        text: root.text
        color: 1, 1, 1, .7


<ItemRoundBackdropBackLayerOfSecondScreen@BoxLayout>
    size_hint_y: None
    height: "40dp"
    spacing: "25dp"
    text: ""

    MDCheckbox:
        group: "size"
        size_hint: None, None
        size: "30dp", "30dp"
        pos_hint: {"center_y": .5}
        selected_color: 1, 1, 1, 1

    MDLabel:
        text: root.text
        color: 1, 1, 1, .7


<MyBackdropFrontLayer@ScrollView>
    backdrop: None
    backlayer: None

    MDGridLayout:
        adaptive_height: True
        cols: 1
        padding: "5dp"

        ItemBackdropFrontLayer:
            text: "Press item"
            secondary_text: "to Shop Electronics"
            icon: "monitor-star"
            on_press:
                root.backlayer.current = "second screen"
                root.backdrop.open()

        ItemBackdropFrontLayer:
            text: "Press item"
            secondary_text: "to Back"
            icon: "arrange-send-backward"
            on_press:
                root.backlayer.current = "one screen"
                root.backdrop.open()

        ItemBackdropFrontLayer:
            text: "Lower the front layer"
            secondary_text: " by 50 %"
            icon: "transfer-down"
            on_press: root.backdrop.open(-Window.height / 2)


<MyBackdropBackLayer@ScreenManager>
    transition: NoTransition()

    MDScreen:
        name: "one screen"

        ScrollView

            MDGridLayout:
                adaptive_height: True
                cols: 1
                padding: "5dp"

                ItemBackdropBackLayer:
                    icon: "theater"
                    text: "TV & Home Theaters"
                ItemBackdropBackLayer:
                    icon: "desktop-mac"
                    text: "Computers"
                ItemBackdropBackLayer:
                    icon: "camera-plus-outline"
                    text: "Camera and Camcorders"
                ItemBackdropBackLayer:
                    icon: "speaker"
                    text: "Speakers"
                ItemBackdropBackLayer:
                    icon: "cellphone-iphone"
                    text: "Mobile Phones"
                ItemBackdropBackLayer:
                    icon: "movie-outline"
                    text: "Movies"
                ItemBackdropBackLayer:
                    icon: "gamepad-variant-outline"
                    text: "Games"
                ItemBackdropBackLayer:
                    icon: "music-circle-outline"
                    text: "Music"

    MDScreen:
        name: "second screen"

        ScrollView

            MDGridLayout:
                adaptive_height: True
                cols: 1
                padding: "15dp"
                spacing: "10dp"

                MDLabel:
                    text: "Types of TVs Home Theater Product"
                    color: 1, 1, 1, 1

                Widget:
                    size_hint_y: None
                    height: "10dp"

                ItemBackdropBackLayerOfSecondScreen:
                    text: "Smart TV"
                ItemBackdropBackLayerOfSecondScreen:
                    text: "4K Ultra HD TVs"
                ItemBackdropBackLayerOfSecondScreen:
                    text: "Curved TVs"
                ItemBackdropBackLayerOfSecondScreen:
                    text: "OLED TVs"
                ItemBackdropBackLayerOfSecondScreen:
                    text: "LED TVs"
                ItemBackdropBackLayerOfSecondScreen:
                    text: "Home Theater Systems"

                MDSeparator:

                Widget:
                    size_hint_y: None
                    height: "15dp"

                MDLabel:
                    text: "Types of TVs Home Theater Product"
                    color: 1, 1, 1, 1

                ItemRoundBackdropBackLayerOfSecondScreen:
                    text: "TVs up to 32\\""
                ItemRoundBackdropBackLayerOfSecondScreen:
                    text: "TVs 39\\"-50\\""
                ItemRoundBackdropBackLayerOfSecondScreen:
                    text: "TVs 55\\" or larger"
"""
)

# Usage example of MDBackdrop.
Builder.load_string(
    """
<ExampleBackdrop>

    MDBackdrop:
        id: backdrop
        on_open: print("on_open")
        on_close: print("on_close")
        left_action_items: [["menu", lambda x: self.open()]]
        title: app.title
        header_text: "Menu:"

        MDBackdropBackLayer:
            MyBackdropBackLayer:
                id: backlayer

        MDBackdropFrontLayer:
            MyBackdropFrontLayer:
                backdrop: backdrop
                backlayer: backlayer
"""
)


class ExampleBackdrop(MDScreen):
    pass


class ItemBackdropBackLayer(ThemableBehavior, MDBoxLayout):
    icon = StringProperty("android")
    text = StringProperty()
    selected_item = BooleanProperty(False)

    def on_touch_down(self, touch):
        if self.collide_point(touch.x, touch.y):
            for item in self.parent.children:
                if item.selected_item:
                    item.selected_item = False
            self.selected_item = True
        return super().on_touch_down(touch)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.title = "KivyMD Example - Backdrop"
        self.theme_cls.primary_palette = "DeepPurple"

    def build(self):
        self.root = ExampleBackdrop()


if __name__ == "__main__":
    MainApp().run()
```