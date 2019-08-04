![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/blob/master/gallery/bottom-navigation.gif)

## Example of using MDBottomNavigation:

```python
from kivy.app import App
from kivymd.theming import ThemeManager


class Test(App):
    theme_cls = ThemeManager()

    def build(self):
        return Builder.load_string(
            '''
#:import MDToolbar kivymd.toolbar.MDToolbar
#:import MDBottomNavigation kivymd.bottomnavigation.MDBottomNavigation
#:import MDBottomNavigationItem kivymd.bottomnavigation.MDBottomNavigationItem


BoxLayout:
    orientation:'vertical'

    MDToolbar:
        id: toolbar
        title: 'Test MDBottomNavigation'
        md_bg_color: app.theme_cls.primary_color
        left_action_items: [['menu', lambda x: '']]

    MDBottomNavigation:

        MDBottomNavigationItem:
            name: 'files1'
            text: 'Python'
            icon: 'language-python'

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: 'I love Python'
                halign: 'center'

        MDBottomNavigationItem:
            name: 'files2'
            text: 'C++'
            icon: 'language-cpp'

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: 'I programming of C++'
                halign: 'center'

        MDBottomNavigationItem:
            name: 'files3'
            text: 'JS'
            icon: 'language-javascript'

            MDLabel:
                font_style: 'Body1'
                theme_text_color: 'Primary'
                text: 'Oh god JS again'
                halign: 'center'
'''
        )

Test().run()
"""
```

Or MDBottomNavigation with custom of panel color:

![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/blob/master/gallery/bottom-navigation-with-custom-color-panel.gif)

```
    MDBottomNavigation:
        panel_color:
            [0.2980392156862745, 0.2823529411764706, 0.32941176470588235, 1]
```