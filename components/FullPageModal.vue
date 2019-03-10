<template>
  <v-layout row justify-center>
    <v-dialog :value="showModal" fullscreen hide-overlay transition="dialog-bottom-transition">
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="$emit('close')">
            <v-icon>close</v-icon>
          </v-btn>
        </v-toolbar>
        <v-container grid-list-xs v-html="content">
          
        </v-container>
      </v-card>
    </v-dialog>
  </v-layout>
</template>
<script>
export default {
  props: {
    content: {
      type: String
    },
    showModal: {
      type: Boolean,
      default: false
    }
  },
}
</script>
