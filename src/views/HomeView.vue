<script lang="ts">
import BookCard from "../components/BookCard.vue";

interface BookObject {
  _id: string;
  title: string;
  author: string;
  publishedDate: string;
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
  <main class="mt-10 mx-8">
    <h1 class="font-bold text-3xl text-center">Book Gallery App P10</h1>
    <div class="grid gap-4 mt-10 grid-cols-1 sm:grid-cols-2 lg:grid-cols-4">
      <BookCard
        v-if="booksData.length"
        v-for="book in booksData"
        :key="book._id"
        :book="book"
      />
    </div>
  </main>
</template>
