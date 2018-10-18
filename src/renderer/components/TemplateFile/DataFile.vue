<template>
    <div>
    <div align="center">
        Drag Your Data File Folder Here
    </div>
    <div class="frame" id="folder" v-on:drop="diropen" v-on:dragover="dirover">
            <div align="center">Datas: </div>
            <span>{{folder}}</span>
        </div>
    <div align="center">
        <button v-on:click="execute">Submit</button>
    </div>
    </div>
</template>

<script>
    // import Dropzone from 'dropzone';
    // var myDropzone = new Dropzone("div#files", { url: "/file/post"});
    import Excel from 'exceljs'

    export default {
        name: "DataFile",
        data(){
            return{
                folder: ''
            }
        },
        methods: {
            diropen:function (event) {
                event.preventDefault();
                event.stopPropagation();

                for (let f of event.dataTransfer.files) {
                    this.folder = f.path;
                    console.log('Folder you dragged here: ', f.path);
                }
            },
            dirover:function (event) {
                event.preventDefault();
                event.stopPropagation();
            },

            execute:function(event){
                // console.log(Excel)
                var workbook = new Excel.Workbook();
                // console.log(workbook)
                workbook.xlsx.readFile('Frametime_Analysis_Template_10-10-2018.xlsx').then(function(){
                    var worksheet = workbook.getWorksheet('Data');
                    console.log(worksheet);
                    var items = worksheet.getColumn('O');
                    console.log (items);

                })
            }
        }
    };


</script>

<style>
    /* @import '~dropzone/dist/dropzone.css'; */

</style>
