<template>
  <transition name="fade">
    <div class="col-sm-12 text-center" v-if="messages.length">
      <div class="alert alert-info">{{pop}}</div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  },
  data: () => {
    return {
      messages: [],
      current: ""
    };
  },
  computed: {
    pop() {
      if (this.messages.length) {
        const lastIdx = this.messages.length - 1;

        setTimeout(() => {
          this.messages.splice(lastIdx, 1);
        }, 3000);

        return this.messages[0];
      }
      return "";
    }
  },
  methods: {
    pushMessage(msg) {
      this.messages.unshift(msg);
    }
  },
  watch: {
    message(msg) {
      this.pushMessage(msg);
    }
  }
};
</script>

<style scoped>
.fade-enter {
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 1s;
}

.fade-leave {
  /* opacity: 1; */
}

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}
</style>