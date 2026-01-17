<template>
  <div class="tw-bg-secondary">
    <div
      data-aos="fade-down"
      data-aos-easing="ease-out-cubic"
      data-aos-duration="200"
    >
      <Logo color="tw-text-white" />

      <div class="tw-grid tw-grid-cols-7 tw-h-screen  tw-w-10/12 tw-mx-auto md:tw-mx-0 md:tw-w-full">
        <div
          class=" 
          tw-mt-8
          md:tw-mt-0
            tw-col-span-7
            md:tw-col-span-3
            tw-bg-secondary
            tw-grid
            tw-grid-cols-5
            tw-justify-center
            md:tw-items-center
            tw-z-40
          "
        >
          <div
            class="
              tw-space-y-12 tw-pt-32 tw-pb-5
              md:tw-col-start-2
              tw-col-span-5
              md:tw-col-span-3
               tw-text-center
               md:tw-text-left
            "
          >
            <p class="main-font tw-text-5xl tw-text-primary">
              {{ allTechs[index]["technology"] }}
            </p>

            <p class="tw-text-white">
              {{ allTechs[index]["description"] }}
            </p>

            <p
              class="
                tw-group tw-text-2xl
                hover:tw-text-white
                tw-text-complimentry tw-text-right
              "
            >
              <i
                v-if="index > 0"
                @click.prevent="decreaseIndex"
                class="
                  tw-text-right
                  tw-p-3
                  tw-bg-gray-600
                  tw-rounded-full
                  tw-cursor-pointer
                  bx
                  hover:tw-text-complimentry
                  bx-left-arrow-alt
                  tw-text-primary
                "
              ></i>
              <i
                v-if="index < allTechs.length - 1"
                @click.prevent="increaseIndex"
                class="
                  tw-text-right
                  tw-p-3
                  tw-bg-gray-600
                  tw-rounded-full
                  tw-cursor-pointer
                  bx
                  hover:tw-text-complimentry
                  bx-right-arrow-alt
                  tw-text-primary
                "
              ></i>
            </p>
          </div>
        </div>
        <div
          class="
            tw-hidden
            md:tw-block
            tw-col-span-7
            md:tw-col-span-4
            tw-relative
          "
        >
          <alltech></alltech>
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
      replace: [{ from: "A Software Engineer", to: "A Product Designer" }],
      index: 0,
      allTechs: [
        {
          technology: "Platform Engineer",
          description: `
Platform Engineer with 8 years of experience leading the design, development, and operation of scalable cloud‑native platforms. I bring a strong leadership mindset to engineering, guiding teams in adopting best practices, improving reliability, and building automation that accelerates delivery. My work spans cloud architecture, Kubernetes orchestration, infrastructure‑as‑code, CI/CD automation, and backend engineering, enabling organisations to ship faster, operate more efficiently, and scale with confidence. I’m known for driving clarity in complex systems, mentoring engineers, and championing modern platform standards that elevate both team performance and product quality.
`,
        },
        {
          technology: "AI Cloud Architect",
          description: `
AI Cloud Architect specialising in the design and delivery of scalable, cloud‑native platforms that power intelligent applications and modern distributed systems. Focused on architecting end‑to‑end AI solutions across major cloud providers, integrating compute, data, orchestration, and automation to support high‑performance workloads.

Experience spans cloud architecture, distributed systems, serverless design, container orchestration, and AI/ML deployment pipelines. Skilled at creating holistic solutions that seamlessly connect user‑facing experiences with robust backend infrastructure, event‑driven systems, and cloud‑based AI services.

Known for evaluating emerging technologies, adopting modern architectural patterns, and translating complex requirements into secure, scalable, and efficient cloud AI platforms. Work blends hands‑on engineering depth with architectural leadership, ensuring every solution is resilient, future‑ready, and aligned with long‑term business goals.          `,
        },
               {
          technology: "Blockchain",
          description: `
Blockchain Architect focused on designing secure, scalable, and production‑ready distributed ledger systems. Experienced in building end‑to‑end blockchain architectures across public, private, and hybrid networks, including smart‑contract platforms, decentralised applications, and Layer‑2 solutions. Skilled at integrating blockchain components with cloud‑native infrastructure, event‑driven systems, and modern DevOps practices. Known for strong architectural leadership, deep understanding of emerging protocols, and the ability to deliver high‑throughput, interoperable, and future‑ready blockchain platforms.
`,
        },
      ],
    };
  },
  methods: {
    decreaseIndex() {
      if (this.index > 0) {
        this.index = this.index - 1;
      }
    },
    increaseIndex() {
      if (this.index < this.allTechs.length - 1) {
        this.index = this.index + 1;
      }
    },
  },
});
</script>
