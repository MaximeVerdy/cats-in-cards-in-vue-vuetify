<template>
  <v-card class="catCard">
    <v-img :src="img" class="img"/>
    <v-card-title style="word-break: break-word" class="justify-center text-center myFontGrey--text bold font-weight-bold" >{{ title }}</v-card-title>
    <v-card-text style="word-break: break-word" class="text-center myFontGrey--text lineHeight">
      {{ coat }} coat
      <br />
      {{ pattern }} pattern
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "CatCard",
  props: {
    title: String,
    coat: String,
    pattern: String,
    img: String,
  },
};
</script>