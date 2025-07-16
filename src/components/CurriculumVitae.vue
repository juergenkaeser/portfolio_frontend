
<script setup>
import data from '../assets/data.json';
</script>

<template>
  <div class="text-container-cv">
    <h2 class="cv__title">Kenntnisse</h2>
    <div class="cv-lists">
      <h3 class="cv-list-headline" role="label">{{ data.experiencesHeadline }}</h3>
      <ul class="cv-list">
        <li class="cv-list-item" v-for="(experience, index) in data.experiences" :key="'experience-' + index">
          <span class="profession">{{ experience.job }}</span> - {{ experience.entry }}
        </li>
      </ul>

      <h3 class="cv-list-headline" role="label">{{ data.educationHeadline }}</h3>
      <ul class="cv-list" aria-label="Education">
        <li class="cv-list-item" v-for="(degree, index) in data.degrees" :key="'degree-' + index">
          {{ degree }}
        </li>
      </ul>

      <h3 class="cv-list-headline" role="label">{{ data.technologiesHeadline }}</h3>
      <ul class="cv-list">
        <li class="cv-list-item" v-for="(tech, index) in data.techologies" :key="'tech-' + index">
          {{ tech }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss">
.text-container-cv {
  height: 100%;
  padding: var(--spacing-xl) var(--spacing-l);

  @media (min-width: 768px) {
    padding: var(--spacing-xxl) var(--spacing-l) var(--spacing-xxl) var(--spacing-l);
  }

  .cv-lists {
    max-height: 100%;
    height: 100%;
    padding: var(--spacing-s);

    @media (min-width: 768px) {
      padding: var(--spacing-l);
    }

    .cv-list {
      padding: 0; 
      margin: var(--spacing-large) 0 0 0;
    }

    .cv-list-item {
      .profession {
        font-style: italic;
      }
    }
  }
}
</style>