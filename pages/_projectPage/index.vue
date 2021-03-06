<template>
  <div id="project-page" class="flex-centered-column">
    <appHeader :changesColor="false" />
    <h1 class="t-header">{{ project.name }}</h1>
    <p class="t-body-primary">{{ project.description }}</p>
    <div v-if="project.additional" id="iframe-container">
      <iframe
        :src="project.additional"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
    </div>
    <section class="project-links">
      <a
        v-if="project.github"
        :href="project.github"
        target="_blank"
        class="t-button"
        >Github</a
      >
      <a v-if="project.url" :href="project.url" target="_blank" class="t-button"
        >Visit</a
      >
    </section>
    <projectFeature
      v-for="(feature, index) in project.features"
      :key="index"
      :name="feature.name"
      :text="feature.text"
      :image="feature.image"
    />
    <p
      v-if="project.learning"
      class="t-body-primary project-learning project-bottom-blocks"
    >
      <span class="t-header-small">Learning: </span>{{ project.learning }}
    </p>
    <p
      v-if="project.problems"
      class="t-body-primary project-problems project-bottom-blocks"
    >
      <span class="t-header-small">Problems: </span>{{ project.problems }}
    </p>
  </div>
</template>

<script>
import projectsJSON from "../../static/projects.json";
import appHeader from "../../components/appHeader";
import projectFeature from "../../components/projectFeature";

export default {
  head() {
    return {
      title: "Joan Carazo - Portfolio",
      link: [
        {
          rel: "stylesheet",
          href:
            "https://fonts.googleapis.com/css2?family=Nunito&family=Space+Mono&display=swap"
        }
      ]
    };
  },
  components: {
    appHeader,
    projectFeature
  },
  data() {
    return {
      project: {}
    };
  },
  created() {
    this.project = projectsJSON.find(
      project => project.id === this.$route.params.projectPage
    );
  }
};
</script>

<style lang="scss">
#project-page {
  h1 {
    margin: 50px 0;
    text-align: center;
  }

  p {
    margin: 0 $margin-regular;
  }
}

#iframe-container {
  position: relative;
  width: 80%;
  overflow: hidden;
  background-color: lightgrey;
  padding: 0;
  margin: 50px;

  @media (min-width: $breakpoint) {
    width: 60%;
  }
}

#iframe-container::after {
  padding-top: 56.25%;
  display: block;
  content: "";
}

#iframe-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.project-learning {
  align-self: flex-end;
  background-color: $secondary-dark;
  justify-content: flex-start;
  text-align: left;

  @media (min-width: $breakpoint) {
    background-color: transparent;
    background-image: url(../../assets/images/svg/learning-background.svg);
    background-size: cover;
    padding-left: 80px !important;
  }
}

.project-problems {
  align-self: flex-start;
  background-color: $accent-color;
  justify-content: flex-end;
  text-align: right;

  @media (min-width: $breakpoint) {
    background-color: transparent;
    background-image: url(../../assets/images/svg/problems-background.svg);
    background-size: cover;
    padding-right: 80px !important;
  }
}

.project-bottom-blocks {
  color: white;
  width: 100%;
  padding: 20px 40px;
  margin: 0 0 -1px !important;

  @media (min-width: $breakpoint) {
    width: 75%;
  }
}

.project-links {
  margin: 50px 0;
}

.project-links a {
  color: black;
  text-decoration: none;
  padding-bottom: 10px;
  border-bottom: 2px solid $accent-bright;
  margin: 0 10px;
}

.project-links a:nth-child(2) {
  border-bottom: 2px solid $secondary-dark;
}
</style>
