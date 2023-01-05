<template>
  <v-row>
    <v-col cols="6">
      <v-card>
        <v-card-title>
          <h1>English</h1>
        </v-card-title>
        <v-card-text>{{ english }}</v-card-text>
      </v-card>
    </v-col>
    <v-col cols="6">
      <v-card>
        <v-card-title>
          <h1>Translation</h1>
        </v-card-title>
        <v-card-text>{{ english }}</v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
<script lang="ts" setup>
defineProps<{
  english: string;
}>();
</script>
