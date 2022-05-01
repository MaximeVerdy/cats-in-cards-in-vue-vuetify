<template>
  <v-app>
    <div class="text-center">
      <v-dialog v-model="dialog" width="500">
        <v-card>
          <v-card-text class="pt-8 pl-8 pr-8">
            {{ fact }}
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="#cc6e2f" text @click="dialog = false"> Close </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>

    <h1 class="text-center pa-10 myFontGrey--text">
      CATS IN CARDS
    </h1>
    <v-container fluid grid-list-xl>
      <v-layout row wrap class="justify-center">
        <v-flex
          d-flex
          xs9
          sm4
          md3
          xl2
          v-for="cat of cats"
          :key="cat.breed"
          @click="seeFactInModal"
        >
          <CatCard
            :img="catPic"
            :title="cat.breed"
            :coat="cat.coat"
            :pattern="cat.pattern"
          />
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>


<script>
import CatCard from "./components/CatCard.vue";
import catPic from "./assets/shadow-cat.jpg";

export default {
  name: "App",
  components: {
    CatCard,
  },

  data() {
    return {
      cats: [],
      fact: "",
      catPic: catPic,
      dialog: false,
    };
  },

  async created() {
    try {
      const data = await fetch("https://catfact.ninja/breeds");
      const body = await data.json();
      this.cats = body.data;
    } catch (e) {
      console.error(e);
    }
  },

  methods: {
    seeFactInModal: async function () {
      try {
        const data = await fetch("https://catfact.ninja/fact");
        const body = await data.json();
        this.fact = body.fact;
      } catch (e) {
        console.error(e);
      }
      this.dialog = true;
    },
  },
};
</script>

<style lang="scss">
@import "@/style/main.scss";
</style>