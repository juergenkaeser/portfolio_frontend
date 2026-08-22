<script setup>
import ProjectItem from './ProjectItem.vue'
import { onMounted, defineProps } from 'vue'
import Glide, { Controls, Swipe, Autoplay } from '@glidejs/glide/dist/glide.modular.esm'
import data from '../assets/data.json';

defineProps({
  fontColorSecondary: {
    type: String,
    default: '',
    required: true
  }
});

onMounted(() => {
  new Glide('.glide', {
    type: 'carousel',
    autoplay: 12000,
    hoverpause: true,
    animationDuration: 1000
  }).mount({ Controls, Swipe, Autoplay })
})
</script>

<template>
  <div class="project-wrapper">
  <h2 class="projects__title">Projekte</h2>
    <div class="glide">
      <div class="glide__track" data-glide-el="track">
        <ul class="glide__slides">
          <li
            class="glide__slide"
            v-for="(project, index) in data.projects"
            :key="index"
          >
            <ProjectItem>
              <template #headline>{{ project.headline }}</template>
              <template #subline>{{ project.subline }}</template>
              {{ project.description }}
              <template v-if="index === data.projects.length - 1">
                <br />
                <br />
                <a
                  href="https://github.com/juergenkaeser/portfolio_frontend"
                  target="_blank"
                >
                  Zum Projekt auf GitHub
                </a>
              </template>
            </ProjectItem>
          </li>
        </ul>
        <div class="glide__bullets" data-glide-el="controls[nav]">
          <button
            v-for="(project, index) in data.projects"
            :key="'bullet-' + index"
            class="glide__bullet"
            :data-glide-dir="'=' + index"
          ></button>
        </div>
      </div>
      <div class="glide__arrows" data-glide-el="controls">
        <button class="glide__arrow glide__arrow--left" data-glide-dir="<">
          <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
            <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
            <g id="SVGRepo_iconCarrier">
              <path
                d="M15 6L9 12L15 18M15 12H15.01"
                :stroke=fontColorSecondary
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              ></path>
            </g>
          </svg>
        </button>
        <button class="glide__arrow glide__arrow--right" data-glide-dir=">">
          <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
            <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
            <g id="SVGRepo_iconCarrier">
              <path
                d="M9 6L15 12L9 18M9 12H9.01"
                :stroke=fontColorSecondary
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              ></path>
            </g>
          </svg>
        </button>
      </div>
    </div>
  </div>
  
</template>

<style lang="scss" scoped>
@import '@glidejs/glide/dist/css/glide.core.min.css';

.project-wrapper {
  height: 100%;
  padding: var(--spacing-xl) var(--spacing-l);

  // glide is used as background-container
  // background: url('../assets/code-example.jpg');
  // background-position: center;
  // background-size: cover;

  // @media (max-width: 768px) {
  //   background: var(--bg-color-light);
  // }

  background: var(--bg-color-light);

  @media (min-width: 768px) {
    padding: var(--spacing-xxl) var(--spacing-l) var(--spacing-xxl) var(--spacing-l);
  }

  .glide {
    height: 80%;

    .projects__title {
      margin-bottom: 0;
    }

    .glide__track {
      height: 100%;

      .glide__slides {
        position: relative;
        height: 100%;

        .glide__slide {
          padding: 0 var(--spacing-xl);

          @media (min-width: 768px) {
            padding: 0 var(--spacing-xxl);
          }
        }
      }

      .glide__bullets {
        position: absolute;
        bottom: 10%;
        left: 50%;
        transform: translateX(-50%);
        width: 60%;
        display: flex;
        justify-content: space-between;

        @media (min-width: 768px) {
          bottom: 10%;
          width: 25%;
        }

        .glide__bullet {
          // TODO: add tokens for 20 and 24px spacing
          width: 20px;
          height: 20px;
          border-radius: 50%;
          padding: 0;
          border: 0;
          background-color: var(--font-color-primary);

          @media (min-width: 768px) {
            width: 24px;
            height: 24px;
          }

          &.glide__bullet--active {
            background-color: var(--font-color-secondary);
          }

          &:hover {
            transition: background-color 0.3s ease-in-out;
            background-color: var(--font-color-secondary);
            cursor: pointer;
          }
        }
      }
    }

    .glide__arrows {
      .glide__arrow {
        position: absolute;
        top: 55%;
        transform: translateY(-50%);
        width: var(--spacing-xl);
        height: var(--spacing-xl);

        @media (min-width: 768px) {
          width: var(--spacing-xxl);
          height: var(--spacing-xxl);
        }

        &.glide__arrow--left {
          left: 0;
        }

        &.glide__arrow--right {
          right: 0;
        }

        &:hover {
          cursor: pointer;
        }

        // deactivates default button styles
        background-color: transparent;
        box-shadow: initial;
        border: none;
        outline: none;

        svg {
          max-height: 100%;
          max-width: 100%;
        }
      }
    }
  }
}
</style>
