== Device specific overlay values ==

How to configure overlay values to enable device specific features
This values must be placed in the overlay folder of the device tree

e.g.
https://github.com/omnirom/android_device_oppo_find5/tree/android-4.4/overlay

If you are wishing to maintain AOSP compliance in your tree or multiple products, consider multiple overlay directories

For example:
''device.mk''
    DEVICE_PACKAGE_OVERLAYS := $(LOCAL_PATH)/overlay

''omni_device.mk''
    DEVICE_PACKAGE_OVERLAYS += $(LOCAL_PATH)/omni_overlay


== LEDS ==

=== Enable ===

If the device has a LED

==== Notifications ====

Enable notification LED support

''frameworks/base - config.xml''

    <bool name="config_intrusiveNotificationLed">true</bool>

==== Charging ====

Enable charging LED support

''frameworks/base - config.xml''

    <bool name="config_intrusiveBatteryLed">true</bool>

If the LED has more then one color

    <bool name="config_multiColorBatteryLed">true</bool>

=== Colors ===

''OmniGears - config.xml''

If device supports RGB colors on LEDs

    <bool name="config_has_multi_color_led" translatable="false">true</bool>

Else a list of supported colors can be provided
the default is red/green

''OmniGears - arrays.xml''

    <string-array name="entries_led_colors" translatable="false">
        <item>@string/led_color_green</item>
        <item>@string/led_color_red</item>
    </string-array>

    <string-array name="values_led_colors" translatable="false">
        <item>#FF00FF00</item>
        <item>#FFFF0000</item>
    </string-array>

== Buttons and Keys ==

=== Config ===

==== Define the number of buttons available on the device ====

''frameworks/base - config.xml''

    Hardware 'face' keys present on the device, stored as a bit field.
         This integer should equal the sum of the corresponding value for each
         of the following keys present:
             1 - Home
             2 - Back
             4 - Menu
             8 - Assistant (search)
            16 - App switch
         For example, a device with Home, Back and Menu keys would set this
         config to 7.

    <integer name="config_deviceHardwareKeys">7</integer>

==== Enable custom button config in Settings ====

''OmniGears - config.xml''

    <bool name="config_has_hardware_buttons">true</bool>

If kernel has volume wake support

    <bool name="config_show_volumeRockerWake">true</bool>

=== Backlight ===

If the device has capacitive buttons with backlight that should be
handled separate of the screen brightness.

==== Enable support of custom button backlight ====

''frameworks/base - config.xml''

    <bool name="config_button_brightness_support">true</bool>

==== Define the default button brightness values for automatic brightness ====

    <integer-array name="config_autoBrightnessButtonBacklightValues">
        <item>14</item>   <!-- 0-10 -->
        <item>28</item>   <!-- 10-50 -->
        <item>37</item>   <!-- 50-100 -->
        <item>51</item>   <!-- 100-200 -->
        <item>71</item>   <!-- 200-400 -->
        <item>80</item>   <!-- 400-500 -->
        <item>96</item>   <!-- 500-800 -->
        <item>108</item>  <!-- 800-1000 -->
        <item>144</item>  <!-- 1000-1600 -->
        <item>181</item>  <!-- 1600-3000 -->
        <item>255</item>  <!-- 3000+ -->
    </integer-array>

This also requires support of setting button backlight separate
in liblights

e.g. https://github.com/omnirom/android_device_oppo_find5/blob/android-4.4/liblight/lights.c
