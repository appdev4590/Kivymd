![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/buttons.gif)

## Example of using Material Buttons:

```python
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.app import MDApp

Builder.load_string(
    """
#:import get_color_from_hex kivy.utils.get_color_from_hex


<ExampleButtons@MDBoxLayout>:
    orientation: "vertical"
    spacing: "10dp"

    MDToolbar:
        id: toolbar
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        background_palette: "Primary"
        elevation: 10
        left_action_items: [["dots-vertical", lambda x: None]]

    ScrollView:
        pos_hint: {"center_x": .5}
        bar_width: 0

        MDBoxLayout:
            adaptive_height: True
            orientation: "vertical"

            MDBoxLayout:
                id: box
                padding: "10dp"
                adaptive_size: True
                spacing: "10dp"
                orientation: "vertical"
                pos_hint: {"center_x": .5}

                MDBoxLayout:
                    adaptive_width: True
                    size_hint_y: None
                    height: "56dp"
                    spacing: "10dp"
                    pos_hint: {"center_x": .5}

                    MDIconButton:
                        icon: "sd"

                    MDFloatingActionButton:
                        icon: "plus"
                        opposite_colors: True
                        elevation: 8
                        md_bg_color: 1, 0, 0, 1

                    MDFloatingActionButton:
                        icon: "check"
                        opposite_colors: True
                        elevation: 8
                        md_bg_color: app.theme_cls.primary_color

                    MDIconButton:
                        icon: "sd"
                        theme_text_color: "Custom"
                        text_color: app.theme_cls.primary_color

                MDFlatButton:
                    text: "MDFlatButton"
                    pos_hint: {"center_x": .5}

                MDRaisedButton:
                    text: "MDRaisedButton"
                    elevation: 8
                    opposite_colors: True
                    pos_hint: {"center_x": .5}

                MDRectangleFlatButton:
                    text: "MDRectangleFlatButton"
                    pos_hint: {"center_x": .5}

                MDRectangleFlatIconButton:
                    text: "MDRectangleFlatIconButton"
                    icon: "language-python"
                    pos_hint: {"center_x": .5}

                MDRoundFlatButton:
                    text: "MDRoundFlatButton"
                    pos_hint: {"center_x": .5}

                MDRoundFlatIconButton:
                    text: "MDRoundFlatIconButton"
                    icon: "language-python"
                    pos_hint: {"center_x": .5}

                MDFillRoundFlatButton:
                    text: "MDFillRoundFlatButton"
                    pos_hint: {"center_x": .5}

                MDFillRoundFlatIconButton:
                    text: "MDFillRoundFlatIconButton"
                    icon: "language-python"
                    pos_hint: {"center_x": .5}

                MDTextButton:
                    text: "MDTextButton"
                    pos_hint: {"center_x": .5}

                MDBoxLayout:
                    orientation: "vertical"
                    spacing: "10dp"
                    adaptive_size: True
                    pos_hint: {"center_x": .5}

                    MDSeparator:

                    Label:
                        text: "Disabled buttons"
                        color: app.theme_cls.text_color
                        font_size: sp(20)
                        size_hint: None, None
                        size: self.texture_size

                    MDSeparator:

                ########################################
                #            DISABLED BUTTONS
                ########################################

                MDBoxLayout:
                    adaptive_width: True
                    size_hint_y: None
                    height: "56dp"
                    spacing: "10dp"
                    pos_hint: {"center_x": .5}

                    MDIconButton:
                        icon: "sd"
                        disabled: True

                    MDFloatingActionButton:
                        icon: "plus"
                        opposite_colors: True
                        disabled: True

                    MDFloatingActionButton:
                        icon: "check"
                        opposite_colors: True
                        disabled: True

                    MDIconButton:
                        icon: "sd"
                        theme_text_color: "Custom"
                        disabled: True

                MDFlatButton:
                    text: "MDFlatButton"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDRaisedButton:
                    text: "MDRaisedButton"
                    disabled: True
                    opposite_colors: True
                    pos_hint: {"center_x": .5}

                MDRectangleFlatButton:
                    text: "MDRectangleFlatButton"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDRectangleFlatIconButton:
                    text: "MDRectangleFlatIconButton"
                    icon: "language-python"
                    disabled: True
                    pos_hint: {"center_x": .5}

                MDRoundFlatButton:
                    text: "MDRoundFlatButton"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDRoundFlatIconButton:
                    text: "MDRoundFlatIconButton"
                    icon: "language-python"
                    disabled: True
                    pos_hint: {"center_x": .5}

                MDFillRoundFlatButton:
                    text: "MDFillRoundFlatButton"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDFillRoundFlatIconButton:
                    text: "MDFillRoundFlatIconButton"
                    icon: "language-python"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDTextButton:
                    text: "MDTextButton"
                    pos_hint: {"center_x": .5}
                    disabled: True

                MDBoxLayout:
                    orientation: "vertical"
                    spacing: "10dp"
                    adaptive_size: True
                    pos_hint: {"center_x": .5}

                    MDSeparator:

                    Label:
                        text: "Button customization"
                        color: app.theme_cls.text_color
                        font_size: "20sp"
                        size_hint: None, None
                        size: self.texture_size
                        pos_hint: {"center_x": .5}

                    MDSeparator:

                    ########################################
                    #         CUSTOMIZATION BUTTONS
                    ########################################

                    MDRaisedButton:
                        text: "MDRaisedButton"
                        elevation: 8
                        theme_text_color: "Custom"
                        text_color: get_color_from_hex("#001975")
                        md_bg_color: get_color_from_hex("#D40078")
                        pos_hint: {"center_x": .5}

                    MDRectangleFlatButton:
                        text: "MDRectangleFlatButton"
                        pos_hint: {"center_x": .5}
                        theme_text_color: "Custom"
                        text_color: get_color_from_hex("#C37C4C")

                    MDRoundFlatButton:
                        text: "MDRoundFlatButton"
                        pos_hint: {"center_x": .5}
                        theme_text_color: "Custom"
                        text_color: get_color_from_hex("#A23651")
                        line_color: get_color_from_hex("#366EA1")
                        line_width: 2

                    MDFillRoundFlatIconButton:
                        text: "MDFillRoundFlatIconButton"
                        icon: "language-python"
                        pos_hint: {"center_x": .5}
                        theme_text_color: "Custom"
                        text_color: 1, 1, 0, 1
                        icon_color: 0, 1, 0, 1
                        md_bg_color: get_color_from_hex("#552A7D")

                MDBoxLayout:
                    orientation: "vertical"
                    spacing: "10dp"
                    adaptive_size: True
                    pos_hint: {"center_x": .5}

                    MDSeparator:

                    Label:
                        text: "MDIconButton customization"
                        color: app.theme_cls.text_color
                        font_size: "20sp"
                        size_hint: None, None
                        size: self.texture_size
                        pos_hint: {"center_x": .5}

                    MDSeparator:

                    MDBoxLayout:
                        spacing: "10dp"
                        adaptive_size: True
                        pos_hint: {"center_x": .5, "center_y": .5}

                        MDIconButton:
                            icon: "language-python"
                            user_font_size: "15sp"

                        MDIconButton:
                            icon: "language-python"
                            user_font_size: "20sp"

                        MDIconButton:
                            icon: "language-python"
                            user_font_size: "24sp"

                        MDIconButton:
                            icon: "language-python"
                            user_font_size: "36sp"

                        MDIconButton:
                            icon: "language-python"
                            user_font_size: "48sp"
"""
)


class MainApp(MDApp):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.title = "KivyMD Examples - Buttons"
        self.theme_cls.primary_palette = "Blue"

    def build(self):
        self.root = Factory.ExampleButtons()


if __name__ == "__main__":
    MainApp().run()
```