<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import NoteComponent from './NoteComponent.vue';
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Your Notes
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <NoteComponent :user="$page.props.user"></NoteComponent>
                <!-- <div class="bg-white overflow-x-hidden overflow-y-auto max-h-5xl shadow-xl sm:rounded-lg">
                    
                </div> -->
            </div>
        </div>
    </AppLayout>
</template>
