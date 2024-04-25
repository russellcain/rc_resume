<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname" style="margin-top: -5px; margin-bottom: 5px">
        {{ person.name.first }} "{{ person.name.nickname }}"
        {{ person.name.last }}
      </div>
      <div class="banner__position">{{ person.position }}</div>
      <!-- <div class="banner__location">{{ person.birth.location }}</div> -->
      <div class="section" style="margin: 0">
        <div class="section-content section-content--plain">
          <a
            v-if="person.contact.github"
            class="section-link"
            :href="contactLinks.github"
          >
            {{ person.contact.github }}
            <i
              class="section-link__icon fa fa-github"
              style="margin-left: 8px; margin-right: 0"
            ></i>
          </a>

          <div class="section-link">
            {{ person.contact.phone }}
            <i
              class="section-link__icon material-icons"
              style="margin-left: 8px; margin-right: 0"
              >phone</i
            >
          </div>

          <a class="section-link" :href="contactLinks.email">
            {{ person.contact.email }}
            <i
              class="section-link__icon material-icons"
              style="margin-left: 8px; margin-right: 0"
              >mail</i
            >
          </a>
        </div>
      </div>
    </div>

    <div class="content">
      <div class="content__left">
        <div class="section">
          <div class="section-headline" style="justify-content: flex-end">
            {{ lang.about }}
          </div>

          <div class="section-content section-content--plain">
            {{ person.about }}
            <br />
            <br />
            {{ person.knowledge }}
            <br />
            <br />
            {{ person.bonus }}
          </div>
        </div>

        <div v-if="person.skills" class="section">
          <div class="section-headline" style="justify-content: flex-end">
            Stack
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.skills"
              class="grid-item"
              :key="index"
              :href="skill.url"
            >
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline" style="justify-content: flex-end">Hobbies</div>
          <div class="section-content section-content--plain">
            <a v-for="(hobby, index) in person.hobbies" class="section-link" :key="index">
              {{ hobby.name }}
              <i
                class="section-link__icon material-icons"
                :style="`margin-left: 8px; margin-right: ${hobby.margin}`"
                >{{ hobby.icon }}</i
              >
            </a>
          </div>
        </div>
      </div>

      <div class="content__right">
        <div class="section">
          <div class="section-headline" style="margin-bottom: -5px">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>

          <div class="section-content">
            <a
              v-for="(experience, index) in person.experience"
              :key="index"
              class="section-content__item"
              style="padding-top: 10px"
              :href="experience.website"
            >
              <span class="section-content__header">
                <div class="section-content__header">{{ experience.position }}</div>
                <div class="section-content__subheader">
                  {{ experience.company }}
                </div>
              </span>

              <i class="section-content__text">
                {{ experience.timeperiod }}
              </i>
              <div
                v-for="(description, inner_index) in experience.descriptions"
                :key="inner_index"
              >
                <span
                  class="section-content section-content__plain"
                  style="margin-top: 15px; padding-left: 1px"
                  >{{ description }}</span
                >
              </div>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i
            >{{ lang.education }}
          </div>

          <div class="section-content">
            <a class="section-content__item">
              <span class="section-content__header"> {{ person.school }} </span>
            </a>
            <a
              v-for="(education, index) in person.education"
              class="section-content__item"
              :key="index"
              :href="education.website"
              style="margin-top: 10px"
            >
              <span class="section-content__header">
                {{ education.school }}
              </span>
              <span class="section-content__subheader">{{ education.degree }}</span>
              <i class="section-content__text">
                {{ education.timeperiod }}
              </i>
              <span class="section-content__text--light">
                {{ education.description }}
              </span>
            </a>
          </div>
        </div>

        <div v-if="person.projects" class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">code</i>{{ lang.projects }}
          </div>

          <div class="section-content">
            <a
              v-for="(project, index) in person.projects"
              :key="index"
              class="section-content__item"
              style="margin-top: 10px"
            >
              <span class="section-content__header"> {{ project.name }} </span>
              <span class="section-content__subheader">{{ project.platform }}</span>
              <span class="section-content__text--light">
                {{ project.description }}
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <img class="picture" />
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'cool-rtl2';
export default Vue.component(name, getVueOptions(name));
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
@accent-color: #744c61;
@banner-color: #4c745f;
@banner-height: 120px;
@picture-size: 120px;
@picture-offset: 35px;
@base-padding: 30px;
@left-column-width: 240px;

@left_side: {
  justify-content: 'flex-end';
};

@right_side: {
  justify-content: 'flex-start';
};

.resume {
  position: relative;
  font-family: 'Roboto' !important;
  font-size: 0.9em;
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 2 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 5px solid @accent-color;
  content: url('../../resume/id.png');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  display: flex;
  flex-direction: column;
  align-items: flex-end;

  color: rgba(255, 255, 255, 0.879);

  &__fullname {
    font-size: 32px;
  }

  &__position {
    font-size: 16px;
  }

  &__location {
    font-size: 12px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: rgba(255, 255, 255, 0.59);
    background-color: @accent-color;

    .section-headline {
      color: white;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 20px 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  justify-content: flex-start;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 8px;
    font-size: 1.4em;
  }
}

.section-link {
  font-size: 1.1em;
  color: rgba(255, 255, 255, 0.59) !important;
  text-decoration: none;
  justify-content: flex-end;

  &__icon {
    color: white;
    &--left {
      margin-left: 8px;
    }
  }
}

.section-content {
  margin-top: 5px;
  padding-left: 32px;
  font-size: 14px;

  &__item {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 5px;
    text-decoration: none;
    color: #00104f;
  }

  &__header {
    display: block;
    font-size: 1.1em;
    font-weight: 500;
  }

  &__subheader {
    display: block;
    font-weight: 400;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;
    }
  }

  &__plain {
    font-weight: 300;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    text-decoration: none;
    color: #00104f;
  }

  &--plain {
    padding: 0;
    text-align: right;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
  justify-content: flex-end;
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid white;
  color: white;
  margin-top: 5px;
  padding: 5px;
}
</style>
