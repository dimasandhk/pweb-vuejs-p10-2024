<script lang="ts">
import BookCard from "../components/BookCard.vue";

interface BookObject {
  _id: string;
  title: string;
  author: string;
  tags: string[];
  publishedDate: string;
  initialQty: number;
  qty: number;
  publisher: string;
}

export default {
  name: "HomeView",
  data: () => ({
    booksData: [] as BookObject[],
  }),
  async mounted() {
    const response = await fetch("http://localhost:3000/books");
    const data = await response.json();
    this.booksData = [...data.data];
  },
  components: {
    BookCard,
  },
};
</script>

<template>
  <main class="mt-10 mx-8 pb-24">
    <h1 class="font-bold text-3xl text-center">Book Gallery App P10</h1>
    <div class="flex flex-wrap justify-center gap-4 mt-10">
      <BookCard
        v-if="booksData.length"
        v-for="book in booksData"
        :key="book._id"
        :book="book"
        class="w-full sm:w-full md:w-2/6 lg:w-1/4"
      />
      <h1 class="font-bold text-3xl text-center w-full" v-else>Loading...</h1>
    </div>
  </main>
</template>
