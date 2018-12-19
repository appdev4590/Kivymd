![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/blob/master/gallery/updatespinner.gif)

## Example of using a class MDUpdateSpinner:

```python
from kivy.app import App
from kivy.lang import Builder
from kivy.factory import Factory
from kivy.clock import Clock

from kivymd.theming import ThemeManager


Builder.load_string("""
#:import Toolbar kivymd.toolbar.Toolbar
#:import MDLabel kivymd.label.MDLabel
#:import MDUpdateSpinner kivymd.updatespinner.MDUpdateSpinner

<ExampleUpdateSpinner@BoxLayout>:
    orientation: 'vertical'

    Toolbar:
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        elevation: 10
        left_action_items: [['menu', lambda x: None]]

    FloatLayout:

        MDLabel:
            id: upd_lbl
            font_style: 'Display2'
            theme_text_color: 'Primary'
            halign: 'center'
            pos_hint: {'center_x': .5, 'center_y': .6}
            size_hint_y: None
            height: self.texture_size[1] + dp(4)
            text: "Pull to string update"
                    
        MDUpdateSpinner:
            event_update: lambda x: app.update_screen(self)
""")


class Example(App):
    theme_cls = ThemeManager()
    theme_cls.primary_palette = 'Teal'
    title = "Update Spinner"
    tick = 0
    screen_update_spinner = None

    def update_screen(self, instance):
        def update_screen(interval):
            self.tick += 1
            if self.tick > 2:
                instance.update = True
                self.tick = 0
                self.screen_update_spinner.ids.upd_lbl.text = "New string"
                Clock.unschedule(update_screen)
        Clock.schedule_interval(update_screen, 1)

    def build(self):
        self.screen_update_spinner = Factory.ExampleUpdateSpinner()
        return self.screen_update_spinner


Example().run()
```