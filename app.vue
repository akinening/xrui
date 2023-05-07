<template>
  <div>
    <NuxtPage />
  </div>
</template>
<script>
export default {
    setup () {
        useHead({
            bodyAttrs: { class: 'body-class' }
        })
    }
}
</script>

<style>
.body-class {
    margin: 0;
}
</style>