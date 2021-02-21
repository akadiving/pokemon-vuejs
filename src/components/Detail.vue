<template>
    <div class="background">
        <v-container>
            <v-row class="justify-center" dense>
                <v-col cols="11">
                    <!-- pokemon card with the list of stats -->
                    <v-card v-if="show"
                        color="#273C43"
                    >
                        <v-card-title class="justify-center white--text pt-6" >
                            {{pokemon.name}}
                        </v-card-title>

                        <v-container>
                            <v-row class="justify-center" no-gutters>
                                <v-col 
                                    cols="auto"
                                    
                                    >
                                    <v-list dense color="#273C43">
                                        
                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-sword
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                atc {{pokemon.stats[1].base_stat}}
                                            </v-chip>
                                        </v-list-item>

                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-shield
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                def {{pokemon.stats[2].base_stat}}
                                            </v-chip>
                                        </v-list-item>

                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-sparkles
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                spec-atc {{pokemon.stats[3].base_stat}}
                                            </v-chip>
                                        </v-list-item>

                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-shield-star
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                spec-def {{pokemon.stats[4].base_stat}}
                                            </v-chip>
                                        </v-list-item>
                                    </v-list>

                                </v-col>

                                <v-col 
                                    cols="auto"
                                    >
                                    <v-list color="#273C43" dense>
                                        
                                        <v-list-item dark>
                                            <v-chip
                                                color="white"
                                                outlined
                                                >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-heart
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                hp {{pokemon.stats[0].base_stat}}
                                            </v-chip>
                                        </v-list-item>
                                    
                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-weight-kilogram
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                {{pokemon.weight / 10 }} kg
                                            </v-chip>
                                        </v-list-item>
 
                                        <v-list-item dark>
                                            <v-chip
                                            color="white"
                                            outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-human-male-height
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                {{pokemon.height / 10 }} m
                                            </v-chip>
                                        </v-list-item>
                                        
                                        <v-list-item dark>
                                            <v-chip
                                                color="white"
                                                outlined
                                            >
                                                <v-list-item-avatar>
                                                    <v-icon dark>
                                                        mdi-run-fast
                                                    </v-icon>
                                                </v-list-item-avatar>
                                                speed {{pokemon.stats[5].base_stat}}
                                            </v-chip>
                                        </v-list-item>

                                    </v-list>
                                </v-col>

                                <v-col 
                                    cols="8"
                                    xl="6"
                                    lg="6"
                                    md="6"
                                    sm="12"
                                    xs="12"
                                    order="first"
                                    >
                                    <v-img
                                        :src="pokemonImage"
                                        contain
                                        height="250"
                                        dark
                                    />
                                </v-col>
                            </v-row>
                        </v-container>
                        
                        <v-btn elevation="2"
                        outlined
                        class="mx-2"
                        fab
                        dark
                        large
                        color="#273C43"
                        @click="closeDetail"
                        ><v-icon color="#ffffff" @click="closeDetail()">mdi-close</v-icon></v-btn>
                        <v-footer color="#273C43" class="mt-8"></v-footer>
                    </v-card>
                    <!-- pokemon card with the list of stats -->

                    <!-- card of not found pokemon -->
                    <v-card v-else
                        color="#273C43"
                    >
                        
                        <v-card-title class="justify-center white--text" >
                            There is no pokemon with the name "{{this.pokemonDetail.slice(34)}}"
                        </v-card-title>
                        <v-btn elevation="2"
                        outlined
                        class="mx-2"
                        fab
                        dark
                        large
                        color="#33334d"
                        @click="closeDetail"
                        ><v-icon color="#ffffff" @click="closeDetail">mdi-close</v-icon></v-btn>
                        <v-footer color="#33334d" c></v-footer>
                    </v-card>
                    <!-- card of not found pokemon -->
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Detail',
    props: {
        pokemonDetail: String,
        imageUrl: String, 
    },
    data: () =>{
        return {
            pokemon: {},
            pokemonUrl: '',
            pokemonImage: '',
            show: false,
        }
    },
    methods: {
        fetchData(){
            axios.get(this.pokemonDetail)
            .then(response => {  
                this.pokemon = response.data;
                this.pokemonImage = response.data.sprites.front_default
                this.show = true;
                console.log(this.pokemon)
                console.log(this.pokemon.name)
                console.log(this.pokemonImage)
                console.log(this.pokemonUrl)
            })
            .catch(err => {
            console.log(err);
            });
        },
        closeDetail(){
            this.$emit('closeDetail')
        }
    },
    created(){
        this.fetchData();
    }
}
</script>

<style scoped>

</style>