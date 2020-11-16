<template>
 <CharacterList :characters="characters" :episodes="episodes" :locations="locations" />
</template>

<script>
import CharacterList from './components/CharacterList.vue'

export default {
  name: 'App',
  components: {
    CharacterList
  },
  data() {
    return {
      characters: [],
      currentPage: 1,
      nextPage: "",
      previousPage: "",
      episodes: [],
      locations: []
    }
  },
  created() {
    this.getAllEpisodes();
    this.getAllLocations();
    this.getInfoFromRicksApi("https://rickandmortyapi.com/api/character/").then(response => {
      this.setCharactersAndPages(response)
    });
  },
  methods: {
    async getInfoFromRicksApi(url) {
      const response = await fetch(url)
      const json = await response.json();
      return json;
    },
    setCharactersAndPages(info) {
      this.characters = info.results;
      this.nextPage = info.info.next;
      this.previousPage = info.info.prev;
    },
    getAllEpisodes() {
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/episode/").then(res => {
        this.episodes = res.results;
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/episode/?page=2").then(res => {
        this.episodes = this.episodes.concat(res.results);
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/episode/?page=3").then(res => {
        this.episodes = this.episodes.concat(res.results);
      })
    },
    getAllLocations() {
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/location/").then(res => {
        this.locations = res.results;
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/location/?page=2").then(res => {
        this.locations = this.locations.concat(res.results);
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/location/?page=3").then(res => {
        this.locations = this.locations.concat(res.results);
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/location/?page=4").then(res => {
        this.locations = this.locations.concat(res.results);
      })
      this.getInfoFromRicksApi("https://rickandmortyapi.com/api/location/?page=5").then(res => {
        this.locations = this.locations.concat(res.results);
      })
      let temp = [...new Set(this.locations)]
      this.locations = temp;
    }
  },
}
</script>

<style>

@font-face {
    font-family: 'Get Schwifty';
    src: url('./assets/GetSchwifty-Regular.eot');
    src: url('./assets/GetSchwifty-Regular.eot?#iefix') format('embedded-opentype'),
        url('./assets/GetSchwifty-Regular.woff2') format('woff2'),
        url('./assets/GetSchwifty-Regular.woff') format('woff'),
        url('./assets/GetSchwifty-Regular.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
}


#app {
  font-family: 'Goldman', cursive, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>
