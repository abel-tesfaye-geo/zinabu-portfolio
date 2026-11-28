---
title: "Vlog"
permalink: /vlog/
classes: wide
author_profile: false
vlog:
  - title: "Assisting students during the surveying course"
    images:
      - "Vlog_1.jpeg"
      - "Vlog_2.jpeg"
---

<style>
.vlog-group {
  font-size: 1.7em; font-weight: 700; border-bottom: 2px solid #ddd;
  padding-bottom: 0.3em; margin: 1.2em 0 1em;
}
.vlog-hint { color: #777; margin-bottom: 1em; }
.vlog-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.4em; align-items: start; margin-bottom: 2em;
}
.vlog-card {
  background: #fff; border-radius: 10px; padding: 0.6em;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1); cursor: zoom-in;
  transition: transform 0.15s, box-shadow 0.15s;
}
.vlog-card:hover { transform: translateY(-3px); box-shadow: 0 6px 18px rgba(0,0,0,0.18); }
.vlog-card img { width: 100%; height: auto; border-radius: 6px; display: block; }
#vlog-lightbox {
  display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.9); z-index: 9999;
  align-items: center; justify-content: center;
}
#vlog-lightbox-img { max-width: 86%; max-height: 92%; border-radius: 6px; background: #fff; }
.vlog-nav {
  position: absolute; top: 50%; transform: translateY(-50%);
  background: none; border: none; color: #fff; font-size: 3.5em;
  line-height: 1; cursor: pointer; padding: 0 0.3em;
}
#vlog-prev { left: 0.5%; }
#vlog-next { right: 0.5%; }
</style>

<p class="vlog-hint">Click a photo to enlarge it.</p>

{%- for group in page.vlog -%}
<h2 class="vlog-group">{{ group.title }}</h2>
<div class="vlog-grid">
{%- for img in group.images -%}
<div class="vlog-card"><img class="vlog-img" src="{{ site.baseurl }}/assets/{{ img }}" alt="{{ group.title }}" loading="lazy"></div>
{%- endfor -%}
</div>
{%- endfor -%}

<div id="vlog-lightbox">
  <button class="vlog-nav" id="vlog-prev" aria-label="Previous">&#8249;</button>
  <img id="vlog-lightbox-img" src="" alt="">
  <button class="vlog-nav" id="vlog-next" aria-label="Next">&#8250;</button>
</div>

<script>
var photos = Array.prototype.slice.call(document.querySelectorAll('.vlog-img'));
var lightbox = document.getElementById('vlog-lightbox');
var lightboxImg = document.getElementById('vlog-lightbox-img');
var current = 0;

function showPhoto(index) {
  current = (index + photos.length) % photos.length;
  lightboxImg.src = photos[current].src;
  lightboxImg.alt = photos[current].alt;
  lightbox.style.display = 'flex';
  document.body.style.overflow = 'hidden';
}

function closePhoto() {
  lightbox.style.display = 'none';
  document.body.style.overflow = '';
}

photos.forEach(function (img, index) {
  img.parentNode.addEventListener('click', function () { showPhoto(index); });
});

document.getElementById('vlog-prev').addEventListener('click', function (e) { e.stopPropagation(); showPhoto(current - 1); });
document.getElementById('vlog-next').addEventListener('click', function (e) { e.stopPropagation(); showPhoto(current + 1); });
lightbox.addEventListener('click', function (e) { if (e.target === lightbox) { closePhoto(); } });
document.addEventListener('keydown', function (e) {
  if (lightbox.style.display !== 'flex') { return; }
  if (e.key === 'Escape') { closePhoto(); }
  if (e.key === 'ArrowLeft') { showPhoto(current - 1); }
  if (e.key === 'ArrowRight') { showPhoto(current + 1); }
});
</script>
