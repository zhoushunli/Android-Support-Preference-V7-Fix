# AndroidX Preference eXtended

This library is meant to fix some of the problems found in the official AndroidX preference library. Also, there are [new preference types](#extra-types) available, such as `RingtonePreference`, `DatePickerPreference`, and `TimePickerPreference`.

[ ![Download](https://api.bintray.com/packages/gericop/maven/com.takisoft.fix%3Apreference-v7/images/download.svg) ](https://bintray.com/gericop/maven/com.takisoft.fix%3Apreference-v7/_latestVersion)

### Donation

If you would like to support me, you may donate some small amount via PayPal.

[ ![Buy me a coffee](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/donate.png)](https://www.paypal.me/korossyg/0eur)

---

## How to use the library?
### 1. Add gradle dependency
**Add** this to your gradle file:
```gradle
implementation "androidx.preference:preference:$androidxVersion"
implementation 'com.takisoft.preferencex:preferencex:1.0.0-alpha1'
```

### 2. Use the appropriate class as your fragment's base

```java
import com.takisoft.preferencex.PreferenceFragmentCompat;

public class MyPreferenceFragment extends PreferenceFragmentCompat {

    @Override
    public void onCreatePreferencesFix(@Nullable Bundle savedInstanceState, String rootKey) {
        setPreferencesFromResource(R.xml.settings, rootKey);
	
	// additional setup
    }
}
```
> **Warning!** Watch out for the correct package name when importing `PreferenceFragmentCompat`, it should come from `com.takisoft.preferencex`.

Now you can enjoy using preferenceX.

---

## Extra types

There are additional preferences not part of the official support library, but decided to add them to some extra libraries. You can add them to your project using Gradle.

Preference | Dependency | Preview
-|-|-
[`RingtonePreference`](https://github.com/Gericop/Android-Support-Preference-V7-Fix/wiki/Preference-types#ringtonepreference) | `implementation 'com.takisoft.preferencex:preferencex-ringtone:1.0.0-alpha1'` | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/ringtone_api26.png)
[`DatePickerPreference`](https://github.com/Gericop/Android-Support-Preference-V7-Fix/wiki/Preference-types#datepickerpreference) | `implementation 'com.takisoft.preferencex:preferencex-datetimepicker:1.0.0-alpha1'` | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/datepicker_api26.png)
[`TimePickerPreference`](https://github.com/Gericop/Android-Support-Preference-V7-Fix/wiki/Preference-types#timepickerpreference) | `implementation 'com.takisoft.preferencex:preferencex-datetimepicker:1.0.0-alpha1'` | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/timepicker_api26.png)
[`ColorPickerPreference`](https://github.com/Gericop/Android-Support-Preference-V7-Fix/wiki/Preference-types#colorpickerpreference) | `implementation 'com.takisoft.preferencex:preferencex-colorpicker:1.0.0-alpha1'` | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/colorpicker_api26_fixed.png)
[`SimpleMenuPreference`](https://github.com/Gericop/Android-Support-Preference-V7-Fix/wiki/Preference-types#simplemenupreference) | `implementation 'com.takisoft.preferencex:preferencex-simplemenu:1.0.0-alpha1'` (can be used independent of `preferencex`) | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/simplemenu_api26.png)

---

## Custom solutions

### Hijacked `EditTextPreference`
The support implementation of `EditTextPreference` ignores many of the basic yet very important attributes as it doesn't forward them to the underlying `EditText` widget. In my opinion this is a result of some twisted thinking which would require someone to create custom dialog layouts for some simple tasks, like showing a numbers-only dialog. This is the main reason why the `EditTextPreference` gets hijacked by this lib: it replaces certain aspects of the original class in order to forward all the XML attributes set (such as `inputType`) on the `EditTextPreference` to the `EditText`, and also provides a `getEditText()` method so it can be manipulated directly.

The sample app shows an example of setting (via XML) and querying (programmatically) the input type of the `EditTextPreference`:
```xml
<EditTextPreference
    android:inputType="phone"
    android:key="edit_text_test" />
```

```java
EditTextPreference etPref = (EditTextPreference) findPreference("edit_text_test");
if (etPref != null) {
    int inputType = etPref.getEditText().getInputType();
    // do something with inputType
}
```
> **Note!** Watch out for the correct package name when importing `EditTextPreference`, it should come from `com.takisoft.preferencex`. If you import from the wrong package (i.e. `androidx.preference`), the `getEditText()` method will not be available, however, the XML attributes will still be forwarded and processed by the `EditText`.

### Others

* Convenience methods in `PreferenceFragmentCompat`;
* `PreferenceCategory` with different colors;
* `AutoSummaryEditTextPreference`;
* `PreferenceActivityResultListener`;
* `EditTextPreference` correctly calls `notifyChange`. ([#66](https://github.com/Gericop/Android-Support-Preference-V7-Fix/pull/66))


---

## Version
The current stable version is **1.0.0-alpha1**.

## Notes #
This demo / bugfix is set to work on API level 14+.

---

## Sample

_Material design - everywhere._

API 15 | API 21 | API 26
-|-|-
![API 15](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/base_api15.png) | ![API 21](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/base_api21.png) | ![API 26](https://raw.githubusercontent.com/Gericop/Android-Support-Preference-V7-Fix/master/images/base_api26.png)

---

### Changelog

**2018-05-11**

New version: 1.0.0-alpha1 (based on v27.1.1)

- No support preferences related changes in the support library.
- Bug fixes (#153, #149, #155, #152).

**2018-04-10**

New version: 27.1.1.0 (based on v27.1.1)

- No support preferences related changes in the support library.
- Some bug fixes (see #147 for more info).

> For older changelogs, check out the [CHANGELOG](CHANGELOG.md) file.

Feel free to ask / suggest anything on this page by creating a ticket (*issues*)!

# License notes #
You can do whatever you want except where noted.
