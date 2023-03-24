<script lang="ts" setup>

import moment from 'moment';

useHead({
  title: 'Detail Posts'
});

const config = useRuntimeConfig();
const router = useRouter();
const route = useRoute();
const {data: post} : any = await useFetch(config.public.apiBase + '/posts/' + route.params.id);

const title = ref(post.value.data.title);
const content = ref(post.value.data.content);
const image = ref(post.value.data.image);

</script>

<template>
  <div class="container mt-5">
    <img :src=image class="rounded" alt="..." height="300px">
    <div class="card mb-3 border-0">
      <div class="card-body mt-2 p-0">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ content }}</p>
        <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
        <NuxtLink to="/posts" class="card-link">Back</NuxtLink>
      </div>
    </div>

  </div>
</template>

<style scoped></style>
