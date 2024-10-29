<script setup>
import { reactive, ref, defineProps, onMounted } from 'vue'
import JobListing from './JobListing.vue';
import jobData from '@/jobs.json';
import { RouterLink } from 'vue-router';
import axios from 'axios';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
})

// const jobs = ref(jobData.jobs);
// const jobs = ref([]);
const state = reactive({
    jobs: [],
    isLoading: true
})


onMounted(async () => {
    try {
        console.log("Fetching jobs...");
        await new Promise(resolve => setTimeout(resolve, 500));
        const res = await axios.get('http://localhost:5000/jobs');
        console.log("Jobs fetched successfully", res.data);
        state.jobs = res.data;

    }
    catch (err) {
        console.error('Error fetching jobs', err);

    } finally {
        state.isLoading = false
    }
})

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Browse Jobs</h2>
            <!-- Show loading spinner while loading is true -->
            <div v-if="state.isLoading" class="text-center text-gray-500 px-6">
                <PulseLoader />
            </div>
            <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>
    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <RouterLink href="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">
            View
            View All Jobs</RouterLink>
    </section>
</template>
