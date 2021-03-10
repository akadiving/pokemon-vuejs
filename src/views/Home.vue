<template>
  <div class="home"
    :class="{ 'dark-mode': darkMode}"
  >
    <div class="search-bar" id='bar' v-bind:class="{homeblur: showDetail}">
      <v-container >
        <v-row class="justify-center" no-gutters style="padding-bottom: 0px;">
          <v-col cols="3"
            md="1"
            sm="1"
            xs="2"
            lg="1"
            xl="1"
            >
            <v-switch
              v-model="darkMode"
              inset
              append-icon="mdi-moon-waning-crescent"
              color="white"
            ></v-switch>
          </v-col>
          <v-col cols='12'
            md="11"
            sm="11"
            xs='12'
            lg="11"
            xl="11"
          >
            <Search 
              @setPokemonUrl="setPokemonUrl"
              :apiUrl="apiUrl"
            />
          </v-col>
        </v-row>
      </v-container>
    </div>
    <v-row justify="end">
      <v-fab-transition>
        <v-btn fab class="ma-0 pa-0" color="#273C43" @click="scrollUp()">
          <v-icon color="white">mdi-chevron-up</v-icon>
        </v-btn>
      </v-fab-transition>
    </v-row>
    <div class="detail" v-if="showDetail" >
      <Detail
      :pokemonDetail="pokemonDetail"
      :imageUrl="imageUrl"
      @closeDetail="closeDetail"
    />
    </div>
    
    <div v-bind:class="{homeblur: showDetail}">
      <List 
      :apiUrl="apiUrl"
      :imageUrl="imageUrl"
      :pokemonDetail='pokemonDetail'
      @setPokemonUrl='setPokemonUrl'
    />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import List from '@/components/List.vue'
import Detail from '@/components/Detail.vue'
import Search from '@/components/Search.vue'

export default {
  name: 'Home',
  components: {
    List,
    Detail,
    Search
  },
    data: () =>{
      return {
        imageUrl: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/`,
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
        showDetail: false,
        pokemonDetail: '',
        darkMode: false,
      }
  },
  methods: {
    // Set's pokemon url when you click on card
    setPokemonUrl(url) {
        this.closeDetail()
        this.pokemonDetail = url;
        this.showDetail = true;
        console.log(this.pokemonDetail)
      },

    // Method to close detail and remove specific URL from pokemonDetail
    closeDetail(){
      this.pokemonDetail = '';
      this.showDetail = false
    },
    scrollUp(){
      window.scrollTo({
        top: 0,
        left: 0,
        behavior: 'smooth'
      })
    },
    mounted(){
      this.scrollUp();
    }
  }
}
</script>
<style scoped>
.home{
  background-color: #EEEEC8;
}

.v-btn{
  top: 91vh;
  right: 1vw;
  position: fixed;
  z-index: 1;
}

.search-bar {
  top: 0px;
  position: sticky;
  z-index: 1;
  
}

.background {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  width: 100%;
  padding: 20px;
  text-align: center;
  height: 100vh;
  overflow: scroll;
}

.homeblur{
  filter: blur(5px);
}

.dark-mode{
  background-color: rgba(24, 23, 23, 0.959);
}

.detail{
  height: 100%;
  box-sizing: border-box;
}
</style>