<script setup>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import { reactive, ref, defineProps, onMounted } from 'vue'
import { RouterLink, useRoute } from 'vue-router';
import axios from 'axios';





</script>

<template>
    <section>
        <div class="container m-auto py-6 px-6">
            <RouterLink to="/jobs" class="text-green-500 hover:text-green-600 flex items-center">
                <i class="pi pi-arrow-circle-left mr-2"></i> Back to Job Listings
            </RouterLink>
        </div>
    </section>
</template>