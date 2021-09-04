![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/textfield_cleartype.gif)

## Example of using MDTextField:

```python
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.app import MDApp

Builder.load_string(
    """
#:import Window kivy.core.window.Window
#:set color_shadow [0, 0, 0, .2980392156862745]


<TextFieldRound@MDTextFieldRound>
    size_hint_x: None
    normal_color: color_shadow
    active_color: color_shadow


<ExampleTextFields@MDBoxLayout>:
    orientation: "vertical"
    spacing: "10dp"

    MDToolbar:
        id: toolbar
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        background_palette: "Primary"
        elevation: 10
        left_action_items: [["menu", lambda x: None]]

    ScrollView:

        MDBoxLayout:
            orientation: "vertical"
            adaptive_height: True
            padding: dp(48)
            spacing: dp(15)

            TextFieldRound:
                hint_text: "Empty field"

            TextFieldRound:
                icon_left: "email"
                hint_text: "Field with left icon"

            TextFieldRound:
                icon_left: "key-variant"
                icon_right: "eye-off"
                hint_text: "Field with left and right icons"

            MDTextField:
                hint_text: "Rectangle mode"
                mode: "rectangle"

            MDTextField:
                hint_text: "With right icon"
                mode: "rectangle"
                fill_color: 0, 0, 0, .4
                icon_right: "arrow-down-drop-circle-outline"
                icon_right_color: app.theme_cls.disabled_hint_text_color

            MDTextField:
                hint_text: "Fill mode"
                mode: "fill"
                fill_color: 0, 0, 0, .4

            MDTextField:
                hint_text: "With right icon"
                mode: "fill"
                fill_color: 0, 0, 0, .4
                icon_right: "arrow-down-drop-circle-outline"

            MDTextField:
                input_filter: "int"
                hint_text: "Numeric field"

            MDTextField:
                hint_text: "No helper text"

            MDTextField:
                hint_text: "With right icon"
                icon_right: "arrow-down-drop-circle-outline"
                icon_right_color: app.theme_cls.disabled_hint_text_color

            MDTextField:
                hint_text: "Helper text on focus"
                helper_text: "This will disappear when you click off"
                helper_text_mode: "on_focus"

            MDTextField:
                hint_text: "line_anim = False"
                line_anim: False                    

            MDTextField:
                hint_text: "Persistent helper text"
                helper_text: "Text is always here"
                helper_text_mode: "persistent"

            Widget:
                size_hint_y: None
                height: "5dp"

            MDTextField:
                hint_text: "Max text length = 10"
                max_text_length: 10

            MDTextField:
                hint_text: "required = True"
                required: True
                helper_text_mode: "on_error"

            MDTextField:
                multiline: True
                hint_text: "Multi-line text"
                helper_text: "Messages are also supported here"
                helper_text_mode: "persistent"

            MDTextField:
                hint_text: "color_mode = \'accent\'"
                color_mode: "accent"

            MDTextField:
                hint_text: "color_mode = \'custom\'"
                color_mode: "custom"
                helper_text_mode: "on_focus"
                helper_text: "Color is defined by \'line_color_focus\' property"
                line_color_focus: self.theme_cls.opposite_bg_normal

            MDTextField:
                hint_text: "disabled = True"
                disabled: True

            MDTextFieldRect:
                size_hint: None, None
                size: Window.width - dp(40), "30dp"
                pos_hint: {"center_y": .5, "center_x": .5}

            MDTextFieldRect:
                hint_text: "line_anim = False"
                line_anim: False
                size_hint: None, None
                size: Window.width - dp(40), "30dp"
                pos_hint: {"center_y": .5, "center_x": .5}
"""
)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.title = "KivyMD Examples - Text Fields"
        self.theme_cls.primary_palette = "Blue"

    def build(self):
        self.root = Factory.ExampleTextFields()


if __name__ == "__main__":
    MainApp().run()
```