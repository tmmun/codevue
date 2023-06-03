<template>
  <div v-for="(code, index) in codeArr" :key="code">
    <div class="codeCont">
      <pre>{{ code }}</pre>
      <div class="butCont">
        <div class="but" @click="$emit('save', index)">add</div>
        <div class="but" @click="$emit('remove', index)">del</div>
      </div>
    </div>
    <div class="codeCont">
      <div class="butCont">
        <div
          class="but"
          v-if="categoryCode[index] == 'none'"
          @click="$emit('add', index, 'js')"
        >
          Js
        </div>

        <div
          class="but"
          v-if="categoryCode[index] == 'none'"
          @click="$emit('add', index, 'c#')"
        >
          c#
        </div>

        <div
          class="but"
          v-if="categoryCode[index] == 'none'"
          @click="$emit('add', index, 'Py')"
        >
          Py
        </div>

         <div
          class="but"
          v-if="categoryCode[index] == 'none'"
          @click="$emit('add', index, 'c++')"
        >
          c++
        </div>

        <div
          class="but"
          v-if="categoryCode[index] != 'none'"
          @click="$emit('add', index, 'none')"
        >
          swap
        </div>
        <div class="cell">{{ categoryCode[index] }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    codeObjekt: Object,
    codeArr: Array,
    categoryCode: Array,
  },
  emits: ["remove", "save", "add"],
};
</script>

<style>
.codeCont {
  display: flex;
  margin-top: 10px;
  background-color: #363636;
  padding: 10px 10px;
  color: #aaaaaa;
  font-family: "Roboto Condensed", sans-serif;
  border-radius: 5px;
}
.cell {
  text-align: center;
  padding: 0px 10px;
  height: 30px;
  background-color: #292929;
  color: #aaaaaa;
  line-height: 28px;
  border-radius: 5px;
  border: solid #292929;
  border-width: 2, 2px;
}
.but {
  margin-right: 5px;
  text-align: center;
  font-size: 15px;
  padding: 0px 10px;
  height: 30px;
  background-color: #363636;
  color: #aaaaaa;
  line-height: 29px;
  border-radius: 5px;
  border: solid #aaaaaa;
  border-width: 2px;
  cursor: pointer;
}
.but:active {
  background-color: #aaaaaa;
  color: #363636;
}
.toolsCont {
  display: flex;
}
.butCont {
  margin-top: 5px;
  display: flex;
}
.codeCont {
  margin-top: 5px;
  display: flex;
  flex-direction: column;
}
</style>