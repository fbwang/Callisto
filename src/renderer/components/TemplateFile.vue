<template>
    <main>
    <div class="left-side">
        <div align="center">
        Drag Your Template File Here
        </div>
        <div class="frame" id="templatefile" v-on:drop="fopen" v-on:dragover="fover">
            <div align="center">Template: </div>
            <span>{{templateFile}}</span>
        </div>
    </div>
    <div class="right-side">
        <data-file></data-file>
    </div>
    </main>
</template>

<script>
    import DataFile from "./TemplateFile/DataFile";
    export default {
        name: "TemplateFile",
        components: {DataFile},
        data () {
            return {
                templateFile: ''
            }
        },
        methods: {
            fopen:function (event) {
                event.preventDefault();
                event.stopPropagation();

                for (let f of event.dataTransfer.files) {
                    this.templateFile = f.path;
                    // this.$broadcast('execute',this.templateFile);
                    console.log('File(s) you dragged here: ', f.path);
                }
            },
            fover:function (event) {
                event.preventDefault();
                event.stopPropagation();
            }
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }
    html{
        height: 100%;
    }

    body { font-family: 'Source Sans Pro', sans-serif; height: 100%}

    #wrapper {
        background:
                radial-gradient(
                        ellipse at top left,
                        rgba(255, 255, 255, 1) 40%,
                        rgba(229, 229, 229, .9) 100%
                );
        height: 100vh;
        padding: 60px 80px;
        width: 100vw;
    }

    #logo {
        height: auto;
        margin-bottom: 20px;
        width: 420px;
    }
    #app{
        height: 100%;
    }

    main {
        display: flex;
        justify-content: space-between;
        height: 100%;
    }

    main > div { flex-basis: 50%; height: 100% }

    .left-side {
        display: flex;
        flex-direction: column;
        border-right: solid 1px #42b983;
    }

    .welcome {
        color: #555;
        font-size: 23px;
        margin-bottom: 10px;
    }

    .title {
        color: #2c3e50;
        font-size: 20px;
        font-weight: bold;
        margin-bottom: 6px;
    }

    .title.alt {
        font-size: 18px;
        margin-bottom: 10px;
    }

    .doc p {
        color: black;
        margin-bottom: 10px;
    }

    .doc button {
        font-size: .8em;
        cursor: pointer;
        outline: none;
        padding: 0.75em 2em;
        border-radius: 2em;
        display: inline-block;
        color: #fff;
        background-color: #4fc08d;
        transition: all 0.15s ease;
        box-sizing: border-box;
        border: 1px solid #4fc08d;
    }

    .doc button.alt {
        color: #42b983;
        background-color: transparent;
    }
    .frame{
        margin: 5px;
        height: 200px;
        border: dashed 1px #42b983;
    }
    span{
        color: aquamarine;
    }
</style>
