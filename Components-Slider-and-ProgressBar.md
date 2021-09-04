![sliders.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/sliders.gif)

## Example of using MDSlider and MDProgressBar:

```python
from kivy.lang import Builder

from kivymd.app import MDApp

root_kv = """
MDScreen:
    name: "progress bar"

    MDBoxLayout:
        orientation:"vertical"
        padding: "8dp"

        MDLabel:
            text: "Slider with [b]hint = True[/b]"
            markup: True
            halign: "center"

        MDSlider:
            id: progress_slider
            min: 0
            max: 100
            value: 40

        MDLabel:
            text: "Slider with [b]hint = False[/b]"
            markup: True
            halign: "center"

        MDSlider:
            id: progress_slider
            min: 0
            max: 100
            value: 40
            hint: False

        MDLabel:
            text: "Examples [b]MDProgressBar[/b]"
            markup: True
            halign: "center"

        MDProgressBar:
            value: progress_slider.value

        MDProgressBar:
            reversed: True
            value: progress_slider.value

        BoxLayout:
            MDProgressBar:
                orientation: "vertical"
                reversed: True
                value: progress_slider.value

            MDProgressBar:
                orientation: "vertical"
                value: progress_slider.value
"""


class MainApp(MDApp):
    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Slider and Progress Bar"
        super().__init__(**kwargs)

    def build(self):
        self.root = Builder.load_string(root_kv)


if __name__ == "__main__":
    MainApp().run()
```