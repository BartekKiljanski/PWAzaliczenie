<template>
  <div class="gallery-page">
    <div class="header">
      <h1>Witaj w mojej galerii w VUE</h1>
      <button class="back-btn" @click="goBack">&lt; Powrót</button>
    </div>
    <div class="search-bar">
      <input type="text" v-model="searchQuery" placeholder="Szukaj...">
    </div>
    <div class="gallery" :data-id="$route.params.id">
      <my-image v-for="(image, index) in images" :key="index" :src="image.thumbnail" :alt-text="image.altText" :index="index" @show-modal="openModal"/>
      <modal v-if="modalOpen" :src="images[selectedImageIndex].src" :alt="images[selectedImageIndex].altText" :current-index="selectedImageIndex" @close-modal="closeModal" @change-image="changeImage"/>
      <img v-for="(value) in dataArr" :key="value.data[0].nasa_id" :src="value.links[0].href" style="width: 100%; height: 100%; cursor: pointer; transition: transform 0.3s ease;" @click="openModal(value.data[0].nasa_id)"/>
    </div>
    <lightbox v-if="lightboxOpen" :images="lightboxImages" :index="lightboxIndex" @close="closeLightbox"></lightbox>
  </div>
</template>

<script>
import MyImage from './MyImage.vue';
import Modal from './Modal.vue';
import Lightbox from './Lightbox.vue';
import axios from "axios";

export default {
  components: {
    MyImage,
    Modal,
    Lightbox
  },
  created() {
    this.fetchData()
  },
  data() {
    return {
      images: [
        {
          thumbnail: 'https://placeimg.com/400/400/animals/grayscale',
          src: 'https://placeimg.com/800/800/animals',
          altText: 'Animals'
        },
        {
          thumbnail: 'https://placeimg.com/400/400/architecture/grayscale',
          src: 'https://placeimg.com/800/800/architecture',
          altText: 'Architecture'
        },
        {
          thumbnail: 'https://placeimg.com/400/400/people/sepia',
          src: 'https://placeimg.com/800/800/people',
          altText: 'People'
        },
        {
          thumbnail: 'https://placeimg.com/400/400/tech/grayscale',
          src: 'https://placeimg.com/800/800/tech',
          altText: 'Tech'
        },
        {
          thumbnail: 'https://placeimg.com/400/400/nature',
          src: 'https://placeimg.com/800/800/nature/sepia',
          altText: 'Nature'
        }
      ],
      modalOpen: false,
      selectedImageIndex: 0,
      dataArr: [],
      searchQuery: '',
      lightboxOpen: false,
      lightboxIndex: 0,
      lightboxImages: []
    };
  },
  computed: {
    filteredImages() {
      return this.images.filter(image => {
        return image.altText.toLowerCase().includes(this.searchQuery.toLowerCase());
      });
    }
  },
  methods: {
    openModal(index) {
      this.modalOpen = true;
      this.selectedImageIndex = index;
    },
    closeModal() {
      this.modalOpen = false;
    },
    changeImage(index) {
      this.selectedImageIndex = index;
    },
    goBack() {
      this.$router.push('/');
    },
    async fetchData() {
      await axios.get('https://images-api.nasa.gov/search?q=sun')
        .then(res => {
          this.dataArr = res.data.collection.items;
        })
        .catch(error => {
          console.log(error)
        })
    },
    openLightbox(index) {
      this.lightboxOpen = true;
      this.lightboxIndex = index;
      this.lightboxImages = this.dataArr.map(value => value.links[0].href);
    },
    closeLightbox() {
      this.lightboxOpen = false;
      this.lightboxIndex = 0;
      this.lightboxImages = [];
    }
  }
};
</script>

<style>
/* Stylizacja dla galerii */
.gallery-page {
  background-color: #f2f2f2;
}

.header {
  background-color: #333;
  color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
}

.header h1 {
  margin: 0;
}

.back-btn {
  background-color: #555;
  border: none;
  color: #fff;
  padding: 0.5rem 1rem;
  cursor: pointer;
}

.back-btn:hover {
  background-color: #777;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 20px;
  padding: 1rem;
}

.gallery img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.gallery img:hover {
  transform: scale(1.1);
}

/* Stylizacja dla lightboxa */
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
  z-index: 9999;
}

.lightbox-content {
  position: relative;
  max-width: 90%;
  max-height: 90%;
}

.lightbox-content button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 3rem;
  color: #fff;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.lightbox-content .close {
  right: 10%;
}

.lightbox-content .prev {
  left: 10%;
}

.lightbox-content .next {
  right: 10%;
}

.lightbox-content img {
  max-width: 100%;
  max-height: 100%;
}
</style>

   
