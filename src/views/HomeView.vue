<template>
  <div>
    <v-card>
      <v-card-title>
        <h1>文章段落</h1>
      </v-card-title>
      <v-card-text>
        <v-textarea solo name="" label="" v-model="textInput"></v-textarea>
      </v-card-text>
    </v-card>
    <v-translateion
      :key="index"
      class="my-5"
      :english="item"
      v-for="(item, index) in setntenceList"
    />
    <v-translateion
      english="The retail dataset contains item clicks from an online apparel store, and browsing logs for the same users."
    />
  </div>
</template>
<script lang="ts" setup>
import { ref, watch, reactive } from 'vue';
import VTranslateion from '@/components/VTranslateion.vue';

const textInput = ref(
  'The retail dataset contains item clicks from an online apparel store, and browsing logs for the same users, collected during May 2013. The apps dataset contains downloads of Windows Phone 8 Apps and browsing logs for the same users, collected between September and November 2013 (inclusive). These datasets were intentionally selected to represent diverse domains: the retail dataset contains page clicks on pages of physical goods, while the apps dataset contains purchases of virtual multimedia goods. Our experimental results, thus, demonstrate the applicability of our enhancement methods across different types of user-item interaction types as well as varied product catalogs.'
);
let setntenceList: string[] = reactive(['i am english']);
// watch
watch(textInput, (val) => {
  console.log(val);
  setntenceList = val
    .replace(/^\.+|\.+$/g, '')
    .split('.')
    .map((item) => item.trim() + '.');
  console.log(setntenceList);
});
</script>
