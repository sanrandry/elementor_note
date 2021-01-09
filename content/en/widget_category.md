---
title: Widget category
description: ""
position: 5
category: Guide
---

## Using widget category

create a widget class and extends the \\Elementor\\Widget_Base class

overwrite the get_categories

exemple

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    public function get_categories() {
        return [ 'basic' ];
    }

}
```

## Create a new category

add the elementor/elements/categories_registered to the init function

and add a function with this code

exemple

```php
public function init() {
add_action( 'elementor/elements/categories_registered', 'add_elementor_widget_categories' );
}

function add_elementor_widget_categories( $elements_manager ) {

    $elements_manager->add_category(
        'first-category',
        [
            'title' => __( 'First Category', 'plugin-name' ),
            'icon' => 'fa fa-plug',
        ]
    );
    $elements_manager->add_category(
        'second-category',
        [
            'title' => __( 'Second Category', 'plugin-name' ),
            'icon' => 'fa fa-plug',
        ]
    );

}
```
