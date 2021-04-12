<template>
  <div class="card">
    <img :src="item.image" :alt="item.alt" />
    <div class="content">
      <div v-if="item.category" class="tag">
        {{ item.category }}
      </div>

      <p v-if="item.description">
        {{
          item.description.length > 100
            ? item.description.slice(0, 100) + '...'
            : item.description
        }}
      </p>
    </div>

    <div class="pricing">
      <p class="flex text-2xl font-semibold">
        <span class="text-sm self-start">$</span> {{ item.price }}
      </p>
      <nuxt-link :to="'/product/' + item.slug" class="enroll">
        enroll</nuxt-link
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      default: () => {},
    },
  },
}
</script>

<style scoped>
.card {
  @apply flex flex-col justify-between border rounded-md;
}
.tag {
  @apply text-gray-500 uppercase text-xs;
}
.content {
  @apply flex flex-col h-full px-4 pt-4;
}
.pricing {
  @apply flex justify-between items-center text-gray-800 p-4;
}
.enroll {
  @apply uppercase rounded-md px-4 py-2 bg-indigo-500 text-white flex items-center ring-0 justify-center transform ease-in-out duration-200 hover:bg-indigo-400 focus:outline-none focus:ring-offset-1 focus:ring-2;
}
img {
  @apply rounded-t-md h-48 object-cover object-center;
}
</style>
