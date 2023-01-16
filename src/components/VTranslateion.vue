<template>
  <v-row>
    <v-col cols="6">
      <v-card>
        <v-card-title>
          <h1>English</h1>
        </v-card-title>
        <v-card-text>
          <v-word
            :active="el.active"
            :word="el.word"
            :key="index"
            v-for="(el, index) in words"
            @mouseenter="clickWord(index)"
          />
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="6">
      <v-card>
        <v-card-title>
          <h1>Translation</h1>
        </v-card-title>
        <v-card-text>{{ translatedSentence }}</v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
<script lang="ts" setup>
import VWord from '@/components/VWord.vue';
import { computed, reactive, ref } from 'vue';
import { watch } from 'vue';
import axios from 'axios';

function debounce<F extends (...params: any[]) => void>(fn: F, delay: number) {
  let timeoutID: number = 0;
  return function (this: any, ...args: any[]) {
    clearTimeout(timeoutID);
    timeoutID = window.setTimeout(() => fn.apply(this, args), delay);
  } as F;
}

function translateToChinese(sourceText: string) {
  let sourceLang = 'en';
  let targetLang = 'zh-tw';

  let url = `https://translate.googleapis.com/translate_a/single?client=gtx&sl=${sourceLang}&tl=${targetLang}&dt=t&q=${encodeURI(
    sourceText
  )}`;
  axios
    .get(url)
    .then((res) => {
      translatedSentence.value = res.data[0][0][0];
    })
    .catch((err) => {
      console.log(err);
    });
}

// axios.get(url).then((res) => {
//   console.log(res.data[0][0][0]);
// });

const props = defineProps<{
  english: string;
}>();
const words = reactive(
  props.english.split(' ').map((item) => {
    return { word: item, active: true };
  })
);
const translatedSentence = ref('');
const activeEnglishSentence = computed(() => {
  return words
    .filter((item) => item.active)
    .map((item) => item.word)
    .join(' ');
});
const updateWatch = debounce((val) => {
  translateToChinese(val);
}, 2000);
// watch translatedSentence changed
watch(activeEnglishSentence, (val) => {
  // updateWatch(val);
});

function clickWord(index: number) {
  words[index].active = !words[index].active;
}
</script>
