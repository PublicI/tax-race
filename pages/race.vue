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
import raceBrackets from '~/assets/cpshouseholdincome.csv';
import Chart from '~/components/Chart.vue';

export default {
    data() {
        const chartTitles = {
            'White alone Non Hispanic': 'White',
            'Totals Hispanic': 'Hispanic',
            'Black or African American alone Non Hispanic': 'Black',
            'Asian alone Non Hispanic': null,
            'Totals Totals': null,
            'Totals Non Hispanic': null,
            'American Indian and Alaska Native alone Non Hispanic': null,
            'Native Hawaiian and Other Pacific Islander alone Non Hispanic': null,
            'Two or more races Non Hispanic': null
        };

        const raceCategories = Object.keys(raceBrackets[0])
            .filter(cat => ['', 'Race', 'Hispanic origin'].indexOf(cat) === -1)
            .map(cat => cat.replace(' pct', ''));

        const raceSeries = raceBrackets
            .map(row => {
                return {
                    name: chartTitles[`${row.Race} ${row['Hispanic origin']}`],
                    data: raceCategories.map(cat => row[`${cat} pct`] * 100)
                };
            })
            .filter(s => s.name);

        raceSeries.splice(1, 0, raceSeries.shift());

        let raceChart = {
            title: 'White people more likely to be wealthy',
            subtitle: 'Percent of race and ethnic groups by income level',
            type: null,
            series: raceSeries,
            categories: raceCategories,
            colors: [
                '#e95b54',
                '#fa8e1c',
                '#427aa8',
                '#6db6b2',
                '#519e4b',
                '#f3c73e',
                '#b37ca1'
            ]
        };

        return {
            groups: [
                {
                    charts: [raceChart]
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
