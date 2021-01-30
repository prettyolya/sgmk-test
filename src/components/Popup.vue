<template>
  <div v-if="showPopup"
       class="overflow"
  >
    <div class="popup">
      <div @click="close"
           class="popup__exit"
      />
      <div class="popup__content">
        <slot/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  model: {
    prop: 'showPopup',
    event: 'change'
  },
  props: {
    showPopup: Boolean
  },
  methods: {
    close() {
      this.$emit("change", false);
    }
  }
}
</script>

<style>
.overflow {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 2;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0,0,0,.6);
}
.popup {
  width: auto;
  min-width: 320px;
  height: auto;
  min-height: 50px;
  padding: 15px;
  background-color: #FEFEFE;
  border-radius: 10px;
}
.popup__exit {
  position: relative;
}
.popup__exit:after {
  content: '\2A2F';
  font-size: 25px;
  position: absolute;
  top: 0;
  right: 0;
}
.popup__content {
  display: flex;
  justify-content: flex-start;
  padding: 20px 30px 0 0;
}
@media screen and (max-width: 1260px) {
  .popup {
   max-width: 80%;
  }
}
@media screen and (max-width: 480px) {
  .popup {
    width: 80%;
    max-width: 80%;
    min-width: 80%;
  }
}
</style>