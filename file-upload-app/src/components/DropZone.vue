<template>
  <div>
    <div 
      class="drop-zone" 
      @dragover.prevent="highlightDropZone"
      @dragleave="unhighlightDropZone"
      @drop.prevent="handleDrop"
      :class="{ 'highlight': isHighlighted }"
    >
      <p v-if="!isHighlighted">Drag and drop a text file here</p>
      <p v-else>Drop the file to upload</p>
    </div>
    <div v-if="fileContent" class="file-content">
      <h3>File Content:</h3>
      <pre>{{ fileContent }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isHighlighted: false,
      fileContent: null
    }
  },
  methods: {
    highlightDropZone() {
      this.isHighlighted = true
    },
    unhighlightDropZone() {
      this.isHighlighted = false
    },
    handleDrop(e) {
      this.isHighlighted = false
      const file = e.dataTransfer.files[0]
      if (file) {
        this.readFileContent(file)
      }
    },
    readFileContent(file) {
      const reader = new FileReader()
      reader.onload = (e) => {
        this.fileContent = e.target.result
      }
      reader.readAsText(file)
    }
  }
}
</script>

<style scoped>
.drop-zone {
  width: 300px;
  height: 200px;
  border: 2px dashed #ccc;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-bottom: 20px;
}

.drop-zone.highlight {
  border-color: #2196f3;
  background-color: #e3f2fd;
}

.file-content {
  max-width: 600px;
  margin-top: 20px;
}

.file-content pre {
  background-color: #f5f5f5;
  padding: 10px;
  border-radius: 4px;
  white-space: pre-wrap;
  word-wrap: break-word;
}
</style>