---
title: "Publications"
permalink: /publications/
classes: wide
author_profile: false
journal:
  - num: 1
    authors: "Sisay, Z. G., Tulu, B., Gesse, B., & Martine, V. (2018)."
    title: "Positional accuracy validation of digital orthophoto mapping: Case Bahir Dar City, Ethiopia."
    venue: "Nordic Journal of Surveying and Real Estate Research."
    pdf: "Pub-1.pdf"
    doi: "https://doi.org/10.30672/njsr.65724"
  - num: 2
    authors: "Sisay, Z. G. (2021)."
    title: "Feature orientation and positional accuracy assessment of digital orthophoto and line map for urban land registration: The case of Bahir Dar town, Ethiopia."
    venue: "African Journal on Land Policy and Geospatial Sciences, 3(3)."
    pdf: "Pub-2.pdf"
    doi: "https://doi.org/10.48346/IMIST.PRSM/ajlp-gs.v3i3.18157"
conference:
  - num: 3
    authors: "Sisay, Z. G., Tulu, B., & Gesse, B. (2017)."
    title: "Feature orientation and positional accuracy assessment of digital orthophoto and line map for large scale mapping: Bahir Dar town, Ethiopia."
    venue: "ISPRS Archives, XLII-1/W1, 47. ISPRS Hannover Workshop, Germany."
    pdf: "Pub-3.pdf"
    doi: "https://doi.org/10.5194/isprs-archives-XLII-1-W1-47-2017"
  - num: 4
    authors: "Sisay, Z. G. (2017)."
    title: "Feature orientation and positional accuracy assessment of digital orthophoto and line map for large scale mapping."
    venue: "RCMRD International Conference, Nairobi, Kenya."
  - num: 5
    authors: "Sisay, Z. G., & Amezene, R. (2019)."
    title: "Optimum sample size determination scenarios for orthophoto positional accuracy test in varied topography for urban land registration: Bahir Dar, Debre Markos and Harar, Ethiopia."
    venue: "Conference on Land Policy in Africa, Abidjan, Côte d’Ivoire."
    link: "https://archive.uneca.org/sites/default/files/uploaded-documents/CLPA/2019/Papers/Data-spatial-information-systems/paper_final_for_clpa-2019-converted.pdf"
  - num: 6
    authors: "Sisay, Z. G., et al. (2023)."
    title: "Socio-technical evaluation of urban cadastral system implementation against international and national standards: Bahir Dar, Debre Markos and Harar, Ethiopia."
    venue: "North Africa Land Administration Governance conference, Rabat, Morocco."
---

<style>
.pub-hint { color: #777; margin-bottom: 1em; }
.pub-group {
  font-size: 1.7em; font-weight: 700; border-bottom: 2px solid #ddd;
  padding-bottom: 0.3em; margin: 1.6em 0 1em;
}
.pub-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.4em; }
.pub-card {
  display: flex; gap: 1em; background: #fff; border-radius: 10px;
  padding: 0.9em; box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
.pub-cover {
  position: relative; flex: 0 0 130px; width: 130px; align-self: flex-start;
  border-radius: 6px; overflow: hidden; background: #eef3f0;
  box-shadow: 0 1px 6px rgba(0,0,0,0.2); transition: transform 0.15s;
}
a.pub-cover:hover { transform: translateY(-3px); }
.pub-cover canvas { width: 100%; height: auto; display: block; }
.pub-cover.empty { height: 170px; display: flex; align-items: center; justify-content: center; }
.pub-badge {
  position: absolute; top: 6px; left: 6px; background: #2D6A4F; color: #fff;
  font-weight: 700; font-size: 0.85em; border-radius: 50%;
  width: 1.8em; height: 1.8em; display: flex; align-items: center; justify-content: center;
}
.pub-body { flex: 1; min-width: 0; }
.pub-authors { font-size: 0.88em; color: #666; line-height: 1.45; }
.pub-title { font-weight: 700; line-height: 1.4; margin: 0.35em 0; }
.pub-venue { font-style: italic; color: #2D6A4F; font-size: 0.92em; line-height: 1.45; }
.pub-links { margin-top: 0.8em; display: flex; gap: 0.5em; flex-wrap: wrap; }
.pub-btn {
  display: inline-block; padding: 0.4em 0.9em; border-radius: 6px; font-size: 0.88em;
  font-weight: 700; background: #2D6A4F; color: #fff !important; text-decoration: none;
}
.pub-btn.alt { background: #fff; color: #2D6A4F !important; border: 2px solid #2D6A4F; }
@media (max-width: 1000px) {
  .pub-grid { grid-template-columns: 1fr; }
}
</style>

<p class="pub-hint">Click a cover to open the full paper.</p>

<h2 class="pub-group">Journal articles</h2>
<div class="pub-grid">
{%- for pub in page.journal -%}
<div class="pub-card">
{%- if pub.pdf -%}
<a class="pub-cover" href="{{ site.baseurl }}/assets/{{ pub.pdf }}" target="_blank" rel="noopener"><canvas data-pdf="{{ site.baseurl }}/assets/{{ pub.pdf }}"></canvas><span class="pub-badge">{{ pub.num }}</span></a>
{%- else -%}
<div class="pub-cover empty"><span class="pub-badge">{{ pub.num }}</span></div>
{%- endif -%}
<div class="pub-body">
<div class="pub-authors">{{ pub.authors }}</div>
<div class="pub-title">{{ pub.title }}</div>
<div class="pub-venue">{{ pub.venue }}</div>
<div class="pub-links">
{%- if pub.pdf -%}<a class="pub-btn" href="{{ site.baseurl }}/assets/{{ pub.pdf }}" target="_blank" rel="noopener">Read full paper</a>{%- endif -%}
{%- if pub.link -%}<a class="pub-btn" href="{{ pub.link }}" target="_blank" rel="noopener">Read online</a>{%- endif -%}
{%- if pub.doi -%}<a class="pub-btn alt" href="{{ pub.doi }}" target="_blank" rel="noopener">DOI</a>{%- endif -%}
</div>
</div>
</div>
{%- endfor -%}
</div>

<h2 class="pub-group">Conference papers</h2>
<div class="pub-grid">
{%- for pub in page.conference -%}
<div class="pub-card">
{%- if pub.pdf -%}
<a class="pub-cover" href="{{ site.baseurl }}/assets/{{ pub.pdf }}" target="_blank" rel="noopener"><canvas data-pdf="{{ site.baseurl }}/assets/{{ pub.pdf }}"></canvas><span class="pub-badge">{{ pub.num }}</span></a>
{%- else -%}
<div class="pub-cover empty"><span class="pub-badge">{{ pub.num }}</span></div>
{%- endif -%}
<div class="pub-body">
<div class="pub-authors">{{ pub.authors }}</div>
<div class="pub-title">{{ pub.title }}</div>
<div class="pub-venue">{{ pub.venue }}</div>
<div class="pub-links">
{%- if pub.pdf -%}<a class="pub-btn" href="{{ site.baseurl }}/assets/{{ pub.pdf }}" target="_blank" rel="noopener">Read full paper</a>{%- endif -%}
{%- if pub.link -%}<a class="pub-btn" href="{{ pub.link }}" target="_blank" rel="noopener">Read online</a>{%- endif -%}
{%- if pub.doi -%}<a class="pub-btn alt" href="{{ pub.doi }}" target="_blank" rel="noopener">DOI</a>{%- endif -%}
</div>
</div>
</div>
{%- endfor -%}
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
document.querySelectorAll('.pub-cover canvas').forEach(function (canvas) {
  var url = canvas.getAttribute('data-pdf');
  pdfjsLib.getDocument(url).promise.then(function (pdf) {
    return pdf.getPage(1);
  }).then(function (page) {
    var base = page.getViewport({ scale: 1 });
    var viewport = page.getViewport({ scale: 400 / base.width });
    canvas.width = viewport.width;
    canvas.height = viewport.height;
    return page.render({ canvasContext: canvas.getContext('2d'), viewport: viewport }).promise;
  }).catch(function () {
    canvas.style.display = 'none';
    canvas.parentNode.classList.add('empty');
  });
});
</script>
