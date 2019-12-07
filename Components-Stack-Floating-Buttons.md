![useranimationcard.gif](https://github.com/HeaTTheatR/KivyMD-data/raw/master/gallery/stackfloatingbuttons.gif)

## Example of using MDStackFloatingButtons:

```python
from kivy.lang import Builder
from kivy.factory import Factory
from kivy.properties import BooleanProperty, DictProperty
from kivymd.app import MDApp
from kivymd.toast import toast
from kivymd.uix.stackfloatingbutton import MDStackFloatingButtons


Builder.load_string(
    """
<ExampleFloatingButtons@BoxLayout>:
    orientation: "vertical"

    MDToolbar:
        title: app.title
        md_bg_color: app.theme_cls.primary_color
        elevation: 10
        left_action_items: [["menu", lambda x: None]]

"""
)


class MainApp(MDApp):
    create_stack_floating_buttons = BooleanProperty(False)
    floating_data = DictProperty(
        {"Python": "language-python", "Php": "language-php", "C++": "language-cpp"}
    )

    def __init__(self, **kwargs):
        self.title = "KivyMD Examples - Stack Floating Buttons"
        self.theme_cls.primary_palette = "Teal"
        super().__init__(**kwargs)

    def build(self):
        screen = Factory.ExampleFloatingButtons()
        # Use this condition otherwise the stack will be created each time.
        if not self.create_stack_floating_buttons:
            screen.add_widget(
                MDStackFloatingButtons(
                    icon="lead-pencil",
                    floating_data=self.floating_data,
                    callback=self.set_my_language,
                )
            )
            self.create_stack_floating_buttons = True
        self.root = screen

    def set_my_language(self, instance_button):
        toast(instance_button.icon)


if __name__ == "__main__":
    MainApp().run()
```