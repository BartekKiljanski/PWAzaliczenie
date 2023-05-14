<template>
  <div class="lightbox">
    <button class="close" @click="$emit('close')">&times;</button>
    <button class="prev" @click="changeImage(currentIndex - 1)" :disabled="currentIndex === 0">&lt;</button>
    <image :src="images[currentIndex].src" :alt="images[currentIndex].altText" />
    <button class="next" @click="changeImage(currentIndex + 1)" :disabled="currentIndex === images.length - 1">&gt;</button>
    
  </div>
</template>

<script>
import MyImage from './MyImage.vue';

export default {
  components: {
    MyImage
  },
  props: {
    images: {
      type: Array,
      required: true
    },
    currentIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    changeImage(index) {
      if (index >= 0 && index < this.images.length) {
        this.$emit('change-image', index);
      }
    }
  }
}
</script>
<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 20px;
}

.gallery img {
  width: 100%;
  height: auto;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.gallery img:hover {
  transform: scale(1.1);
}

.lightbox {
  background-color: rgba(0, 0, 0, 0.8);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lightbox .lightbox-content {
  position: relative;
}

.lightbox .lightbox-content button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 3rem;
  color: #fff;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.lightbox .lightbox-content .close {
  right: 10%;
}

.lightbox .lightbox-content .prev {
  left: 10%;
}

.lightbox .lightbox-content .next {
  right: 10%;
}

.lightbox .lightbox-content img {
  max-width: 90%;
  max-height: 90%;
}
</style>
