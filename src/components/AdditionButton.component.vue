<template>
  <div class="btn" @click="operate">{{ operator }}</div>
</template>

<script>
export default {
  name: "AdditionButton",
  props: {
    operator: String,
    actionClick: null,
  },
  methods: {
    operate: function() {
      this.$emit("setOperator", this.operator);
    },
  },
};
</script>

<style scoped>
.btn {
  font-weight: bold;
  font-size: 1.2rem;
  background-color: #f7dbdb;
  width: 100%;
  height: 100%;
  text-align: center;
  border-radius: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: #333333 solid 3px;
}

.btn:active {
  transform: translateY(3px);
}

@media only screen and (min-width: 760px) {
  .btn {
    font-size: 2rem;
  }
}
</style>
