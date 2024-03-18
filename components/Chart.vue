<script setup lang="ts">
import  Chart from 'Chart.js/auto';

const labels = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'june',
];

const data = {
    labels: labels,
    datasets: [{
        label: 'My First datasets',
        backgroundColor: 'rgb(225, 99, 132)',
        borderColor: 'rgb(225, 99, 132)',
        data: [15, 10, 5, 2, 20, 30, 45],
    }]

};

const config = {
    type: 'bar',
    data: data,
    options: {}
};

onUnmounted(() => {
    const myChart = new Chart(
        document.getElementById('myChart'),
        config
    );
})
</script>

<template>
    <div>
        <canvas id="myChart"></canvas>
    </div>
</template>