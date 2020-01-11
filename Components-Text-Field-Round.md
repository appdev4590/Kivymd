![textfieldrect.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/md-text-field-round.gif)

## Example of using MDTextFieldRound:

```python
from kivymd.app import MDApp
from kivy.lang import Builder

KV = """
#:import Window kivy.core.window.Window
#:set color_shadow [0, 0, 0, .2980392156862745]


<KitchenSinkTextFieldRound@MDTextFieldRound>
    size_hint_x: None
    normal_color: color_shadow
    active_color: color_shadow


Screen:

    BoxLayout:
        orientation: "vertical"
        spacing: "10dp"

        MDToolbar:
            md_bg_color: app.theme_cls.primary_color
            title: "MDTextFieldsRound"
            elevation: 10
            left_action_items: [["arrow-left", lambda x: x]]

        ScrollView:

            BoxLayout:
                orientation: 'vertical'
                size_hint_y: None
                height: self.minimum_height
                padding: dp(48)
                spacing: dp(15)

                KitchenSinkTextFieldRound:
                    hint_text: 'Empty field'

                KitchenSinkTextFieldRound:
                    icon_left: 'email'
                    hint_text: 'Field with left icon'

                KitchenSinkTextFieldRound:
                    icon_left: 'key-variant'
                    icon_right: 'eye-off'
                    hint_text: 'Field with left and right icons'

                KitchenSinkTextFieldRound:
                    hint_text: 'Field with custom `normal_color`'
                    normal_color: 1, 1, 0, .5
"""


class TestMDTextFieldsRound(MDApp):
    def build(self):
        return Builder.load_string(KV)


TestMDTextFieldsRound().run()
```