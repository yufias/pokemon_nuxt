<template>
    <div class="rounded-lg mt-3 p-4 flex flex-col border-2 w-1/2">
        <div class="flex justify-center w-full">
            <h1 class="text-heading-4 font-bold font-label">{{ name.toUpperCase() }}</h1>
        </div>
        <div class="flex justify-between">
            <div class="flex flex-col w-1/2">
                <figure className="relative rounded-full overflow-hidden mr-3 w-96">
                    <img
                        :src="image"
                        alt="photo"
                        class="w-full"
                    />
                </figure>
            </div>
            <div class="flex flex-col w-1/2 p-2 justify-center gap-2">
                <span>Types: {{ types.toString() }}</span>
                <span>Abilities: {{ abilities.toString() }}</span>
                <span>Height: {{ height }}</span>
                <span>Weight: {{ weight }}</span>
                <span>Color: {{ color }}</span>
                <span>Egg Groups: {{ egg_groups.toString() }}</span>
            </div>
        </div>
        <div class="flex flex-col items-center h-96">
            <h1>Stats</h1>
            <GChart
                type="ColumnChart"
                :settings="{packages: ['bar']}"
                :data="chartData"
                :options="chartOptions"
                :resizeDebounce="500"
                :createChart="(el, google) => new google.charts.Bar(el)"
                @ready="onChartReady"
            />
        </div>
    </div>
</template>

<script>
import { GChart } from 'vue-google-charts/legacy'

export default {
    name: 'PokemonCard',
    components: {
        GChart
    },
    props: ['name', 'image', 'types', 'abilities', 'height', 'weight', 'color', 'egg_groups', 'stats'],
    data() {
        return{
            chartData: this.stats,
            chartOptions: {
                chart: {
                    title: 'Pokemon Stats',
                },
                bars: 'vertical',
                hAxis: { format: 'decimal' },
                height: 300,
                width: 550
            }
        }
    },
    methods: {
        onChartReady (chart, google) {
            this.chartsLib = google
        },
    }
}
</script>

<style>

</style>