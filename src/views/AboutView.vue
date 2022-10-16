<template>
  <div class="about">
    <div class="card" v-for="course in courses" :key="course">
      <h3 class="">{{ course.title }}</h3>
      <p>{{ course.desc }}</p>
      <strong>{{ course.ratings }}</strong>
      <button class="btn">click me</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      courses: [
        {
          title: "Clean code",
          desc: "nice programming code...",
          ratings: 4,
        },
        {
          title: "dirty code",
          desc: "dirty programming code...",
          ratings: 6,
        },
        {
          title: "mad code",
          desc: "mad programming code...",
          ratings: 5,
        },
        {
          title: "fading code",
          desc: "fading programming code...",
          ratings: 2,
        },
      ],
    };
  },
};
</script>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
    background-color: rgb(86, 86, 177);
    justify-items: center;
    align-items: center;
    display: flex;
    gap: 2px;
    margin: 1px;
  }
  .card {
    display: flex;
    color: black;
    flex-direction: column;
    padding: 2px;
    justify-items: center;
    align-items: center;
    background-color: bisque;
    box-shadow: black 2px;
  }
}
</style>
