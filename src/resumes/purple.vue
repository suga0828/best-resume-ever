<template>
  <section class="resume">
    <header>
      <h1>{{ person.name.first }} {{ person.name.middle }}  {{ person.name.last }}</h1>
      <h2>{{ person.position }}</h2>
      <ul role="list">
        <li>
          <i class="fa fa-envelope" aria-hidden="true"></i>
          <a :href='"mailto:" + person.contact.email'>{{ person.contact.email}}</a>
        </li>
        <li>
          <i class="fa fa-phone-square" aria-hidden="true"></i>
          <a :href='"tel:" + person.contact.phone'>{{ person.contact.phone }}</a>
        </li>
        <li v-if="person.contact.website">
          <i class="fa fa-home" aria-hidden="true"></i>
          <a :href='person.contact.website'>{{ person.contact.website }}</a>
        </li>
        <li v-if="person.contact.github">
          <i class="fa fa-github" aria-hidden="true"></i>
          <a :href='contactLinks.github'>{{ person.contact.github }}</a>
        </li>
      </ul>
    </header>
    <section class="body">
      <article>
        <h1>{{ lang.experience }}</h1>
        <hr />
        <div v-for="experience in person.experience" :key="experience.company">
          <h2>{{ experience.position }}</h2>
          <h3>{{ experience.company }} <template v-if="experience.timeperiod">| <span>{{ experience.timeperiod }}</span></template>
          </h3>

          <p v-if="experience.description">{{ experience.description }}</p>
          <ul v-if="experience.list">
              <li v-for="(item, index) in experience.list" :key="index">{{ item }}</li>
          </ul>
        </div>
      </article>
      <article>
        <h1>{{ lang.education }}</h1>
        <hr />
        <div v-for="education in person.education" :key="education.degree">
          <h2>{{ education.degree }}</h2>
          <h3>{{ education.description }} <template v-if="education.timeperiod"> | <span>{{ education.timeperiod }}</span></template>
          </h3>
        </div>
      </article>
      <article v-if="person.skills != []">
        <h1>{{ lang.skills }}</h1>
        <hr />
        <p class="spacing" v-if="person.knowledge">{{ person.knowledge }}</p>
        <ul class="four-columns">
          <li v-for="skill in person.skills" :key="skill.name">{{ skill.name }}</li>
        </ul>
      </article>
    </section>
    <footer v-if="person.about">
      <section>
        <h1>{{ lang.about }}</h1>
        <p>{{ person.about }}</p>
      </section>
    </footer>
  </section>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'purple';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@font-family: 'Open Sans', sans-serif;

@primary-text-color: white;
@secondary-text-color: #680568;

@bg-color: purple;
@box-shadow: inset 0px 0px 200px #301030;

@padding-layout:  40px 100px;

.resume {
  color: white;
  font-family: @font-family;
}

h1, h2, h3, hr, p, ul {
  margin: 0;
}

a {
  color: inherit;
}

header {
  color: @primary-text-color;
  min-height: 136px;
  background-color: @bg-color;
  box-shadow: @box-shadow;
  padding: @padding-layout;
  padding-bottom: 20px;
  text-align: center;

  h1 {
    font-size: 28px;
    line-height: 1.25;
  }

  h2 {
    font-size: 18px;
    margin-bottom: 16px;
  }

  ul {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 0;
    font-size: 12px;

    &[role="list"] {
      list-style: none;
    }
  }

  li {
    display: flex;
    align-items: center;
    padding: 2px 10px;

    i {
      font-size: 22px;
      margin-right: 8px;
    }
  }
}

.body {
  padding: @padding-layout;
  color: @secondary-text-color;

  & > article {
    h1 {
      font-size: 26px;
      text-transform: uppercase;
    }

    div {
      margin: 10px 0 10px 50px;
    }

    h2 {
      font-size: 16px;
      font-weight: bold;
    }

    h3 {
      font-size: 12px;
      font-weight: 400;
      margin-bottom: 8px;
    }

    span {
      color: rgba(@secondary-text-color, .5);
      font-size: 12px;
    }

    p {
      font-size: 12px;
    }

    .spacing {
      margin: 4px 0 6px;
    }

    ul {
      font-size: 12px;
    }

    .four-columns {
      column-count: 4;
    }
  }
}

footer {
  padding: @padding-layout;
  min-height: 136px;
  background-color: @bg-color;
  box-shadow: @box-shadow;
  box-sizing: border-box;
  position: absolute;
  bottom: 0;
  width: 100%;

  h1 {
    font-size: 24px;
  }

  p {
    font-size: 14px;
  }
}

</style>
