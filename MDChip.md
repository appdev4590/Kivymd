![chips.gif](https://raw.githubusercontent.com/HeaTTheatR/KivyMD/master/gallery/chips.gif)

## Example of using MDChip:

```python
from kivy.app import App
from kivy.lang import Builder

from kivymd.theming import ThemeManager
from kivymd.toast import toast

kv = """
#:import Toolbar kivymd.toolbar.Toolbar
#:import Window kivy.core.window.Window
#:import MDChip kivymd.chips.MDChip


BoxLayout:
    orientation: 'vertical'

    Toolbar:
        title: 'Example Chips'
        md_bg_color: app.theme_cls.primary_color
        left_action_items: [['menu', lambda x: x]]
        background_palette: 'Primary'

    BoxLayout:
        orientation: 'vertical'
        spacing: dp(10)

        Image:
            source: 'demos/kitchen_sink/assets/tangerines-1111529_1280.jpg'
            size_hint: 1, None
            height: dp(Window.height * 35 // 100)
            allow_stretch: True
            keep_ratio: False

        StackLayout:
            padding: dp(5)
            spacing: dp(5)

            MDChip:
                label: 'Coffee'
                color: .4470588235294118, .19607843137254902, 0, 1
                icon: 'coffee'
                callback: app.callback

            MDChip:
                label: 'Duck'
                color: .9215686274509803, 0, 0, 1
                icon: 'duck'
                callback: app.callback

            MDChip:
                label: 'Earth'
                color: .21176470588235294, .09803921568627451, 1, 1
                icon: 'earth'
                callback: app.callback

            MDChip:
                label: 'Face'
                color: .20392156865098, .48235294117606, .43529411764705883, 1
                icon: 'face'
                callback: app.callback

            MDChip:
                label: 'Facebook'
                color: .5607843137254902, .48235294164706, .435294117705883, 1
                icon: 'facebook'
                callback: app.callback

            MDChip:
                label: 'Without icon'
                icon: ''
                callback: app.callback

            MDChip:
                label: 'Check'
                icon: ''
                check: True
                callback: app.callback

        Widget:
"""


class MyApp(App):
    theme_cls = ThemeManager()
    theme_cls.primary_palette = 'Red'

    def callback(self, name_chip):
        toast(name_chip)

    def build(self):
        return Builder.load_string(kv)


MyApp().run()
```