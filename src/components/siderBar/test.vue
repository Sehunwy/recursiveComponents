<template>
  <div>
    <ul>
      <li v-for="(item,index) in menus" :key="index">
        <p
          style="background: pink"
          @click="open($event,numbers==null?index+'':numbers+''+index)"
        >{{item.name}}-- {{index}}--第{{currlayer}}层===number:----{{numbers}}</p>
        <div v-if="item.children">
          <childSider
            :number="numbers==null?index+'':numbers+''+index "
            :layer="currlayer"
            :menus="item.children"
            :showArr="showArrs"
          ></childSider>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: "childSider",
  data() {
    return {
      currlayer: this.layer,
      isShow: "hide",
      numbers: this.number,
      showArrs: this.showArr
    };
  },
  created() {
    this.currlayer++;
    this.showArrs.push(this.number);
    console.log(this.showArrs);
    // this.numbers++;
  },
  methods: {
    open: function(e, index) {
      //   console.log(e.currentTarget);
      //   console.log(index);
      const dom = e.target.nextElementSibling;
      console.log(dom);
      if (dom != null) {
        if (dom.className === "show") {
          dom.className = "hide";
        } else {
          dom.className = "show";
        }
      }
    }
  },
  props: {
    menus: {},
    layer: {},
    number: {
      default: null
    },
    showArr: {
      default: () => {
        return [];
      }
    }
  }
};
</script>

<style>
.hide {
  display: none;
}
.show {
  display: block;
}
</style>
