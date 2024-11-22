<script lang="ts">
import { defineComponent } from "vue";

interface Rating {
  average: number;
  count: number;
}

interface BookDetail {
  rating: Rating;
  _id: string;
  title: string;
  author: string;
  publishedDate: string;
  publisher: string;
  description: string;
  coverImage: string;
  tags: string[];
  initialQty: number;
  qty: number;
  createdAt: string;
  updatedAt: string;
  __v: number;
}

export default defineComponent({
  name: "DetailBookView",
  data: () => ({
    bookDetail: {} as BookDetail,
  }),
  async mounted() {
    const response = await fetch(
      `http://localhost:3000/book/${this.$route.params.id}`
    );
    const data = await response.json();
    console.log(data);
    this.bookDetail = { ...data.data };
  },
  computed: {
    starRating(): string {
      const stars = Math.floor(this.bookDetail.rating.average);
      return "⭐".repeat(stars);
    },
  },
});
</script>

<template>
  <main class="mt-14 mx-8 pb-14">
    <RouterLink
      to="/"
      class="px-4 text-white py-2 md:ml-12 lg:ml-24 bg-blue-400 font-semibold rounded-xl inline-block"
      >⬅️ Back to Home</RouterLink
    >
    <div v-if="bookDetail.title" class="mt-8">
      <div class="flex md:ml-12 lg:ml-24 gap-x-10 flex-col md:flex-row">
        <div>
          <img
            src="https://placehold.co/300x200"
            class="rounded-xl w-full lg:w-[500px]"
            alt="Book Cover"
          />
        </div>
        <div class="mt-10 md:mt-0">
          <h1 class="font-bold text-3xl text-left">
            Buku {{ bookDetail.title }} by {{ bookDetail.author }}
          </h1>
          <h5 class="text-sm text-gray-500 font-bold">
            {{ bookDetail.rating.average }} {{ starRating }} ({{
              bookDetail.rating.count
            }})
          </h5>
          <hr class="border border-black my-2" />
          <h3 class="text-xl text-left">
            <span class="font-bold">About:</span> {{ bookDetail.description }}
          </h3>
          <h3 class="text-xl text-left">
            <span class="font-bold">Published:</span>
            {{ bookDetail.publishedDate }} by
            {{ bookDetail.publisher }}
          </h3>
          <h3 class="text-xl text-left">
            <span class="font-bold">Category:</span>
            {{ bookDetail.tags.join(", ") }}
          </h3>
          <h3 class="text-xl text-left">
            <span class="font-bold">Stock:</span>
            {{ bookDetail.qty }} of {{ bookDetail.initialQty }} books
          </h3>
        </div>
      </div>
    </div>
    <div class="mt-8" v-else>
      <h1 class="font-bold text-3xl text-center">Loading...</h1>
    </div>
  </main>
</template>
