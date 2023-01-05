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
    <v-row :key="index" class="my-3" v-for="(item, index) in setntenceList">
      <v-col cols="6">
        <v-card>
          <v-card-title>
            <h1>English</h1>
          </v-card-title>
          <v-card-text>
            {{ item }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card>
          <v-card-title>
            <h1>Translation</h1>
          </v-card-title>
          <v-card-text>
            {{ item }}
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<script lang="ts" setup>
import { ref, watch, reactive } from 'vue';

const textInput = ref(
  'The retail dataset contains item clicks from an online apparel store, and browsing logs for the same users, collected during May 2013. The apps dataset contains downloads of Windows Phone 8 Apps and browsing logs for the same users, collected between September and November 2013 (inclusive). These datasets were intentionally selected to represent diverse domains: the retail dataset contains page clicks on pages of physical goods, while the apps dataset contains purchases of virtual multimedia goods. Our experimental results, thus, demonstrate the applicability of our enhancement methods across different types of user-item interaction types as well as varied product catalogs.'
);
let setntenceList: string[] = reactive([]);
// watch
watch(textInput, (val) => {
  console.log(val);
  setntenceList = val
    .replace(/^\.+|\.+$/g, '')
    .split('.')
    .map((item) => item + '.');
  console.log(setntenceList);
});
</script>
