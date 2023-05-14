<template>
  <img :src="src" :alt="altText" @click="showModal"/>
</template>

<script>
export default {
  props: {
    src: {
      type: String,
      required: true
    },
    altText: {
      type: String,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  methods: {
    showModal() {
      this.$emit('show-modal', this.index);
    }
  }
}
</script>
