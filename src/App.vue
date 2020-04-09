<template>
  <div id="q-app"/>
</template>

<script>

import html2canvas from 'html2canvas';

async function getBase64FromImageURL(url, pixels = 100) {
  const img = document.createElement('img');
  img.id = 'render-logo-base';
  img.style.height = `${pixels}px`;
  img.style.width = `${pixels}px`;
  img.crossOrigin = 'anonymous';
  img.src = url;
  document.body.appendChild(img);

  const canvas = await html2canvas(document.getElementById(img.id), { useCORS: true, scale: 2 });
  const base64 = canvas.toDataURL('image/png');
  document.body.removeChild(img);

  return base64;
}

async function addImage(url) {
  const base64a = await getBase64FromImageURL(url, 100);

  const imgBase64 = document.createElement('img');
  imgBase64.id = 'render-logo';
  imgBase64.crossOrigin = 'anonymous';
  imgBase64.src = base64a;

  document.body.appendChild(imgBase64);
}

export default {
  name: 'App',
  async mounted() {
    await addImage('https://miro.medium.com/max/1400/1*rGTE8tsjuN42_HnvYvFN5g.jpeg');
    await addImage('./statics/app-logo-128x128.png');
  },
};
</script>
