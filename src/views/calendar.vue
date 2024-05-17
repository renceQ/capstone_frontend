<template>
  <div class="customization-container">
    <h2>Customize Your Item</h2>
    <div class="customization-options">
      <label for="color">Color:</label>
      <select v-model="selectedColor" id="color">
        <option v-for="color in colors" :key="color" :value="color">{{ color }}</option>
      </select>

      <label for="size">Size:</label>
      <select v-model="selectedSize" id="size">
        <option v-for="size in sizes" :key="size" :value="size">{{ size }}</option>
      </select>
    </div>
    <div class="preview" :style="{ backgroundColor: selectedColor }">
      <p>Selected Color: {{ selectedColor }}</p>
      <p>Selected Size: {{ selectedSize }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedColor: 'Red',
      selectedSize: 'M',
      colors: ['Red', 'Blue', 'Green', 'Yellow'],
      sizes: ['S', 'M', 'L', 'XL'],
    };
  },
};
</script>

<style scoped>
.customization-container {
  text-align: center;
  margin: 20px;
}

.customization-options {
  margin-bottom: 20px;
}

.preview {
  padding: 20px;
  border: 1px solid #000;
  display: inline-block;
  margin-top: 10px;
}
</style>
