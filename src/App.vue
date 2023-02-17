<template>
  <div class="h-full w-full">
    <header class="py-36">
      <h1 class="text-center text-4xl font-bold">
        CSS3 Perspective Playground
      </h1>
    </header>
    <main
      class="mx-auto flex w-1/2 flex-col-reverse items-center justify-center lg:max-w-4xl lg:flex-row"
    >
      <section class="w-full lg:mr-8 lg:w-1/2">
        <div class="flex-col">
          <!-- Perspective -->
          <label>perspective: {{ perspective }}px;</label>
          <input type="range" min="0" max="999" v-model="perspective" />

          <!-- RotateX -->
          <label>rotateX: {{ rotateX }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateX" />

          <!-- RotateY -->
          <label>rotateY: {{ rotateY }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateY" />

          <!-- RotateZ -->
          <label>rotateZ: {{ rotateZ }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateZ" />

          <div class="mt-4 space-x-4 lg:space-x-8">
            <!-- Reset -->
            <button
              class="bg-purple-600 px-4 py-1 text-2xl text-white transition-colors duration-150 hover:bg-purple-700"
              @click.prevent="reset"
            >
              Reset
            </button>

            <!-- Copy -->
            <button
              class="bg-purple-600 px-4 py-1 text-2xl text-white transition-colors duration-150 hover:bg-purple-700"
              @click.prevent="copy"
            >
              Copy
            </button>
          </div>
        </div>
      </section>
      <section class="mb-10 lg:mb-0 lg:w-1/2">
        <div class="max-w-fit border border-solid border-[#8d81f3] p-12">
          <div
            class="h-16 w-16 bg-[#8d81f3] md:h-36 md:w-36"
            :style="box"
          ></div>
        </div>
      </section>
    </main>
  </div>
</template>
<script setup>
import { computed, ref } from "vue";

const perspective = ref(100);
const rotateX = ref(0);
const rotateY = ref(0);
const rotateZ = ref(0);

const box = computed(() => {
  return {
    transform: `
    perspective(${perspective.value}px)
    rotateX(${rotateX.value}deg)
    rotateY(${rotateY.value}deg)
    rotateZ(${rotateZ.value}deg)
    `,
  };
});

const reset = () => {
  perspective.value = 0;
  rotateX.value = 0;
  rotateY.value = 0;
  rotateZ.value = 0;
};

const copy = async () => {
  let text = `transform:${box.value.transform};`;

  await navigator.clipboard.writeText(text);

  alert("CSS Copied to Clipboard!");
};
</script>
