![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/blob/master/gallery/bottom-navigation.gif)

## Example of using MDBottomNavigation:

```python
from kivy.app import App
from kivy.lang import Builder

from kivymd.theming import ThemeManager


KV = """
#:import MDBottomNavigation kivymd.tabs.MDBottomNavigation


BoxLayout:
    orientation:'vertical'

    MDBottomNavigation:

        MDBottomNavigationItem:
            name: 'movies'
            text: 'Movies'
            icon: "movie"

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: "Movie"
                halign: 'center'

        MDBottomNavigationItem:
            name: 'files'
            text: "Files"
            icon: "file"

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: "Files"
                halign: 'center'

        MDBottomNavigationItem:
            name: 'android'
            text: "Android"
            icon: "android"

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: "Android"
                halign: 'center'

        MDBottomNavigationItem:
            name: 'python-language'
            text: "Files"
            icon: 'language-python'

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: "Python"
                halign: 'center'
"""


class Example(App):
    theme_cls = ThemeManager()

    def build(self):
        from kivy.core.window import Window
        Window.size = (540, 720)
        return Builder.load_string(KV)


Example().run()
```