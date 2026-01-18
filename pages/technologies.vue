<template>
  <div class="tw-bg-secondary tw-h-screen tw-flex tw-flex-col">
    <div
      data-aos="fade-down"
      data-aos-easing="ease-out-cubic"
      data-aos-duration="200"
      class="tw-flex-1 tw-flex tw-flex-col"
    >
      <Logo color="tw-text-white" />

      <!-- MAIN GRID -->
      <div class="tw-grid tw-grid-cols-7 tw-h-full tw-w-11/12 tw-mx-auto md:tw-w-full">

        <!-- LEFT SECTION -->
        <div
          class="
            tw-col-span-7 md:tw-col-span-3
            tw-grid tw-grid-cols-5
            tw-items-center
            tw-justify-center
            tw-h-full
          "
        >
          <div
            class="
              tw-col-span-5 md:tw-col-start-2 md:tw-col-span-3
              tw-text-center md:tw-text-left
              tw-space-y-8
              tw-py-10 md:tw-py-0
            "
          >
            <!-- TECHNOLOGY TITLE -->
            <p class="main-font tw-text-3xl sm:tw-text-4xl md:tw-text-5xl lg:tw-text-6xl tw-text-primary">
              {{ allTechs[index].technology }}
            </p>

            <!-- DESCRIPTION -->
            <p class="tw-text-white tw-text-sm sm:tw-text-base md:tw-text-lg tw-leading-relaxed">
              {{ allTechs[index].description }}
            </p>

            <!-- NAVIGATION ARROWS -->
            <p class="tw-text-right tw-text-2xl tw-text-complimentry tw-group">
              <i
                v-if="index > 0"
                @click.prevent="decreaseIndex"
                class="bx bx-left-arrow-alt tw-p-3 tw-bg-gray-600 tw-rounded-full tw-cursor-pointer tw-text-primary hover:tw-text-complimentry"
              ></i>

              <i
                v-if="index < allTechs.length - 1"
                @click.prevent="increaseIndex"
                class="bx bx-right-arrow-alt tw-p-3 tw-bg-gray-600 tw-rounded-full tw-cursor-pointer tw-text-primary hover:tw-text-complimentry"
              ></i>
            </p>
          </div>
        </div>

        <!-- RIGHT SECTION (IMAGE / ANIMATION) -->
        <div
          class="tw-hidden md:tw-block tw-col-span-7 md:tw-col-span-4 tw-relative tw-h-full"
        >
          <alltech />
        </div>

      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "project",
  data() {
    return {
      index: 0,
      allTechs: [
        {
          technology: "Platform Engineer",
          description: `
          A Platform Engineer with eight years of experience building and operating scalable cloud‑native systems. Skilled in cloud architecture, Kubernetes, infrastructure‑as‑code, CI/CD automation, and backend engineering, with a strong focus on leadership, reliability, and driving engineering best practices.
          `,
        },
        {
          technology: "AI Cloud Architect",
          description: `
          AI Cloud Architect specialising in scalable, cloud‑native platforms powering intelligent applications. Experienced in distributed systems, serverless design, container orchestration, and AI/ML deployment pipelines.
          `,
        },
        {
          technology: "Blockchain",
          description: `
          Blockchain Architect focused on secure, scalable distributed ledger systems. Skilled in smart‑contract platforms, decentralised applications, and Layer‑2 solutions.
          `,
        },
      ],
    };
  },
  methods: {
    decreaseIndex() {
      if (this.index > 0) this.index--;
    },
    increaseIndex() {
      if (this.index < this.allTechs.length - 1) this.index++;
    },
  },
});
</script>

<style scoped>
/* Optional: improve readability on very small screens */
@media (max-width: 480px) {
  p {
    line-height: 1.4;
  }
}
</style>
