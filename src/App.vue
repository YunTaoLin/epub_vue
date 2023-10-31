<template>
  <div id="app">
    <div class="bookWrap" v-if="rendition">
      <div id="book"></div>
      <div class="option">
        <button id="prev" @click="rendition.prev()">Prev</button>
        <button id="next" @click="rendition.next()">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
import Epub from "epubjs";

let book = Epub();
book.open("https://yuntaolin.github.io/epub_example/");

export default {
  name: "App",
  components: {},
  data() {
    return {
      rendition: null,
    };
  },
  mounted() {
    this.rendition = book.renderTo("book", {
      width: "60vw",
      height: "60vh", // 分页模式下 最好固定宽高
      snap: true, // 预加载
      flow: "paginated",
      manager: "continuous",
      allowScriptedContent: true,
    });
    this.rendition.display();
  },
  methods: {
    // handleChangeFile(e) {
    //   let file = e.target.files[0];
    //   if (window.FileReader) {
    //     let reader = new FileReader();
    //     reader.onload = (r) => {
    //       try {
    //         console.log("test", r.target.result);
    //         book.open(r.target.result, "epub");
    //       } catch (err) {
    //         console.log(err);
    //       }
    //     };
    //     reader.readAsArrayBuffer(file);
    //   }
    // },
  },
};
</script>

<style>
body,
html {
  padding: 0;
  margin: 0;
  height: 100%;
  width: 100%;
}
#app {
  background-color: #f5f5f5;
  height: 100%;
  width: 100%;
}
.bookWrap {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 40px;
}

.bookWrap #book {
  border: 2px solid #aaa;
  background-color: #fff;
}
.option {
  padding: 12px;
  display: flex;
  justify-content: center;
  margin-top: 2px;
}

.option button {
  margin: 0 12px;
  padding: 8px 24px;
  font-size: 18px;
  border-radius: 12px;
  background-color: rgb(28, 139, 224);
  color: #fff;
}
</style>
