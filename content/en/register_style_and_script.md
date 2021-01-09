---
title: Register style and script
description: ""
position: 4
category: Guide
---

## register a style

add the elementor/frontend/after_enqueue_styleselementor/frontend/after_enqueue_styles to the init fuction

create a fucntion to register all the style

exemple

```php
public function init() {

    // Register Widget Styles
    add_action( 'elementor/frontend/after_enqueue_styles', [ $this, 'widget_styles' ] );

}

public function widget_styles() {

    wp_register_style( 'widget-1', plugins_url( 'css/widget-1.css', __FILE__ ) );
    wp_register_style( 'widget-2', plugins_url( 'css/widget-2.css', __FILE__ ) );

}
```

## register a script

add the elementor/frontend/after_register_scriptselementor/frontend/after_register_scripts action to the init method and create a fuction to register all the script

exemple

```php
public function init() {

    // Register Widget Scripts
    add_action( 'elementor/frontend/after_register_scripts', [ $this, 'widget_scripts' ] );

}


public function widget_scripts() {

    wp_register_script( 'some-library', plugins_url( 'js/libs/some-library.js', __FILE__ ) );
    wp_register_script( 'widget-1', plugins_url( 'js/widget-1.js', __FILE__ ) );
    wp_register_script( 'widget-2', plugins_url( 'js/widget-2.js', __FILE__ ), [ 'jquery', 'some-library' ] );

}
```

**NB: the style and script is not enquee yet, it was been registered** **only**
