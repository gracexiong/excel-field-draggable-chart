<template>
  <div>
    <input type="file" id="aaa" hidden="true" @change="inputChanged">
    <label for="aaa">
      <slot></slot>
    </label>
  </div>
</template>
<script>
  import csv from "csv";
  export  default{
    name: "vue-csv-table",
    props: [],
    data(){
      return {
        rawFile: null
      }
    },
    methods: {
      inputChanged(e){
        if (this.rawFile !== null) {
          return
        }
        this.rawFile = e.target.files[0];
        this.fileConvertToWorkbook(this.rawFile)
      },

      fileConvertToWorkbook (file) {
        let reader = new FileReader()
//        let fixdata = (data) => {
//          let o = "", l = 0, w = 10240
//          for( ; l<data.byteLength/w ; ++l) {
//            o += String.fromCharCode.apply(null,new Uint8Array(data.slice(l*w,l*w+w)))
//          }
//          o += String.fromCharCode.apply(null, new Uint8Array(data.slice(l*w)))
//          return o
//        }
        return new Promise((resolve, reject) => {
          try {
            reader.onload = (renderEvent) => {
              let data = renderEvent.target.result;
//               csv.parse(data,function (aaa) {
//                 console.log(aaa)
//               });;
            }
            reader.onerror = (error) => {
              reject(error)
            };
            reader.readAsArrayBuffer(file)
//            if (this.rABS) {
//              reader.readAsBinaryString(file)
//            } else {
//              reader.readAsArrayBuffer(file)
//            }
          } catch (error) {
            reject(error)
          }
        })
      },
      selectFile(){
        this.$emit("on-select-file", 32)
      }
    },

  }
</script>
