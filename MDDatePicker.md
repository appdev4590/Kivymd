![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/blob/master/gallery/data-picker.gif)

## Example of using MDDatePicker:

```python
from kivy.app import App
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.theming import ThemeManager
from kivymd.pickers import MDDatePicker


KV = """
#:import MDCheckbox kivymd.selectioncontrols.MDCheckbox
#:import MDLabel kivymd.label.MDLabel
#:import MDRaisedButton kivymd.button.MDRaisedButton


<Pickers@Screen>
    name: 'pickers'

    BoxLayout:
        orientation: 'vertical'
        pos_hint: {'center_x': .5, 'center_y': .5}
        size_hint_y: None
        height: self.minimum_height

        MDRaisedButton:
            text: "Open date picker"
            size_hint: None, None
            size: 3 * dp(48), dp(48)
            pos_hint: {'center_x': .5, 'center_y': .5}
            opposite_colors: True
            on_release: app.show_example_date_picker()
        MDLabel:
            id: date_picker_label
            theme_text_color: 'Primary'
            size_hint: None, None
            size: dp(48)*3, dp(48)
            pos_hint: {'center_x': .5, 'center_y': .5}
        BoxLayout:
            size: dp(48)*3, dp(48)
            size_hint: (None, None)
            pos_hint: {'center_x': .5, 'center_y': .5}
            MDLabel:
                theme_text_color: 'Primary'
                text: "Start on previous date"
                size_hint: None, None
                size: dp(130), dp(48)
            MDCheckbox:
                id: date_picker_use_previous_date
                size_hint: None, None
                size: dp(48), dp(48)
"""


class TabsApp(App):
    theme_cls = ThemeManager()
    pickers = None
    previous_date = ''

    def build(self):
        Builder.load_string(KV)
        self.pickers = Factory.Pickers()
        return self.pickers

    def show_example_date_picker(self, *args):
        if self.pickers.ids.date_picker_use_previous_date.active:
            pd = self.previous_date
            try:
                MDDatePicker(self.set_previous_date,
                             pd.year, pd.month, pd.day).open()
            except AttributeError:
                MDDatePicker(self.set_previous_date).open()
        else:
            MDDatePicker(self.set_previous_date).open()

    def set_previous_date(self, date_obj):
        self.previous_date = date_obj
        self.pickers.ids.date_picker_label.text = str(date_obj)


TabsApp().run()
```