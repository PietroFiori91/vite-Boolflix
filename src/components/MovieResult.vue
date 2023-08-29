<script>
export default {
  props: {
    movie: Object,
  },
  data() {
    return {
      hover: false,
    };
  },
  methods: {
    getImageUrl(posterPath) {
      return `https://image.tmdb.org/t/p/w342${posterPath}`;
    },
    // BANDIERE ---> NON FUNZIONA
    getLanguageFlag(language) {
      const languageMap = {
        IT: {
          flag: "it",
          country: "Italia (IT)",
          URL: "https://flagsapi.com/IT/flat/64.png",
        },
        EN: {
          flag: "gb",
          country: "Inghilterra (GB)",
          URL: "https://flagsapi.com/GB/flat/64.png",
        },
        FR: {
          flag: "fr",
          country: "Francia (FR)",
          URL: "https://flagsapi.com/FR/flat/64.png",
        },
        DE: {
          flag: "de",
          country: "Germania (DE)",
          URL: "https://flagsapi.com/DE/flat/64.png",
        },
        ES: {
          flag: "es",
          country: "Spagna (ES)",
          URL: "https://flagsapi.com/ES/flat/64.png",
        },
        PT: {
          flag: "pt",
          country: "Portogallo (PT)",
          URL: "https://flagsapi.com/PT/flat/64.png",
        },
        JA: {
          flag: "jp",
          country: "Giappone (JP)",
          URL: "https://flagsapi.com/JP/flat/64.png",
        },
        ZH: {
          flag: "cn",
          country: "Cina (CN)",
          URL: "https://flagsapi.com/CN/flat/64.png",
        },
        AR: {
          flag: "sa",
          country: "Arabia Saudita (SA)",
          URL: "https://flagsapi.com/SA/flat/64.png",
        },
        RU: {
          flag: "ru",
          country: "Russia (RU)",
          URL: "https://flagsapi.com/RU/flat/64.png",
        },
      };

      if (languageMap[language]) {
        return `<img src="${languageMap[language].URL}"/>`;
      } else {
        return language;
      }
    },
    // 5 STAR REVIEW
    convertRatingToStars(rating) {
      const maxRating = 5;
      const numStars = Math.ceil(rating / 2);
      const fullStars = '<i class="fas fa-star"></i>'.repeat(numStars);
      const emptyStars = '<i class="far fa-star"></i>'.repeat(
        maxRating - numStars
      );
      return `${fullStars}${emptyStars}`;
    },
  },
};
</script>

<template>
  <div class="col-md-4 mb-3">
    <!-- WRAPPER PER TRANSITION :HOVER -->
    <div
      class="card-wrapper"
      @mouseover="hover = true"
      @mouseleave="hover = false"
    >
      <!-- CARD ORIGINALE -->
      <div class="card">
        <img :src="getImageUrl(movie?.poster_path)" class="card-img-top" />
      </div>

      <!-- INFO ON :HOVER -->
      <div class="movie-info-card" v-if="hover">
        <div class="movie-info">
          <h5 class="card-title">{{ movie.title || movie.name }}</h5>
          <p>
            Original Title:
            {{ movie.original_title || movie.original_name }}
          </p>
          <p>
            Language:
            {{ getLanguageFlag(movie.original_language) }}
          </p>
          <p class="card-text">
            Rating:
            <span v-html="convertRatingToStars(movie.vote_average)"></span>
          </p>
          <p class="card-text" v-if="hover">{{ movie.overview }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  transition: 0.3s;
}

.card-wrapper {
  position: relative;
  transition: 0.3s;
}

.card-wrapper:hover .card {
  opacity: 0;
}

.movie-info-card {
  display: none;
  position: absolute;
  top: 0;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 20px;
  z-index: 1; /* Ensure the movie info card is displayed above the original card */
}

.card-wrapper:hover .movie-info-card {
  display: block;
}
</style>
