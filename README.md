# P-DIALOG-MODAL

![](https://img.shields.io/badge/webpack-3.9.1-blue.svg)
![](https://img.shields.io/badge/vue-2.5.9-brightgreen.svg)
![](https://img.shields.io/badge/Author-PDK-yellow.svg)

## Explain

1 . Confirm Dialog Modal

2 . Support customization，for example: color 、 position 、 text ...

3 . `normal confirm dialog` and `input confirm dialog`

4 . .....(There will be more follow ups)

---

## Demo

<img src='https://github.com/PDKSophia/p-dialog-modal/raw/master/image/image1.png' width='250'>

<img src='https://github.com/PDKSophia/p-dialog-modal/raw/master/image/image2.png' width='250'>

---

## Usage

### 1.1 Installation

```javascript
  npm install p-dialog-modal --save
```

### 1.2 ES6 Import

```javascript
import ConfirmModal from 'p-dialog-modal'

export default {
  components: {
    ConfirmModal
  }
}
```

## Basic Example

html

```html
<template>
  <div>
    <confirm-modal
      :type="confirmModal.type"
      :title="confirmModal.title"
      :content="confirmModal.content"
      :cancelText="confirmModal.cancelText"
      :submitText="confirmModal.submitText"
      :cssStyle="confirmModal.cssStyle"
      :noneToastText="confirmModal.noneToastText"
      :isMarginTop="confirmModal.isMarginTop"
      @onHandleCancel="handleOnCancel"
      @onHandleOnOk="handleOnOk"
    />
  </div>
</template>
```

js

```javascript
import ConfirmModal from 'p-dialog-modal'

export default {
  components: {
    ConfirmModal
  },
  data() {
    return {
      confirmModal: {
        type: 'input',
        title: '请输入用户名',
        content: '你要给我点个赞嘛 ?',
        cancelText: '取消',
        submitText: '确认',
        cssStyle: {
          bgTitleColor: '#4d4d4d',
          textTitleColor: '#ffffff',
          bgCancelColor: '#fff',
          textCancelColor: '#555',
          bgSubmitColor: '#4d4d4d',
          textSubmitColor: '#fff'
        },
        isMarginTop: '35%'
      }
    }
  },
  methods: {
    // submit
    handleOnOk(type, bool, value) {
      if (type === 'normal') {
        console.log(type, bool, value) // normal  true  ''
      } else {
        console.log(type, bool, value) // normal  true  value
      }
    },
    // cancel
    handleOnCancel(type, bool) {
      console.log('?????', type, bool)
    }
  }
}
```

### Props

|    props    |  type  |      default       |                                    description                                     |
| :---------: | :----: | :----------------: | :--------------------------------------------------------------------------------: |
|    type     | String |       normal       | `normal` represents a regular modal，`input` represents a regular modal with input |
|    title    | String |     弹窗提示您     |                                Confirm Modal Title                                 |
|   content   | String | 你要给我点个赞嘛 ? |                               Confirm Modal Content                                |
| cancelText  | String |        取消        |                                 Cancel Button Text                                 |
| submitText  | String |        确认        |                                 Submit Button Text                                 |
|  cssStyle   | Object |         {}         |                                Confirm Modal Style                                 |
| isMarginTop | String |        35%         |                 The distance between the elastic layer and the top                 |

---

`Here is the props of **cssStyle**`

|      props      |  type  | default |          description           |
| :-------------: | :----: | :-----: | :----------------------------: |
|  bgTitleColor   | String | #ffffff |     title background color     |
| textTitleColor  | String | #4a4a4a |        title text color        |
|  bgCancelColor  | String | #ffffff | Cancel button background color |
| textCancelColor | String |  #555   |    Cancel button text color    |
|  bgSubmitColor  | String | #4d4d4d | Submit button background color |
| textSubmitColor | String |  #fff   |    Submit button text color    |

### Event

When you press the confirm modal **cancel** button，trigger `handleOnCancel()`

```javascript
    handleOnCancel(type, bool) {
      console.log('close modal', type, bool)
    }
```

When you press the confirm modal **submit** button，trigger `handleOnOk(type, value)`

```javascript
    handleOnOk(type, value) {
      if (type === 'normal') {
        console.log('OK')
        console.log('close modal')
      } else {
        console.log('callback value is : ', value)
        console.log('close modal')
      }
    }
```
