<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { onMounted, ref } from 'vue';
import TempMock from './components/tempMock.vue';
//here is simple work for this example.
const loadFromAPI = ref("");
const loading = ref(true);

let fetch_mockJSON = async () => {
    try {
        let response = await fetch('https://jsonplaceholder.typicode.com/todos/');
        if (!response.ok) throw new Error('unable to fetch.');
        let data = await response.json();

        //mock load data for 3s.
        setInterval(() => {
            loading.value = false;
            loadFromAPI.value = data;
        }, 3000);
    } catch (e) {
        console.log(e);
    }
}
onMounted(() => {
    //init
    fetch_mockJSON();
});
</script>

<template>

    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg p-6">
                    <div class=" text-gray-900">You're logged in!</div>
                    <div>Here i going to make async function to simulate download 50 <br />
                        of row data from jsonplaceholder.
                    </div>
                    <span>JSON placeholder was loaded from here.</span>
                    <Suspense>
                        <template #default>
                            <div v-if="!loading" class="flex flex-wrap gap-2 items-center max-w-screen-2xl">
                                <TempMock v-for="obj in loadFromAPI" :key="obj.userId" :obj="obj"></TempMock>
                            </div>
                            <!-- <pre v-if="!loading">{{ loadFromAPI }}</pre> -->
                            <div v-else>Loading...</div>
                        </template>
                    </Suspense>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>


<style lang="scss" scoped></style>