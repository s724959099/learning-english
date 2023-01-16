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
    {{ setntenceList }}
    {{ demo }}
  </div>
</template>
<script lang="ts" setup>
import { ref, watch, reactive } from 'vue';
import VTranslateion from '@/components/VTranslateion.vue';

const textInput = ref('');
const demo = ref('');

let setntenceList: string[] = reactive([]);
// watch
watch(textInput, (val) => {
  demo.value = val;
  console.log(val);
  setntenceList = val
    .replace(/^\.+|\.+$/g, '')
    .split('.')
    .map((item) => item.trim() + '.');
  console.log(setntenceList.length);
  console.log(setntenceList);
});
</script>
