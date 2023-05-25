<script setup>
import { QuillEditor } from '@vueup/vue-quill';
import BlotFormatter from 'quill-blot-formatter'
import ImageUploader from 'quill-image-uploader';
import '@vueup/vue-quill/dist/vue-quill.snow.css';
import 'quill-image-uploader/dist/quill.imageUploader.min.css';

const toolbar = [
    [{ header: [1, 2, false] }],
    ['bold', 'italic', 'underline'],
    ['image', 'code-block']
];

const modules = [
    {
        name: 'blotFormatter',
        module: BlotFormatter,
        options: {/* options */ }
    },
    {
        name: 'imageUploader',
        module: ImageUploader,
        options: {
            upload: file => {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        resolve(
                            "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/480px-JavaScript-logo.png"
                        );
                    }, 3500);
                });
            }
        }
    }
];

const editorContent = ref("<p>Hello World!</p>");
const contentHTML = ref("");

function showContent() {
    contentHTML.value = editorContent.value;
}

</script>

<template>
    <h1>This is VueQuill</h1>
    <QuillEditor theme="snow" :toolbar="toolbar" :modules="modules" v-model:content="editorContent" content-type="html" />
    <br>
    <button @click="showContent">Show Content</button>
    <br>
    <div id="content_container" class="ql-container ql-snow">
        <div id="content" class="ql-editor" v-html="contentHTML"></div>
    </div>
</template>

<style>
#content_container {
    border: none;
}
</style>