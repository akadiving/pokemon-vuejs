<template>
  <v-container>
    <v-row class="text-center">
      <v-col 
      cols="12"
      xl="2"
      lg="3"
      md="4"
      sm="6"
      xs="12"
      v-for="(pokemon, index) in pokemons"
      :key="index"
      >
        <v-card 
        class="pa-2 rounded"
        outlined
        tile
        hover
        v-if="pokemonUrl[index] && imageUrl"
        @click="setPokemonUrl(pokemon.url)"
        color="#AA5935"
        dark
        >
          <v-img
            :src="imageUrl + pokemonUrl[index] + '.png'"
            class="my-3"
            contain
            height="200"
          />
          <v-card-title class="justify-center" v-if="pokemon.name">
            {{pokemon.name}}
          </v-card-title>
        </v-card>
      </v-col>
    
      <v-col
      cols="12"
      xl="2"
      lg="3"
      md="4"
      sm="6"
      xs="12"
      class="justify-center"
      align-self="center"
      >
        <v-container>
          <v-row class="justify-center">
            <v-col>
              <v-progress-circular
                :size="70"
                :width="7"
                color="#AA5935"
                indeterminate
              ></v-progress-circular>
            </v-col>
          </v-row>
        </v-container> 
      </v-col>
    </v-row>
    <div v-if="pokemons.length" v-observe-visibility="scroll"></div>

  </v-container>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'List',
    components: {

    },
    props: {
      imageUrl: String,
      apiUrl: String,
    },

    data: () => {
      return{
        pokemons: [],
        pokemonUrl: [],
        currentUrl: '',
      }
    },

    methods: {
      scroll(isVisible) {
        if (!isVisible) {
          return
        }
        this.next()
      },
      setPokemonUrl(url) {
        this.$emit('setPokemonUrl', url);
      },
      next(){
        this.load = true;
        this.fetchData();
      },
      
      
      
      fetchData(){
        axios.get(this.currentUrl)
        .then(response => {  
          for (let i = 0; i < response.data.results.length; i++){
            this.pokemons.push(response.data.results[i]) 
            this.pokemonUrl.push(response.data.results[i].url.split('/')[response.data.results[i].url.split('/').length-2])
          }
          this.currentUrl = response.data.next
          this.load = false;
          
        })
        .catch(err => {
          console.log(err);
        });
      },
    },
      
    created(){
      this.currentUrl = this.apiUrl;
      this.fetchData();
    },
    mounted(){
      this.scroll();
    }
  }
</script>
<style scoped>
.dark-card{
  color: rgba(241, 195, 195, 0.76);
}
.v-progress-circular {
  margin: 1rem;
}
</style>