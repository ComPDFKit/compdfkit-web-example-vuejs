<template>
  <div id="webviewer" ref="viewer"></div>
</template>

<script>
import { ref, onMounted } from "vue";
import ComPDFKitViewer from "@compdfkit_pdf_sdk/webviewer";

export default {
  name: "WebViewer",
  setup(props) {
    const viewer = ref(null);
    let docViewer = null
    onMounted(() => {
      ComPDFKitViewer.init({
        pdfUrl: './example/developer_guide_web.pdf',
        license: '<Input your license here>'
      }, viewer.value).then((core) => {
        docViewer = core.docViewer
        docViewer.addEvent('documentloaded', async () => {
          console.log('document loaded')
        })
      })
    });
    return {
      viewer,
      docViewer
    };
  },
};
</script>

<style>
#webviewer {
  height: 100vh;
  overflow: hidden;
}

button {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
}
</style>
