<template>
    <section>
        <highcharts :options="chartOptions"></highcharts>
    </section>
</template>

<script>
import { Chart } from 'highcharts-vue';

export default {
    data() {
        return {
            chartOptions: {
                series: [
                    {
                        data: [1, 2, 3] // sample data
                    }
                ]
            }
        };
    },
    components: {
        highcharts: Chart
    },
    head() {
        return {
            title: 'examples'
        };
    }
};
</script>

<style scoped>
.examples {
    list-style: none;
    margin: 0;
    padding: 0;
}
.example {
    margin: 10px 0;
}
</style>
