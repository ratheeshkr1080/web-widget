<template>
  <div class="container">
    <div class="grid-container" v-bind:class="{ disableddiv: !editable }">
      <div class="paper">
        <div class="card" v-if="enhanced">
          <div class="card-checkbox">
            <input type="checkbox" v-on:click="handleToggleAll(left)" />
          </div>
          <div class="card-header">
            <label for="Choices">Choices</label>
            <label for="Choices">{{
              `${numberOfChecked(left)}/${left.length} selected`
            }}</label>
          </div>
        </div>
        <div class="list-content">
          <div :key="leftValue.id" v-for="leftValue in left">
            <ListItem
              :name="leftValue.name"
              @change="handleToggle(leftValue)"
              :checked="checked.indexOf(leftValue) !== -1"
            />
          </div>
        </div>
      </div>
      <div class="btn-container">
        <Button
          :label="allMoveRightImage"
          v-on:click="handleAllRight"
          v-if="viewAllTransferBtn"
        />
        <Button :label="largeThanImage" v-on:click="handleCheckedRight()" />
        <Button :label="lessthanImage" v-on:click="handleCheckedLeft()" />
        <Button
          :label="allMoveLeftImage"
          v-on:click="handleAllLeft"
          v-if="viewAllTransferBtn"
        />
      </div>
      <div class="paper">
        <div class="card" v-if="enhanced">
          <div class="card-checkbox">
            <input type="checkbox" id="" v-on:click="handleToggleAll(right)" />
          </div>
          <div class="card-header">
            <label for="Choosen">Choosen : </label>
            <label for="Choosen">{{
              `${numberOfChecked(right)}/${right.length} selected`
            }}</label>
          </div>
        </div>
        <div class="list-content">
          <div :key="rightValue.id" v-for="rightValue in right">
            <ListItem
              :key="rightValue.id"
              :name="rightValue.name"
              @change="handleToggle(rightValue)"
              :checked="checked.indexOf(rightValue) !== -1"
            />
          </div>
        </div>
      </div>
    </div>
    <!-- <div>{{ customList("ratheesh", [1, 2, 3, 4, 5]) }}</div> -->
  </div>
</template>
<script>
import Button from "./Button.vue";
import ListItem from "./ListItem.vue";

function not(a, b) {
  return a.filter((value) => b.indexOf(value) === -1);
}

function intersection(a, b) {
  return a.filter((value) => b.indexOf(value) !== -1);
}

function union(a, b) {
  return [...a, ...not(b, a)];
}

export default {
  name: "TransferList",
  components: {
    Button,
    ListItem,
  },
  props: {
    enhanced: Boolean,
    onChangedValues: Function,
    initValues: Array,
    transfferdItems: Array,
    editable: Boolean,
    lessthanImage: String,
    largeThanImage: String,
    allMoveRightImage: String,
    allMoveLeftImage: String,
    viewAllTransferBtn: Boolean,
  },

  data() {
    return {
      checked: [],
      left: [],
      right: [],
    };
  },

  created() {
    console.log("initValues", this.initValues);
    console.log("transfferdItems", this.transfferdItems);
    const leftfiltered = this.initValues.filter((el) => {
      return this.transfferdItems.indexOf(el.value) === -1;
    });
    this.left = leftfiltered;
    const rightfiltered = this.initValues.filter((el) => {
      return this.transfferdItems.indexOf(el.value) !== -1;
    });
    this.right = rightfiltered;
  },

  methods: {
    emitToParent() {
      this.$emit("onChangedValues", this.right);
    },
    numberOfChecked(items) {
      const noCheckedvalue = intersection(this.checked, items).length;
      return noCheckedvalue;
    },
    leftChecked() {
      const leftCheckedvalue = intersection(this.checked, this.left);
      return leftCheckedvalue;
    },
    rightChecked() {
      const rightCheckedvalue = intersection(this.checked, this.right);
      return rightCheckedvalue;
    },

    handleToggle(value) {
      const currentIndex = this.checked.indexOf(value);
      const newChecked = [...this.checked];
      if (currentIndex === -1) {
        newChecked.push(value);
      } else {
        newChecked.splice(currentIndex, 1);
      }
      this.checked = newChecked;
    },

    handleToggleAll(items) {
      if (this.numberOfChecked(items) === items.length) {
        this.checked = not(this.checked, items);
      } else {
        this.checked = union(this.checked, items);
      }
    },
    handleCheckedRight() {
      this.right = this.right.concat(this.leftChecked());
      this.left = not(this.left, this.leftChecked());
      // this.checked = not(this.checked, this.leftChecked());
      this.checked = [];
      // this.emitToParent();
      
    },
    handleCheckedLeft() {
      this.left = this.left.concat(this.rightChecked());
      this.right = not(this.right, this.rightChecked());
      // this.checked = not(this.checked, this.rightChecked());
       this.checked = [];
    },

    handleAllLeft() {
      this.left = this.left.concat(this.right);
      this.right = [];
      this.checked=[];
    },

    handleAllRight() {
      this.right = this.right.concat(this.left);
      this.left = [];
           this.checked=[];
      console.log("this.right", this.right);
    },
  },
  computed: {
    customListw(title, items) {
      return (
        <div>
          <div>{title} </div>
          <div>{items} </div>
        </div>
      );
    },
  },
};
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  background-color: #f5f5f5;
  border: 2px solid blcak;
}
.grid-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin: 50px;
}
.paper {
  background-color: white;
  width: 200px;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
}
.list-content {
  height: 300px;
  overflow: auto;
}

.btn-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 62px;
  padding: 50px 20px;
}
.card {
  display: flex;
  justify-content: center;
  text-align: center;
  border-bottom: 2px solid #f2f2f2;
  padding: 15px;
}
.card-header {
  display: flex;
  flex-direction: column;
  line-height: 22px;
}
.disableddiv {
  pointer-events: none;
  opacity: 0.4;
}
</style>