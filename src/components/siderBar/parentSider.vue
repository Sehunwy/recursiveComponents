<template>
  <div style="height: 100%;width: 100%;">
    <childSider :menus="menus" :layer="-1" :menusLen="menusLen" :firstMenu="firstMenu"></childSider>
  </div>
</template>

<script>
/* eslint-disable */
import childSider from "@/components/siderBar/childSider";
export default {
  name: "parentSider",
  data() {
    return {
      menus: [
        {
          name: "菜单1",
          children: [
            {
              name: "菜单1-1",
              children: [
                {
                  name: "菜单1-1-1"
                },
                {
                  name: "菜单1-1-2"
                }
              ]
            },
            {
              name: "菜单1-2",
              children: [
                {
                  name: "菜单1-2-1"
                },
                {
                  name: "菜单1-2-2"
                }
              ]
            }
          ]
        },
        {
          name: "菜单2",
          children: [
            {
              name: "菜单2-1",
              children: [
                {
                  name: "菜单2-1-1"
                },
                {
                  name: "菜单2-1-2"
                }
              ]
            },
            {
              name: "菜单2-2",
              children: [
                {
                  name: "菜单2-2-1"
                },
                {
                  name: "菜单2-2-2"
                }
              ]
            }
          ]
        },
        {
          name: "菜单3",
          children: [
            {
              name: "菜单3-1",
              children: [
                {
                  name: "菜单3-1-1"
                },
                {
                  name: "菜单3-1-2"
                }
              ]
            },
            {
              name: "菜单3-2",
              children: [
                {
                  name: "菜单3-2-1"
                },
                {
                  name: "菜单3-2-2",
                  children: [
                    {
                      name: "菜单3-2-2-1"
                    },
                    {
                      name: "菜单3-2-2-2"
                    }
                  ]
                }
              ]
            }
          ]
        }
      ],
      menusLen: 0,
      firstMenu: ''
    };
  },
  created() {
      this.menusLen = this.menus.length;
      this.firstMenu = this.menus[0].name;
      console.log(this.menus.length,this.firstMenu)
  },
  components: {
    childSider
  }
};
</script>

<style>
</style>
