<template>
    <div id="bottom">
        <div v-if="warning === ''" class="alert alert-success" role="alert">Warning:{{warning}}</div>
        <div v-else class="alert alert-danger" role="alert">Warning:{{warning}}</div>
        <a v-on:click="execute" class="button button-block button-rounded button-action button-large">Submit</a>

        <div class="progress">
            <keep-alive>
            <div class="progress-bar progress-bar-striped bg-success" role="progressbar"  v-bind:aria-valuenow="{count}" aria-valuemin="0" aria-valuemax="100" v-bind:style="{width: percent}"></div>
            </keep-alive>
        </div>
        <div>{{count}}</div>

    </div>
</template>

<script>
    import XLSX from 'xlsx';
    import TWEEN from '@tweenjs/tween.js'
    // import Sleep from 'sleep';
    import fs from 'fs';
    import parse from 'csv-parse';
    export default {
        name: "Bottom",
        data () {
            return {
                warning: '',
                count: 0,
                total: 0,
                percent: '0%',
                tweenedCount: 0,
            }
        },
        created: function(){

        },
        watch: {
          percent: function () {
              function animate() {

                  if (TWEEN.update()) {
                      requestAnimationFrame(animate);
                  }
              }

              new TWEEN.Tween(this.tweenedCount).to(this.count,2).start();
              animate();
          }
        },
        computed: {
          percentage: function () {
              var str = Number(this.count*100/this.total).toFixed(1);
              str += "%";
              return str;
          }
        },
        methods: {
            execute: function (event) {
                var templateFile = this.$parent.$children[0].templateFile;
                var files =        this.$parent.$children[0].$children[0].files;
                var folder = this.$parent.$children[0].$children[0].folder;
                // console.log(files);
                if (templateFile === ''){
                    this.warning = 'No Template File Provided';
                }else {
                    this.warning ='';
                    // console.log(templateFile);
                    if (files === undefined){
                        this.warning = "No Data Files Provided";
                    } else {
                        this.warning = '';
                        console.log(this.count);
                        this.count = 20;
                        this.percent = '0%';
                        var workbook = XLSX.readFile(templateFile);
                        const sheetNames = workbook.SheetNames;
                        console.log(sheetNames);
                        this.percent = '10%';
                        var i = 1;
                        for (i = 1; i<files.length-1; i++){
                            var parser = parse({delimiter: ';'},function (err, data){
                                console.log(data);
                                console.log(i);
                            });

                            fs.createReadStream(folder+'/'+files[i]).pipe(parser);
                        }
                    }
                }
                //
            }
        }
    }
</script>

<style scoped>
    @import "~Buttons/css/buttons.css";
    @import "~bootstrap/dist/css/bootstrap.css";
    #bottom{
        border-top: 1px solid #4fc08d;
        padding: 5px;
    }

</style>
