<template>
  <div>
    <TransferList
      :enhanced="true"
      :initValues="initValues"
      :transfferdItems="transfferdItems"
      :editable="true"
      :lessthanImage="lessthanImage"
      :largeThanImage="largeThanImage"
      :allMoveRightImage="allMoveRightImage"
      :allMoveLeftImage="allMoveLeftImage"
      :viewAllTransferBtn="true"
      :onChangedValues="updatedTransferList"
    />
    <DummyComp :valuess="valuearray" />
  </div>
</template>

<script>
import TransferList from "./TransferList.vue";
import DummyComp from "./DummyComp.vue";
export default {
  name: "TestTransferList",
  components: {
    TransferList,
    DummyComp,
  },
  data() {
    return {
      initValues: [],
      transfferdItems: [],
      transfferdItemslist: [],
      lessthanImage: "<",
      largeThanImage: ">",
      allMoveRightImage: ">>",
      allMoveLeftImage: "<<",
      valuearray: [
        {
          id: 1,
          name: "List Item1",
          value: "item1",
        },
        {
          id: 2,
          name: "List Item2",
          value: "item2",
        },
      ],
    };
  },
  created() {
    this.initValues = [
      {
        id: 1,
        name: "List Item1",
        value: "item1",
      },
      {
        id: 2,
        name: "List Item2",
        value: "item2",
      },
      {
        id: 3,
        name: "List Item3",
        value: "item3",
      },
      {
        id: 4,
        name: "List Item4",
        value: "item4",
      },
      {
        id: 5,
        name: "List Item5",
        value: "item5",
      },
      {
        id: 6,
        name: "List Item6",
        value: "item6",
      },
      {
        id: 7,
        name: "List Item7",

        value: "item7",
      },
      {
        id: 8,
        name: "List Item8",
        value: "item8",
      },
    ];

    this.transfferdItems = ["item4", "item5"];
  },
  methods: {
    updatedTransferList(value) {
      console.log("updatedTransferList+++", value);
      alert("updatedTransferList+++", value);

    },
  },
};
</script>

<style>

</style>
