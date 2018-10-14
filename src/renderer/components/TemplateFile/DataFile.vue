<template>
    <div>
    <div align="center">
        Drag Your Data File Folder Here
    </div>
    <div class="frame" id="test">
        <form action="/upload" class="dropzone"></form>
    </div>
    </div>
</template>

<script>
    import Dropzone from 'dropzone';
    // var myDropzone = new Dropzone("div#files", { url: "/file/post"});

    export default {
        name: "DataFile",
        data(){
            return{
                folder: ''
            }
        },
        methods: {
            fopen: function (e) {
                e.preventDefault();
                e.stopPropagation();
                for (let f of event.dataTransfer.files) {
                    this.folder = f.path;
                    console.log('File(s) you dragged here: ', f.path);
                }
            },
            fover:function (event) {
                event.preventDefault();
                event.stopPropagation();
            }
        }
    };


</script>

<style>
    @import '~dropzone/dist/dropzone.css';

</style>
