<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="9">
        <v-text-field
          v-model="searchMovie"
          label="Pretraži recenzije filmova"
          prepend-inner-icon="mdi-magnify"
          solo
          @input="filterMovies"
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="3">
        <v-select
          v-model="author"
          :items="authors"
          label="Filtriraj po autoru"
          solo
          @change="filterByAuthor"
        ></v-select>
      </v-col>
    </v-row>

    <v-row>
      <v-col v-for="review in paginatedMovies" :key="review._id" cols="12" sm="6" class="d-flex align-center">
        <v-card class="mx-auto my-2">
          <v-img
            :src="getImageUrl(review)"
            class="card-img"
          ></v-img>

          <v-card-title>{{ review.headline.main }}</v-card-title>

          <v-card-subtitle>{{ review.byline.original }}</v-card-subtitle>

          <v-card-text>
            <p>{{ review.snippet }}</p>
          </v-card-text>

          <v-card-actions>
            <v-btn :href="review.web_url" target="_blank" color="primary" text>
              Pročitaj Više
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <v-pagination
          v-model="page"
          :length="totalPages"
          @input="updatePaginatedMovies"
          rounded="circle"
        ></v-pagination>
      </v-col>
    </v-row>

    <v-row class="d-flex justify-center">
  <v-col cols="auto">
    <v-btn @click="openReviewForm" color="primary" class="mt-4">Dodaj Novu Recenziju</v-btn>
  </v-col>
</v-row>
    <ReviewForm ref="reviewForm" />
  </v-container>
</template>

<script>
import ReviewForm from '@/components/ReviewForm.vue';
import axios from 'axios';

export default {
  name: "HomeView",
  components: {
    ReviewForm,
  },
  data() {
    return {
      reviews: [],
      filteredMovies: [],
      paginatedMovies: [],
      authors: [], 
      author: null, 
      perPage: 4,
      page: 1,
      searchMovie: "",
    };
  },
  watch: {
    filteredMovies() {
      this.page = 1;
      this.updatePaginatedMovies();
    },
    page() {
      this.updatePaginatedMovies();
    }
  },
  computed: {
    totalPages() {
      return Math.ceil(this.filteredMovies.length / this.perPage);
    },
  },
  created() {
    this.getMovieReviews();
  },
  methods: {
    getMovieReviews() {
      const apiKey = 'VpWgHfUegfwE9Gn8coe5ARWU8W1pIULk';
      const url = `https://api.nytimes.com/svc/search/v2/articlesearch.json?fq=section_name:%22Movies%22%20AND%20type_of_material:%22Review%22&sort=newest&page=0&api-key=${apiKey}`;

      axios.get(url)
        .then((response) => {
          this.reviews = response.data.response.docs;
          this.filteredMovies = this.reviews;
          this.authors = [...new Set(this.reviews.map(review => review.byline.original))]; 
          this.updatePaginatedMovies();
        })
        .catch((error) => {
          console.error("Error fetching movie reviews:", error);
        });
    },
    getImageUrl(review) {
      if (review.multimedia && review.multimedia.length > 0) {
        return `https://www.nytimes.com/${review.multimedia[0].url}`;
      }
      return null;
    },
    filterMovies() {
      const searchMovieLower = this.searchMovie.toLowerCase();
      this.filteredMovies = this.reviews.filter((review) =>
        review.headline.main.toLowerCase().includes(searchMovieLower)
      );
      if (this.author) {
        this.filterByAuthor(); 
      }
    },
    filterByAuthor() {
      if (this.author) {
        this.filteredMovies = this.reviews.filter((review) =>
          review.byline.original === this.author
        );
      } else {
        this.filteredMovies = this.reviews;
      }
      this.updatePaginatedMovies();
    },
    updatePaginatedMovies() {
      const start = (this.page - 1) * this.perPage;
      const end = this.page * this.perPage;
      this.paginatedMovies = this.filteredMovies.slice(start, end);
    },
    openReviewForm() {
      this.$refs.reviewForm.modal = true;
    },
  },
};
</script>

<style scoped>
.text-center {
  text-align: center;
}

.card-img {
  height: 300px;
  width: 100%;
}
</style>
