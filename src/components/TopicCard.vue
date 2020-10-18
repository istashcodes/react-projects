<template>
  <div>
    <div
      class="accordion"
      v-bind:key="topic.id"
      v-for="(topic, i) in topics"
      v-bind:class="{ 'accordion-expanded': topic.expanded, 'accordion-archived': topic.archived }"
    >
      <!-- The click event of each accordion menu -->
      <div class="accordion-header">
        <a href="#" v-on:click.prevent="expand($event, i)">
          <div class="accordion-header">
            <div class="accordion-header-div">
             <img src="../assets/icon-edit.svg" />
            </div>
            <div class="accordion-header-div">{{ topic.title }}</div>
            <div class="accordion-header-div archive" @click.stop="archive(i)">
              <img src="../assets/icon-archive.png" />
              move to archive
            </div>
          </div>
          <div class="accordion-header-div">
            <div class="accordion-caret"></div>
          </div>
        </a>
      </div>
      <div class="accordion-body" v-bind:ref="'accordion-body-' + i">
        <div class="accordion-content">{{ topic.description }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { TweenLite, Elastic, Bounce } from 'gsap'
export default {
  name: 'topiccard',
  props: ['topics'],
  methods: {
    archive: function(i) {
      this.topics[i].archived = !this.topics[i].archived
    },
    expand: function(e, i) {
      // e.preventDefault()

      let el = this.$refs['accordion-body-' + i][0]

      if (this.topics[i].expanded === false) {
        this.topics[i].expanded = true

        TweenLite.to(el, 1, {
          height: el.scrollHeight,
          ease: Elastic.easeOut.config(1, 0.3)
        })
      } else {
        this.topics[i].expanded = false

        TweenLite.to(el, 0.5, {
          height: 0,
          ease: Bounce.easeOut
        })
      }
    }
  }
}
</script>

<style lang="scss">
$base-color: #000000;
$base-width: 700px;
$base-time: 200ms;

$app-background-color: #ffffff;
$app-padding: 2rem;

$accordion-background-color: #efefef;
$accordion-max-width: $base-width;
$accordion-padding: 2rem 1rem;
$accordion-border-radius: 0.3rem;
$accordion-box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);

$accordion-header-font-size: 1.2rem;
$accordion-header-height: 1rem;
$accordion-header-padding: 1rem 1rem 1rem 1rem;
$accordion-header-border-radius: 0.6rem;
$accordion-header-transition: background-color $base-time ease-in-out;

$accordion-header-hover-background-color: #ffffff;

$accordion-caret-color: $base-color;
$accordion-caret-background-image: linear-gradient(
  to top right,
  transparent 50%,
  $accordion-caret-color 50%
);
$accordion-caret-width: 16px;
$accordion-caret-height: 10px;
$accordion-caret-transform: scale(1);
$accordion-caret-transforming: scale(0.5);
$accordion-caret-expanded-transform: scale(1) rotate(180deg);

$accordion-body-content-padding: 1rem;

$archive-text-font-weight: 300;
$archive-text-font-size: 0.9rem;
$archive-text-line-height: 1.6rem;
$archive-text-font-style: italic;
$archive-text-font-color: #000aff;

@import url('https://fonts.googleapis.com/css?family=Montserrat:400,400i,700');

html,
body,
#app {
  color: $base-color;
  font-family: Roboto, Montserrat, sans-serif;
  font-size: 14px;
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

.accordion,
.accordion-header,
.accordion-body {
  font-family: inherit;
}

#app {
  background-color: $app-background-color;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  align-content: space-between;
}

.accordion {
  background-color: $accordion-background-color;
  width: 100%;
  max-height: 100%;
  max-width: $accordion-max-width;
  padding: none;
  margin: auto;
  margin-left: 0;
  margin-bottom: 16px;
  box-sizing: border-box;
  overflow: auto;
  box-shadow: $accordion-box-shadow;
  .accordion-caret {
    animation: accordion-is-expanded $base-time linear forwards;
  }
}

.accordion-archived {
  display: none;
}

.accordion-expanded {
  .accordion-caret {
    animation: accordion-is-inexpanded $base-time linear forwards;
  }
}

.accordion-header {
  color: inherit;
  font-size: $accordion-header-font-size;
  font-weight: bold;
  position: relative;
  display: flex;
  a {
    color: inherit;
    text-decoration: none;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
    border-radius: $accordion-header-border-radius;
    transition: $accordion-header-transition;
    &:not(.accordion-expanded):hover {
      background-color: $accordion-header-hover-background-color;
    }
  }
}

.accordion-header-div {
  padding: $accordion-header-padding;
  &.archive {
    font-weight: $archive-text-font-weight;
    font-size: $archive-text-font-size;
    line-height: $archive-text-line-height;
    font-style: $archive-text-font-style;
    color: $archive-text-font-color;
  }
  &:last-child {
    padding-left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

.accordion-caret {
  // background-image: $accordion-caret-background-image;
  background-image: url('../assets/icon-chevron-down.svg');
  width: $accordion-caret-width;
  height: $accordion-caret-height;
  // animation: accordion-is-expanded $base-time linear forwards;
}

.accordion-body {
  height: 0;
  overflow: hidden;
}

.accordion-content {
  padding: $accordion-body-content-padding;
}

@keyframes accordion-is-inexpanded {
  0% {
    transform: $accordion-caret-transform;
  }
  50% {
    transform: $accordion-caret-transforming;
  }
  100% {
    transform: $accordion-caret-expanded-transform;
  }
}

@keyframes accordion-is-expanded {
  0% {
    transform: $accordion-caret-expanded-transform;
  }
  50% {
    transform: $accordion-caret-transforming;
  }
  100% {
    transform: $accordion-caret-transform;
  }
}

@media screen and (min-width: $base-width) {
  #app {
    padding: $app-padding;
    overflow: auto;
  }

  .accordion {
    max-height: none;
    border-radius: $accordion-border-radius;
  }
}
</style>
