<template>
    <section>
        <highcharts :options="chartOptions"></highcharts>
    </section>
</template>

<script>
import data from '~/assets/indexed-means.json';
import { Chart } from 'highcharts-vue';
import Highcharts from 'highcharts';

export default {
    methods: {
        makeDates(floatArr) {
            let tar = [];
            for (let i = 0; i < floatArr.length; i++) {
                tar[i] = Date.UTC(floatArr[i], 0, 1);
            }
            return tar;
        },
        makeSeries(mydata) {
            const tar = [];
            let seriesI = {};
            seriesI.name = 'National average';
            seriesI.data = mydata.data[0];
            seriesI.pointStart = Date.UTC(2008, 0, 1);
            seriesI.pointIntervalUnit = 'year';
            seriesI.marker = { symbol: 'circle' }; //  radius: 2
            tar.push(seriesI);
            return tar;
        }
    },
    data() {
        let dSeries = this.makeSeries(data);
        return {
            chartOptions: {
                chart: {
                    marginLeft: 50,
                    fontFamily: 'tablet-gothic-narrow'
                },
                colors: ['#3D7FA6'],
                credits: {
                    enabled: false
                },
                plotOptions: {
                    series: {
                        lineWidth: 3,
                        marker: {
                            radius: 3,
                            lineWidth: 1
                        },
                        states: {
                            hover: {
                                enabled: false
                            }
                        }
                    }
                },
                xAxis: {
                    gridLineWidth: 0.5,
                    max: Date.UTC(2016, 0, 1),
                    endOnTick: true,
                    labels: {
                        style: {
                            fontSize: '12px',
                            color: '#888'
                        }
                    },
                    type: 'datetime'
                },
                yAxis: {
                    title: {
                        text: ''
                    },
                    labels: {
                        formatter() {
                            return `${Highcharts.numberFormat(this.value, 0)}%`;
                        },
                        style: {
                            fontSize: '12px',
                            color: '#888'
                        }
                    },
                    plotLines: [
                        {
                            width: 0.5,
                            color: '#bebebe'
                        }
                    ]
                },
                tooltip: {
                    pointFormat: '{series.name}:<b>{point.y:.1f}%</b>',
                    crosshairs: false,
                    enabled: false
                },
                legend: {
                    enabled: false,
                    align: 'right',
                    verticalAlign: 'bottom',
                    borderWidth: 0
                },
                series: dSeries,
                title: {
                    text: '<b>... and Medicaid spending is increasing</b>',
                    align: 'left',
                    style: {
                        color: '#666'
                    }
                },
                subtitle: {
                    text:
                        'Percentage of total state spending on Medicaid, including federal assistance',
                    align: 'left',
                    style: {
                        fontSize: '15px',
                        color: '#666'
                    }
                }
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
