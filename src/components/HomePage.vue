<template>
  <div id="app">
    <!------------------------------------------------------------------------------------------------->
    <!-- 1. Template Syntax -->
    <h3 style="background: red">1. Template Syntax</h3>

    <!-- a) Text Interpolation -->
    <h1>{{ msg }}</h1>

    <!-- b) Raw HTML (v-html) -->
    <div v-html="paragraph"></div>
    <div>{{ paragraph }}</div>

    <!-- c) Attribute Bindings (v-bind:id) -->
    <div :id="id">This element's ID is: {{ id }}</div>

    <!-- d) JS Expressions Inside Syntax -->
    <div>{{ check ? "True" : "False" }}</div>
    <!------------------------------------------------------------------------------------------------->

    <!------------------------------------------------------------------------------------------------->
    <!-- 7. Event Handling [v-on:click] -->
    <h3 style="background: red">7. Event Handling</h3>
    <!-- a) Inline Handlers -->
    <button v-on:click="incrementMe++">Increment Me: {{ incrementMe }}</button>

    <!-- b) Method Handlers -->
    <button @:click="handleClick">Click Me</button>
    <!------------------------------------------------------------------------------------------------->

    <!------------------------------------------------------------------------------------------------->
    <!-- 6. List Rendering -->
    <h3 style="background: red">6. List Rendering</h3>
    <!-- a) v-for with an Object -->
    <div v-for="value in myObject" :key="value">{{ value }}</div>

    <!-- b) v-for with a Range -->
    <span v-for="n in 10" :key="n">{{ n }}</span>

    <!-- c) v-for on <template> -->
    <div v-for="name in names" :key="name">
      <p>{{ name }}</p>
      <hr />
    </div>

    <!-- d) v-for with v-if -->
    <div v-for="(name, i) in names" :key="i">
      <p v-if="name === 'mario'">{{ name }}</p>
    </div>

    <!-- e) v-for with a Component -->
    <!--                           -->
    <!--                           -->
    <!--                           -->

    <!------------------------------------------------------------------------------------------------->

    <!------------------------------------------------------------------------------------------------->
    <!-- 8. Form Input Bindings -->
    <h3 style="background: red">8. Form Input Binding</h3>
    <!-- a & b). v-model & v-model modifiers -->
    <input type="text" v-model.lazy="search" />
    <div v-for="name in nameSearch" :key="name">{{ name }}</div>
    <!------------------------------------------------------------------------------------------------->

    <!------------------------------------------------------------------------------------------------->
    <!-- 10. Components -->
    <h3 style="background: red">10. Components</h3>
    <!-- a, b & c). Props, Events & Slots -->
    <div :style="{ fontSize: postFontSize + 'em' }">
      <TestComponent :tests="testValues" @enlargeText="postFontSize += 0.1"
        >Some Text</TestComponent
      >
    </div>
    <!------------------------------------------------------------------------------------------------->

    <!------------------------------------------------------------------------------------------------->
    <!-- 11. Router -->
    <h3 style="background: red">11. Router</h3>
    <router-link to="/about">About Page</router-link>
    <!------------------------------------------------------------------------------------------------->
  </div>
</template>

<script>
import { ref, computed, watch, watchEffect } from "vue";
import TestComponent from "../components/TestComponent.vue";
export default {
  name: "HomePage",
  components: { TestComponent },
  emits: ["enlargeText"],
  setup() {
    // 3. Reactivity Fundamentals [ref(), <script setup>]
    const msg = ref("Hello World!");
    const postFontSize = ref(1);
    const paragraph = ref("<p>Hello</p>");
    const id = ref("1");
    const check = ref(false);
    const incrementMe = ref(0);
    const search = ref("");
    const myObject = ref({
      title: "Harry Potter",
      author: "J. K. Rowling",
      publishedAt: "1997-06-26",
    });
    const names = ref(["bowser", "mario", "luigi", "yoshi", "toad", "peach"]);

    // 2. Methods
    const handleClick = () => {
      alert("Clicked");
    };

    // 4. Computed Properties
    const nameSearch = computed(() => {
      return names.value.filter((name) => name.includes(search.value));
    });

    // 9. Watchers
    watch(search, () => {
      console.log("watching...");
    });
    watchEffect(() => {
      console.log("Watch Effect Ran", search.value);
    });

    // 10. Components
    const testValues = ref([
      { title: "title1", body: "body1", id: 1 },
      { title: "title2", body: "body2", id: 2 },
    ]);
    return {
      msg,
      paragraph,
      id,
      check,
      incrementMe,
      myObject,
      handleClick,
      nameSearch,
      testValues,
      postFontSize,
      names,
      search,
    };
  },
};
</script>
