<template lang="pug">
  #snippet
    #header
      span {{title}}
    v-treeview#tree(
      v-model="tree",
      :open="open",
      :items="directories",
      :open-all="all"
      item-key="name",
      hoverable,
      open-on-click
    )
      template(v-slot:prepend="{ item, open }")
        v-icon.pa-2(v-if="!item.file", size="20", v-bind:class="{'purple--text':(item.color==='purple'), 'blue--text':(item.color==='blue')}")
          | {{ open ? files.folderOpen : files.folder }}
        v-icon.pa-2.svg(v-else, size="20" v-bind:class="{'purple--text':(item.color==='purple'), 'blue--text':(item.color==='blue')}")
          | {{ files[item.file] }}

</template>

<script>
import items from "./items";

export default {
  props: {
    path: String,
    title: String,
    all: String,
    pin: Array
  },
  data: () => ({
    items: items,
    open: ["public", "aep"],
    files: {
      html: "mdi-language-html5",
      js: "mdi-nodejs",
      json: "mdi-json",
      md: "mdi-markdown",
      pdf: "mdi-file-pdf",
      png: "mdi-file-image",
      txt: "mdi-file-document-outline",
      xls: "mdi-file-excel",
      folder: "fas fa-folder",
      folderOpen: "fas fa-folder-open",
      comp: "far fa-file-alt",
      asset: "fas fa-box",
      assetVersion: "fas fa-archive",
      shot: "fas fa-camera-retro",
      seq: "fas fa-film",
      task: "far fa-clipboard",
      check: "fas fa-check"
    }
  }),
  computed: {
    directories() {
      let a = items;
      let s = "items";
      // console.log(this.path.split("|"));
      this.path.split("|").forEach(e => {
        // console.log('e', e)
        if (isNaN(+e)) {
          a = a[`${e}`];
          s += `.${e}`;
          // console.log("str", e, s, a);
        } else {
          a = a[e];
          s += `[${e}]`;
          // console.log("num", e, s, a);
        }
        // console.log((a = +e ? a.e : a[e]))
        // return (a = +e ? a.e : a[e])
      });
      // console.log("Final", s);
      return !!a ? a : items;
      // return items[0].children[1].children

      // return !a ? items : a;
      // this.path.split("|").forEach(e => {
      //   if (isNaN(+e)) {
      //     a = a.e
      //     console.log('str', e, a)
      //   } else {
      //     a = a[e]
      //     console.log('num', e, a)
      //   }
      //   return a
      //   // if (+e === isNaN) {
      //   //   console.log('number')
      //   // }
      //   // return (a = +e ? a.e : a[e]);
      // });
      // return a
      // // return !a ? items : a;
    }
  }
};
//   created() {
//     let a = items;
//     const s = this.path.split("|").forEach(e => {
//       a = +e ? a.e : a[e];
//       console.log(e, a);
//     });
//     // const total = s.reduce((accumulator, currentValue) => {
//     //   console.log(isNaN(currentValue), currentValue);
//     //   console.log(+`${currentValue}`)
//     //   return `${accumulator}|${currentValue}`;
//     // });

//     console.log("test", a);
//     // console.log('test', GetPropertyValue(items, "$0.children"))
//     // console.log(s, "total", total, items);
//   }
// };
// this.property = 'Example property update.'

// console.log('propertyComputed will update, as this.property is now reactive.')
</script>

<style>
#snippet {
  margin-top: 20px;
  border-radius: 10px;
  box-shadow: 0px 4px 8px 2px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

#snippet #header {
  display: flex;
  justify-content: stretch;
  align-items: center;
  padding: 0px 36px;
  background: dodgerblue;
  height: 80px;
}

#snippet #header span {
  width: 100%;
  color: white;
  padding: 8px 32px;
  border-radius: 40px;
  background: rgb(69, 162, 255);
}

#snippet #tree {
  height: 292px;
  padding: 20px;
  overflow-x: hidden;
  overflow-y: scroll;
}

.small > * {
  color: red !important;
  fill: red !important;
}
</style>

