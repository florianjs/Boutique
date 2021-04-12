<template>
  <section class="bg-gray-50">
    <section
      class="h-screen flex justify-center items-center bg-cover bg-center"
      :style="{ backgroundImage: 'url(' + product.image + ')' }"
    >
      <h1 class="text-white text-center text-4xl w-3/4 sm:text-6xl font-light">
        {{ product.title }}
      </h1>
    </section>
    <section
      class="grid md:grid-cols-3 gap-4 md:w-3/4 mx-auto p-8"
      :class="product.video ? 'md:grid-cols-3 gap-4' : 'md:grid-cols-2 gap-4'"
    >
      <div
        v-if="product.video"
        class="w-full col-span-3 lg:col-span-1 h-96 relative"
      >
        <video
          class="absolute rounded-md w-full h-full object-cover"
          playsinline
          autoplay
          muted
          loop
          id="bgvid"
        >
          <source :src="product.video" type="video/mp4" />
        </video>
      </div>

      <img
        :src="img.src"
        :alt="img.alt"
        v-for="img in product.gallery"
        :key="img.id"
        class="col-span-3 lg:col-span-1 h-96 w-full object-cover rounded-md"
      />
      <div class="flex text-justify flex-col col-span-3 lg:col-span-2">
        <h2 class="text-3xl font-semibold py-4">{{ product.description }}</h2>
        <nuxt-content class="text-gray-800" :document="product" />
      </div>
    </section>
    <section
      v-if="product.socialProof"
      class="p-4 mx-auto w-full h-48 grid grid-cols-1 md:grid-cols-3 gap-4"
    >
      <a
        v-for="item in product.socialProof"
        :key="item.id"
        :href="item.link"
        class="flex flex-col justify-evenly shadow rounded-md p-4 bg-white transform duration-150 ease-in-out hover:-translate-y-2"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          class="twitter fill-current mx-auto"
        >
          <path
            d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"
          />
        </svg>
        <p class="text-center w-full">
          {{ item.text }}
          -
          <span class="font-bold twitter">{{ item.author }}</span>
        </p>
      </a>
    </section>

    <div class="sticky bottom-4 flex justify-center mx-auto">
      <a
        :href="product.buy"
        class="bg-blue-300 flex flex-col sm:flex-row items-center px-8 py-6 text-2xl text-justify justify-center shadow m-4 rounded-lg text-white bg-gradient-to-br from-indigo-500 to-purple-600 hover:from-purple-600 to:indigo-500 transform duration-200 ease-out"
      >
        <h3 class="">Buy {{ product.title }} today for</h3>

        <div class="pricing">
          <span class="text-base justify-start">$</span> {{ product.price }}
        </div>
      </a>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const product = await $content('products', params.slug)
      .where({ published: true })
      .fetch()

    return {
      product,
    }
  },
}
</script>

<style>
.twitter {
  color: #1da1f2;
}
.enroll {
  @apply uppercase rounded-md px-4 py-2 text-white flex items-center ring-0 justify-center transform ease-in-out duration-200 hover:bg-indigo-400 focus:outline-none focus:ring-offset-1 focus:ring-2;
}
.pricing {
  @apply flex ml-2 items-center font-bold;
}
.nuxt-content h2 {
  @apply text-2xl py-4;
}
.nuxt-content h {
  @apply text-xl;
}
</style>
