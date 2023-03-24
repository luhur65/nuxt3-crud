<script lang="ts" setup></script>

<template>
  <div>

    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container">
        <a class="navbar-brand" href="#">Crud Nuxt3</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav float-left">
            <NuxtLink to="/" class="nav-link" exact-active-class="active" >Home</NuxtLink>
            <NuxtLink to="/posts" class="nav-link" exact-active-class="active" >Posts</NuxtLink>
          </div>
        </div>
      </div>
    </nav>

    <!-- render page -->
    <slot />
  </div>
</template>

<style scoped>

body {
  font-family: 'Quicksand', sans-serif;
}

</style>
