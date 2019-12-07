![banner.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/ezgif-5-8eaea5b6cec4.gif)

## Example of using MDCard with Expansion:

```python
from kivy.uix.boxlayout import BoxLayout

from kivymd.app import MDApp
from kivy.lang import Builder

KV = """
#:import Content __main__.Content
#:import get_hex_from_color kivy.utils.get_hex_from_color
#:import Animation kivy.animation.Animation


<Content>
    orientation: 'vertical'
    padding: dp(10)
    spacing: dp(10)
    size_hint_y: None
    height: self.minimum_height

    TwoLineIconListItem:
        text: "(050)-123-45-67"
        secondary_text:
            "[color=%s]Mobile[/color]" \
            % get_hex_from_color(app.theme_cls.primary_color)

        IconLeftWidget:
            icon: 'phone'

    TwoLineIconListItem:
        text: "kivydevelopment@gmail.com"
        secondary_text:
            "[color=%s]Work[/color]" \
            % get_hex_from_color(app.theme_cls.primary_color)

        IconLeftWidget:
            icon: 'email'


Screen:

    MDCard:
        orientation: "vertical"
        size_hint: .6, None
        height: self.minimum_height
        pos_hint: {"center_x": .5, "center_y": .5}

        BoxLayout:
            id: box
            size_hint_y: None
            height: dp(150)

            FitImage:
                source: "image.png"

        MDExpansionPanel:
            on_open: Animation(height=(box.height + self.content.height) - dp(70), d=.2).start(box)
            on_close: Animation(height=(box.height - self.content.height) + dp(70), d=.2).start(box)
            icon: "avatar.png"
            content: Content()
            title: "HeaTTheatR"
"""


class Content(BoxLayout):
    pass


class Test(MDApp):
    def build(self):
        self.theme_cls.primary_palette = "Teal"
        return Builder.load_string(KV)


Test().run()
```