---
layout: page
permalink: /cv/
title: CV
nav: true
nav_order: 2
description: Curriculum Vitae of Junghyeok Lee.
---

<style>
.post-header {
  display: none;
}

.cv-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.2rem;
}

.cv-title-block {
  display: flex; 
  flex-direction: column;
  gap: 0.15rem;
}

.cv-title-block .cv-main-title {
  margin: 0;
  font-size: 2.35rem;
  font-weight: 800;
  line-height: 1.15;
  color: var(--global-text-color);
}

.cv-title-block .cv-name {
  margin: 0;
  font-size: 1.15rem;
  font-weight: 400;
  color: var(--global-text-color-light);
}

.cv-download-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 6rem;
  height: 6rem;
  border: 1px solid var(--global-divider-color);
  border-radius: 999px;
  color: var(--global-text-color);
  text-decoration: none;
  font-size: 3rem;
  transition: all 0.15s ease-in-out;
}

.cv-download-icon:hover {
  color: var(--global-theme-color);
  border-color: var(--global-theme-color);
  text-decoration: none;
  transform: translateY(-1px);
}

.cv-pdf-container {
  width: 100%;
  height: 85vh;
  border: 1px solid var(--global-divider-color);
  border-radius: 12px;
  overflow: hidden;
  background: var(--global-bg-color);
}

.cv-pdf-pages {
  width: 100%;
  box-sizing: border-box;
  padding: 14px;
}

.cv-pdf-page {
  display: block;
  max-width: 100%;
  height: auto;
  margin: 0 auto 14px;
  background: #ffffff;
  box-shadow: 0 1px 8px rgba(0, 0, 0, 0.12);
}

.cv-pdf-status,
.cv-pdf-fallback {
  padding: 1rem;
  text-align: center;
}

.cv-pdf-fallback {
  margin: 0;
  padding-top: 0.35rem;
  font-size: 0.88rem;
}

.cv-pdf-container iframe {
  width: 100%;
  height: 100%;
  min-height: 60vh;
  border: 0;
}
</style>

<div class="cv-header">
  <div class="cv-title-block">
    <h1 class="cv-main-title">Curriculum Vitae</h1>
    <p class="cv-name">Junghyeok Lee</p>
  </div>

  <a
    class="cv-download-icon"
    href="{{ '/assets/pdf/CV_Junghyeok_Lee_2026_10.pdf' | relative_url }}"
    target="_blank"
    aria-label="Download CV PDF"
    title="Download CV PDF"
  >
    <i class="fas fa-file-pdf"></i>
  </a>
</div>

<div class="cv-pdf-container" aria-label="CV PDF preview">
  <div id="cv-pdf-status" class="cv-pdf-status" role="status">Loading CV preview…</div>
  <div id="cv-pdf-pages" class="cv-pdf-pages"></div>
</div>

<p class="cv-pdf-fallback">
  If the preview does not load, <a href="{{ '/assets/pdf/CV_Junghyeok_Lee_2026_10.pdf' | relative_url }}" target="_blank" rel="noopener">open the CV PDF directly</a>.
</p>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
  (async function () {
    const pdfUrl = "{{ '/assets/pdf/CV_Junghyeok_Lee_2026_10.pdf' | relative_url }}";
    const pages = document.getElementById("cv-pdf-pages");
    const status = document.getElementById("cv-pdf-status");

    try {
      if (!window.pdfjsLib) {
        throw new Error("PDF.js library unavailable");
      }

      pdfjsLib.GlobalWorkerOptions.workerSrc =
        "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";

      const pdf = await pdfjsLib.getDocument(pdfUrl).promise;

      for (let pageNumber = 1; pageNumber <= pdf.numPages; pageNumber++) {
        status.textContent = "Rendering CV: " + pageNumber + " / " + pdf.numPages;

        const page = await pdf.getPage(pageNumber);
        const originalViewport = page.getViewport({ scale: 1 });
        const availableWidth = Math.max(240, pages.clientWidth - 28);
        const viewport = page.getViewport({
          scale: availableWidth / originalViewport.width,
        });
        const pixelRatio = Math.min(window.devicePixelRatio || 1, 2);
        const canvas = document.createElement("canvas");
        const context = canvas.getContext("2d");

        canvas.className = "cv-pdf-page";
        canvas.setAttribute("role", "img");
        canvas.setAttribute("aria-label", "CV page " + pageNumber);
        canvas.width = Math.ceil(viewport.width * pixelRatio);
        canvas.height = Math.ceil(viewport.height * pixelRatio);
        canvas.style.width = viewport.width + "px";
        canvas.style.height = viewport.height + "px";
        pages.appendChild(canvas);

        await page.render({
          canvasContext: context,
          viewport: viewport,
          transform: pixelRatio !== 1 ? [pixelRatio, 0, 0, pixelRatio, 0, 0] : undefined,
        }).promise;
      }

      status.hidden = true;
    } catch (error) {
      console.error("Unable to render CV with PDF.js:", error);
      status.textContent = "The interactive preview is unavailable. You can still view the PDF below or open it using the link.";
      pages.innerHTML = "";
      const iframe = document.createElement("iframe");
      iframe.src = pdfUrl + "#toolbar=1";
      iframe.title = "Junghyeok Lee CV PDF";
      iframe.loading = "lazy";
      pages.appendChild(iframe);
    }
  })();
</script>
