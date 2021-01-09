<template>
  <div class="header-container">
    <div id="header">
      <div
        @click.prevent="windowStatus = 'normal'"
        class="console-app"
        v-if="windowStatus === 'close'"
      >
        <div class="console-icon">>_</div>
        Informations
      </div>
      <div class="animate__animated animate__fadeInDown animate__delay-1s mb-6">
        <h1>
          Alexandre
          <br />
          <span class="opacity-50">Muhl</span>
        </h1>
        <hr/>
        <h2>Développeur Web Frontend / Backend</h2>
      </div>

      <am-console
        title="Informations"
        v-model="windowStatus"
        class="m-4"
        :class="windowClasses"
        @close="closeWindow"
        @minimize="minimizeWindow"
      >
        <h3 class="line1" :style="{ animationDelay: `${linesDelay}ms` }">
          📧
          <a href="mailto:contact@alexandre-muhl.fr"
            >contact@alexandre-muhl.fr
          </a>
        </h3>
        <br />
        <h3 class="line2" :style="{ animationDelay: `${linesDelay + 1080}ms` }">
          📞 <a href="tel:+33613466802">0613466802</a>
        </h3>
        <br />
        <h3
          class="line3"
          :style="{ animationDelay: `${linesDelay + 1080 + 480}ms` }"
        >
          ➡️
          <a
            href="https://www.linkedin.com/in/alexandre-muhl-441737a3"
            target="_blank"
            >https://www.linkedin.com/in/alexandre-muhl-441737a3</a
          >
          <span
            class="caret"
            :style="{ animationDelay: `${linesDelay + 1080 + 480 + 2000}ms` }"
            >|</span
          >
        </h3>
      </am-console>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    setTimeout(() => {
      this.windowClasses = "animate__animated animate__zoomIn";
      this.linesDelay = 200;
    }, 8060);
  },
  data() {
    return {
      windowClasses: "animate__animated animate__fadeInLeft animate__delay-2s",
      windowStatus: "normal",
      linesDelay: 2500,
    };
  },
  methods: {
    closeWindow() {
      this.windowClasses = "animate__animated animate__zoomOut";
      this.linesDelay = 200;
      setTimeout(() => {
        this.windowClasses = "animate__animated animate__zoomIn";
        this.windowStatus = "close";
      }, 200);
    },
    minimizeWindow() {
      this.windowClasses = "";
      setTimeout(() => {
        this.windowClasses = "animate__animated animate__zoomIn";
      }, 100);
    },
  },
};
</script>

<style lang="scss">
.header-container {
  #header {
    @apply w-full z-10 bg-gradient-to-br from-indigo-100 to-indigo-300 flex flex-col items-center justify-center;
    height: 75vh;
    border-bottom-left-radius: 100px;
    top: calc(-75vh + 100px);
    hr{
      @apply w-12 h-2 mx-auto my-4 bg-gradient-to-br from-gray-600 to-gray-900;
    }
    
    h1 {
      @apply text-2xl md:text-5xl text-center uppercase font-bold leading-none;
      font-family: "Roboto";
      .lastname {
        @apply font-black;
      }
    }

    h2 {
      @apply text-xl md:text-3xl;
      font-family: "Source Code Pro", monospace;
    }

    .console-app {
      @apply absolute left-8 top-8 flex flex-col items-center justify-center cursor-pointer;

      .console-icon {
        @apply w-12 h-12 flex justify-center items-center bg-gray-800 text-white text-2xl leading-none rounded-lg font-bold;
      }
    }

    h3 {
      @apply inline font-semibold relative text-white text-xs md:text-xl pl-0 md:pl-8 mr-2 my-1 leading-5 transition-all duration-200 ease-in-out;

      &::before {
        @apply text-green-400 absolute hidden md:inline;
        content: "~#";
        left: 0;
      }

      top: -1px;

      &.line1 {
        &::after {
          content: "|";
          @apply absolute right-0 bottom-0 top-0 w-full text-transparent bg-gray-800;
          animation: typing 1080ms steps(27) forwards;
          animation-delay: inherit;
        }
      }

      &.line2 {
        &::after {
          content: "|";
          @apply absolute right-0 bottom-0 top-0 w-full text-transparent bg-gray-800;
          animation: typing 480ms steps(12) forwards;
          animation-delay: inherit;
        }
      }

      &.line3 {
        @apply pr-2;
        &::after {
          content: "|";
          @apply absolute right-0 bottom-0 top-0 w-full text-transparent bg-gray-800;
          animation: typing 2000ms steps(51) forwards;
          animation-delay: inherit;
        }
        .caret {
          @apply text-white absolute bottom-0 top-0 right-1 hidden md:block;
          animation: caret 1s step-end infinite;
        }
      }

      a:hover {
        text-decoration: underline;
      }
    }
  }
}

@keyframes typing {
  0% {
    color: white;
  }
  99% {
    width: 0;
    color: white;
  }
  100% {
    width: 0;
    color: transparent;
  }
}

@keyframes caret {
  50% {
    color: transparent;
  }
}
</style>