<script lang="ts" setup>

useHead({
  title: 'Data Posts - Nuxt3',
  meta: [
    {
      name: 'description',
      content: 'Posts page description',
    },
  ],
})

// init config
const config = useRuntimeConfig()

// fetch data from api with "AsyncData"
const { data: posts} : any = await useAsyncData('posts', () => $fetch(`${config.public.apiBase}/posts`))

// delete post
const deletePost = async (id: number) => {
  await $fetch(`${config.public.apiBase}/posts/${id}`, {
    method: 'DELETE',
  }).then(() => {
    // refresh data
    refreshNuxtData('posts')
  })
}

</script>

<template>
  <div class="container mt-5 mb-5">
    <div class="row">
      <div class="col-md-12">
        <NuxtLink to="/posts/create" class="btn btn-primary mb-3">Create Post</NuxtLink>
        <div class="card border-0 rounded shadow-sm mb-3">
          <div class="card-body">
            <table class="table table-hovered">
              <thead>
                <tr>
                  <!-- <th scope="col">#</th> -->
                  <th scope="col">Image</th>
                  <th scope="col">Title</th>
                  <th scope="col">Content</th>
                  <th scope="col">Actions</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(post, index) in posts.data.data" :key="index">
                  <th scope="row" class="text-center">
                    <img :src="post.image" class="img-fluid rounded" width="50" />
                  </th>
                  <td>
                    <NuxtLink :to="`/posts/detail/${post.id}`">{{ post.title }}</NuxtLink>
                  </td>
                  <td>
                    <div class="d-inline-block text-truncate" style="max-width: 150px;">
                      {{ post.content }}</div>
                  </td>
                  <td>
                    <div class="grip gap-3">
                      <div class="p-1 g-col-6">
                        <NuxtLink :to="`/posts/edit/${post.id}`" class="btn btn-sm btn-primary">Edit</NuxtLink>
                      </div>
                      <div class="p-1 g-col-6">
                        <button @click="deletePost(post.id)" class="btn btn-sm btn-danger">Delete</button>
                      </div>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
