<template>
  <div>
    <div
      class="text-5xl text-center header h-64 flex justify-center items-center bg-cover bg-no-repeat"
    >
      Lyrics Finder Application
    </div>
    <div>
      <form @submit.prevent="searchLyrics" class="text-center pt-5">
        <input
          v-model="artist"
          type="text"
          placeholder="Enter artist name"
          class="pt-1"
        />
        <input
          v-model="title"
          type="text"
          placeholder="Enter song title"
          class="pt-1"
        />
        <button
          type="submit"
          class="bg-black text-white pr-4 pl-4 rounded pt-1 pb-1"
        >
          Search
        </button>
      </form>
    </div>
    <div class="pt-4 max-w-sm text-center m-auto">
      <p>{{ lyrics }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // bind data
      artist: "chris brown",
      title: "heat",
      lyrics: [],
    };
  },
  async created() {
    //Called synchronously after the instance is created
    //api.lyrics.ovh/v1/Coldplay/Adventure of a Lifetime
    try {
      const response = await fetch(
        `https://api.lyrics.ovh/v1/${this.artist}/${this.title}`
      );
      const data = await response.json();
      console.log(data);
      this.lyrics = data.lyrics;
      console.log(this.lyrics);
      // reset the data object to prevent from showing in the form input
      this.artist = "";
      this.title = "";
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async searchLyrics() {
      // fetch lyrics from api here
      try {
        const response = await fetch(
          `https://api.lyrics.ovh/v1/${this.artist}/${this.title}`
        );
        const data = await response.json();
        // reset the data object to prevent from showing in the form input
        this.artist = "";
        this.title = "";
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
.header {
  background-image: url("../assets/pexels-miguel-á-padriñán-194094.jpg");
}
</style>
