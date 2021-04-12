<template>
  <section class="bg-gray-50">
    <section
      class="h-screen flex justify-center items-center bg-cover"
      style="background-image: url(/img/bg.jpg)"
    >
      <h1 class="text-white text-center text-4xl w-3/4 sm:text-6xl font-light">
        Learn how to climb with the best video courses.
      </h1>
    </section>
    <section class="grid md:grid-cols-3 gap-4 md:w-3/4 mx-auto p-8">
      <div class="w-full col-span-3 lg:col-span-1 h-96 relative">
        <video
          class="absolute rounded-md shadow-xl w-full h-full object-cover"
          playsinline
          autoplay
          muted
          loop
          id="bgvid"
        >
          <source src="~assets/videos/video.mp4" type="video/mp4" />
        </video>
      </div>
      <div
        class="flex items-center justify-center text-center col-span-3 lg:col-span-2 flex-col"
      >
        <h2 class="text-gray-800 text-4xl sm:text-6xl">
          Learn how to climb with the best video courses.
        </h2>
        <h3 class="text-gray-500">
          Videos courses to climb in the best places around the world
        </h3>
      </div>
      <Card
        v-for="(item, index) in products"
        :item="item"
        :key="index"
        class="col-span-3 lg:col-span-1 bg-white"
      />
    </section>
  </section>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const products = await $content('products')
      .where({ type: 'product', published: true })
      .fetch()

    return {
      products,
    }
  },
  data() {
    return {
      image: {
        src:
          'https://images.unsplash.com/photo-1538370965046-79c0d6907d47?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80',
        alt: 'Image alt',
      },
    }
  },
}
</script>

<style>
video {
  /* Center the video */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
