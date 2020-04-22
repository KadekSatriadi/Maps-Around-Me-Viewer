<template >
  <div class="layout-component">
      <img ref="layout-img" :src="`./figures/${view}/${pid}_${task}.png`" v-bind:class="'layoutimg'" @mousedown="enlarge" @mouseup="normalsize" />
      <span>P{{ pid }}<span v-if="tasklabel == 'yes'" > - {{task}}</span></span>
  </div>
</template>

<script>
export default {
  name: 'LayoutComponent',
  props: {
    pid: String,
    task: String,
    view: String,
    tasklabel: String
  },
  methods: {
    enlarge: function(){     
      var lens = document.getElementById("modal");
      lens.style.display = "block";
      var lensimgt = document.getElementById("lens-img-t");
      var lensimgf = document.getElementById("lens-img-f");
      var lensimgr = document.getElementById("lens-img-r");
      var lensimgl = document.getElementById("lens-img-l");
      var lensimgd = document.getElementById("lens-img-d");

      var id = this.$refs["layout-img"].currentSrc;
      var srct = id;
      var split = srct.split("/")
      var task = split[split.length - 2];
      var srcf = srct.replace(task, "Front");
      var srcr = srct.replace(task, "Right");
      var srcl = srct.replace(task, "Left");
      var srcd = srct.replace(task, "TwoHalf");
      srct = srct.replace(task, "TopDown");

      lensimgt.setAttribute("src",srct);
      lensimgf.setAttribute("src",srcf);
      lensimgr.setAttribute("src",srcr);
      lensimgl.setAttribute("src",srcl);
      lensimgd.setAttribute("src",srcd);

      document.getElementById("modal-view-t").innerHTML = "Top-down";
      document.getElementById("modal-view-f").innerHTML = "Front";
      document.getElementById("modal-view-r").innerHTML = "Right";
      document.getElementById("modal-view-l").innerHTML = "Left";
      document.getElementById("modal-view-p").innerHTML = "Perspective";
      
      document.getElementById("modal-pid").innerHTML = "Participant " + id.split("/")[5].split("_")[0] + ", " + id.split("/")[5].split("_")[1].split(".")[0] + " task.";
    },
    normalsize: function(){
      var lens = document.getElementById("modal");
      lens.style.display = "none";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.layout-component{
  cursor: pointer;
}
.layoutimg {
  width: 100%;
}
</style>
