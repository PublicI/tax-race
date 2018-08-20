<template>
    <section class="charts">
        <div v-for="chart in charts" class="chart">
            <highcharts :options="chart"></highcharts>
        </div>
    </section>
</template>

<script>
import { Chart } from 'highcharts-vue';
// import clone from 'lodash.clonedeep';

export default {
    props: {
        series: Array,
        type: String,
        categories: Array,
        stacked: Boolean,
        grid: Boolean,
        suffix: String,
        colors: Array,
        title: String,
        subtitle: String
    },
    computed: {
        charts() {
            if (!this.categories || !this.series) {
                return [];
            }

            let options = {
                colors: this.colors || [
                    '#427aa8',
                    '#fa8e1c',
                    '#e95b54',
                    '#6db6b2',
                    '#519e4b',
                    '#f3c73e',
                    '#b37ca1'
                ],
                chart: {
                    backgroundColor: null,
                    type: this.type,
                    // height: 140,
                    // paddingLeft: -10,
                    style: {
                        fontFamily: 'tablet-gothic-narrow'
                    }
                },
                xAxis: {
                    tickLength: 0,
                    align: 'right',
                    title: {
                        text: null
                    },
                    labels: {
                        // enabled: false,
                        reserveSpace: true,
                        allowOverlap: true,
                        // step: 1,
                        style: {
                            fontSize: '12.5px',
                            color: '#383838'
                        }
                    },
                    categories: this.categories
                },
                yAxis: {
                    // tickInterval: 15,
                    gridLineWidth: this.type !== null ? 0 : 1,
                    title: {
                        text: null
                    },
                    labels: {
                        format: '{value}%', // %
                        enabled: this.type === null
                    }
                },
                legend: {
                    enabled: true,
                    itemHoverStyle: {
                        color: '#333333',
                        cursor: 'initial'
                    }
                },
                tooltip: {
                    enabled: false
                },
                credits: {
                    enabled: false
                },
                title: {
                    text: this.title,
                    align: 'left',
                    style: {
                        fontSize: '17px',
                        fontWeight: 'bold'
                        // color: '#666'
                    }
                },
                subtitle: {
                    text: this.subtitle,
                    align: 'left',
                    style: {
                        fontSize: '15px',
                        color: '#666'
                    }
                },
                plotOptions: {
                    bar: {
                        dataLabels: {
                            enabled: true
                        },
                        stacking: this.stacked ? 'normal' : null
                    },
                    column: {
                        dataLabels: {
                            enabled: true
                        },
                        stacking: this.stacked ? 'normal' : null
                    },
                    line: {
                        marker: {
                            symbol: 'circle'
                        }
                    },
                    series: {
                        events: {
                            legendItemClick() {
                                return false;
                            }
                        },
                        // pointWidth: 11,
                        // color: '#3D7FA6',
                        states: {
                            hover: {
                                enabled: false
                            }
                        }
                    }
                },
                series: this.series
            };

            // let options = clone(this.chartOptions);

            return [options];
        }
    },
    components: {
        highcharts: Chart
    }
};
</script>

<style scoped>
</style>
