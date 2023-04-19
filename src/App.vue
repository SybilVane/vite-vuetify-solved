<script>
import axios from 'axios';
import FavDogCard from './components/FavDogCard.vue'
export default {
  components: {
    FavDogCard
  },
  data() {
    return {
      currentDogLink: "https://images.dog.ceo/breeds/chihuahua/n02085620_3407.jpg",
      favoriteDogs: [],
    };
  },
  methods: {
    loadNewDog() {
      axios
          .get("https://dog.ceo/api/breeds/image/random")
          .then(response => {
            this.currentDogLink = response.data.message;
          })
          .catch(error => {
            console.log(error);
          });
    },
    addToFavorites() {
      this.favoriteDogs.push(this.currentDogLink)
    },
    removeFromFavorites(index) {
      this.favoriteDogs.splice(index, 1)
    },
  },
  computed: {
    isAlreadyInFavorites() {
      return this.favoriteDogs.includes(this.currentDogLink)
    },
  },
  created() {
    this.loadNewDog()
  }
};
</script>

<template>
  <v-app>
    <v-main class="dogs-layout">
      <v-container fill-height>
        <div class="dogs-overlay">
          <h1 class="display-2 text-xs-center">Choose your favorite dogs</h1>
          <v-card class="dog-card">
            <v-img height="400px" :src="currentDogLink"/>
            <v-card-actions>
              <v-spacer/>
              <v-btn icon :disabled="isAlreadyInFavorites">
                <span class="material-icons" @click="addToFavorites">favorite</span>
              </v-btn>
              <v-btn icon @click="loadNewDog">
                <span class="material-icons">forward</span>
              </v-btn>
            </v-card-actions>
          </v-card>
          <v-container grid-list-md fluid>
            <v-row>
              <v-col cols="3" v-for="(pet, index) in favoriteDogs">
                <FavDogCard :dog-image-src="pet" @remove="removeFromFavorites(index)"/>
              </v-col>
            </v-row>
          </v-container>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>


<style>
img {
  max-width: 100%;
}

h1 {
  padding-bottom: 15px;
}

.dogs-layout {
  width: 100%;
  background: #fff url("https://github.com/FrontEndFoxes/projects/blob/main/petshop/images/bg3.jpg?raw=true") repeat center;
}

.dogs-overlay {
  width: 100%;
  padding: 20px;
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
}

@media (max-width: 768px) {
  .dogs-overlay {
    margin: 0;
  }
}

.dog-card {
  width: 100%;
  max-width: 600px;
}

.material-icons {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;  /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: 'liga';
}
</style>
