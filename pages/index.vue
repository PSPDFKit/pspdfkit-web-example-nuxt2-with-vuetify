<template>
  <div id="app">
    <div style="gap: 10px" class="d-flex flex-column mb-10">
      <DropdownComponent />
      <AutocompleteComponent />
    </div>
    <div class="d-flex flex-column mb-2">
      <label for="file-upload" class="custom-file-upload"> Open PDF </label>
      <input id="file-upload" type="file" class="btn" @change="openDocument" />
    </div>
    <PSPDFKitContainer :pdf-file="pdfFile" @loaded="handleLoaded" />
  </div>
</template>

<script>
import PSPDFKitContainer from '../components/PSPDFKitContainer.vue'

export default {
  name: 'App',
  /**
   * Render the `PSPDFKitContainer` component.
   */
  components: {
    PSPDFKitContainer,
  },

  data() {
    return {
      pdfFile: this.pdfFile || 'document.pdf',
    }
  },

  /**
   * Our component has two methods — one to check when the document is loaded, and the other to open the document.
   */
  methods: {
    handleLoaded(instance) {
      console.log('PSPDFKit has loaded: ', instance)
      // Do something.
    },

    openDocument(event) {
      if (this.pdfFile && this.pdfFile.startsWith('blob:')) {
        window.URL.revokeObjectURL(this.pdfFile)
      }
      this.pdfFile = window.URL.createObjectURL(event.target.files[0])
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}

input[type='file'] {
  display: none;
}

.custom-file-upload {
  border: 1px solid #ccc;
  border-radius: 4px;
  display: inline-block;
  padding: 6px 12px;
  cursor: pointer;
  background: #4a8fed;
  color: #fff;
  font: inherit;
  font-size: 16px;
  font-weight: bold;
}
</style>
