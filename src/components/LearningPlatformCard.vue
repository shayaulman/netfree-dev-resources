<template>
  <g-link
    :to="link"
    :style="`border-top: 3px solid ${color}`"
    class="m-3 w-72 h-48 flex justify-center bg-custom-bg-card rounded-md transform hover:-translate-y-1 ease-in duration-100"
  >
    <div class="py-2 px-4 w-full flex flex-col justify-between">
      <div class="h-20">
        <div
          :class="{ 'flex-row-reverse': isHebrew(name) }"
          class="flex justify-center items-center"
        >
          <img
            :src="`https://www.google.com/s2/favicons?domain=${link}`"
            alt="Platform logo"
            class="m-1"
          />
          <h1
            :style="`color: ${color}`"
            class="m-1 text-lg text-custom-text-primary"
          >
            {{ name }}
          </h1>
        </div>
        <p
          class="mt-1 px-4 text-center text-xs text-custom-gray-1 font-hairline"
        >
          {{ desc }}
        </p>
      </div>

      <ul class="rtl flex flex-wrap -mx-2 text-xs p-4">
        <li
          v-for="tag in tags"
          @click.prevent="$emit('tag-selected', tag.name)"
          :key="tag.name"
          :style="`color: ${tag.color}; background: ${tag.background}`"
          :class="{ 'shadow-outline': selectedTag === tag.name }"
          class="m-1 px-3 py-1 text-xxs rounded-full"
        >
          {{ tag.name }}
        </li>
      </ul>
    </div>
  </g-link>
</template>

<script>
import IsraelFlagIcon from "~/components/UI/IsraelFlagIcon";
export default {
  name: "LearningPlatformCard",
  components: { IsraelFlagIcon },
  props: {
    name: String,
    desc: String,
    link: String,
    color: String,
    tags: Array,
    selectedTag: String,
  },
  computed: {
    direction() {
      return this.hebrew ? "rtl" : "ltr";
    },
  },
  methods: {
    isHebrew(text) {
      const HEBREW = RegExp("[\u0590-\u05FF]");
      return HEBREW.test(text);
    },
  },
};
</script>

<style lang="scss" scoped>
.bg {
  background: repeating-linear-gradient(
    45deg,
    var(--bg-card-2),
    var(--bg-card-2) 10px,
    #03a87c70 10px,
    #03a87c70 20px
  );
}
</style>
