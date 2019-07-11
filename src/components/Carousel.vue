<template>
  <div>
    <div class="card-carousel">
      <ArrowButton
        arrowType="left"
        :onClick="showPrevElement"
        :disabled="this.reachedMaxLeft"
      />
      <Card
        class="current-element"
        v-touch:swipe="this.swipeHandler"
        :headline="currentElement.headline"
        :text="currentElement.text"
        :imgName="currentElement.imgName"
      />
      <ArrowButton
        arrowType="right"
        :onClick="showNextElement"
        :disabled="this.reachedMaxRight"
      />
    </div>
    <Indicators
      :elements="this.cards"
      :currentElementIndex="this.currentElementIndex"
      :showElement="this.showElement"
    />
  </div>
</template>

<script>
import Card from "./Card";
import ArrowButton from "./ArrowButton";
import Indicators from "./Indicators";

export default {
  name: "Carousel",
  props: { cards: Array },
  components: { Card, ArrowButton, Indicators },
  data() {
    return {
      currentElementIndex: 0
    };
  },
  computed: {
    currentElement() {
      return this.cards[this.currentElementIndex];
    },
    reachedMaxLeft() {
      return this.currentElementIndex === 0;
    },
    reachedMaxRight() {
      return this.currentElementIndex === this.cards.length - 1;
    }
  },
  methods: {
    showNextElement() {
      this.currentElementIndex++;
    },
    showPrevElement() {
      this.currentElementIndex--;
    },
    showElement(elementIndex) {
      this.currentElementIndex = elementIndex;
    },
    swipeHandler(direction) {
      if (direction === "right" && !this.reachedMaxLeft) {
        this.showPrevElement();
      }
      if (direction === "left" && !this.reachedMaxRight) {
        this.showNextElement();
      }
    }
  }
};
</script>

<style src="../assets/styles/Carousel.css" scoped />
