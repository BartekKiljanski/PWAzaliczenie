<template>
    <div class="modal" @click.self="$emit('close-modal')">
      <img :src="src" :alt="alt" class="modal-img">
      <button class="prev" @click="prevImage">&lt;</button>
      <button class="next" @click="nextImage">&gt;</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      src: {
        type: String,
        required: true
      },
      alt: {
        type: String,
        required: true
      },
      currentIndex: {
        type: Number,
        required: true
      },
      images: {
        type: Array,
        required: true
      }
    },
    methods: {
      prevImage() {
        const newIndex = this.currentIndex - 1;
        if (newIndex >= 0) {
          this.$emit('change-image', newIndex);
        }
      },
      nextImage() {
        const newIndex = this.currentIndex + 1;
        if (newIndex < this.images.length) {
          this.$emit('change-image', newIndex);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .modal {
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
  
  .modal-img {
    max-width: 80%;
    max-height: 80%;
  }
  
  .prev,
  .next {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    font-size: 3rem;
    color: #fff;
    background-color: transparent;
    border: none;
    cursor: pointer;
  }
  
  .prev {
    left: 10%;
  }
  
  .next {
    right: 10%;
  }
  </style>
  