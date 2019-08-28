<template>
  <transition name="slider">
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

/** slider transitions */
.slider-enter {
  /* transform: translateY(20px); */
}

.slider-enter-active {
  animation: slide-in 1s ease-out forwards;
}

.slider-leave {
}

.slider-leave-active {
  animation: slide-out 1s ease-out forwards;
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