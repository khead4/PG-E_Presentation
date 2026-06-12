const slides = Array.from(document.querySelectorAll(".slide"));
const slideNav = document.getElementById("slideNav");
const prevSlide = document.getElementById("prevSlide");
const nextSlide = document.getElementById("nextSlide");
const slideCount = document.getElementById("slideCount");
const progressBar = document.getElementById("progressBar");
const modal = document.getElementById("modal");
const modalTitle = document.getElementById("modalTitle");
const modalCopy = document.getElementById("modalCopy");
const modalLaunch = document.getElementById("modalLaunch");
const previewPane = document.getElementById("previewPane");
const livePane = document.getElementById("livePane");
const tabs = Array.from(document.querySelectorAll(".tab"));
const wireframeCarousels = Array.from(document.querySelectorAll("[data-wireframe-carousel]"));

let activeIndex = 0;
let lastModalTrigger = null;

function pad(value) {
  return String(value).padStart(2, "0");
}

function slideViewScale(index) {
  const slideNumber = index + 1;
  if (slideNumber === 1) return "50";
  if (slideNumber === 12) return "25";
  return "33";
}

slides.forEach((slide, index) => {
  slide.dataset.viewScale = slideViewScale(index);
});

function buildNav() {
  slideNav.innerHTML = slides.map((slide, index) => `
    <button class="nav-item ${index === activeIndex ? "active" : ""}" type="button" data-slide="${index}" ${index === activeIndex ? 'aria-current="page"' : ""}>
      <span>${pad(index + 1)}</span>
      <strong>${slide.dataset.title || `Slide ${index + 1}`}</strong>
    </button>
  `).join("");
}

function updateSlide(index) {
  activeIndex = Math.max(0, Math.min(slides.length - 1, index));
  const viewScale = slideViewScale(activeIndex);
  document.documentElement.dataset.deckViewScale = viewScale;
  document.body.dataset.deckViewScale = viewScale;
  slides.forEach((slide, slideIndex) => {
    slide.classList.toggle("active", slideIndex === activeIndex);
  });
  Array.from(document.querySelectorAll(".nav-item")).forEach((item, itemIndex) => {
    item.classList.toggle("active", itemIndex === activeIndex);
    if (itemIndex === activeIndex) {
      item.setAttribute("aria-current", "page");
    } else {
      item.removeAttribute("aria-current");
    }
  });
  slideCount.textContent = `${pad(activeIndex + 1)} / ${pad(slides.length)}`;
  progressBar.style.width = `${((activeIndex + 1) / slides.length) * 100}%`;
  prevSlide.disabled = activeIndex === 0;
  nextSlide.disabled = activeIndex === slides.length - 1;
  const url = new URL(window.location.href);
  url.searchParams.set("slide", String(activeIndex + 1));
  window.history.replaceState({}, "", url);
}

function setTab(tabName) {
  tabs.forEach(tab => tab.classList.toggle("active", tab.dataset.tab === tabName));
  document.querySelectorAll(".tab-pane").forEach(pane => pane.classList.remove("active"));
  document.getElementById(`${tabName}Pane`)?.classList.add("active");
}

function openModal(trigger) {
  lastModalTrigger = trigger;
  const title = trigger.dataset.title || "Preview";
  const copy = trigger.dataset.copy || "";
  const src = trigger.dataset.src || "";
  const img = trigger.dataset.img || "";

  modalTitle.textContent = title;
  modalCopy.textContent = copy;
  modalLaunch.href = src || "#";
  modalLaunch.style.display = src ? "inline-flex" : "none";

  if (img) {
    previewPane.innerHTML = `<img src="${img}" alt="${title} preview">`;
  } else {
    previewPane.innerHTML = `<div class="fallback-preview"><div><strong>${title}</strong><p>${copy || "Open the live tab for this source."}</p></div></div>`;
  }

  if (src) {
    livePane.innerHTML = `<iframe src="${src}" title="${title} live view" loading="lazy"></iframe>`;
  } else {
    livePane.innerHTML = `<div class="fallback-preview">No live source is attached to this view.</div>`;
  }

  setTab("preview");
  modal.hidden = false;
  modal.querySelector(".close-button")?.focus();
}

function closeModal() {
  modal.hidden = true;
  livePane.innerHTML = "";
  lastModalTrigger?.focus();
}

function trapModalFocus(event) {
  if (modal.hidden || event.key !== "Tab") return;
  const focusable = Array.from(modal.querySelectorAll("a[href], button:not([disabled]), iframe, [tabindex]:not([tabindex='-1'])"))
    .filter(element => element.offsetParent !== null);
  if (!focusable.length) return;
  const first = focusable[0];
  const last = focusable[focusable.length - 1];
  if (event.shiftKey && document.activeElement === first) {
    event.preventDefault();
    last.focus();
  } else if (!event.shiftKey && document.activeElement === last) {
    event.preventDefault();
    first.focus();
  }
}

function initialSlideIndex() {
  const params = new URLSearchParams(window.location.search);
  const fromQuery = Number(params.get("slide"));
  if (Number.isFinite(fromQuery) && fromQuery > 0) return fromQuery - 1;
  const fromHash = Number(window.location.hash.replace("#", ""));
  if (Number.isFinite(fromHash) && fromHash > 0) return fromHash - 1;
  return 0;
}

function updateWireframeCarousel(carousel, index) {
  const screens = Array.from(carousel.querySelectorAll(".wireframe-screen"));
  if (!screens.length) return;
  const activeWireframe = Math.max(0, Math.min(screens.length - 1, index));
  carousel.dataset.activeWireframe = String(activeWireframe);
  screens.forEach((screen, screenIndex) => {
    const isActive = screenIndex === activeWireframe;
    screen.classList.toggle("active", isActive);
    screen.setAttribute("aria-hidden", String(!isActive));
  });
  const title = carousel.querySelector("[data-wireframe-title]");
  const count = carousel.querySelector("[data-wireframe-count]");
  if (title) title.textContent = screens[activeWireframe].dataset.wireframeName || `Wireframe ${activeWireframe + 1}`;
  if (count) count.textContent = `${pad(activeWireframe + 1)} / ${pad(screens.length)}`;
}

buildNav();
updateSlide(initialSlideIndex());
const initialWireframe = Number(new URLSearchParams(window.location.search).get("wireframe"));
wireframeCarousels.forEach(carousel => {
  const requestedWireframe = Number.isFinite(initialWireframe) && initialWireframe > 0 ? initialWireframe - 1 : 0;
  updateWireframeCarousel(carousel, requestedWireframe);
});

slideNav.addEventListener("click", event => {
  const button = event.target.closest("[data-slide]");
  if (button) updateSlide(Number(button.dataset.slide));
});

prevSlide.addEventListener("click", () => updateSlide(activeIndex - 1));
nextSlide.addEventListener("click", () => updateSlide(activeIndex + 1));

document.addEventListener("keydown", event => {
  if (!modal.hidden && event.key === "Escape") {
    closeModal();
    return;
  }
  trapModalFocus(event);
  if (!modal.hidden) return;
  if (event.key === "ArrowRight" || event.key === "PageDown") updateSlide(activeIndex + 1);
  if (event.key === "ArrowLeft" || event.key === "PageUp") updateSlide(activeIndex - 1);
  if (event.key === "Home") updateSlide(0);
  if (event.key === "End") updateSlide(slides.length - 1);
});

document.querySelectorAll("[data-open-modal]").forEach(trigger => {
  trigger.addEventListener("click", () => openModal(trigger));
  if (!trigger.matches("button, a, input, select, textarea")) {
    trigger.addEventListener("keydown", event => {
      if (event.key === "Enter" || event.key === " ") {
        event.preventDefault();
        openModal(trigger);
      }
    });
  }
});

document.querySelectorAll("[data-close-modal]").forEach(button => {
  button.addEventListener("click", closeModal);
});

tabs.forEach(tab => {
  tab.addEventListener("click", () => setTab(tab.dataset.tab));
});

wireframeCarousels.forEach(carousel => {
  carousel.querySelector("[data-wireframe-prev]")?.addEventListener("click", () => {
    const screens = carousel.querySelectorAll(".wireframe-screen");
    const current = Number(carousel.dataset.activeWireframe || "0");
    updateWireframeCarousel(carousel, (current - 1 + screens.length) % screens.length);
  });
  carousel.querySelector("[data-wireframe-next]")?.addEventListener("click", () => {
    const screens = carousel.querySelectorAll(".wireframe-screen");
    const current = Number(carousel.dataset.activeWireframe || "0");
    updateWireframeCarousel(carousel, (current + 1) % screens.length);
  });
});
