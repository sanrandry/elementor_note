---
title: Register Widget Controls
description: ""
position: 2
category: Guide
---

use the \_register\_controls() method

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    protected function _register_controls() {

        $this->start_controls_section();

        $this->add_control();

        $this->end_controls_section();

    }

}
```

## Add Control Section

Sections are created using two methods, the start\_controls\_section() method which creates a new section and the end\_controls\_section() method to close the section.

exemple: Sections in Multiple Tabs

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    protected function _register_controls() {

        $this->start_controls_section(
            'content_section',
            [
                'label' => __( 'Content', 'plugin-name' ),
                'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
            ]
        );

        $this->add_control();

        $this->add_control();

        $this->add_control();

        $this->end_controls_section();

        $this->start_controls_section(
            'info_section',
            [
                'label' => __( 'Info', 'plugin-name' ),
                'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
            ]
        );

        $this->add_control();

        $this->add_control();

        $this->add_control();

        $this->end_controls_section();

        $this->start_controls_section(
            'style_section',
            [
                'label' => __( 'Style', 'plugin-name' ),
                'tab' => \Elementor\Controls_Manager::TAB_STYLE,
            ]
        );

        $this->add_control();

        $this->add_control();

        $this->add_control();

        $this->end_controls_section();

    }

}
```

## Adding New Control

New controls are added using the add_control() method

exemple

simple text control

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    protected function _register_controls() {

        $this->start_controls_section(
            'content_section',
            [
                'label' => __( 'Content', 'plugin-name' ),
            ]
        );

        $this->add_control(
            'title',
            [
                'label' => __( 'Title', 'plugin-name' ),
                'type' => \Elementor\Controls_Manager::TEXT,
                'placeholder' => __( 'Enter your title', 'plugin-name' ),
            ]
        );

        $this->end_controls_section();

    }

}
```

for more control type: visite this elementor official documentation: [https://developers.elementor.com/add-controls-to-widgets/](https://developers.elementor.com/add-controls-to-widgets/)

## Add Group Controls to Widgets

comming soon...

## Add Responsive Controls to Widgets

comming soon...

## Add Control Tabs to Widgets

comming soon...

## Add Control Popovers to Widgets

 \- create a new popover-toggle control

\- use start\_popover() method and the end\_popover() method.

exemple

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    protected function _register_controls() {

        $this->start_controls_section(
            'style_section',
            [
                'label' => __( 'Style Section', 'plugin-name' ),
                'tab' => \Elementor\Controls_Manager::TAB_STYLE,
            ]
        );

        $this->add_control(
            'popover-toggle',
            [
                'label' => __( 'Box', 'plugin-name' ),
                'type' => \Elementor\Controls_Manager::POPOVER_TOGGLE,
                'label_off' => __( 'Default', 'your-plugin' ),
                'label_on' => __( 'Custom', 'your-plugin' ),
                'return_value' => 'yes',
            ]
        );

        $this->start_popover();

        $this->add_control();

        $this->add_control();

        $this->add_control();

        $this->end_popover();

        $this->end_controls_section();

    }

}
```
