<template>
  <q-page class="q-pa-lg">
    <div class="row full-width q-col-gutter-md justify-center">
      here is the text we want to scroll
      <q-input
        v-model="text"
        class="full-width full-height"
        filled
        type="textarea"
      />
    </div>
    <div class="row q-mt-xl justify-center">
      <q-btn
        class="q-mx-lg"
        color="primary"
        size="lg"
        label="Slow"
        @click="decreaseScrollSpeed"
      />
      <q-btn
        v-if="!isScrollStarted"
        color="primary"
        size="lg"
        label="start"
        @click="startScrolling"
      />
      <q-btn
        v-else="isScrollStarted"
        color="primary"
        size="lg"
        label="Stop"
        @click="stopScrolling"
      />
      <q-btn
        class="q-mx-lg"
        color="primary"
        size="lg"
        label="Fast"
        @click="increaseScrollSpeed"
      />
    </div>
    <div class="row">
      <q-scroll-area ref="scrollArea" style="width: 100%; height: 620px">
        <div style="font-size: 50px">
          {{ text }}
        </div>
      </q-scroll-area>
    </div>
  </q-page>
</template>

<script>
import text from "../assets/text.js";

export default {
  name: "PageIndex",
  data() {
    return {
      text: text,
      isScrollStarted: false
    };
  },
  methods: {
    startScrolling() {},
    stopScrolling() {},
    decreaseScrollSpeed() {},
    increaseScrollSpeed() {}
  }
};
</script>
