<script>
export default {
  name: "Card",
  props: {
    title: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
    publishAt: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      default: "Default desc",
    },
    author: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      isRead: false,
    };
  },
  emits: ["read"],
  methods: {
    handleMarkAsRead() {
      this.isRead = !this.isRead;
      this.$emit("read", this.isRead);
    },
  },
};
</script>

<template>
  <div class="card">
    <div>
      <span v-if="!isRead">UNREAD</span>
      <span v-else>READ</span>
    </div>
    <figure>
      <img :src="image" alt="" />
    </figure>
    <h2>{{ title }}</h2>
    <p>
      <small>{{ publishAt }}</small>
    </p>
    <div class="card__desc">{{ description }}</div>
    <div class="card__author">{{ author.firstname }} {{ author.lastname }}</div>
    <button @click="handleMarkAsRead">Mark as {{ !isRead ? "read" : "unread" }}</button>
  </div>
</template>

<style lang="scss" scoped>
.card {
  box-shadow: 0 0 2px 2px rgba(#000, 0.2);
}
</style>
