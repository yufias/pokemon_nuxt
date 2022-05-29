<template>
    <div class="container mx-auto p-4 mb-4">
        <div class="flex justify-center">
            <button type="button" class="bg-blue-600 p-3 rounded-lg text-white hover:bg-blue-700" @click="getPokemon">Generate</button>
        </div>
        <div class="flex justify-center items-center mt-4" v-if="loading">
            <div class="border border-blue-300 shadow rounded-md p-4 max-w-xl w-full mx-auto">
                <div class="animate-pulse flex space-x-4">
                    <div class="rounded-sm bg-gray-500 h-20 w-20"></div>
                    <div class="flex-1 space-y-6 py-1">
                        <div class="h-2 bg-gray-500 rounded"></div>
                        <div class="h-2 bg-gray-500 rounded"></div>
                        <div class="h-2 bg-gray-500 rounded"></div>
                        <div class="space-y-3">
                            <div class="grid grid-cols-3 gap-4">
                                <div class="h-2 bg-gray-500 rounded col-span-2"></div>
                                <div class="h-2 bg-gray-500 rounded col-span-1"></div>
                            </div>
                            <div class="h-2 bg-gray-500 rounded"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex justify-center" v-else>
            <PokemonCard 
                :name="name"
                :image="image"
                :types="types"
                :abilities="abilities"
                :height="height"
                :weight="weight"
                :color="color"
                :egg_groups="egg_groups"
                :stats="stats"
            />
        </div>
    </div>
</template>

<script>
import PokemonCard from '../PokemonCard'
import axios from 'axios'

export default {
    name: 'RandomSection',
    components: { PokemonCard },
    data () {
        return {
            name: '',
            image: '',
            types: [],
            abilities: [],
            loading: true,
            height: 0,
            weight: 0,
            color: '',
            egg_groups: [],
            stats: [
                ['Stats Detail', 'Hp', 'Attack', 'Defence', 'Special-Attack', 'Special-Defence', 'Speed'],
            ]
        }
    },
    created() {
        this.getPokemon()
    },
    methods: {
        async getPokemon() {
            this.loading = true
            const randomId = Math.floor(Math.random() * 898) + 1; // Returns a random integer from 1 to 898, 899++ not found:
            const pokemon = await axios.get(`https://pokeapi.co/api/v2/pokemon/${randomId}/`)
            const response  = pokemon.data
            const species = await axios.get(response.species.url)
            const speciesResponse = species.data

            this.name = response.name
            this.image = response.sprites.front_default
            this.types = response.types.map(el => el.type.name)
            this.abilities = response.abilities.map(el => el.ability.name)
            this.height = response.height
            this.weight = response.weight
            this.color = speciesResponse.color.name
            this.egg_groups = speciesResponse.egg_groups.map(el => el.name)
            const statsDetail = response.stats.map(el => el.base_stat)
            
            //Set up the format for data bar cart
            const temp2 = ['stats'].concat(statsDetail)
            this.stats.push(temp2)
            this.loading = false

            console.log(this.stats)
            

            // console.log(speciesResponse, "====")
            console.log(response, "====")
        }
    },
}
</script>

<style>

</style>