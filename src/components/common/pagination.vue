<script>
export default {
    props: {
        pills: {
            type: Boolean,
            default: true,
        }
    },
    data() {
        // return { ex4Rows: 100, }
        return { 
            current_page: null,
         }
    }
}
</script>

<template>
    <div class="mt-3">
        <!-- <BPagination v-model="ex4CurrentPage" :pills="pills" :total-rows="ex4Rows" align="end" /> -->
        <b-pagination v-model="current_page" :pills="pills" align="end"
        :total_rows="total"
        :per_page="per_page"
        aria-controls="data-proyek"></b-pagination>
    </div>
</template>