<template>
  <div class="hello">
    <div >test camera</div>
    <div id="interactive" class="viewport">
  <!-- QuaggaJS will populate this element -->
    </div>
    <button @click="testing">aqui</button>
  </div>
</template>

<script>
import  Quagga from "quagga"

export default {
  name: "HelloWorld",
  props: {},
  methods: {
    testing: async function () {
      Quagga.init({
    inputStream: {
      constraints: {
        facingMode: 'environment' // restrict camera type
      },
      area: { // defines rectangle of the detection
        top: '40%',    // top offset
        right: '0%',  // right offset
        left: '0%',   // left offset
        bottom: '40%'  // bottom offset
      },
    },
    decoder: {
      readers: ['ean_reader'] // restrict code types
    },
  },
  (err) => {
    if (err) {
      this.errorMessage = `QuaggaJS could not be initialized, err: ${err}`;
    } else {
      Quagga.start();
      Quagga.onDetected((res) => {
        window.alert(`code: ${res.codeResult.code}`);
      })
    }
  });
      
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.viewport::ng-deep video {
  width: 100%;
  height: 240px;
  object-fit: cover;
}
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
</style>
