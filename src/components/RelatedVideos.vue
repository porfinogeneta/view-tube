<template>
  <SearchResults v-if="relatedResults" :results="relatedResults"/>
</template>

<script>
import SearchResults from "@/components/SearchResults";
export default {
  name: "RelatedVideos",
  components: {SearchResults},
  props: {
    id: String
  },
  async mounted() {
    // dane o filmach, które są powiązane z tym
    await this.$store.dispatch('getListOfMovies', { link: `https://youtube.googleapis.com/youtube/v3/search?part=snippet&relatedToVideoId=${this.currentID}&type=video&key=${this.$store.state.API_key}`})
  },
  computed: {
    currentID() {
      return this.id
    },
    // powiązane filmy, ale wyrzucenie pobrango wcześniej filmu aktualnie oglądanego
    relatedResults() {
      return this.$store.state.movies.filter(film => film.id !== this.currentID)
    }
  }
}
</script>

<style scoped>

</style>