<template>
  <div class="gallery">
    <div class="gallery-header">
      <h1>{{ galleryTitle }}</h1>
    </div>
    <div class="gallery-content">
      <div v-for="(image, index) in images" :key="index" class="gallery-item">
        <img :src="image.url" @click="openModal(index)" />
      </div>
    </div>
    <modal :images="images" :is-open="modalIsOpen" :current-index="currentIndex" @close-modal="closeModal" @previous-image="previousImage" @next-image="nextImage"></modal>
  </div>
</template>

<script>
import Modal from './ImageGalleryModal.vue';

export default {
  components: {
    Modal,
  },
  data() {
    return {
      galleryTitle: 'My Photo Gallery',
      images: [
        { url: 'path/to/image1.jpg' },
        { url: 'path/to/image2.jpg' },
        { url: 'path/to/image3.jpg' },
      ],
      modalIsOpen: false,
      currentIndex: 0,
    };
  },
  methods: {
    openModal(index) {
      this.currentIndex = index;
      this.modalIsOpen = true;
    },
    closeModal() {
      this.modalIsOpen = false;
    },
    previousImage() {
      this.currentIndex--;
      if (this.currentIndex < 0) {
        this.currentIndex = this.images.length - 1;
      }
    },
    nextImage() {
      this.currentIndex++;
      if (this.currentIndex > this.images.length - 1) {
        this.currentIndex = 0;
      }
    },
  },
};
</script>

<style scoped>
.gallery {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.gallery-header {
  margin-bottom: 20px;
}

.gallery-content {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.gallery-item {
  margin: 10px;
  cursor: pointer;
}

img {
  max-width: 100%;
  height: auto;
}

</style>
