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
  </div>
</template>
<script lang="ts" setup>
import { ref, reactive, watchEffect } from 'vue';
import VTranslateion from '@/components/VTranslateion.vue';

const textInput = ref('');

let setntenceList: string[] = reactive([]);

// watch
watchEffect(() => {
  const result = textInput.value
    .replace(/^\.+|\.+$/g, '')
    .split('.')
    .map((item) => item.trim() + '.');
  setntenceList.length = 0;
  setntenceList.push(...result);
});
</script>
