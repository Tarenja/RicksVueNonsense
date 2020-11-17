<template>
  <div>
    <h1>Rick's Biographical Nonsense</h1>
    <div class="pagination">
      <p v-if="previousPage" @click="$emit('previous-page')">Previous</p>
      <p
        class="pagination__number"
        :class="{ selected: i === currentPage }"
        v-for="i in totalPages"
        :key="i"
        @click="$emit('select-page', i)"
      >
        {{ i }}
      </p>
      <p v-if="nextPage" @click="$emit('next-page')">Next</p>
    </div>
    <div class="characters" v-if="characters">
      <div
        class="character"
        v-for="character in characters"
        :key="character.id"
      >
        <img v-if="character.image" :src="character.image" />
        <h2 v-if="character.name">{{ character.name }}</h2>
        <div class="character__stats">
          <p v-if="character.gender"><b>Gender:</b> {{ character.gender }}</p>
          <p v-if="character.species">
            <b>Species:</b> {{ character.species }}
          </p>
          <p v-if="character.type"><b>Type:</b> {{ character.type }}</p>
          <p v-if="character.status"><b>Status:</b> {{ character.status }}</p>
        </div>
        <div class="character__origin-location">
          <h3 v-if="character.origin.url">Origin</h3>
          <template v-for="location in locations" :key="location.id">
            <div v-if="character.origin.name === location.name">
              <p><b>Name:</b> {{ location.name }}</p>
              <p><b>Type:</b> {{ location.type }}</p>
              <p><b>Dimension:</b> {{ location.dimension }}</p>
              <p><b>Residents known:</b> {{ location.residents.length }}</p>
            </div>
          </template>
          <h3 v-if="character.location.url">Current Location</h3>
          <template v-for="location in locations" :key="location.id">
            <div v-if="character.location.name === location.name">
              <p><b>Name:</b> {{ location.name }}</p>
              <p><b>Type:</b> {{ location.type }}</p>
              <p><b>Dimension:</b> {{ location.dimension }}</p>
              <p><b>Residents seen:</b> {{ location.residents.length }}</p>
            </div>
          </template>
        </div>
        <ul class="character__episodes" v-if="character.episode">
          <h3><b>Seen in episodes:</b></h3>
          <template v-for="episode in episodes" :key="episode.id">
            <li v-if="character.episode.includes(episode.url)">
              <p>{{ episode.id }}. {{ episode.name }}</p>
            </li>
          </template>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterList",
  props: [
    "characters",
    "episodes",
    "locations",
    "totalPages",
    "nextPage",
    "previousPage",
    "currentPage",
  ],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2,
h3 {
  font-family: "Get Schwifty";
  text-align: center;
}

.pagination {
  text-align: center;
  padding: 3rem;
}

.pagination p {
  display: inline-block;
  width: fit-content;
  height: 2.5rem;
  box-sizing: border-box;
  margin: 0.3rem;
  padding: 0.6rem 0.3rem 0.3rem;
  border-radius: 3px;
}

p.pagination__number {
  width: 2.5rem;
}

.pagination__number.selected {
  background-color: #e5f1f0;
}

.pagination p:hover {
  cursor: pointer;
  background-color: #b9e6e2;
}

.characters {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  grid-gap: 2rem;
}

.character {
  background-color: #e5f1f0;
  border: 1px solid black;
  border-radius: 3px;
  margin: 1rem;
  padding: 1.5rem;
  text-align: center;
}

img {
  border-radius: 3px;
}

.character__stats,
.character__origin-location {
  text-align: left;
}

.character__episodes {
  list-style: none;
  text-align: left;
}
</style>
