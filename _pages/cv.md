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

.cv-pdf-container iframe {
  width: 100%;
  height: 100%;
  border: none;
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

<div class="cv-pdf-container">
  <iframe
    src="https://docs.google.com/gview?embedded=true&url=https://jhy20k.github.io/assets/pdf/CV_Junghyeok_Lee_2026_10.pdf"
    title="Junghyeok Lee CV">
  </iframe>
</div>
