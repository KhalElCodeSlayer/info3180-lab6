<template>
    <div class="container">
      <div class="text-center">
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
        <h1>{{ message }}</h1>
      </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: "Hello World! Welcome to VueJS"
        };
    }
}
</script>

<style>
/* Add any component specific styles here */
</style>