<template>
  <div class="cannon">
    <div class="cannon__path cannon__path--sm cannon__path--angle-2">
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-1"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-2"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-1"
      ></div>
      <div class="cannon__confetti-spacer"></div>
    </div>
    <div class="cannon__path cannon__path--md cannon__path--angle-1">
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-2"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-2"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-1"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-4"
      ></div>
      <div class="cannon__confetti-spacer"></div>
    </div>
    <div class="cannon__path cannon__path--lg cannon__path--angle0">
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-1"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-4"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-2"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div class="cannon__confetti-spacer"></div>
    </div>
    <div class="cannon__path cannon__path--md cannon__path--angle1">
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-1"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-4"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-2"
      ></div>
      <div class="cannon__confetti-spacer"></div>
    </div>
    <div class="cannon__path cannon__path--sm cannon__path--angle2">
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-2"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-3"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--flake cannon__confetti--color-4"
      ></div>
      <div
        class="cannon__confetti cannon__confetti--ribbon cannon__confetti--color-1"
      ></div>
      <div class="cannon__confetti-spacer"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: '',
};
</script>

<style lang="scss" scoped>
$color-violet: #492684;
$color-purple: #bea4ff;
$color-yellow: #feb535;
$color-red: #ff6e83;
$color-cyan: #58cafe;
$animation-duration: 2.5s;

/* debug */
$debug-animation-count: infinite;

/* Cannon */
.cannon {
  height: 70vh;
  width: 1px;
  position: relative;
  transform-origin: 30% 100%;
  animation: cannon-explosion $animation-duration
    cubic-bezier(0.18, 0.89, 0.32, 1.28) both;

  // debug
  animation-iteration-count: $debug-animation-count;

  @keyframes cannon-explosion {
    0% {
      transform: scale(0);
    }
    80% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  /* Paths */
  &__path {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    transform-origin: 50% 100%;
    padding-bottom: 30%;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: space-around;
    align-items: center;

    &--lg {
      height: 100%;
    }

    &--md {
      height: 95%;
    }

    &--sm {
      height: 90%;
    }

    &--angle {
      &-2 {
        transform: rotate(-15deg);
      }

      &-1 {
        transform: rotate(-7.5deg);
      }

      &1 {
        transform: rotate(7.5deg);
      }

      &2 {
        transform: rotate(15deg);
      }
    }
  }

  /* Confettis */
  &__confetti {
    flex: 0 1 auto;
    animation-duration: $animation-duration;
    animation-timing-function: ease-out;
    animation-fill-mode: both;
    animation-iteration-count: $debug-animation-count;

    &:nth-child(even) {
      animation-name: confetti-rotate-l;

      @keyframes confetti-rotate-l {
        0% {
          transform: rotate(0) scaleY(1);
        }
        50% {
          transform: rotate(2turn) scaleY(1.5);
        }
        100% {
          transform: rotate(2.05turn) scaleY(1);
        }
      }
    }

    &:nth-child(odd) {
      animation-name: confetti-rotate-r;

      @keyframes confetti-rotate-r {
        0% {
          transform: rotate(0) scaleY(1);
        }
        50% {
          transform: rotate(-2turn) scaleY(1.5);
        }
        100% {
          transform: rotate(-2.05turn) scaleY(1);
        }
      }
    }

    /* Types */
    &--ribbon {
      height: 1em;
      width: 0.5em;
      border-radius: 0.1em;
    }

    &--flake {
      height: 0.5em;
      width: 0.5em;
      border-radius: 50%;
    }

    /* Colors */
    &--color-1 {
      background-color: $color-yellow;
    }

    &--color-2 {
      background-color: $color-purple;
    }

    &--color-3 {
      background-color: $color-red;
    }

    &--color-4 {
      background-color: $color-cyan;
    }
  }
}

.party-popper {
  position: absolute;
  left: 50%;
  bottom: 13vh;
  font-size: 2em;
  transform: translateX(-50%) rotate(-45deg);
}

.cannon {
  position: absolute;
  bottom: 5vh;
  left: 50%;
}
</style>
