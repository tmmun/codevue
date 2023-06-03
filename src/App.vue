<template>
  <div class="baseCont">
    <input
      type="range"
      min="150"
      max="500"
      step="10"
      v-model="height"
      @change="heightIncrease()"
      class="height-slider"
    />
    <textarea
      class="codeBlock"
      v-model="codeObjekt.codeText"
      name=""
      id=""
      cols="30"
      rows="10"
      :style="codeObjekt.styleCodeBlock"
    ></textarea>

    <code-cell
      :codeArr="codeObjekt.codeArr"
      @remove="deleteCode"
      @save="saveCode"
      @add="addCategory"
      :categoryCode="codeObjekt.categoryCode"
    />

    <div @click="addCell()" class="butt">add new cell</div>
  </div>
</template>

<script>
import CodeCell from "./components/codeCell.vue";
export default {
  components: { CodeCell },
  data() {
    return {
      height: 150,

      codeObjekt: {
        codeArr: ["<N0>"],
        categoryCode: ["<N0>"],
        codeText: "",
        cellCount: 0,
        styleCodeBlock: {
          height: "150px",
        },
      },
    };
  },
  methods: {
    saveCode(index) {
      if (this.codeObjekt.codeArr.includes(this.codeObjekt.codeText)) {
        this.codeObjekt.codeText = "Уже есть";
      } else {
        localStorage.setItem("codeCell" + index, this.codeObjekt.codeText);
        this.codeObjekt.codeArr[index] = this.codeObjekt.codeText;
        console.log(this.codeObjekt.codeArr[index]);
      }
    },
    deleteCode(index) {
      localStorage.setItem("codeCell" + index, "<N" + index + ">");
      this.codeObjekt.codeArr[index] = "<N" + index + ">";
      console.log(this.codeObjekt.codeArr[index]);
    },
    addCategory(index, cat) {
      this.codeObjekt.categoryCode[index] = cat;
      localStorage.setItem("categoryCell" + index, cat);
    },
    addCell() {
      this.codeObjekt.cellCount++;
      this.codeObjekt.codeArr.push("<N" + this.codeObjekt.cellCount + ">");
      this.codeObjekt.categoryCode.push("<N" + this.codeObjekt.cellCount + ">");
      localStorage.setItem("cellCountKey", this.codeObjekt.cellCount);
      localStorage.setItem(
        "codeCell" + this.codeObjekt.cellCount,
        "<N" + this.codeObjekt.cellCount + ">"
      );
      localStorage.setItem(
        "categoryCell" + this.codeObjekt.cellCount,
        "<N" + this.codeObjekt.cellCount + ">"
      );

      console.log(this.codeObjekt);
    },
    heightIncrease() {
      this.codeObjekt.styleCodeBlock.height = this.height + "px";
    },
  },
  mounted() {
    {
      //cell code generate
      if (localStorage.length == 0) {
        localStorage.setItem("cellCountKey", this.codeObjekt.cellCount);

        for (let i = 0; i <= this.codeObjekt.cellCount; i++) {
          localStorage.setItem("codeCell" + i, this.codeObjekt.codeArr[i]);
          localStorage.setItem("categoryCell" + i, this.codeObjekt.codeArr[i]);
        }
      } else {
        this.codeObjekt.cellCount = localStorage.getItem("cellCountKey");

        for (let i = 0; i <= this.codeObjekt.cellCount; i++) {
          this.codeObjekt.codeArr[i] = localStorage.getItem("codeCell" + i);
          this.codeObjekt.categoryCode[i] = localStorage.getItem(
            "categoryCell" + i
          );
        }
      }

      console.log(this.codeObjekt.codeArr);
    }
  },
};
</script>

<style>
.butt {
  margin-top: 5px;
  text-align: center;
  font-size: 15px;
  padding: 0px 10px;
  height: 30px;
  background-color: #363636;
  color: #aaaaaa;
  line-height: 29px;
  border-radius: 5px;
  font-family: "Roboto Condensed", sans-serif;
  cursor: pointer;
}
.height-slider {
  appearance: none;
  background-color: #1f1e1e;
  border-radius: 7px;
  margin-bottom: 10px;
  width: 99.7%;
}
.height-slider::-webkit-slider-thumb {
  appearance: none;
  background-color: #aaaaaa;
  width: 10px;
  height: 10px;
  border-radius: 2px;
}
.codeBlock {
  padding: 10px 10px;
  color: #aaaaaa;
  resize: none;
  width: 97.5%;
  border-radius: 5px;
  background-color: rgb(31, 30, 30);
  border-width: 0px;
  height: 151px;
  resize: none;
}
.codeBlock:focus {
  outline: none;
}
.baseCont {
  width: 800px;
  background-color: #292929;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
  margin-bottom: 30px;
  padding: 30px 30px;
  border-radius: 5px;
}
.back {
  background-color: #141414;
}
.codeBlock::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}
.codeBlock::-webkit-scrollbar-track-piece {
  background: transparent;
  -webkit-border-radius: 6px;
}
.codeBlock::-webkit-scrollbar-thumb:vertical {
  height: 5px;
  background-color: #292929;
  border-radius: 3px;
}
.codeBlock::-webkit-scrollbar-thumb:horizontal {
  width: 5px;
  background-color: #292929;
}
</style>