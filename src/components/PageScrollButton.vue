<template>
  <div class="page-scroll-btn-mobile">
    <div class="page-scroll-btn-mobile-up" @click="scrollTop">
      <img
          alt=""
          src="../assets/images/arrow-up.svg"
      />
    </div>
    <div class="page-scroll-btn-mobile-down" @click="scrollBottom">
      <img
          alt=""
          src="../assets/images/arrow-down.svg"
      />
    </div>
  </div>

  <div :style="scrollMobileBtnStyle" class="page-scroll-btn">
    <img
        src="../assets/images/arrow-up.svg"
        class="page-scroll-btn-up"
        :style="clientPosition !== 'top' ? 'display: block' : 'display: none'"
        alt=""
        @click="scrollUp"
    />
    <img
        src="../assets/images/arrow-down.svg"
        class="page-scroll-btn-down"
        :style="clientPosition !== 'bottom' ? 'display: block' : 'display: none' "
        alt=""
        @click="scrollDown"
    />
  </div>
</template>

<script>
export default {
  name: "PageScrollButton",
  data() {
    return {
      clientPosition: "top"
    };
  },
  mounted() {
    window.addEventListener("scroll", () => {
      this.setClientPosition();
    });
  },
  computed: {
    scrollMobileBtnStyle() {
      if (this.clientPosition === 'middle') {
        return {
          'min-height': '86px',
          'max-height': '86px'

        }
      } else {
        return {
          'min-height': '43px',
          'max-height': '43px'
        }
      }
    }
  },
  methods: {
    setClientPosition() {
      if (document.documentElement.scrollTop === 0) {
        this.clientPosition = "top";
      } else if (document.documentElement.scrollHeight - 5 < document.documentElement.scrollTop + document.documentElement.clientHeight) {
        this.clientPosition = "bottom";
      } else {
        this.clientPosition = "middle";
      }
    },
    scrollUp() {
      window.scrollTo(0, 0);
    },
    scrollDown() {
      const documentHeight = Math.max(
          document.body.scrollHeight, document.documentElement.scrollHeight,
          document.body.offsetHeight, document.documentElement.offsetHeight,
          document.body.clientHeight, document.documentElement.clientHeight
      );
      window.scrollTo(0, documentHeight);
    },
    scrollTop() {
      const topElem = document.getElementById('top')
      topElem.scrollIntoView({
        behavior: 'smooth',
        block: "start"
      })
    },
    scrollBottom() {
      const bottomElem = document.getElementById('bottom')
      bottomElem.scrollIntoView({
        behavior: 'smooth',
        block: "end"
      })
    },
  }
}
</script>

<style lang="scss" scoped>

$mobile-breakpoint: 768px;
$container-width: 1200px;
$container-width-mobile: 560px;

.page-scroll {
  &-btn, &-btn-mobile {
    position: fixed;
    bottom: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    background-color: rgba(#cccccc, 0.4);
    border-radius: 50px;
    transition: all 0.2s;
    z-index: 100;
  }

  &-btn {
    right: auto;
    left: calc((100vw - 1200px) / 2 + 1210px);

    &:hover {
      opacity: 0.7;
    }

    @media (max-width: $container-width + 170px) {
      right: 10px;
      left: auto;
    }

    @media (max-width: $mobile-breakpoint) {
      display: none;
    }

    &-up, &-down {
      transition: all 0.2s;
      cursor: pointer;
      z-index: 100;

      &:hover {
        transform: scale(1.2);
      }
    }

    &-up {
      padding: 14px 10px 17px;
    }

    &-down {
      padding: 17px 10px 14px;
    }

    &-mobile {
      display: none;
      z-index: 100;

      @media (max-width: $mobile-breakpoint) {
        right: 10px;
        left: auto;
        display: flex
      }

      &-up, &-down {
        z-index: 100;

        > img {
          width: 16px;
        }
      }

      &-up {
        padding: 8px 7px 14px;
      }

      &-down {
        padding: 14px 7px 8px;
      }
    }
  }
}

</style>