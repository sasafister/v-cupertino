# [Cupertino Pane](https://github.com/roman-rr/cupertino-pane#cupertino-pane) for Vue 3

<img src="https://img.shields.io/badge/vuejs%20-%2335495e.svg?&style=for-the-badge&logo=vue.js&logoColor=%234FC08D"/>
<img src="https://img.shields.io/badge/typescript%20-%23007ACC.svg?&style=for-the-badge&logo=typescript&logoColor=white"/>
<img src="https://img.shields.io/badge/github%20-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/>

> ## How works

## **Props**
| props | type | example | comments |
|-|-|-|-|
| :drawerOptions ( optional ) | `CupertinoSettings` |  `<v-cupertino :drawerOptions="yourSettingsObject">` | The same as the Cupertinos Options; **constraints** you cannot override cupertino's callbacks even if you specified in the `CupertinoSettings`' Object|
| :entryAnimation ( optional ) | `Boolean` | `<v-cupertino :entryAnimation="Boolean">` | Whether the drawer should present, destroy or hide with a smooth animation |
| :entryComponent ( optional ) | `Component` | `<v-cupertino :entryComponent="Component">` | The component itself use slots, but I think it would be faster to toggle between component from scripts instead of using v-if also components remember their state because are wrapped by `<keep-alive>` tag|

<br>
<br>

## **Events**
 _**Note:** Are the same hooks as the Cupertino pane but instead of camelCase are kebak-case and without the prefix **on**: `@will-dismiss, @backdrop-tap...`_


| events | return | comments |
| - | - | - |
| @did-dismiss | `() => void` | |
| @will-dismiss | `() => void` | |
| @did-present | `() => cupertinoInstance` | **Returns:** the cupertino instance inside the component when the drawer is already visible, this is useful when you need to have access to the instance once is visible  | 
| @will-present | `() => cupertinoInstance` | **Returns:** the cupertino instance inside the component when the drawer will be visible, this is useful when you need to have access to the instance before is visible | 
| @drag-start | `() => number` | **Returns:** the property `y` from the method `getBoundingClientRect()` that belongs to the `DOMRect` |
| @drag | `() => number` | **Returns:** the property `y` from the method `getBoundingClientRect()` that belongs to the `DOMRect` |
| @drag-end | `() => number` | **Returns:** the property `y` from the method `getBoundingClientRect()` that belongs to the `DOMRect` |
| @backdrop-tap | `() => void` | |
| @transition-start | `() => void` | |
| @transition-end | `() => void` | |

<br>
<br>

> ## How to get access to the public method from the instance Cupertino inside the component <v-cupertino />

Theres actually **three** ways to get the instance of `<v-cupertino />` component from its parent container:

* refs
* From the instance returned by @did-present event
* From the instance returned by @will-present event

### **Getting the instance with refs**

![ref](assets/ref_example_x1.svg)

### **Getting the instance from @did-present or @will-present event**

![ref](assets/event_example_x1.svg)

<br>
<br>

## Using public methods

Here an [overview](https://github.com/roman-rr/cupertino-pane/blob/master/README.md#public-methods) of all the public methods

> Using the *refs* example to access public methods

```javascript
import { CupertinoPane } from "cupertino-pane";
import { defineComponent, onMounted, ref, Ref } from "vue";
import VCupertino from "./components/VCupertino.vue";

export default defineComponent({
  name: "App",
  components: {
    VCupertino,
  },
  setup() {
    const cupertinoRef: Ref<typeof VCupertino> = ref(VCupertino);

    onMounted(() => {
      const cupertino = cupertinoRef.value.cupertino as CupertinoPane;
      cupertino.setDarkMode({ enable: Boolean }); // param: 
      cupertino.moveToBreak(String); // Will change pane position with animation to selected breakpoint. param: required('top' | 'middle' | 'bottom')
      cupertino.moveToHeight(Number); // Will move pane to exact height with animation. Breakpoints will saved. param: required
      cupertino.hide(); // Dissappear pane from screen, still keep pane in DOM.
      cupertino.present({ animated: Boolean }); // Will render pane DOM and show pane with setted params. param: optional
      cupertino.destroy({ animated: Boolean }); // Remove pane from DOM and clear styles
      // to check more public methods to *overview* that is above
    });

    return {
      cupertinoRef,
    };
  },
});
```

<br>
<br>
<br>

# License
Licensed under the MIT License. [View original LICENSE](https://github.com/roman-rr/cupertino-pane/blob/master/LICENSE)

Lol, that's all, thanks





