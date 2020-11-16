<template>
  <div>
    <h1>Rick's Biographical Nonsense</h1>
    <div v-if="characters">
        <div class="character" v-for="character in characters" :key="character.id">
            <img v-if="character.image" :src="character.image" />
            <h2 v-if="character.name">{{ character.name}}</h2>
            <div class="character__stats">
                <p v-if="character.gender">Gender: {{ character.gender }}</p>
                <p v-if="character.species">Species: {{ character.species }}</p>
                <p v-if="character.type">Type: {{ character.type }}</p>
                <p v-if="character.status">Status: {{ character.status }}</p>
            </div>
            <div class="character__origin-location">
                <h3>Origin</h3>
                    <template v-for="location in locations" :key="location.id">
                        <div v-if="character.origin.url === location.url">
                            <p>Name: {{ location.name }}</p>
                            <p>Type: {{ location.type }}</p>
                            <p>Dimension: {{ location.dimension }}</p>
                            <p>Residents seen: {{ location.residents.length }}</p>
                        </div>
                    </template>
                <h3>Current Location</h3>
                   <template v-for="location in locations" :key="location.id">
                        <div v-if="character.location.url === location.url">
                            <p>Name: {{ location.name }}</p>
                            <p>Type: {{ location.type }}</p>
                            <p>Dimension: {{ location.dimension }}</p>
                            <p>Residents seen: {{ location.residents.length }}</p>
                        </div>
                    </template>
            </div>
            <ul class="character__episodes" v-if="character.episode">
                <h3>Seen in episodes:</h3>
                <template v-for="episode in episodes" :key="episode.id">
                <li v-if="character.episode.includes(episode.url)">
                    <p>{{episode.name}}</p>
                </li>
                </template>
            </ul>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CharacterList',
  props: ["characters", "episodes", "locations"]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1, h2, h3 {
        font-family: 'Get Schwifty';
    }
</style>
