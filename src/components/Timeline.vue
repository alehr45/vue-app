<script setup lang="ts">
import { usePosts } from "../stores/posts";
import TimelineItem from "../components/TimelineItem.vue";
import { periods } from "../constants";

const postsStore = usePosts();

await postsStore.fetchPosts();
</script>

<template>
  <nav class="is-primary panel">
    <span class="panel-tabs">
      <a
        v-for="period of periods"
        :key="period"
        v-bind:class="{ 'is-active': period === postsStore.selectedPeriod }"
        @click="postsStore.setSelectedPeriod(period)"
      >
        {{ period }}
      </a>
    </span>

    <TimelineItem
      v-for="post of postsStore.filteredPosts"
      :key="post.id"
      :post="post"
      class="panel-block is-flex is-flex-direction-column is-align-items-flex-start"
    />
  </nav>
</template>

<style></style>
