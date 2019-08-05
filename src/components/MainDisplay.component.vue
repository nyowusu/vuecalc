<template>
  <div class="container">
    <div id="aux" class="display display-aux">{{ auxilliary }}display aux</div>
    <div id="main" class="display display-main">{{ main }} display main</div>
  </div>
</template>

<script>
export default {
  name: "Displays",
  props: {
    main: String,
    auxilliary: String
  }
};
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: 2fr 3fr;
  grid-template-areas:
    "auxilliary"
    "main";
}

.display {
  background-color: #333;
  color: white;
  padding: 0.44em;
  text-align: right;
}
.display-main {
  border-radius: 0 0 1rem 1rem;
  font-size: 1.75rem;
  grid-area: main;
  border-top: 2px solid red;
}

.display-aux {
  border-radius: 1rem 1rem 0em 0em;
  font-size: 1.25rem;
  font-weight: bold;
  grid-area: auxilliary;
}
</style>
