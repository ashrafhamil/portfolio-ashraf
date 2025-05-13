<template>
  <section id="skills" class="light-section">
    <div class="container-fluid">
      <h1 class="section-header">{{ heading }}</h1>

      <!-- start of filters -->
      <div class="row filters flex-column justify-content-center">
        <ul class="list-inline d-flex justify-content-center flex-wrap gap-3" data-aos="fade-right"
          data-aos-duration="1000">
          <li v-for="category in uniqueCategories" :key="category" class="list-inline-item">
            <a class="nav-item p-2 p-md-4" :class="category === currentCategory" :data-category="category"
              @click="setCategory">
              {{ category }}
            </a>
          </li>
        </ul>
      </div>
      <!-- end of filters -->


      <div style="display: flex; align-items: center;">
        <!-- start of skill container -->
        <div id="skill-container" data-aos="fade-up" data-aos-duration="800"
          class="d-flex flex-wrap justify-content-center mt-4">
          <div v-for="item in filteredSkills" :key="item.skillName"
            class="d-flex flex-column align-items-center text-center m-3" style="min-width: 120px;">
            <i :class="[item.faClass.replace('colored', ''), { 'colored': isHovered === item.skillName }]"
              class="skill-icon mb-2" @mouseover="isHovered = item.skillName" @mouseleave="isHovered = null" />
            <span style="font-size: 1rem;">
              {{ item.skillName }}
            </span>
          </div>
        </div>
        <!-- end of skill container -->
      </div>

    </div>
    <!-- end of main container  -->
    <Arrow />
  </section>
</template>

<script>
import data from "../../data/data.json";
import Arrow from "../components/Arrow.vue";

export default {
  name: "Skills",
  props: {},
  components: {
    Arrow,
  },
  data() {
    return {
      isHovered: null,
      skills: data.skills.categories,
      heading: data.main.headings.skills,
      currentCategory: data.skills.defaultCategory,
    };
  },
  computed: {
    filteredSkills() {
      return this.skills.filter((x) => x.category === this.currentCategory);
    },
    uniqueCategories() {
      return [...new Set(this.skills.map((x) => x.category))];
    }
  },
  methods: {
    setCategory(event) {
      this.currentCategory = event.target.dataset.category;
    },
  },
};
</script>

<style lang="scss">
.skill-icon {
  font-size: 5rem;
  color: rebeccapurple;
  transition: all 0.3s ease;
}
</style>
