<template>
  <div ref="console" class="console" :class="status">
    <a @click="animate('maximize')" class="toggle"></a>
    <a @click="animate('close')" class="icon-toggle">
      <div class="icon">>_</div>
      <div class="icon-title">{{ title }}</div>
    </a>
    <div class="bar">
      <small>>_ {{ title }}</small>
      <div class="dots">
        <div @click.prevent="animate('maximize')"></div>
        <div @click.prevent="animate('minimize')"></div>
        <div @click.prevent="animate('close')"></div>
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
      status: null,
      top: 0,
      left: 0,
      width: 0,
      height: 0,
    };
  },
  methods: {
    animate(status) {
      if (this.status === status) {
        this.$refs.console.style.top = `${this.top}px`;
        this.$refs.console.style.left = `${this.left}px`;
        this.$refs.console.style.width = `${this.width}px`;
        this.$refs.console.style.height = `${this.height}px`;
        setTimeout(() => {
          this.status = null;
          this.$refs.console.style.top = null;
          this.$refs.console.style.left = null;
          this.$refs.console.style.width = null;
          this.$refs.console.style.height = null;
          this.top = 0;
          this.left = 0;
          this.width = null;
          this.height = null;
        }, 200);
      } else {
        this.top = this.$refs.console.offsetTop;
        this.left = this.$refs.console.offsetLeft;
        this.width = this.$refs.console.offsetWidth;
        this.height = this.$refs.console.offsetHeight;
        this.$refs.console.style.top = `${this.top}px`;
        this.$refs.console.style.left = `${this.left}px`;
        this.$refs.console.style.width = `${this.width}px`;
        this.$refs.console.style.height = `${this.height}px`;
        this.status = status;
        setTimeout(() => {
          this.$refs.console.style.top = null;
          this.$refs.console.style.left = null;
          this.$refs.console.style.width = null;
          this.$refs.console.style.height = null;
        }, 50);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.console {
  @apply bg-gray-800 px-2 py-1 rounded-lg relative;
  font-family: "Source Code Pro", monospace;

  .toggle {
    @apply hidden absolute top-0 bottom-0 left-0 right-0 cursor-pointer;
  }

  .icon-toggle {
    @apply hidden flex-col items-center justify-center cursor-pointer;
  }

  &.minimize {
    @apply absolute transition-all ease-in-out duration-200;
    top: calc(100vh - 3rem);
    left: 2rem;

    &:hover {
      top: calc(100vh - 3.5rem);
    }

    .toggle {
      @apply block;
    }

    .bar .dots {
      @apply hidden;
    }

    .slot {
      @apply max-w-0 max-h-0 opacity-0;
    }
  }

  &.maximize {
    @apply absolute transition-all ease-in-out duration-200 top-0 left-0 m-0 w-full h-full;
  }

  &.close {
    @apply absolute transition-all ease-in-out duration-200 w-auto h-auto top-4 left-4 opacity-0 bg-transparent;

    .bar,
    .slot {
      display: none;
    }

    .icon-toggle {
      @apply flex;

      .icon{
        @apply w-14 h-14 bg-gray-800 text-white text-2xl font-bold rounded-xl flex justify-center items-center;
      }
    }
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