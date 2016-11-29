## Vue2-Editor

HTML Editor using Vue.js 2.0 and Quilljs
<br>
[Vue.js](https://vuejs.org)
</br>
[Quill](http://quilljs.com/)

<!-- ## Demo -->

<!-- [fiddle](https://jsfiddle.net/su9zv0w9/1/) -->

## Install

```bash
$ npm install --save vue2-editor
```
</br>

## Use
```js
import { VueEditor } from 'vue2-editor'
```
</br>

## Props

**_editor-content_**:
<br>
You can set the the content of the editor dynamically. If you don't need this feature then do not include it.
```html
<template>
  <div id="app">
    <button type="button"
      @click="setEditorContent">
    </button>

    <vue-editor
      :editor-content="htmlForEditor">
    </vue-editor>
  </div>
</template>

<script>
  import { VueEditor } from 'vue2-editor'

  export default {
    data: function () {
      return {
        htmlForEditor: null  
      }
    },

    methods: {
      setEditorContent: function () {
        this.htmlForEditor = '<h1>Html For Editor</h1>'
      }
    }
  }
</script>
```

</br>
**_show-preview_**:
<br>
This is set to FALSE by default. To enable:

```html
<vue-editor
  :show-preview="true">
</vue-editor>
```

</br>
**_editor-toolbar_**:
<br>
If you want to use a custom toolbar then you can set it to a property from the data object.

```html
<template>
  <div id="app">
    <vue-editor
      :editor-toolbar="customToolbar">
    </vue-editor>
  </div>
</template>

<script>
  import { VueEditor } from 'vue2-editor'

  export default {
    data: function () {
      return {
        customToolbar: [
            ['bold', 'italic', 'underline'],
            [{ 'list': 'ordered'}, { 'list': 'bullet' }],
            ['image', 'code-block']
          ]
      }
    }
  }
</script>
```
</br>
**_use-save-button_**:
</br>
This is set to true by default. Set to false to use your own button.

</br>
**_button-text_**:
</br>
The default text is 'Save Content'. If you want to use the built in Save button but with different text then you can set this prop to a String.
```html
<vue-editor
  button-text="Custom Save Message">
</vue-editor>
```
</br>


## Events

**_editor-updated_**:
</br>
Emitted when the editor contents change. You will want to listen for this event if using your own save button.

</br>
**_save-content_**:
</br>
Emitted when the default save button is clicked.

</br>
## How do I get the html content from the text editor?
_There are 2 different scenarios we need to address._
</br></br>

### 1. Using the default Save Button

   When the button is clicked, the '**_save-content_**' event is emitted with the current contents of the editor.
   You need to create a method that runs when this event is emitted.

   Note: You will need to pass a parameter to the method you create. This parameter holds the editor contents.

EX:
```html
<template>
  <div id="app">
    <h1>Write Your Message and save it!</h1>
    <vue-editor
      @save-content="handleSavingContent">
    </vue-editor>
  </div>
</template>

<script>
import { VueEditor } from 'vue2-editor'

export default {
  methods: {
    handleSavingContent: function (contentsToBeSaved) {
      console.log(contentsToBeSaved)
    }
  }  
}
</script>
```

</br>
### Using your own button

The event '**_editor-updated_**' is emitted when the text inside the editor changes. The current editor contents are sent with this event.

You need to create a method that runs when this event is emitted.

EX:
```html
<template>
  <div id="app">

    <vue-editor
      :use-save-button="false"
      @editor-updated=handleUpdatedContent>
    </vue-editor>

    <button type="button" name="save-content"
      @click="saveTheContent">
      Our Own Button
    </button>

  </div>
</template>

<script>
import { VueEditor } from 'vue2-editor'

export default {
  data: function () {
    return {
      htmlFromEditor: null
    }
  },

  methods: {
    handleUpdatedContent: function (value) {
      this.htmlFromEditor = value
    },

    saveTheContent: function () {
      // Do whatever you want
      console.log(this.htmlFromEditor)
    }
  }
}
</script>
```

###Example using several configuration options

```html
<template>
  <div id="app">
    <vue-editor
      :editor-content="htmlForEditor"
      :show-preview="true"
      @editor-updated="handleUpdatedContent"
      @save-content="handleSavingContent"
      button-text="Save Your Content">
    </vue-editor>
  </div>
</template>

</br>
<script>
  import { VueEditor } from 'vue2-editor'

  export default {
    data: function () {
      return {
        htmlForEditor: null  
      }
    },

    methods: {
      handleSavingContent: function (value) {
        console.log(value)
      },

      handleUpdatedContent: function (value) {
        console.log(value);
      },

      setEditorContent: function () {
        this.htmlForEditor = '<h1>Html For Editor</h1>'
      }
    }  
  }
</script>
```
# License
MIT