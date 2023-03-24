<script lang="ts" setup>

useHead({
  title: 'Create Post - Nuxt3',
  meta: [
    {
      name: 'description',
      content: 'Create Post page description',
    },
  ],
});

// init config
const config = useRuntimeConfig();

// init router
const router = useRouter();

// define state
const title = ref('');
const content = ref('');
const image = ref('');
const errors:any = ref({});

// method for image changes
const onImageChange = (e: any) => {
  image.value = e.target.files[0]
}

// method store post
const storePost = async () => {

  // create form data
  const formData = new FormData();
  formData.append('title', title.value);
  formData.append('content', content.value);
  formData.append('image', image.value);

  // send request
  await $fetch(`${config.public.apiBase}/posts`, {
    method: 'POST',
    body: formData,
  }).then(() => {
    // redirect to posts page
    router.push("/posts");

  }).catch((error) => {
    // assign error to state "errors"
    errors.value = error.data;
    
  });

  // redirect to posts page
  // router.push('/posts');

}

</script>

<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-7 mx-auto">
        <div class="card border-0 rounded shadow">
          <div class="card-body">
            <form @submit.prevent="storePost()">
              <div class="mb-3">
                <label for="title" class="form-label fw-bold">Title</label>
                <input type="text" class="form-control" id="title" v-model="title" placeholder="Title post">
                <div v-if="errors.title" class="alert alert-danger mt-2">
                  <span>{{ errors.title[0] }}</span>
                </div>
              </div>
              <div class="mb-3">
                <label for="content" class="form-label fw-bold">Content</label>
                <textarea class="form-control" id="content" v-model="content" rows="3"></textarea>
                <div v-if="errors.content" class="alert alert-danger mt-2">
                  <span>{{ errors.content[0] }}</span>
                </div>
              </div>
              <div class="mb-3">
                <label for="image" class="form-label fw-bold">Image</label>
                <input class="form-control" type="file" id="image" @change="onImageChange($event)">
                <div v-if="errors.image" class="alert alert-danger mt-2">
                  <span>{{ errors.image[0] }}</span>
                </div>
              </div>
              <button type="submit" class="btn btn-primary shadow border-0">Submit</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
