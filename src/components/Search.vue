<template>
    <v-container> 
        <v-row class="justify-center">
            <v-col cols="12">
                <v-text-field
                label="Pokemon..."
                outlined
                dense
                solo
                v-on:keydown.13="setPokemonUrl"
                v-model="searchValue"
                @submit.prevent="setPokemonUrl()"
                dark
                clearable
                >
                    <v-btn plain slot="append" @click="setPokemonUrl()">
                        <v-icon>mdi-pokeball</v-icon> 
                    </v-btn>
                </v-text-field>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    name: 'Search',
    props: {
        apiUrl: String,
        
    },

    data: () =>{
        return {
            searchValue: '',
        }
    },

    methods: {
        setPokemonUrl() {
            if(this.searchValue !== ''){
                this.$emit('setPokemonUrl', this.apiUrl + this.searchValue.toLowerCase())
            }
        },
    },
    mounted(){
        this.setPokemonUrl();
    }
}
</script>

<style scoped>

</style>