<template>
<!-- Displays close button -->
  <v-col cols="12" class="align-start pa-0">
    <v-btn icon aria-label="Close" @click="close">
      <v-icon small dark class="material-icons close-icon">close</v-icon>
    </v-btn>
  </v-col>
</template>
<style>
.close-button{
  top: 0 !important;
  right: 0px !important;
  width: 16px !important;
  height: 16px !important;
  background-color: transparent;
  border-color: transparent;
  text-align:center;
}
.close-icon{
  font-size: 16px;
  padding-left:0px;
  padding-right:0px;
}
</style>
<script>
export default {
  name: 'CloseButton',
  props: {
    index: {
      required: true
    },
    layout: {
      required: true
    },
    websocket: {
      required: false
    }
  },
  methods: {
    // When we push the close button
    close : function() {
      if (this.websocket){
        // We want to send to the client that we are deleting this widget from the pool
        this.websocket.send(JSON.stringify({"Action": "Delete"}));
        this.websocket.close();
      }
      // Removes it from the local layout array which holds all the widget information
      this.$delete(this.layout, this.index);
    }
  }
}
</script>
