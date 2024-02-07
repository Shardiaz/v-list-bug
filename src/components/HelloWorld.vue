<template>
  <v-container class="fill-height">
    <v-list
      :items="items"
      :item-value="['nested', 'index']"
      select-strategy="classic"
      open-strategy="multiple"
      item-title="name"
      v-model:selected="selected"
      @update:selected="console.log('update:selected', $event)"
      v-model:opened="opened"
    >
    </v-list>
    {{ selected }}
    {{ opened }}
  </v-container>
</template>

<script setup lang="ts">
import { ref } from "vue";

const opened = defineModel<any[]>("opened", {
  default: [],
  required: false,
});

const items = ref(
  Array.from(new Array(15)).map((_, index) => ({
    name: `Item ${index + 1}`,
    nested: {
      index,
    },
    children: [
      {
        name: `Child ${index + 1}`,
        nested: {
          index,
        },
        children: [
          {
            name: `GrandChild ${index + 1}`,
            nested: {
              index,
            },
          },
        ],
      },
    ],
  }))
);

const selected = ref([]);
</script>
