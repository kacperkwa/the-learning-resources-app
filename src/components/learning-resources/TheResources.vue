<template>
  <BaseCard>
    <BaseButton @click="setSelectedTab('stored-resources')"
      >Stored Resources</BaseButton
    >
    <BaseButton @click="setSelectedTab('add-resource')"
      >Add Resource</BaseButton
    >
  </BaseCard>
  <component :is="selectedTab"></component>
</template>

<script setup>
import { ref } from 'vue';
let selectedTab = ref('stored-resources');
const setSelectedTab = (tab) => {
  selectedTab = tab;
};
</script>
