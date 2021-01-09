<template>
  <div class="console" :class="[consoleStatus, consoleAnimation ? 'anim' : '']">
    <a
      href="#"
      v-if="consoleStatus === 'minimize'"
      @click.prevent="toggleMinimize"
      class="absolute top-0 bottom-0 left-0 right-0"
    ></a>
    <div class="bar">
      <small>>_ {{ title }}</small>
      <div class="dots">
        <div @click.prevent="toggleMaximize"></div>
        <div @click.prevent="toggleMinimize"></div>
        <div @click.prevent="toggleClose"></div>
      </div>
    </div>
    <div class="slot">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    value: String,
  },
  data() {
    return {
      consoleAnimation: false,
    };
  },
  computed: {
    consoleStatus: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("input", value);
      },
    },
  },
  methods: {
    toggleMaximize() {
      this.consoleStatus = "maximize";
    },
    toggleMinimize() {
      if (this.consoleStatus != "minimize") {
        this.$emit("minimize");
        this.consoleAnimation = true;
        this.consoleStatus = "minimize";
        setTimeout(() => {
          this.consoleAnimation = false;
        }, 100);
      } else {
        this.consoleStatus = "normal";
      }
    },
    toggleClose() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped>
.console {
  @apply bg-gray-800 px-2 py-1 rounded-lg;
  transition: all 200ms ease-in-out;
  transform: translate(0px, 0px) scale(1) !important;
  font-family: "Source Code Pro", monospace;
  &.maximize {
    @apply fixed top-0 left-0 right-0 min-w-full min-h-full;
  }

  &.minimize {
    &.anim{
      transform: translate(-50vw, 50vh) scale(0) !important;
    }

    &:not(.anim){
      transform: translate(0px, 0px) scale(1) !important;
      @apply fixed left-2;
      top: calc(100vh - 3.5rem);

      &:hover {
        top: calc(100vh - 4.5rem);
      }

      .bar {
        .dots {
          @apply max-w-0;
        }
      }
      .slot {
        @apply invisible max-w-0;
      }
    }
  }

  &.close {
    display: none !important;
  }

  .bar {
    @apply flex justify-between items-center mb-3 mt-1;

    small {
      @apply text-white;
    }

    .dots {
      @apply hidden md:flex justify-end items-center max-w-full;
      div {
        @apply w-4 h-4 ml-2 rounded-full cursor-pointer;

        &:nth-child(1) {
          @apply bg-green-400;
        }
        &:nth-child(2) {
          @apply bg-yellow-400;
        }
        &:nth-child(3) {
          @apply bg-red-400;
        }
      }
    }
  }
}
</style>