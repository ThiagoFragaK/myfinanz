<template>
    <div>
        <apexchart
            type="line"
            :options="options"
            :series="series"
            height="350"
        />
    </div>
</template>

<script>
export default {
    props: {
        series: {
            type: Object,
            required: true,
        },
        options: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            optionsD: {
                chart: {
                    id: 'sales-bar',
                    toolbar: { show: false }
                },
                xaxis: {
                    categories: ['Jan', 'Feb', 'Mar', 'Apr']
                },
                colors: ['#347571', '#533f41', '#344c5b']
            },
            seriesD: [
                { name: 'Online Sales', data: [90, 30, 65, 50] },
                { name: 'In-Store Sales', data: [30, 40, 15, 30] },
                { name: 'Wholesale', data: [30, 20, 15, 50] }
            ],
        }
    }
}
</script>