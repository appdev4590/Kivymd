![useranimationcard.gif](https://raw.githubusercontent.com/HeaTTheatR/KivyMD/master/gallery/card.gif)

## Example of using a class MDCardPost:

```python
from kivy.app import App
from kivy.lang import Builder
from kivy.factory import Factory

from kivymd.card import MDCardPost
from kivymd.theming import ThemeManager
from kivymd.toast import toast


Builder.load_string("""
#:import Toolbar kivymd.toolbar.Toolbar


<ExampleCardPost@BoxLayout>:
    orientation: 'vertical'
    spacing: dp(5)

    Toolbar:
        id: toolbar
        title: app.title
        left_action_items: [['menu', lambda x: None]]
        elevation: 10
        md_bg_color: app.theme_cls.primary_color


    ScrollView:
        id: scroll
        size_hint: 1, 1
        do_scroll_x: False

        GridLayout:
            id: grid_card
            cols: 1
            spacing: dp(5)
            padding: dp(5)
            size_hint_y: None
            height: self.minimum_height
""")


class Example(App):
    theme_cls = ThemeManager()
    theme_cls.primary_palette = 'Teal'
    title = "Card Post"

    def build(self):
        self.screen = Factory.ExampleCardPost()
        return self.screen

    def on_start(self):
        def callback_for_menu_items(text_item):
            toast(text_item)

        def callback(instance, star):
            if star:
                toast('Set like in %d stars' % star)

        instance_grid_card = self.screen.ids.grid_card
        path_to_avatar = 'data/logo/kivy-icon-512.png'
        menu_items = [
            {'viewclass': 'MDMenuItem',
             'text': 'Example item %d' % i,
             'callback': callback_for_menu_items}
            for i in range(2)
        ]

        instance_grid_card.add_widget(
            MDCardPost(
                path_to_avatar=path_to_avatar,
                text_post='Card with text'))
        instance_grid_card.add_widget(
            MDCardPost(
                right_menu=menu_items,
                path_to_avatar=path_to_avatar,
                text_post='Card with a button to open the menu MDDropDown.'))
        instance_grid_card.add_widget(
            MDCardPost(
                likes_stars=True, callback=callback,
                path_to_avatar=path_to_avatar,
                text_post='Card with asterisks for voting.'))


Example().run()
```

## Add card behavior swipe

![useranimationcard.gif](https://raw.githubusercontent.com/HeaTTheatR/KivyMD/master/gallery/cardswipe.gif)

(Add option **swipe=True** to class **MDCardPost**):

```python
    def on_start(self):
        def callback(instance, star):
            if star:
                toast('Set like in %d stars' % star)
            else:
                self.screen.ids.grid_card.remove_widget(instance)
                toast('Delete post %s' % str(instance))

        instance_grid_card.add_widget(
            MDCardPost(
                path_to_avatar=path_to_avatar, swipe=True,
                text_post='Card with text', callback=callback))
        instance_grid_card.add_widget(
            MDCardPost(
                right_menu=menu_items, swipe=True,
                path_to_avatar=path_to_avatar, callback=callback,
                text_post='Card with a button to open the menu MDDropDown.'))
        instance_grid_card.add_widget(
            MDCardPost(
                likes_stars=True, callback=callback,
                path_to_avatar=path_to_avatar, swipe=True,
                text_post='Card with asterisks for voting.'))
```