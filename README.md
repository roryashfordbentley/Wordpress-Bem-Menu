# Wordpress BEM Menu

Say goodbye to badly named menus in Wordpress and say hello to Wordpress BEM Menus!

To use simply drop the contents of wp_bem_menu.php into your functions.php file.


## Usage

First you need to register a nav menu in your themes `functions.php` file.

`register_nav_menu('my_menu', 'primary site menu');`

You also need to create a menu in wp-admin and make sure it is assigned a theme location that matches your registered nav menu above.

Then insert the following function into your theme. The first argument is the theme location (as defined in wp-admin) and the second argument is the class prefix you would like to use for this particular menu. The class prefix will be applied to the menu `<ul>`, every child `<li>` and `<a>` as the 'block'. The third optional argument accepts either an `array()` or a `string`.

```php
<?php bem_menu('menu_location', 'my-menu', 'my-menu--my-modifier'); ?>
```
If you want to add multiple modifiers to the `<ul>` use an array e.g:
```php
<?php bem_menu('menu_location', 'my-menu', array('my-menu--my-modifier','my-menu--my-other-modifier')) ?>
```
Please note that these modifier classes are not inherited by descendants. this is by design to avoid bloated navigation markup. You can still target children of a specific modifier like so: `.my-menu--my-modifier .my-menu__item{}`

## html output
```html
<ul class="my-menu my-menu--my-modifier">
    <li class="my-menu__item  my-menu__item--active  my-menu__item--78"><a class="my-menu__link" href="#">Home</a></li>
    <li class="my-menu__item  my-menu__item--79"><a class="my-menu__link" href="#">Page 2</a></li>
    <li class="my-menu__item  my-menu__item--84"><a class="my-menu__link" href="#">Page 3</a></li>
</ul>
```

## Css classes

The syntax is very simple, all menu items are logically grouped by depth to avoid some of the nesting issues of the standard output.

```css
/* Top level items */
.my-menu__item{}

/* Specific item (where x = post_id) */
.my-menu__item--x{}

/* Parent item */
.my-menu__item--parent{}

/* Active page item */
.my-menu__item--active{}

/* Parent of the current active page */
.my-menu__item--parent--active{}

/* Ancestor of the current active page */
.my-menu__item--ancestor--active{}

/* Link */
.my-menu__link{}

/* sub menu class */
.my-menu__sub-menu{}

/* sub menu item */
.my-menu__sub-menu__item{}

/* sub menu link */
.my-menu__sub-menu__link{}

/* Specific sub menu (where x is the menu depth) */
.my-menu__sub-menu--x{}

```

## Modification

BEM syntax is very subjective and different developers use different conventions. If you wish to change or adapt the syntax to go with your own implemntation all the menu suffixes are contained within the `$this->item_css_classes` array:

```php
$this->item_css_classes = array(
    'item'                      => '__item',
    'parent_item'               => '__item--parent',
    'active_item'               => '__item--active',
    'parent_of_active_item'     => '__item--parent--active',
    'ancestor_of_active_item'   => '__item--ancestor--active',
    'link'                      => '__link',
    'sub_menu'                  => '__sub-menu',
    'sub_menu_item'             => '__sub-menu__item'
);

```

## Custom Css classes set in wp-admin>menus

If you add a custom class to a menu item in wp-admin Wordpress-Bem-Menu now adds the class to the item converted to a BEM modifier. If for example you add a class of `my-class` to a menu item the output would be `<li class="main-menu  main-menu__item  main-menu__item--my-class"></li>`
