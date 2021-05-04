<script>
import { onMounted, ref, watch } from "vue";
export default {
  props: {
    buttonColor: {
      type: String,
      default: "#006694",
    },
    containerRadius: {
      type: String,
      default: "0.5rem",
    },
    shadow: {
      type: String,
      default: "0 0 10px rgba(0, 0, 0, 0.5);",
    },
  },
  setup() {
    const currentIndex = ref(1);
    const sliderLength = ref(1);

    watch(currentIndex, (_, __) => {
      if (currentIndex.value <= 0) {
        currentIndex.value = sliderLength.value;
      }
      if (currentIndex.value > sliderLength.value) {
        currentIndex.value = 1;
      }
      window.location.href = `#carousel-${currentIndex.value}`;
    });

    onMounted(() => {
      const carousel = document.querySelector(".carousel");
      sliderLength.value = carousel.querySelectorAll(".carousel-item").length;
      carousel.querySelectorAll(".carousel-item").forEach((item) => {
        item.setAttribute("draggable", true);
      });
      carousel.addEventListener("dragend", (e) => {
        e.preventDefault();
      });

      carousel.addEventListener("dragover", (e) => {
        e.preventDefault();
      });

      carousel.addEventListener("dragstart", (e) => {
        const width = e.target.clientWidth / 2;
        if (e.clientX > width) {
          currentIndex.value++;
        } else {
          currentIndex.value++;
        }
      });
    });
    return {
      currentIndex,
    };
  },
};
</script>

<template>
  <div class="vue3-carousel-container">
    <div
      :style="`box-shadow: ${shadow}; border-radius: ${containerRadius} `"
      class="carousel"
    >
      <slot />
    </div>
    <a
      :style="'background-color:' + buttonColor"
      role="button"
      @click="currentIndex--"
      class="left"
      >left</a
    >
    <a
      :style="'background-color:' + buttonColor"
      role="button"
      @click="currentIndex++"
      class="right"
      >right</a
    >
  </div>
</template>


<style>
.vue3-carousel-container {
  position: relative;
  min-height: 25rem;
  width: 60%;
}
@media (max-width: 500px) {
  .vue3-carousel-container {
    width: 90%;
  }
}
.vue3-carousel-container .carousel {
  scroll-behavior: smooth;
  scrollbar-width: none;
  overflow-x: scroll;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
}
.vue3-carousel-container .carousel-item {
  width: 100%;
  flex-shrink: 0;
}
.vue3-carousel-container a {
  font-family: sans-serif;
  color: white;
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  height: 4rem;
  width: 4rem;
  border-radius: 50%;
  border: none;
  display: grid;
  place-items: center;
  text-decoration: none;
}
.vue3-carousel-container a.left {
  left: 5%;
}
.vue3-carousel-container a.right {
  right: 5%;
}
</style>