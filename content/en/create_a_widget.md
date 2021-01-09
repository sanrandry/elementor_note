---
title: creating a widget
description: ""
position: 6
category: Guide
---

create a widget class that extends the \\Elementor\\Widget_Base

overwrite some methode like this exemple

exemple

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {
        // return a widget name that will be used in the code
        public function get_name() {}
        
        // return the widget title that will be displayed as the widget label
    	public function get_title() {}
        
        // set the widget icon
        // you can use any of the eicon or font-awesome icons, simply return the class name as a string
    	public function get_icon() {}
        
        // set the category of the widget
        //return the category name as a string
   	public function get_categories() {}
        
        // define which controls (setting fields) your widget will have
    	protected function _register_controls() {}
        
        // render the code and generate the final HTML on the frontend using PHP
   	 protected function render() {}
        
        // render the editor output to generate the live preview using a Backbone JavaScript template
    	protected function _content_template() {}

}
```

require the class file and add this file to init_widgets method in the plugin-name.php file

```php
public function init_widgets()
    {

        // Include Widget files
        require_once(__DIR__ . '/widgets/Elem-lab-embed.php');

        // Register widget
        \Elementor\Plugin::instance()->widgets_manager->register_widget_type(new \Elem_lab_embed());
    }
```

exemple

simple embed widget

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    public function get_name() {
        return 'oembed';
    }

    public function get_title() {
        return __( 'oEmbed', 'plugin-name' );
    }

    public function get_icon() {
        return 'fa fa-code';
    }

    public function get_categories() {
        return [ 'general' ];
    }

}
```

#### Widget Controls

add the widget controls using the \_register\_controls() method.

in this case, we only have one control which is a simple URL input:

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

        $this->add_control(
            'url',
            [
                'label' => __( 'URL to embed', 'plugin-name' ),
                'type' => \Elementor\Controls_Manager::TEXT,
                'input_type' => 'url',
                'placeholder' => __( 'https://your-link.com', 'plugin-name' ),
            ]
        );

        $this->end_controls_section();

    }

}
```

## Frontend RenderingFrontend Rendering

in this exemple we implement our render() method which takes the URL the user inputs in the above URL control and get the oEmbed content to display using the native wp\_oembed\_get() function

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

    protected function render() {

        $settings = $this->get_settings_for_display();

        $html = wp_oembed_get( $settings['url'] );

        echo '<div class="oembed-elementor-widget">';

        echo ( $html ) ? $html : $settings['url'];

        echo '</div>';

    }

}
```

this is a final code exemple form the official elementor documentation

```php
<?php
/**
 * Elementor oEmbed Widget.
 *
 * Elementor widget that inserts an embbedable content into the page, from any given URL.
 *
 * @since 1.0.0
 */
class Elementor_oEmbed_Widget extends \Elementor\Widget_Base {

    /**
     * Get widget name.
     *
     * Retrieve oEmbed widget name.
     *
     * @since 1.0.0
     * @access public
     *
     * @return string Widget name.
     */
    public function get_name() {
        return 'oembed';
    }

    /**
     * Get widget title.
     *
     * Retrieve oEmbed widget title.
     *
     * @since 1.0.0
     * @access public
     *
     * @return string Widget title.
     */
    public function get_title() {
        return __( 'oEmbed', 'plugin-name' );
    }

    /**
     * Get widget icon.
     *
     * Retrieve oEmbed widget icon.
     *
     * @since 1.0.0
     * @access public
     *
     * @return string Widget icon.
     */
    public function get_icon() {
        return 'fa fa-code';
    }

    /**
     * Get widget categories.
     *
     * Retrieve the list of categories the oEmbed widget belongs to.
     *
     * @since 1.0.0
     * @access public
     *
     * @return array Widget categories.
     */
    public function get_categories() {
        return [ 'general' ];
    }

    /**
     * Register oEmbed widget controls.
     *
     * Adds different input fields to allow the user to change and customize the widget settings.
     *
     * @since 1.0.0
     * @access protected
     */
    protected function _register_controls() {

        $this->start_controls_section(
            'content_section',
            [
                'label' => __( 'Content', 'plugin-name' ),
                'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
            ]
        );

        $this->add_control(
            'url',
            [
                'label' => __( 'URL to embed', 'plugin-name' ),
                'type' => \Elementor\Controls_Manager::TEXT,
                'input_type' => 'url',
                'placeholder' => __( 'https://your-link.com', 'plugin-name' ),
            ]
        );

        $this->end_controls_section();

    }

    /**
     * Render oEmbed widget output on the frontend.
     *
     * Written in PHP and used to generate the final HTML.
     *
     * @since 1.0.0
     * @access protected
     */
    protected function render() {

        $settings = $this->get_settings_for_display();

        $html = wp_oembed_get( $settings['url'] );

        echo '<div class="oembed-elementor-widget">';

        echo ( $html ) ? $html : $settings['url'];

        echo '</div>';

    }

}
```