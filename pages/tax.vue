<template>
    <section class="charts">
        <div v-for="group in groups" class="group">
            <h2></h2>

            <div v-for="chart in group.charts" class="chart">
                <chart v-bind="chart"></chart>
            </div>
        </div>
    </section>
</template>

<script>
import taxBrackets from '~/assets/jcttaxcutsbyincomeovertime.csv';
import Chart from '~/components/Chart.vue';

export default {
    data() {
        const taxCategories = Object.keys(taxBrackets[0]).filter(
            cat => ['Year'].indexOf(cat) === -1
        );

        const taxSeries = taxBrackets
            .map(row => {
                return {
                    name: row.Year,
                    data: taxCategories.map(cat => row[cat] * 100)
                };
            })
            .filter(s => s.name !== '2018');

        let taxChart = {
            title: 'Wealthy get bigger breaks in tax cuts',
            subtitle: 'Reduction in average rate by income level',
            type: null,
            series: taxSeries,
            categories: taxCategories,
            colors: [
                '#6db6b2',
                '#519e4b',
                '#f3c73e',
                '#b37ca1'
            ]
        };

        return {
            groups: [
                {
                    charts: [taxChart]
                }
            ]
        };
    },
    components: {
        chart: Chart
    }
};
</script>

<style scoped>
/*
.group {
    float: left;
    width: 300px;
}
*/
</style>
