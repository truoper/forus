<template>
    <div class="modal" v-show="isOpen">
      <div class="modal-overlay" @click="closeModal"></div>
      <div class="modal-content">
        <img :src="images[currentIndex].url" />
        <button @click="previousImage" v-show="currentIndex > 0">Previous</button>
        <button @click="nextImage" v-show="currentIndex < images.length - 1">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      images: {
        type: Array,
        required: true,
      },
      isOpen: {
        type: Boolean,
        required: true,
      },
      currentIndex: {
        type: Number,
        required: true,
      },
    },
    methods: {
      closeModal() {
        this.$emit('close-modal');
      },
      previousImage() {
        this.$emit('previous-image');
      },
      nextImage() {
        this.$emit('next-image');
      },
    },
  };
  </script>
  
  <style scoped>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }
  
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.8);
  }
  
  .modal-content {
    position: relative;
  }
  
  img {
    max-width: 80%;
    max-height: 80%;
    object-fit: contain;
  }
  </style>
  