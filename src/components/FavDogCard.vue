<script>
export default {
  props: {
    dogImageSrc: {
      type: String
    }
  }
};
</script>

<template>
    <v-card class="dog-card">
      <v-img height="150px" :src="dogImageSrc"/>
      <v-card-actions>
        <v-spacer/>
        <v-btn icon @click="$emit('remove')">
          <span class="material-icons">delete</span>
        </v-btn>
      </v-card-actions>
    </v-card>
</template>