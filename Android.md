# Android

## Code

**Code should match JAVA standards. See [relative guide](Java.md) for more details.**

### Architecture

You should separate activities from adapters. Ditto for fragments. 

```
views/
  |-- activities/
  |-- fragments/     // Gathers dialogs and fragments
  |-- adapters/
```

### Performances

#### 65k limit

Android apps must have less than 65K methods, including libraries. Then, you should be attentive to import only methods/classes you need (even if there is a work around to overcome this problem).

Remove useless code. Proguard can help you for that.

#### Avoids getters & setters

Even if it is usually a good pattern to follow, you should avoid having getters and setters to access fields in Android. Direct access can improve performances from 3x to 7x. 

#### Do not block UI thread (aka main thread)

Anytime, you should steer clear of blocking UI thread. Indeed, when you are performing long operations, such as pulling data from remote server or engining random stuff in business part, you are freezing your app. User cannot perform interactions anymore.

For instance, avoid to set adapters, pull data from database or server on main thread. To get round this problem, use threads. In particular, Android provides to developers the `AsyncTask` interface. 

#### Avoid Java hashes

Android development implies to be careful about performances and memory management. Instead of using Java hashes (such as `HashMap`), you should use built-in ones, as `SparseArray`. They are designed for being reverent of Android devices. 

#### Manages your memory

Memory is an important resource and quite limited. You should be attentive to free objets, resources and assets as soon as possible. Stop operations when your activity is hidden. Do not let services running for peccadilloes.

#### Do not use enums

Enums are almost 3x eager in memory than static fields. You should use those ones instead, even if for integers.

#### Use static methods (if possible)

Static calls may be 3x faster than classic ones. Use them as much as possible, especially when you need no fields or context (e.g. helpers).

#### Use `float` instead of `double`

Double uses 2x more space than float. What are you still using them?

## Resources

### Indentation

Indentation should be **4 soft spaces**.

```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    >
    
    <TexView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello!"
        />
        
</LinearLayout>
```

### Case

All resources should be snake cased.

```
layout/activity_landing.xml
style/style_activity_landing.xml
```

### Metrics

In order to keep your design responsive, you should only use `dp` and `sp` units. First one for sizes, the other for fonts.

Especially, avoid using pixel units.

### Layouts

#### Attribute order

Attributes should be ordered as below:

```xml
<LinearLayout
    android:id="@+id/my_id"
    
    android:layout_width="match_parent"
    
    style="@style/MyStyle"
    />
```

`android:id` should be the first one. Then, append properties. Finally add style.

#### Close tag

Close tag should be on a new line. Adding properties will be easier to perform.

```xml
<RelativeLayout
    />
```

#### Name

Layout names should match this pattern: `[[type]]_[[name]]`.

```
MainActivity ~> layout/activity_main.xml
AlertDialog ~> layout/dialog_alert.xml
PictureInsightFragment ~> layout/fragment_picture_insight.xml
```

### Styles

**Try using as many styles as possible. Like CSS/HTML coding, you should avoid setting properties in layout code.** It increases maintainability and preserves your layout file.

#### Name

File name should match this pattern: `style_[[type]]_[[name]]`.

```
MainActivity ~> style_activity_main.xml
PictureInsightFragment ~> style_fragment_picture_insight.xml
```

#### Layout

Style should follow this skeleton:

```xml
<style name="MyStyle" parent="MyParentStyle">
    <!-- Firstly layout args (size, position, orientation, gravity etc.) -->
    <item name="android:layout_width">match_parent</item>
    <item name="android:orientation">vertical</item>
    
    <!-- Then, margins and paddings -->
    <item name="android:layout_marginTop">10dp</item>
    <item name="android:paddingLeft">5dp</item>
    
    <!-- Relative to fonts -->
    <item name="android:textColorHint">#ccc</item>
    <item name="android:textSize">15sp</item>
    
    <!-- Colors and extra -->
    <item name="android:background">#eee</item>
</style>
```

### Colors

Color file should only define a palette and not being specific to your business.

```xml
<!-- DO -->
<color name="hippie_blue">#5696BC</color>
<color name="picton_blue">#52befb</color>
<color name="orange">#ff9900</color>

<!-- DO NOT -->
<color name="back_button_color">#5696BC</color>
<color name="main_background">#52befb</color>
<color name="font_color">#ff9900</color>
```

### Dimensions

Like colors, dimensions should not be relative to your business.

```xml
<!-- DO -->
<dimen name="small_avatar">50dp</dimen>
<dimen name="medium_avatar">100dp</dimen>
<dimen name="large_avatar">150dp</dimen>

<!-- DO NOT -->
<dimen name="comment_avatar">50dp</dimen>
<dimen name="landing_avatar">100dp</dimen>
<dimen name="profile_avatar">150dp</dimen>
```

### Performances

#### Limit hierarchy

Avoid complex hierarchy. More complex it is, slower rendering engine will be. If you have too many nested layouts, you may have a `StackOverflowException`. Refactors your layout frequently to improve your performances. 

#### Reuse components

You should use reuse components as much as possible. Use `merge` or `include` directives for this purpose. UI engine will optimise rendering consequently. 

#### Stubs views

When using scrollable containers, you may be interested in using `ViewStub`. Ditto when using hidden components.

`ViewStub` allows you to mock a component and renders it when you really need it. It an easy way to boost your performances.

#### Limit image rendering

If you have a bunch of images in an `AdapterView` (either list or grid), it can really impact your performances to load all of them. To overcome this issue, you can use a `ViewHolder` to load images in the background. Then, you keep your `ListView` or `GridView` smooth to scroll.
