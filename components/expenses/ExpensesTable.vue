<template>
    <TableComponent
        :data="data"
        :columns="columns"
        :isLoading="isLoading"
        @selectedRows="updateSelectedRows"
    >
        <template #cell-cards="{ data }">
            {{ data.row.cards.name }}
        </template>
        <template #cell-value="{ data }">
            {{ "R$ " + data.row.value }}
        </template>
    </TableComponent>
</template>

<script>
    import StatusBadge from "@/components/global/StatusBadgeComponent.vue";
    import TableComponent from "@/components/global/TableComponent.vue";
    export default {
        components: {
            TableComponent,
            StatusBadge
        },
        data: () => ({
            columns: [
                { key: "name", label: "Name" },
                { key: "description", label: "Description" },
                { key: "cards", label: "Card" },
                { key: "parcel_numbers", label: "Parcels" },
                { key: "value", label: "Value" },
            ],
            data: [],
            selectedRows: [],
            isLoading: true,
        }),
        methods: {
            getExpenses() {
                this.isLoading = true;
                this.$axios.get(`expenses`)
                    .then(({ data }) => {
                        this.data = data.data;
                    })
                    .finally(() => {
                        this.isLoading = false;
                    });
            },
            updateSelectedRows(rows) {
                this.selectedRows = rows;
                this.$emit("allowActions", rows);
            },
        },
        created() {
            this.getExpenses();
        }
    }
</script>