<template>
  <div class="bg-gray-800 h-screen">

    <section class="grid md:grid-cols-3 gap-4 md:w-3/4 mx-auto p-8">

    <input class="border col-span-3 rounded-md focus:outline-none px-4 py-2 shadow mt-16" placeholder="What are you looking for ?" type="text" v-model="searchQuery">

    <Card
        v-for="(item, index) in items"
        :item="item"
        :key="index"
        class="col-span-3 lg:col-span-1 bg-white"
      />
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
            items: [],

    }
  },
   watch: {
    async searchQuery(searchQuery) {
      if (!searchQuery) {
        this.items = []
        return
      }
      this.items = await this.$content('products')
        .search(searchQuery)
        .where({ published: true })
        .fetch()
    },
  },
}
</script>

<style lang="scss" scoped></style>
