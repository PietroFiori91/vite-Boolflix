<script>
export default {
  props: {
    movie: Object,
  },
};
</script>

<template>
  <div class="col-md-4 mb-3">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ movie.title }}</h5>
        <p class="card-text">Titolo Originale: {{ movie.original_title }}</p>
        <p class="card-text">Lingua: {{ movie.original_language }}</p>
        <p class="card-text">Voto: {{ movie.vote_average }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
