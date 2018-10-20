<template>
    <div>
    <button>Bottom</button>
    </div>
</template>

<script>
    import Excel from 'exceljs';
    import XLSX from 'xlsx';
    import fs from 'fs';

    export default {
        name: "DataFile",
        data(){
            return{
                folder: '',
                file: {}
            }
        },
        methods: {
            diropen:function (event) {
                event.preventDefault();
                event.stopPropagation();

                for (let f of event.dataTransfer.files) {
                    this.folder = f.path;
                    console.log('Folder you dragged here: ', f.path);
                    this.files = fs.readdirSync(this.folder);
                    // console.log(this.files);
                }
            },
            dirover:function (event) {
                event.preventDefault();
                event.stopPropagation();
            },

            execute:function(items){
                if (this.$parent.templateFile === ''){
                    
                }
                console.log(this.$parent.templateFile)
                var workbook = XLSX.readFile(this.$parent.templateFile);
                const sheetNames = workbook.SheetNames;
                console.log(sheetNames);
            }
        }
    };


</script>

<style>
    /* @import '~dropzone/dist/dropzone.css'; */

</style>
