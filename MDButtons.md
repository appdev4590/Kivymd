![useranimationcard.gif](https://raw.githubusercontent.com/HeaTTheatR/KivyMD/master/gallery/buttons.gif)

## Example of using a class MDButtons:

```python
from kivy.app import App
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.theming import ThemeManager

Builder.load_string("""
#:import Toolbar kivymd.toolbar.Toolbar
#:import MDIconButton kivymd.button.MDIconButton
#:import MDFloatingActionButton kivymd.button.MDFloatingActionButton
#:import MDFlatButton kivymd.button.MDFlatButton
#:import MDRaisedButton kivymd.button.MDRaisedButton
#:import MDRectangleFlatButton kivymd.button.MDRectangleFlatButton
#:import MDRoundFlatButton kivymd.button.MDRoundFlatButton
#:import MDRoundFlatIconButton kivymd.button.MDRoundFlatIconButton
#:import MDFillRoundFlatButton kivymd.button.MDFillRoundFlatButton


<ExampleButtons@BoxLayout>:
    orientation: 'vertical'

    Toolbar:
        id: toolbar
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        background_palette: 'Primary'
        elevation: 10
        left_action_items: [['dots-vertical', lambda x: None]]

    Screen:
        BoxLayout:
            size_hint_y: None
            height: '56'
            spacing: '10dp'
            pos_hint: {'center_y': .9}

            Widget:

            MDIconButton:
                icon: 'sd'

            MDFloatingActionButton:
                icon: 'plus'
                opposite_colors: True
                elevation_normal: 8

            MDFloatingActionButton:
                icon: 'check'
                opposite_colors: True
                elevation_normal: 8
                md_bg_color: app.theme_cls.primary_color

            MDIconButton:
                icon: 'sd'
                theme_text_color: 'Custom'
                text_color: app.theme_cls.primary_color

            Widget:

        MDFlatButton:
            text: 'MDFlatButton'
            pos_hint: {'center_x': 0.5, 'center_y': .75}

        MDRaisedButton:
            text: "MDRaisedButton"
            elevation_normal: 2
            opposite_colors: True
            pos_hint: {'center_x': 0.5, 'center_y': .65}

        MDRectangleFlatButton:
            text: "MDRectangleFlatButton"
            pos_hint: {'center_x': 0.5, 'center_y': .55}

        MDRectangleFlatIconButton:
            text: "I love Python"
            icon: "language-python"
            pos_hint: {'center_x': 0.5, 'center_y': .45}

        MDRoundFlatButton:
            text: "I love Python"
            icon: "language-python"
            pos_hint: {'center_x': 0.5, 'center_y': .35}

        MDRoundFlatIconButton:
            text: "I love Python"
            icon: "language-python"
            pos_hint: {'center_x': 0.5, 'center_y': .25}

        MDFillRoundFlatButton:
            text: "I love Python"
            pos_hint: {'center_x': 0.5, 'center_y': .15}
""")


class Example(App):
    theme_cls = ThemeManager()
    theme_cls.primary_palette = 'Blue'
    title = "Example Buttons"
    main_widget = None

    def build(self):
        return Factory.ExampleButtons()


Example().run()
```