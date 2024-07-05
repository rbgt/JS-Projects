<!-- src/App.vue -->
<template>
  <div id="app">
    <DropArea :onFileRead="updateFileContent" />
    <div v-if="fileContent">
      <h3>File Content:</h3>
      <pre>{{ fileContent }}</pre>
    </div>
  </div>
</template>

<script>
import DropArea from './components/DropArea.vue';

export default {
  components: {
    DropArea,
  },
  data() {
    return {
      fileContent: null,
    };
  },
  methods: {
    updateFileContent(content) {
      this.fileContent = content;
    },
  },
};
</script>

<style>
/* Add any global styles here if necessary */
</style>
