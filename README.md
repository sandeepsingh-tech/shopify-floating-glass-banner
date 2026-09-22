
# Shopify Liquid Dynamic Glassmorphic Floating Banner

A lightweight, high-converting glassmorphic announcement banner and greeting slider engineered specifically for Shopify themes. Built entirely with pure CSS3 hardware-accelerated animations and vanilla JavaScript—zero dependencies, zero external libraries (no jQuery, Slick, or Swiper).

---

## 🚀 Key Benefits

* **No-Code Merchant Friendly:** Any non-technical store manager, client, or copywriter can add, delete, reorder slides, alter badge tags, update copy, and configure redirect URLs directly inside Shopify's native Theme Customizer without touching theme code.
* **Unified Click Architecture:** Every slide acts as a single cohesive tap target. The badge, announcement text, and action chevron all route seamlessly to the designated collection or product link.
* **Smart Mobile 2-Line Wrapping:** Eliminates awkward text clipping on small viewports by naturally wrapping text across 2 balanced lines while keeping the badge and navigation icons vertically centered.
* **Zero Performance Tax:** Uses hardware-accelerated CSS properties (`transform`, `opacity`) and vanilla JavaScript to deliver smooth 60fps animations without impacting Google Core Web Vitals or mobile Lighthouse scores.
* **Customizable Branding Asset:** The directional up/down control buttons feature vector bees with interactive wing-flutter animations on click/tap, but can be easily replaced with any custom brand icon (such as gift boxes, stars, shopping bags, or simple chevrons).



## 🛠️ Installation & Theme Integration

1. In your Shopify Admin, navigate to **Online Store** > **Themes**.
2. Click **Actions (...)** > **Edit code**.
3. In the **Sections** folder, click **Add a new section**.
4. Name the file `floating-banner.liquid`.
5. Paste the complete Liquid code provided below into the file and click **Save**.
6. Open **Customize Theme**, click **Add section** directly below your Header, and choose **Floating Glass Banner**.

---

## ⚙️ How Non-Technical Users Manage Content

1. Open **Shopify Theme Customizer**.
2. Click on **Floating Glass Banner** in the left section tree.
3. Use the slider to set **Rotation Speed** (2 to 8 seconds).
4. Under **Blocks**, click any slide (or click **Add Slide Message**):
* **Pill Badge:** Enter short tags like `WELCOME`, `TRENDING`, or `DEAL`.
* **Message Content:** Type your promotional text.
* **Click Target (URL):** Pick any collection, specific product, page, blog post, or paste an external URL.


5. Drag blocks to reorder or delete slides anytime, then click **Save**.

---

## 💻 Source Code: `sections/floating-banner.liquid`

```liquid
{%- style -%}
.hm-banner-wrapper {
  padding: 8px 16px;
  width: 100%;
  display: flex;
  justify-content: center;
  box-sizing: border-box;
  position: relative;
  z-index: 1;
}

/* Glassmorphic bar: Solid warm core dissolving smoothly toward transparent ends */
.hm-glass-banner {
  position: relative;
  width: 100%;
  max-width: 1100px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 14px;
  padding: 8px 20px;
  border-radius: 9999px;
  background: radial-gradient(
    ellipse 75% 100% at 50% 50%,
    rgba(255, 248, 220, 0.98) 0%,
    rgba(254, 240, 185, 0.90) 45%,
    rgba(253, 230, 138, 0.55) 70%,
    rgba(255, 255, 255, 0.20) 90%,
    transparent 100%
  );
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 
    0 8px 25px rgba(210, 161, 69, 0.16),
    0 2px 6px rgba(0, 0, 0, 0.04);
  animation: hmFloatIn 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
  z-index: 1;
}

/* Shimmering border gradient */
.hm-glass-banner::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.5px;
  background: linear-gradient(
    90deg,
    rgba(210, 161, 69, 0.2),
    rgba(245, 158, 11, 0.95),
    rgba(255, 215, 0, 0.95),
    rgba(245, 158, 11, 0.95),
    rgba(210, 161, 69, 0.2)
  );
  background-size: 300% 100%;
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
  animation: hmAmberFlow 7s ease infinite;
}

/* Slider Track */
.hm-slider-container {
  display: flex;
  align-items: center;
  gap: 12px;
  flex: 1;
  min-width: 0;
}

.hm-message-viewport {
  position: relative;
  width: 100%;
  height: 30px;
  overflow: hidden;
}

.hm-slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transform: translateY(100%);
  transition: transform 0.45s cubic-bezier(0.2, 0.8, 0.2, 1), opacity 0.45s ease, visibility 0.45s ease;
  user-select: none;
}

.hm-slide.active {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.hm-slide.slide-out {
  opacity: 0;
  visibility: hidden;
  transform: translateY(-100%);
}

/* Clickable Interactive Pill Link */
.hm-slide-link {
  color: #2b251e;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  max-width: 100%;
  cursor: pointer;
  padding: 3px 12px;
  border-radius: 9999px;
  transition: transform 0.2s ease, color 0.2s ease, background 0.2s ease;
}

.hm-slide-link:hover {
  color: #92400e;
  background: rgba(255, 255, 255, 0.45);
}

.hm-badge {
  background: rgba(210, 161, 69, 0.24);
  color: #8c5d0a;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.6px;
  padding: 3px 10px;
  border-radius: 9999px;
  flex-shrink: 0;
}

.hm-slide-text {
  font-size: 13.5px;
  font-weight: 600;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
}

/* Inline Action Arrow */
.hm-action-arrow {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
  color: #8c5d0a;
  transition: transform 0.2s cubic-bezier(0.2, 0.8, 0.2, 1);
  flex-shrink: 0;
}

.hm-slide-link:hover .hm-action-arrow {
  transform: translateX(4px);
}

/* Directional Control Pedestal */
.hm-bee-btn {
  background: radial-gradient(
    circle,
    rgba(217, 119, 6, 0.45) 0%,
    rgba(245, 158, 11, 0.25) 45%,
    rgba(251, 191, 36, 0.08) 70%,
    transparent 100%
  );
  border: none;
  border-radius: 50%;
  cursor: pointer;
  width: 34px;
  height: 34px;
  padding: 0;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.25s ease, background 0.25s ease, box-shadow 0.25s ease;
  flex-shrink: 0;
}

.hm-bee-btn:hover {
  transform: scale(1.12);
  background: radial-gradient(
    circle,
    rgba(217, 119, 6, 0.65) 0%,
    rgba(245, 158, 11, 0.38) 50%,
    transparent 85%
  );
  box-shadow: 0 0 10px rgba(245, 158, 11, 0.32);
}

.hm-bee-svg {
  width: 20px;
  height: 20px;
  display: block;
}

.hm-bee-up .hm-bee-svg {
  transform: rotate(0deg);
}

.hm-bee-down .hm-bee-svg {
  transform: rotate(180deg);
}

/* Wing Flutter Animations */
.hm-bee-btn:hover .wing-left,
.hm-bee-btn.flutter .wing-left {
  animation: hmLeftWingBack 0.12s ease-in-out infinite alternate;
  transform-origin: 9.5px 12px;
}

.hm-bee-btn:hover .wing-right,
.hm-bee-btn.flutter .wing-right {
  animation: hmRightWingBack 0.12s ease-in-out infinite alternate;
  transform-origin: 14.5px 12px;
}

@keyframes hmLeftWingBack {
  0% { transform: rotate(0deg) scaleX(1); }
  100% { transform: rotate(-24deg) scaleX(0.75); }
}

@keyframes hmRightWingBack {
  0% { transform: rotate(0deg) scaleX(1); }
  100% { transform: rotate(24deg) scaleX(0.75); }
}

/* Entrance & Shimmer Keyframes */
@keyframes hmFloatIn {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes hmAmberFlow {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Mobile: 2-line layout with vertically centered pill badge */
@media (max-width: 768px) {
  .hm-banner-wrapper {
    padding: 6px 10px;
  }

  .hm-glass-banner {
    padding: 8px 12px;
    gap: 8px;
    border-radius: 9999px;
  }

  .hm-bee-btn {
    width: 28px;
    height: 28px;
    align-self: center;
  }

  .hm-bee-svg {
    width: 17px;
    height: 17px;
  }

  .hm-message-viewport {
    height: 38px;
  }

  .hm-slide-link {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    gap: 8px;
    padding: 0 4px;
    width: 100%;
  }

  .hm-badge {
    font-size: 9.5px;
    padding: 2px 7px;
    align-self: center;
    line-height: 1.2;
  }

  .hm-slide-text {
    font-size: 12px;
    line-height: 1.3;
    white-space: normal;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-align: center;
    max-width: calc(100% - 75px);
  }

  .hm-action-arrow {
    font-size: 12px;
    align-self: center;
  }
}
{%- endstyle -%}

<div class="hm-banner-wrapper" id="Banner-{{ section.id }}">
  <div class="hm-glass-banner">
    
    <div class="hm-slider-container">
      {%- if section.blocks.size > 1 -%}
        <!-- Control Up -->
        <button class="hm-bee-btn hm-bee-up hm-prev-btn" aria-label="Previous message">
          <svg class="hm-bee-svg" viewBox="0 0 24 24" fill="none" xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)">
            <defs>
              <linearGradient id="goldWingUp-{{ section.id }}" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#FFF9DB" stop-opacity="0.95"/>
                <stop offset="55%" stop-color="#FCD34D" stop-opacity="0.85"/>
                <stop offset="100%" stop-color="#D97706" stop-opacity="0.65"/>
              </linearGradient>
            </defs>
            <path d="M10.5 4.5L9 2M13.5 4.5L15 2" stroke="#4A3419" stroke-width="1.2" stroke-linecap="round"/>
            <circle cx="12" cy="6" r="2.8" fill="#3D2612"/>
            <ellipse cx="12" cy="13.5" rx="4.8" ry="6.5" fill="#FBBF24"/>
            <path d="M7.6 11.5H16.4M7.4 14.2H16.6M8.6 17H15.4" stroke="#2B1E10" stroke-width="1.4" stroke-linecap="round"/>
            <path d="M12 20L12 21.8" stroke="#2B1E10" stroke-width="1.5" stroke-linecap="round"/>
            <path class="wing-left" d="M9.5 11C6.5 13 4 16.5 5.5 18.5C7 20 9.5 17 11 14.5" fill="url(#goldWingUp-{{ section.id }})" stroke="#B45309" stroke-width="1" stroke-linecap="round"/>
            <path class="wing-right" d="M14.5 11C17.5 13 20 16.5 18.5 18.5C17 20 14.5 17 13 14.5" fill="url(#goldWingUp-{{ section.id }})" stroke="#B45309" stroke-width="1" stroke-linecap="round"/>
          </svg>
        </button>
      {%- endif -%}

      <div class="hm-message-viewport" id="Viewport-{{ section.id }}">
        {%- for block in section.blocks -%}
          {%- assign target_link = block.settings.link | default: '#' -%}
          <div 
            class="hm-slide {% if forloop.first %}active{% endif %}" 
            data-index="{{ forloop.index0 }}"
            {{ block.shopify_attributes }}
          >
            <a href="{{ target_link }}" class="hm-slide-link">
              {%- if block.settings.badge != blank -%}
                <span class="hm-badge">{{ block.settings.badge | escape }}</span>
              {%- endif -%}

              <span class="hm-slide-text">{{ block.settings.message | escape }}</span>

              <span class="hm-action-arrow">&rarr;</span>
            </a>
          </div>
        {%- endfor -%}
      </div>

      {%- if section.blocks.size > 1 -%}
        <!-- Control Down -->
        <button class="hm-bee-btn hm-bee-down hm-next-btn" aria-label="Next message">
          <svg class="hm-bee-svg" viewBox="0 0 24 24" fill="none" xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)">
            <defs>
              <linearGradient id="goldWingDown-{{ section.id }}" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#FFF9DB" stop-opacity="0.95"/>
                <stop offset="55%" stop-color="#FCD34D" stop-opacity="0.85"/>
                <stop offset="100%" stop-color="#D97706" stop-opacity="0.65"/>
              </linearGradient>
            </defs>
            <path d="M10.5 4.5L9 2M13.5 4.5L15 2" stroke="#4A3419" stroke-width="1.2" stroke-linecap="round"/>
            <circle cx="12" cy="6" r="2.8" fill="#3D2612"/>
            <ellipse cx="12" cy="13.5" rx="4.8" ry="6.5" fill="#FBBF24"/>
            <path d="M7.6 11.5H16.4M7.4 14.2H16.6M8.6 17H15.4" stroke="#2B1E10" stroke-width="1.4" stroke-linecap="round"/>
            <path d="M12 20L12 21.8" stroke="#2B1E10" stroke-width="1.5" stroke-linecap="round"/>
            <path class="wing-left" d="M9.5 11C6.5 13 4 16.5 5.5 18.5C7 20 9.5 17 11 14.5" fill="url(#goldWingDown-{{ section.id }})" stroke="#B45309" stroke-width="1" stroke-linecap="round"/>
            <path class="wing-right" d="M14.5 11C17.5 13 20 16.5 18.5 18.5C17 20 14.5 17 13 14.5" fill="url(#goldWingDown-{{ section.id }})" stroke="#B45309" stroke-width="1" stroke-linecap="round"/>
          </svg>
        </button>
      {%- endif -%}
    </div>

  </div>
</div>

<script>
document.addEventListener('DOMContentLoaded', () => {
  const root = document.getElementById('Banner-{{ section.id }}');
  if (!root) return;

  const slides = root.querySelectorAll('.hm-slide');
  const viewport = root.querySelector('#Viewport-{{ section.id }}');
  const prevBtn = root.querySelector('.hm-prev-btn');
  const nextBtn = root.querySelector('.hm-next-btn');

  if (slides.length <= 1) return;

  let current = 0;
  let timer = null;
  const speed = {{ section.settings.rotation_speed | default: 4 }} * 1000;

  function triggerFlutter(btn) {
    if (!btn) return;
    btn.classList.add('flutter');
    setTimeout(() => {
      btn.classList.remove('flutter');
    }, 600);
  }

  function goToSlide(nextIndex) {
    slides[current].classList.remove('active');
    slides[current].classList.add('slide-out');

    const prevIndex = current;
    setTimeout(() => {
      slides[prevIndex].classList.remove('slide-out');
    }, 450);

    current = (nextIndex + slides.length) % slides.length;
    slides[current].classList.add('active');
  }

  function nextSlide() {
    goToSlide(current + 1);
  }

  function prevSlide() {
    goToSlide(current - 1);
  }

  function startAutoplay() {
    stopAutoplay();
    timer = setInterval(nextSlide, speed);
  }

  function stopAutoplay() {
    if (timer) clearInterval(timer);
  }

  startAutoplay();
  root.addEventListener('mouseenter', stopAutoplay);
  root.addEventListener('mouseleave', startAutoplay);

  if (nextBtn) {
    nextBtn.addEventListener('click', () => {
      triggerFlutter(nextBtn);
      nextSlide();
      startAutoplay();
    });
  }

  if (prevBtn) {
    prevBtn.addEventListener('click', () => {
      triggerFlutter(prevBtn);
      prevSlide();
      startAutoplay();
    });
  }

  // Mobile Touch Swipe Handling
  let touchStartY = 0;
  viewport.addEventListener('touchstart', (e) => {
    touchStartY = e.touches[0].clientY;
    stopAutoplay();
  }, { passive: true });

  viewport.addEventListener('touchend', (e) => {
    const touchEndY = e.changedTouches[0].clientY;
    const diff = touchStartY - touchEndY;

    if (Math.abs(diff) > 30) {
      if (diff > 0) {
        triggerFlutter(nextBtn);
        nextSlide();
      } else {
        triggerFlutter(prevBtn);
        prevSlide();
      }
    }
    startAutoplay();
  }, { passive: true });
});
</script>

{% schema %}
{
  "name": "Floating Glass Banner",
  "settings": [
    {
      "type": "range",
      "id": "rotation_speed",
      "min": 2,
      "max": 8,
      "step": 1,
      "unit": "s",
      "label": "Rotation Speed (Seconds)",
      "default": 4
    }
  ],
  "blocks": [
    {
      "type": "announcement",
      "name": "Slide Message",
      "settings": [
        {
          "type": "text",
          "id": "badge",
          "label": "Pill Badge (e.g. Welcome / Trending)",
          "default": "Welcome"
        },
        {
          "type": "text",
          "id": "message",
          "label": "Message Content",
          "default": "👋 Welcome to our store • Handpicked finds just for you"
        },
        {
          "type": "url",
          "id": "link",
          "label": "Click Target (Collection or Product URL)"
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Floating Glass Banner",
      "blocks": [
        {
          "type": "announcement",
          "settings": {
            "badge": "Welcome",
            "message": "👋 Welcome to our store • Handpicked finds just for you"
          }
        },
        {
          "type": "announcement",
          "settings": {
            "badge": "Trending",
            "message": "Check out our newest collection arrivals!"
          }
        }
      ]
    }
  ]
}
{% endschema %}

```

---

## 🎨 Asset Customization Guide (Replacing the Animated Mascot)

If you wish to use a different brand asset instead of the bee mascot, change the inner content of `.hm-bee-btn`:

1. Locate both `<button class="hm-bee-btn ...">` elements in the HTML structure.
2. Replace the `<svg class="hm-bee-svg" ...>` tags with your preferred SVG icon (e.g., shopping bag, gift box, sparkling star, or chevron).
3. Adjust the CSS `@keyframes` and `transform-origin` rules to match the animation behavior desired for your custom graphic.

---

## 📄 License

MIT License. Free to use, modify, and distribute across commercial and personal Shopify stores.



```
