<template>
  <v-card outlined>
    <v-card-subtitle class="text-overline py-2 text--primary">{{ author }}</v-card-subtitle>
    <v-card-subtitle class="text-subtitle-1 pt-0 pb-2 text--primary">{{ header }}</v-card-subtitle>
    <v-card-text class="text--primary">
      <slot></slot>
    </v-card-text>
</v-card>
</template>

<script>
export default {
  name: "UserPost",
  props: ["header", "author"]
}
</script>