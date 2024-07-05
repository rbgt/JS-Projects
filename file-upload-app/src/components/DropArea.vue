<!-- src/components/DropArea.vue -->
<template>
  <div
    class="drop-area"
    @dragover.prevent
    @drop="handleDrop"
  >
    Drop a file here
  </div>
</template>

<script>
export default {
  props: {
    onFileRead: {
      type: Function,
      required: true,
    },
  },
  methods: {
    handleDrop(event) {
      const file = event.dataTransfer.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.onFileRead(e.target.result);
        };
        reader.readAsText(file);
      }
    },
  },
};
</script>

<style scoped>
.drop-area {
  border: 2px dashed #ccc;
  border-radius: 4px;
  padding: 20px;
  text-align: center;
  margin: 20px;
  cursor: pointer;
}
</style>
