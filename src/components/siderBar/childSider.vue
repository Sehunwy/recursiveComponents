<template>
  <div class="menus-list">
    <ul>
      <li v-for="(item,index) in menus" :key="index">
        <div
          class="menus-name"
          :class="showClass(currlayer)"
          @click.stop="isOpen(item.name,currlayer,item.children!=undefined)"
        >{{item.name}}==层数{{currlayer}}</div>
        <div v-if="item.children">
          <childSider
            v-show="isShow[item.name]"
            :menus="item.children"
            :layer="currlayer"
            :menusLen="menusLen"
            :firstMenu="firstMenu"
            :unfoldArr="unfold"
            :isShowObj="isShow"
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
      isShow: this.isShowObj,
      firstShow: "",
      levelClass: ["level1", "level2", "level3", "level4"],
      unfold: this.unfoldArr
    };
  },
  methods: {
    isOpen: function(name, layer, hasChildren) {
      if (hasChildren) {
        this.$set(this.isShow, name, !this.isShow[name]);
        if (this.unfold[layer] == undefined) {
          this.unfold[layer] = {};
        }
        var obj = this.unfold[layer]; // 得到第layer层的对象
        if (this.isShow[name]) {
          obj[name] = name;
          this.unfold[layer] = obj;
        } else {
          delete this.unfold[layer][name];
        }
        var copyUnfold = JSON.parse(JSON.stringify(this.unfold));
        var keys;
        for (var i = layer; i < copyUnfold.length; i++) {
          keys = Object.keys(copyUnfold[i]);
          for (var j = 0; j < keys.length; j++) {
            if (name != keys[j]) {
              this.$set(this.isShow, keys[j], false);
              delete this.unfold[i][keys[j]];
            }
          }
        }
      }
    },

    // isOpen: function(name, layer, hasChildren) {
    //   this.$set(this.isShow, name, !this.isShow[name]);
    //   if (layer == 0) {
    //     var copyUnfold = JSON.parse(JSON.stringify(this.unfold));
    //     for (var i = 0; i < copyUnfold.length; i++) {
    //       if (copyUnfold[i] != name) {
    //         this.$set(this.isShow, copyUnfold[i], false);
    //         var indexOf = this.unfold.indexOf(copyUnfold[i]);
    //         console.log(indexOf, i, copyUnfold[i]);
    //         this.unfold.splice(indexOf, 1);
    //       }
    //     }
    //   }
    //   if (this.isShow[name] && this.unfold.indexOf(name) == -1 && hasChildren) {
    //     this.unfold.push(name);
    //   } else if (!this.isShow[name]) {
    //     var indexOf = this.unfold.indexOf(name);
    //     this.unfold.splice(indexOf, 1);
    //   }
    //   console.log(this.unfold);
    // },
    showClass: function(layer) {
      return this.levelClass[layer];
    }
  },
  created() {
    this.currlayer++;
    if (this.menusLen == 1) {
      this.$set(this.isShow, this.firstMenu, true);
    }
  },
  props: {
    menus: {},
    layer: {},
    menusLen: {},
    firstMenu: {},
    unfoldArr: {
      default: () => {
        return [];
      }
    },
    isShowObj: {
      default: () => {
        return {};
      }
    }
  }
};
</script>

<style>
.menus-list {
  width: 180px;
  height: 100%;
  background: #38455a;
}

.menus-name {
  height: 44px;
  line-height: 44px;
  color: #ffffff;
  padding-left: 20px;
}

.level1 {
  background: #38455a;
}

.level2 {
  background: #2a374d;
}

.level3 {
  background: red;
}

.level4 {
  background: pink;
}
</style>
