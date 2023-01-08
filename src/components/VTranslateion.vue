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
import { computed, reactive } from 'vue';

const props = defineProps<{
  english: string;
}>();
const words = reactive(
  props.english.split(' ').map((item) => {
    return { word: item, active: true };
  })
);
const translatedSentence = computed(() => {
  return words
    .filter((item) => item.active)
    .map((item) => item.word)
    .join(' ');
});

function clickWord(index: number) {
  words[index].active = !words[index].active;
  console.log('clickWord', index);
}
</script>
