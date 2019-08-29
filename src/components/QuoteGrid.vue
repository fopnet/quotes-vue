<template>
  <div class="row">
    <transition-group name="slider">
      <app-quote
        :key="quote"
        v-for="(quote, index) in quotes"
        @click.native="deleteQuote(index)"
      >{{ quote }}</app-quote>
    </transition-group>
  </div>
</template>

<script>
import Quote from "./Quote.vue";

export default {
  props: ["quotes"],
  components: {
    appQuote: Quote
  },
  methods: {
    deleteQuote(index) {
      this.$emit("quoteDeleted", index);
    }
  }
};
</script>

<style scoped>
/** slider transitions */
.slider-enter {
  opacity: 0;
}

.slider-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 0.5s;
}

.slider-leave {
}

.slider-leave-active {
  animation: slide-out 1s ease-out forwards;
  transition: opacity 1s;
  opacity: 0;
}

@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0px);
  }
}
@keyframes slide-out {
  from {
    transform: translateY(0px);
  }
  to {
    transform: translateY(20px);
  }
}
</style>