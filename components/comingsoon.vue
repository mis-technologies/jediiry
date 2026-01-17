<template>
 <div class="tw-relative">
  <div class="tw-my-10 tw-grid tw-grid-cols-1 sm:tw-grid-cols-2 lg:tw-grid-cols-2 tw-gap-6">
    <div
      class="tw-bg-grey tw-rounded-lg"
      :key="index"
      v-for="(item, index) in items"
    >
      <a target="_blank" :href="item.url">
        <div class="tw-relative">
          <div
            class="show_bg_2 tw-rounded-2xl"
            :style="{
              'background-image': `linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 1)), ${getUrl(item.image)}`,
            }"
          >
            <button class="tw-main-badge tw-py-1 tw-px-6 tw-bg-white tw-text-black tw-rounded-2xl">
              {{ item.badge }}
            </button>

            <div class="tw-text-2xl tw-text-white tw-main-bottom">
              <p>{{ item.content }}</p>
              <p class="tw-text-xs">{{ item.body }}</p>
            </div>
          </div>
        </div>
      </a>
    </div>
  </div>
</div>
</template>

<script >
import defaultSavings from "~/assets/images/bursary.png";
import defaultPanza from "~/assets/images/sproutly.png";
import defaultMother from "~/assets/images/shikaan.png";
import chop from "~/assets/images/hupchop.png";
export default {
  name: "StatsCard",
  props: {
    items: {
      type: Array,
      default: () => {
        return [
          {
            badge: "2022",
            content: "Bursary",
            body: "SproutlyAfrica test contestst",
            image: defaultSavings,
            tag: "",
            url: "https://bursary.ng/",
          },
          {
            badge: "2022",
            content: "SproutlyAfrica",
            body: `
                 This is a platform where I led a team of developers to build Sproutly Africa, a fintech‑education solution designed for schools in Nigeria. The project focuses on delivering secure, modern, and accessible digital financial tools tailored to the educational sector.
            `,
            image: defaultPanza,
            tag: "",
            url: "https://sproutly.africa/sproutly-books/overview",
          },
          {
            badge: "2024",
            content: "Croner I",
            body: `
                  This is a platform that I lead and manage, where I oversee the implementation of new AI features and the continuous upgrade of the underlying infrastructure.
            `,
            image: defaultMother,
            tag: "",
            url: "https://library.croneri.co.uk",
          },
          {
            badge: "2024",
            body: `
                 This was a blockchain event hosted and sponsored by Polygon, where I spoke about the transformative impact blockchain will have on the fintech industry. I highlighted how organisations can leverage blockchain’s security, transparency, and decentralisation to reshape financial systems and drive the next generation of fintech innovation
            `,
            content: "Polygon DabClub Brimingham",
            image: chop,
            tag: "",
            url: "https://www.linkedin.com/posts/michael-ejeh-6735711b6_last-weekend-we-launched-the-polygon-devx-activity-7205795472450469888-d7TC?utm_source=share&utm_medium=member_ios&rcm=ACoAACBHqsQB4wE8jdBW1IyueyhmUsmGQqOY2M0",
          },
        ];
      },
    },
  },
  data() {
    return {
      flickity: null,
    };
  },
  methods: {
    getUrl(img) {
      return `url(${img})`;
    },
    nextSlide() {
      this.flickity.next();
    },
    previousSlide() {
      this.flickity.previous();
    },
  },
  mounted() {
    this.flickity = new Flickity(".coming-carousel", {
      initialIndex: 1,
      prevNextButtons: false,
      pageDots: true,
      wrapAround: true,
      autoPlay: 5000,
      draggable: true,
      freeScroll: true,
      contain: true,
      rightToLeft: false,
      pauseAutoPlayOnHover: true,
    });
  },
};
</script>

<style lang="scss" scoped>
.show_bg_2 {
  width: 500px;
  height: 300px;
  background-size: cover;
  color: white;
  padding: 20px;
}
.carousel-cell {
  min-width: 300px;
  margin-right: 50px;
}
.carousel-control {
  position: absolute;
  color: white;
  top: 50%;
  width: 100%;
  margin-top: -50px;
}
.tw-left-control {
  background-color: white;
  border-radius: 5px;
  padding: 1rem 1.5rem;
  margin-left: -2rem;
  box-shadow: 20px 20px 80px rgb(185, 185, 185);
}
.tw-right-control {
  background-color: white;
  border-radius: 5px;
  padding: 1rem 1.5rem;
  margin-right: -2rem;
  box-shadow: 20px 20px 80px rgb(199, 199, 199);
}
.tw-main-bottom {
  position: absolute;
  bottom: 2rem;
  left: 1rem;
  text-align: left;
  padding: 1rem;
}
.tw-main-badge {
  position: absolute;
  top: 2rem;
  right: 1rem;
}
</style>
