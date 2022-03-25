<template>
  <div ref="root" class="inline-block md:w-1/3 w-2/3">
    <input class="search" placeholder="Word" spellcheck="false"/>
  </div>
</template>

<script>
export default {
  name: "search"
}
</script>

<style scoped>

.search {
  font-family: 'Lato', sans-serif;
  @apply w-full bg-[#dad5d5] h-[35px] outline-none;
  @apply pl-3 rounded-md mt-[20px];
  @apply border-[2px] border-[#6254FF]
}

</style>
