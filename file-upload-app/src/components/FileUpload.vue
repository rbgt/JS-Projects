<template>
  <div class="file-upload">
    <input type="file" @change="handleFileUpload" />
    <div v-if="fileContent">
      <h3>File Content:</h3>
      <pre>{{ fileContent }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileContent: null
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.fileContent = e.target.result;
        };
        reader.readAsText(file);
      }
    }
  }
};
</script>

<style scoped>
.file-upload {
  margin: 20px;
}
</style>