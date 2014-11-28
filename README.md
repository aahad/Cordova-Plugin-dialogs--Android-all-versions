# Cordova/PhoneGap: How to make dialog plugin work on all Android devices

***

**Since Oct 16, 2014** (commit: 23bebf96f7a3388c7483afc0091faecf943692d3), the **dialog Plugin supports API 17 on-wards.**

This commit was to **properly** format **right-to-left** and **left-to-right languages**, as shown below in the snapshot. ([Check for setTextDirection API level](https://github.com/apache/cordova-plugin-dialogs/commit/23bebf96f7a3388c7483afc0091faecf943692d3))
 
Example: without any code modification

![Dialog Plugin running on API 17](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dialog_API_17.jpeg)

Now if there is **NO** need to properly format localized strings (or **no use of localization at all**) then if these lines are **removed** then the plugin support will be available from **API 14 on-wards**.

## Bring down to API 14 or 11

Currently dialog plugin is using device's light theme (`AlertDialog.THEME_DEVICE_DEFAULT_LIGHT`) that is available since **API 14**. http://developer.android.com/reference/android/app/AlertDialog.html#THEME_DEVICE_DEFAULT_LIGHT 

So if it can be **changed** with something else like `AlertDialog.THEME_HOLO_LIGHT`, `AlertDialog.THEME_HOLO_DARK`  or `AlertDialog.THEME_TRADITIONAL` as **these** are present **since API 11**. In this way we can make the **plugin work on API 11**. I tried `AlertDialog.THEME_HOLO_LIGHT` and found exactly **same results** as of with `AlertDialog.THEME_DEVICE_DEFAULT_LIGHT`.


Using `AlertDialog.THEME_TRADITIONAL`, I see following result

![Dialog with traditional theme](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dialog_API14traditional_.jpeg)


Using `AlertDialog.THEME_HOLO_DARK`, I see following result


![Dialog with holo dark theme](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dialog_API14_holodark.jpeg)


## Bring down to API 7

`AlertDialog.Builder(Context context, int theme)` was used to create instance of AlertDialog and this **two parameter based constructor** was added in **API 11**. While the basic original AlertDialog **constructor **that takes **single parameter** was present since** API 1**. So if there is **NO hard** need for a **specific theme** then by skipping the two parameter based constructor and by using single parameter based constructor we can easily get down to **API 7**. 



### 1. Notification - Since API 14 onwards

This is for someone who doesn’t need localization formatting in their app.

**Note: -** Even after removing these lines, still localized strings/text will appear as shown below; but the proper formatting will be out. Though it’s not visible in the snapshot but it is expected.

Results:

![Dialog with traditional theme](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dialog_API14traditional_.jpeg)
![Dialog with holo dark theme](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dialog_API14_holodark.jpeg)


### 2. Notification - Since API 7 onwards

This is for someone with **NO hard** requirement for any **specific theme or localization** and just need dialog functionality to work on **older devices**.

Results:

![Dialog on API 7](https://github.com/aahad/Cordova-Plugin-dialogs--Android-all-versions/blob/master/snapshots/dailog_API_7.jpeg)
