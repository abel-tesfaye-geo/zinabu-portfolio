---
title: "Certificates"
permalink: /certificates/
classes: wide
author_profile: false
---

<style>
.cert-section-title {
  font-size: 2em;
  font-weight: 700;
  border-bottom: 2px solid #ddd;
  padding-bottom: 0.3em;
  margin-top: 1em;
  margin-bottom: 0.4em;
}
.cert-hint {
  color: #777;
  margin-bottom: 1.5em;
}
.cert-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.4em;
  margin-bottom: 2em;
}
.cert-card {
  background: #fff;
  border-radius: 10px;
  padding: 0.6em;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  cursor: zoom-in;
  min-height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.15s, box-shadow 0.15s;
}
.cert-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 18px rgba(0,0,0,0.18);
}
.cert-card canvas {
  width: 100%;
  height: auto;
  border-radius: 6px;
  display: block;
}
#cert-lightbox {
  display: none;
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.9);
  z-index: 9999;
  align-items: center;
  justify-content: center;
}
#cert-lightbox-canvas {
  max-width: 86%;
  max-height: 92%;
  border-radius: 6px;
  background: #fff;
}
.cert-nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: #fff;
  font-size: 3.5em;
  line-height: 1;
  cursor: pointer;
  padding: 0 0.3em;
}
#cert-prev { left: 0.5%; }
#cert-next { right: 0.5%; }
@media (max-width: 1100px) {
  .cert-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 600px) {
  .cert-grid { grid-template-columns: 1fr; }
}
</style>

<div class="cert-section-title">Professional Certifications, Training and Recognitions</div>
<div class="cert-hint">Click any certificate to enlarge it. Use the arrow keys to move between them.</div>
<div class="cert-grid" id="cert-grid"></div>

<div id="cert-lightbox">
  <button class="cert-nav" id="cert-prev" aria-label="Previous">&#8249;</button>
  <canvas id="cert-lightbox-canvas"></canvas>
  <button class="cert-nav" id="cert-next" aria-label="Next">&#8250;</button>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

var TOTAL = 30;
var BASE = '{{ site.baseurl }}/assets/';

// Files that are NOT pdf. Format: number: 'ending'
var OTHER = { 25: 'jpeg', 26: 'jpeg' };

var urls = [];
for (var i = 1; i <= TOTAL; i++) {
  urls.push(BASE + i + '.' + (OTHER[i] || 'pdf'));
}

var grid = document.getElementById('cert-grid');
var lightbox = document.getElementById('cert-lightbox');
var lightboxCanvas = document.getElementById('cert-lightbox-canvas');
var current = 0;
var token = 0;

async function renderPdfPage(canvas, url, width) {
  var pdf = await pdfjsLib.getDocument(url).promise;
  var page = await pdf.getPage(1);
  var base = page.getViewport({ scale: 1 });
  var viewport = page.getViewport({ scale: width / base.width });
  canvas.width = viewport.width;
  canvas.height = viewport.height;
  await page.render({ canvasContext: canvas.getContext('2d'), viewport: viewport }).promise;
}

function renderImage(canvas, url, width) {
  return new Promise(function (resolve, reject) {
    var img = new Image();
    img.onload = function () {
      var scale = Math.min(1, width / img.naturalWidth);
      canvas.width = Math.round(img.naturalWidth * scale);
      canvas.height = Math.round(img.naturalHeight * scale);
      canvas.getContext('2d').drawImage(img, 0, 0, canvas.width, canvas.height);
      resolve();
    };
    img.onerror = reject;
    img.src = url;
  });
}

function renderItem(canvas, url, width) {
  if (/\.pdf$/i.test(url)) { return renderPdfPage(canvas, url, width); }
  return renderImage(canvas, url, width);
}

async function showCert(index) {
  current = (index + urls.length) % urls.length;
  var mine = ++token;
  lightbox.style.display = 'flex';
  document.body.style.overflow = 'hidden';
  try {
    var temp = document.createElement('canvas');
    await renderItem(temp, urls[current], 1600);
    if (mine !== token) { return; }
    lightboxCanvas.width = temp.width;
    lightboxCanvas.height = temp.height;
    lightboxCanvas.getContext('2d').drawImage(temp, 0, 0);
  } catch (e) {}
}

function closeCert() {
  token++;
  lightbox.style.display = 'none';
  document.body.style.overflow = '';
}

var observer = new IntersectionObserver(function (entries) {
  entries.forEach(function (entry) {
    if (!entry.isIntersecting) { return; }
    var card = entry.target;
    observer.unobserve(card);
    renderItem(card.querySelector('canvas'), card.getAttribute('data-file'), 600)
      .catch(function () { card.style.display = 'none'; });
  });
}, { rootMargin: '300px' });

urls.forEach(function (url, index) {
  var card = document.createElement('div');
  card.className = 'cert-card';
  card.setAttribute('data-file', url);
  card.appendChild(document.createElement('canvas'));
  card.addEventListener('click', function () { showCert(index); });
  grid.appendChild(card);
  observer.observe(card);
});

document.getElementById('cert-prev').addEventListener('click', function (e) { e.stopPropagation(); showCert(current - 1); });
document.getElementById('cert-next').addEventListener('click', function (e) { e.stopPropagation(); showCert(current + 1); });
lightbox.addEventListener('click', function (e) { if (e.target === lightbox) { closeCert(); } });
document.addEventListener('keydown', function (e) {
  if (lightbox.style.display !== 'flex') { return; }
  if (e.key === 'Escape') { closeCert(); }
  if (e.key === 'ArrowLeft') { showCert(current - 1); }
  if (e.key === 'ArrowRight') { showCert(current + 1); }
});
</script>
