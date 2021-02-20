<template>
  <q-page>
    <div class="column full-width">
      <div class="row full-width q-col-gutter-md justify-center">
        here is the text we want to scroll
        <q-input
          v-model="text"
          class="full-width full-height"
          filled
          type="textarea"
        />
      </div>
    </div>

    <div class="column ">
      <div class="row q-mt-xl justify-center q-pa-lg">
        <q-btn
          class="q-mx-lg"
          color="primary"
          size="lg"
          label="Slower"
          @click="decreaseScrollSpeed"
          icon="arrow_circle_down"
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
          label="Faster"
          @click="increaseScrollSpeed"
          icon-set="material-icons"
          icon-right="arrow_circle_up"
        />
      </div>
    </div>
    <div class="column" style="flex: 1">
      <q-scroll-area ref="scrollArea" style="width: 100%; height: 800px">
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
      isScrollStarted: false,
      scrollSpeed: 0.2,
      scrollSpeedIncrement: 0.1,
      currentScrollLocation: 1,
      scrollIntervalTimeMs: 1,
      scrollTimeInterval: null
    };
  },
  mounted() {},

  methods: {
    startScrolling() {
      this.isScrollStarted = true;
      const height = this.$refs.scrollArea.$el.querySelector("div")
        .scrollHeight;

      let scrollAreaDivRef = this.$refs.scrollArea?.$el.querySelector("div");
      this.currentScrollLocation = this.$refs.scrollArea.scrollPosition;

      this.scrollTimeInterval = setInterval(() => {
        scrollAreaDivRef.scrollTo(0, this.currentScrollLocation);

        this.currentScrollLocation += this.scrollSpeed;

        if (this.currentScrollLocation > height) {
          this.stopScrolling();
        }
      }, this.scrollIntervalTimeMs);
    },
    stopScrolling() {
      this.isScrollStarted = false;
      clearInterval(this.scrollTimeInterval);
      // scrollAreaDivRef.scrollTop(0);
    },
    decreaseScrollSpeed() {
      if (
        this.scrollSpeed > 0 &&
        this.scrollSpeed - this.scrollSpeedIncrement > 0
      ) {
        this.scrollSpeed -= this.scrollSpeedIncrement;
      }
    },
    increaseScrollSpeed() {
      this.scrollSpeed += this.scrollSpeedIncrement;
    }
  }
};
</script>

<style>
body {
  scroll-behavior: smooth;
}
</style>
