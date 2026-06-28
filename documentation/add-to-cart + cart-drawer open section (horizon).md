```liquid
{% comment %}
  Daily Vital Bundle - Premium Hero Banner Section
  Fully customizable via Shopify Theme Editor(horizon)
{% endcomment %}

{%- liquid
  assign section_width = section.settings.section_width
  assign bg_color = section.settings.background_color
  assign badge_bg = section.settings.badge_background_color
  assign badge_text_color = section.settings.badge_text_color
  assign badge_text = section.settings.badge_text
  assign heading_line1 = section.settings.heading_line1
  assign heading_line2 = section.settings.heading_line2
  assign heading_color = section.settings.heading_color
  assign subheading = section.settings.subheading
  assign subheading_color = section.settings.subheading_color
  assign body_text = section.settings.body_text
  assign body_color = section.settings.body_color
  assign btn_text = section.settings.button_text
  assign btn_url = section.settings.button_url
  assign btn_bg = section.settings.button_bg_color
  assign btn_text_color = section.settings.button_text_color
  assign btn_hover_bg = section.settings.button_hover_bg_color
  assign product_image = section.settings.product_image
  assign image_alt = section.settings.image_alt
  assign section_padding_top = section.settings.padding_top
  assign section_padding_bottom = section.settings.padding_bottom
  assign mobile_padding_top = section.settings.mobile_padding_top
  assign mobile_padding_bottom = section.settings.mobile_padding_bottom
  assign image_position = section.settings.image_position
  assign border_radius = section.settings.section_border_radius
  assign content_align = section.settings.content_vertical_align
  assign atc_product = all_products[section.settings.atc_product]
  assign atc_mode = section.settings.button_mode
  assign content_w = section.settings.content_col_width
  assign image_w = section.settings.image_col_width
-%}

{%- style -%}
  #shopify-section-{{ section.id }} {
    background-color: {{ bg_color }};
  }

  .dvb-{{ section.id }} {
    padding-top: {{ section_padding_top }}px;
    padding-bottom: {{ section_padding_bottom }}px;
  }

  .dvb-{{ section.id }} .dvb-container {
    {% if section_width == 'full' %}
      max-width: 100%;
      padding-left: 0;
      padding-right: 0;
    {% elsif section_width == '1170' %}
      max-width: 1170px;
    {% elsif section_width == '1470' %}
      max-width: 1470px;
    {% elsif section_width == '1570' %}
      max-width: 1570px;
    {% elsif section_width == '1770' %}
      max-width: 1770px;
    {% else %}
      max-width: 1570px;
    {% endif %}
    margin-left: auto;
    margin-right: auto;
    {% if section_width != 'full' %}
      padding-left: {{ section.settings.container_side_padding }}px;
      padding-right: {{ section.settings.container_side_padding }}px;
    {% endif %}
  }

  .dvb-{{ section.id }} .dvb-inner {
    display: grid;
    grid-template-columns: {% if image_position == 'right' %}{{ content_w }}% {{ image_w }}%{% else %}{{ image_w }}% {{ content_w }}%{% endif %};
    align-items: {{ content_align }};
    gap: {{ section.settings.column_gap }}px;
    border-radius: {{ border_radius }}px;
    overflow: hidden;
    background-color: {{ bg_color }};
  }

  .dvb-{{ section.id }} .dvb-content {
    padding: {{ section.settings.content_padding_vertical }}px {{ section.settings.content_padding_horizontal }}px;
    order: {% if image_position == 'right' %}1{% else %}2{% endif %};
  }

  .dvb-{{ section.id }} .dvb-image-wrap {
    position: relative;
    overflow: hidden;
    order: {% if image_position == 'right' %}2{% else %}1{% endif %};
    min-height: {{ section.settings.image_min_height }}px;
    border-radius: {% if section_width == 'full' %}0{% else %}{{ section.settings.image_border_radius }}px{% endif %};
  }

  .dvb-{{ section.id }} .dvb-image-wrap img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: {{ section.settings.image_focal_point }};
    display: block;
    transition: transform 0.6s ease;
  }

  .dvb-{{ section.id }} .dvb-image-wrap:hover img {
    transform: scale({{ section.settings.image_hover_zoom }});
  }

  /* Badge */
  .dvb-{{ section.id }} .dvb-badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background-color: {{ badge_bg }};
    color: {{ badge_text_color }};
    font-size: {{ section.settings.badge_font_size }}px;
    font-weight: {{ section.settings.badge_font_weight }};
    letter-spacing: {{ section.settings.badge_letter_spacing }}px;
    text-transform: uppercase;
    padding: {{ section.settings.badge_padding_v }}px {{ section.settings.badge_padding_h }}px;
    border-radius: {{ section.settings.badge_border_radius }}px;
    margin-bottom: {{ section.settings.badge_margin_bottom }}px;
  }

  .dvb-{{ section.id }} .dvb-badge .material-symbols-outlined {
    font-size: {{ section.settings.badge_icon_size }}px;
    color: {{ badge_text_color }};
  }

  /* Heading */
  .dvb-{{ section.id }} .dvb-heading {
    color: {{ heading_color }};
    font-size: {{ section.settings.heading_font_size }}px;
    font-weight: {{ section.settings.heading_font_weight }};
    line-height: {{ section.settings.heading_line_height }};
    letter-spacing: {{ section.settings.heading_letter_spacing }}px;
    text-transform: {{ section.settings.heading_text_transform }};
    margin: 0 0 {{ section.settings.heading_margin_bottom }}px 0;
  }

  /* Subheading */
  .dvb-{{ section.id }} .dvb-subheading {
    color: {{ subheading_color }};
    font-size: {{ section.settings.subheading_font_size }}px;
    font-weight: {{ section.settings.subheading_font_weight }};
    line-height: {{ section.settings.subheading_line_height }};
    margin: 0 0 {{ section.settings.subheading_margin_bottom }}px 0;
  }

  /* Body */
  .dvb-{{ section.id }} .dvb-body {
    color: {{ body_color }};
    font-size: {{ section.settings.body_font_size }}px;
    font-weight: {{ section.settings.body_font_weight }};
    line-height: {{ section.settings.body_line_height }};
    margin: 0 0 {{ section.settings.body_margin_bottom }}px 0;
  }

  /* Feature Pills */
  .dvb-{{ section.id }} .dvb-features {
    display: flex;
    flex-wrap: wrap;
    gap: {{ section.settings.features_gap }}px;
    margin-bottom: {{ section.settings.features_margin_bottom }}px;
  }

  .dvb-{{ section.id }} .dvb-feature-pill {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    background-color: {{ section.settings.pill_bg_color }};
    color: {{ section.settings.pill_text_color }};
    font-size: {{ section.settings.pill_font_size }}px;
    font-weight: {{ section.settings.pill_font_weight }};
    padding: {{ section.settings.pill_padding_v }}px {{ section.settings.pill_padding_h }}px;
    border-radius: {{ section.settings.pill_border_radius }}px;
    border: {{ section.settings.pill_border_width }}px solid {{ section.settings.pill_border_color }};
  }

  .dvb-{{ section.id }} .dvb-feature-pill .material-symbols-outlined {
    font-size: {{ section.settings.pill_icon_size }}px;
    color: {{ section.settings.pill_icon_color }};
  }

  /* Button */
  .dvb-{{ section.id }} .dvb-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    background-color: {{ btn_bg }};
    color: {{ btn_text_color }};
    font-size: {{ section.settings.button_font_size }}px;
    font-weight: {{ section.settings.button_font_weight }};
    letter-spacing: {{ section.settings.button_letter_spacing }}px;
    text-decoration: none;
    padding: {{ section.settings.button_padding_v }}px {{ section.settings.button_padding_h }}px;
    border-radius: {{ section.settings.button_border_radius }}px;
    border: {{ section.settings.button_border_width }}px solid {{ section.settings.button_border_color }};
    cursor: pointer;
    transition: background-color 0.25s ease, transform 0.2s ease, box-shadow 0.25s ease;
    min-width: {{ section.settings.button_min_width }}px;
    text-align: center;
    line-height: 1;
    box-sizing: border-box;
  }

  .dvb-{{ section.id }} .dvb-btn:hover {
    background-color: {{ btn_hover_bg }};
    transform: translateY(-2px);
    box-shadow: 0 6px 20px {{ btn_hover_bg }}55;
  }

  .dvb-{{ section.id }} .dvb-btn .material-symbols-outlined {
    font-size: {{ section.settings.button_icon_size }}px;
    line-height: 1;
    display: inline-flex;
    align-items: center;
  }

  /* Divider */
  .dvb-{{ section.id }} .dvb-divider {
    width: {{ section.settings.divider_width }}px;
    height: {{ section.settings.divider_height }}px;
    background-color: {{ section.settings.divider_color }};
    border-radius: 99px;
    margin-bottom: {{ section.settings.divider_margin_bottom }}px;
    {% unless section.settings.show_divider %}display: none;{% endunless %}
  }

  /* Overlay tint on image */
  .dvb-{{ section.id }} .dvb-image-overlay {
    position: absolute;
    inset: 0;
    background: {{ section.settings.image_overlay_color }};
    opacity: {{ section.settings.image_overlay_opacity | divided_by: 100.0 }};
    pointer-events: none;
  }

  /* ===================== TABLET ===================== */
  @media screen and (max-width: 1024px) {
    .dvb-{{ section.id }} .dvb-heading {
      font-size: {{ section.settings.tablet_heading_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-subheading {
      font-size: {{ section.settings.tablet_subheading_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-body {
      font-size: {{ section.settings.tablet_body_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-inner {
      gap: {{ section.settings.tablet_column_gap }}px;
    }
    .dvb-{{ section.id }} .dvb-content {
      padding: {{ section.settings.tablet_content_padding_v }}px {{ section.settings.tablet_content_padding_h }}px;
    }
    .dvb-{{ section.id }} .dvb-image-wrap {
      min-height: {{ section.settings.tablet_image_min_height }}px;
    }
  }

  /* ===================== MOBILE ===================== */
  @media screen and (max-width: 768px) {
    .dvb-{{ section.id }} {
      padding-top: {{ mobile_padding_top }}px;
      padding-bottom: {{ mobile_padding_bottom }}px;
    }
    .dvb-{{ section.id }} .dvb-container {
      padding-left: {{ section.settings.mobile_side_padding }}px;
      padding-right: {{ section.settings.mobile_side_padding }}px;
    }
    .dvb-{{ section.id }} .dvb-inner {
      grid-template-columns: 1fr;
      gap: 0;
    }
    .dvb-{{ section.id }} .dvb-content {
      order: {% if section.settings.mobile_content_first %}1{% else %}2{% endif %};
      padding: {{ section.settings.mobile_content_padding_v }}px {{ section.settings.mobile_content_padding_h }}px;
      text-align: {{ section.settings.mobile_text_align }};
    }
  .dvb-{{ section.id }} .dvb-image-wrap {
    order: {% if section.settings.mobile_content_first %}2{% else %}1{% endif %};
    min-height: {{ section.settings.mobile_image_height }}px;
    padding: {{ section.settings.mobile_image_padding }}px;
    border-radius: 0 !important;
    background-color: {{ bg_color }};
  }
  .dvb-{{ section.id }} .dvb-image-wrap img {
    border-radius: {{ section.settings.mobile_image_inner_radius }}px;
  }

    .dvb-{{ section.id }} .dvb-heading {
      font-size: {{ section.settings.mobile_heading_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-subheading {
      font-size: {{ section.settings.mobile_subheading_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-body {
      font-size: {{ section.settings.mobile_body_font_size }}px;
    }
    .dvb-{{ section.id }} .dvb-features {
      {%- if section.settings.mobile_text_align == 'center' -%}
        justify-content: center;
      {%- elsif section.settings.mobile_text_align == 'right' -%}
        justify-content: flex-end;
      {%- else -%}
        justify-content: flex-start;
      {%- endif -%}
    }
    .dvb-{{ section.id }} .dvb-btn {
      {% if section.settings.mobile_button_full_width %}width: 100%; max-width: 100%;{% endif %}
      font-size: {{ section.settings.mobile_button_font_size }}px;
      padding: {{ section.settings.mobile_button_padding_v }}px {{ section.settings.mobile_button_padding_h }}px;
    }
    .dvb-{{ section.id }} .dvb-badge {
      {% if section.settings.mobile_text_align == 'center' %}margin-left: auto; margin-right: auto; display: inline-flex;{% endif %}
    }
  }
{%- endstyle -%}

<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" />

<section
  class="dvb-{{ section.id }}"
  id="dvb-{{ section.id }}"
  aria-label="{{ heading_line1 }} {{ heading_line2 }}"
>
  <div class="dvb-container">
    <div class="dvb-inner">

      {%- comment -%} ── CONTENT COLUMN ── {%- endcomment -%}
      <div class="dvb-content">

        {%- if section.settings.show_badge and badge_text != blank -%}
          <div class="dvb-badge">
            {%- if section.settings.badge_icon != blank -%}
              <span class="material-symbols-outlined" aria-hidden="true">{{ section.settings.badge_icon }}</span>
            {%- endif -%}
            {{ badge_text }}
          </div>
        {%- endif -%}

        {%- if heading_line1 != blank or heading_line2 != blank -%}
          <h2 class="dvb-heading">
            {%- if heading_line1 != blank -%}{{ heading_line1 }}<br>{%- endif -%}
            {%- if heading_line2 != blank -%}{{ heading_line2 }}{%- endif -%}
          </h2>
        {%- endif -%}

        {%- if section.settings.show_divider -%}
          <div class="dvb-divider" aria-hidden="true"></div>
        {%- endif -%}

        {%- if subheading != blank -%}
          <p class="dvb-subheading">{{ subheading }}</p>
        {%- endif -%}

        {%- if body_text != blank -%}
          <p class="dvb-body">{{ body_text }}</p>
        {%- endif -%}

        {%- comment -%} Feature pills {%- endcomment -%}
        {%- assign show_any_pill = false -%}
        {%- for block in section.blocks -%}
          {%- if block.type == 'feature_pill' -%}
            {%- assign show_any_pill = true -%}
          {%- endif -%}
        {%- endfor -%}

        {%- if show_any_pill -%}
          <div class="dvb-features">
            {%- for block in section.blocks -%}
              {%- if block.type == 'feature_pill' -%}
                <span class="dvb-feature-pill" {{ block.shopify_attributes }}>
                  {%- if block.settings.pill_icon != blank -%}
                    <span class="material-symbols-outlined" aria-hidden="true">{{ block.settings.pill_icon }}</span>
                  {%- endif -%}
                  {{ block.settings.pill_label }}
                </span>
              {%- endif -%}
            {%- endfor -%}
          </div>
        {%- endif -%}

        {%- if btn_text != blank -%}
          {%- if atc_mode == 'atc' and atc_product != blank -%}
            {%- assign atc_variant = atc_product.selected_or_first_available_variant -%}
            <div class="dvb-atc-wrapper" id="dvb-atc-{{ section.id }}">
              <form method="post" action="/cart/add" id="dvb-form-{{ section.id }}" data-dvb-form>
                <input type="hidden" name="id" value="{{ atc_variant.id }}">
                <input type="hidden" name="quantity" value="1">
                <button
                  type="submit"
                  class="dvb-btn dvb-atc-btn"
                  data-dvb-atc
                  data-variant-id="{{ atc_variant.id }}"
                  {%- unless atc_variant.available %} disabled aria-disabled="true"{%- endunless -%}
                >
                  {%- if section.settings.button_icon_position == 'left' and section.settings.button_icon != blank -%}
                    <span class="material-symbols-outlined" aria-hidden="true">{{ section.settings.button_icon }}</span>
                  {%- endif -%}
                  <span class="dvb-btn-text">
                    {%- unless atc_variant.available -%}
                      {{ 'products.product.sold_out' | t }}
                    {%- else -%}
                      {{ btn_text }}
                    {%- endunless -%}
                  </span>
                  <span class="dvb-btn-loading" aria-hidden="true">
                    <svg width="{{ section.settings.button_icon_size }}" height="{{ section.settings.button_icon_size }}" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" style="display:block;">
                      <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-dasharray="31.4 31.4" transform="rotate(-90 12 12)">
                        <animateTransform attributeName="transform" type="rotate" from="-90 12 12" to="270 12 12" dur="0.8s" repeatCount="indefinite"/>
                      </circle>
                    </svg>
                  </span>
                  {%- if section.settings.button_icon_position == 'right' and section.settings.button_icon != blank -%}
                    <span class="material-symbols-outlined" aria-hidden="true">{{ section.settings.button_icon }}</span>
                  {%- endif -%}
                </button>
              </form>
            </div>
          {%- else -%}
            <a
              href="{{ btn_url }}"
              class="dvb-btn"
              {%- if section.settings.button_open_new_tab %} target="_blank" rel="noopener noreferrer"{%- endif -%}
            >
              {%- if section.settings.button_icon_position == 'left' and section.settings.button_icon != blank -%}
                <span class="material-symbols-outlined" aria-hidden="true">{{ section.settings.button_icon }}</span>
              {%- endif -%}
              {{ btn_text }}
              {%- if section.settings.button_icon_position == 'right' and section.settings.button_icon != blank -%}
                <span class="material-symbols-outlined" aria-hidden="true">{{ section.settings.button_icon }}</span>
              {%- endif -%}
            </a>
          {%- endif -%}
        {%- endif -%}

      </div>

      {%- comment -%} ── IMAGE COLUMN ── {%- endcomment -%}
      <div class="dvb-image-wrap">
        {%- if product_image != blank -%}
          {{
            product_image
            | image_url: width: 1400
            | image_tag:
              loading: 'lazy',
              alt: image_alt,
              widths: '400, 600, 800, 1000, 1200, 1400',
              sizes: '(max-width: 768px) 100vw, 55vw'
          }}
        {%- else -%}
          {{ 'product-1' | placeholder_svg_tag: 'dvb-placeholder-svg' }}
        {%- endif -%}
        <div class="dvb-image-overlay" aria-hidden="true"></div>
      </div>

    </div>
  </div>
</section>



{%- comment -%} ── ATC BUTTON STATES CSS ── {%- endcomment -%}
<style>
  /* Loading state: hide text/icons, show spinner — no height shift */
  .dvb-{{ section.id }} .dvb-atc-btn .dvb-btn-loading { display: none; }
  .dvb-{{ section.id }} .dvb-atc-btn.is-loading .dvb-btn-text { display: none; }
  .dvb-{{ section.id }} .dvb-atc-btn.is-loading > .material-symbols-outlined { display: none; }
  .dvb-{{ section.id }} .dvb-atc-btn.is-loading .dvb-btn-loading {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: {{ section.settings.button_icon_size }}px;
    height: {{ section.settings.button_icon_size }}px;
  }
  .dvb-{{ section.id }} .dvb-atc-btn.is-success { background-color: {{ section.settings.button_success_color }} !important; }
  .dvb-{{ section.id }} .dvb-atc-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none !important; box-shadow: none !important; }

  /* Success icon inside btn-text */
  .dvb-{{ section.id }} .dvb-atc-btn.is-success .dvb-btn-text {
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }
  .dvb-{{ section.id }} .dvb-atc-btn.is-success .dvb-btn-text .material-symbols-outlined {
    font-size: {{ section.settings.button_icon_size }}px;
    line-height: 1;
  }
</style>

{%- comment -%} ── ATC JAVASCRIPT ── {%- endcomment -%}
<script>
(function() {

  function patchDrawer() {
    var drawer = document.querySelector('cart-drawer-component');
    if (!drawer || drawer._dvbPatched) return;
    drawer._dvbPatched = true;

    var dialog = drawer.querySelector('dialog');
    if (!dialog) return;

    // ── Scroll fix ──────────────────────────────────────────────
    dialog.addEventListener('close', function() {
      requestAnimationFrame(function() {
        window.scrollTo({ top: window._dvbScrollY || 0, behavior: 'instant' });
      });
    });

    // ── Cancel fix (ESC key) ─────────────────────────────────────
    dialog.addEventListener('cancel', function(e) {
      e.preventDefault();
      drawer.open = false;
    });

    // ── Backdrop click fix ───────────────────────────────────────
    dialog.addEventListener('click', function(e) {
      var rect = dialog.getBoundingClientRect();
      var outside = e.clientX < rect.left || e.clientX > rect.right ||
                    e.clientY < rect.top  || e.clientY > rect.bottom;
      if (outside) {
        e.stopImmediatePropagation();
        e.preventDefault();
        drawer.open = false;
      }
    }, true);
  }

  window.addEventListener('scroll', function() {
    window._dvbScrollY = window.scrollY;
  }, { passive: true });

  function initPatch() {
    patchDrawer();
    var drawerRoot = document.querySelector('cart-drawer-component');
    if (!drawerRoot) return;
    new MutationObserver(function() {
      drawerRoot._dvbPatched = false;
      patchDrawer();
    }).observe(drawerRoot, { childList: true });
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', initPatch);
  } else {
    initPatch();
  }

  // ── ATC Form ────────────────────────────────────────────────────
  function dvbInit_{{ section.id | replace: '-', '_' }}() {
    var form = document.getElementById('dvb-form-{{ section.id }}');
    if (!form) return;

    form.addEventListener('submit', function(e) {
      e.preventDefault();

      var btn = form.querySelector('[data-dvb-atc]');
      var variantId = btn.getAttribute('data-variant-id');
      if (!variantId || btn.disabled) return;

      var textEl = btn.querySelector('.dvb-btn-text');
      var origHTML = textEl.innerHTML;

      btn.classList.add('is-loading');
      btn.disabled = true;

      fetch('/cart/add.js', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'X-Requested-With': 'XMLHttpRequest'
        },
        body: JSON.stringify({ id: parseInt(variantId), quantity: 1 })
      })
      .then(function(res) {
        if (!res.ok) throw new Error('Cart add failed: ' + res.status);
        return res.json();
      })
      .then(function() {
        return fetch('/cart.js').then(function(r) { return r.json(); });
      })
      .then(function(cart) {

        // Show success icon instead of text — no height shift
        btn.classList.remove('is-loading');
        textEl.innerHTML = '<span class="material-symbols-outlined" aria-hidden="true" style="font-size:{{ section.settings.button_icon_size }}px;line-height:1;">check_circle</span>';
        btn.classList.add('is-success');

        var drawerEl = document.querySelector('cart-drawer-component');

        function openDrawerDialog() {
          if (drawerEl) drawerEl.open = true;
          var dialog = drawerEl ? drawerEl.querySelector('dialog') : null;
          if (dialog && !dialog.open) {
            try { dialog.showModal(); } catch(err) {}
          }
          drawerEl._dvbPatched = false;
          patchDrawer();
        }

        if (drawerEl) {
          var obs = new MutationObserver(function(m, o) {
            o.disconnect();
            openDrawerDialog();
          });
          obs.observe(drawerEl, { childList: true, subtree: true });
          setTimeout(function() { obs.disconnect(); openDrawerDialog(); }, 800);
        }

        document.dispatchEvent(new CustomEvent('cart:update', {
          bubbles: true,
          detail: { data: { itemCount: cart.item_count, source: 'product-form-component' } }
        }));

        setTimeout(function() {
          document.querySelectorAll([
            'cart-count-component',
            '[data-cart-count]',
            '[data-cart-item-count]',
            '.cart-count',
            '.cart__count'
          ].join(',')).forEach(function(el) {
            if (el.children.length === 0) {
              el.textContent = cart.item_count;
            } else {
              var inner = el.querySelector('span, [data-count]');
              if (inner) inner.textContent = cart.item_count;
            }
          });
        }, 150);

        setTimeout(function() {
          btn.classList.remove('is-success');
          textEl.innerHTML = origHTML;
          btn.disabled = false;
        }, 2500);

      })
      .catch(function(err) {
        console.error('DVB ATC error:', err);
        btn.classList.remove('is-loading');
        btn.disabled = false;
        form.submit();
      });
    });
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', dvbInit_{{ section.id | replace: '-', '_' }});
  } else {
    dvbInit_{{ section.id | replace: '-', '_' }}();
  }

  document.addEventListener('shopify:section:load', function(e) {
    if (e.detail && e.detail.sectionId === '{{ section.id }}') {
      dvbInit_{{ section.id | replace: '-', '_' }}();
    }
  });
})();
</script>



{% schema %}
{
  "name": "Daily Vital Bundle Banner",
  "tag": "section",
  "class": "dvb-section-wrap",
  "settings": [
    {
      "type": "header",
      "content": "Layout & Width"
    },
    {
      "type": "select",
      "id": "section_width",
      "label": "Section max-width",
      "default": "1570",
      "options": [
        { "value": "1170", "label": "1170px" },
        { "value": "1470", "label": "1470px" },
        { "value": "1570", "label": "1570px (Default)" },
        { "value": "1770", "label": "1770px" },
        { "value": "full", "label": "Full Width" }
      ]
    },
    {
      "type": "range",
      "id": "container_side_padding",
      "label": "Container side padding (px)",
      "min": 0,
      "max": 80,
      "step": 4,
      "default": 24
    },
    {
      "type": "select",
      "id": "image_position",
      "label": "Image position",
      "default": "right",
      "options": [
        { "value": "right", "label": "Right" },
        { "value": "left", "label": "Left" }
      ]
    },
    {
      "type": "range",
      "id": "content_col_width",
      "label": "Content column width (%)",
      "min": 20,
      "max": 80,
      "step": 5,
      "default": 50,
      "info": "Image column will take the remaining width. Both should ideally add up to 100%."
    },
    {
      "type": "range",
      "id": "image_col_width",
      "label": "Image column width (%)",
      "min": 20,
      "max": 80,
      "step": 5,
      "default": 50
    },
    {
      "type": "select",
      "id": "content_vertical_align",
      "label": "Vertical alignment",
      "default": "center",
      "options": [
        { "value": "start", "label": "Top" },
        { "value": "center", "label": "Center" },
        { "value": "end", "label": "Bottom" }
      ]
    },
    {
      "type": "range",
      "id": "column_gap",
      "label": "Column gap (px)",
      "min": 0,
      "max": 120,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "section_border_radius",
      "label": "Section border radius (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "header",
      "content": "Colors"
    },
    {
      "type": "color",
      "id": "background_color",
      "label": "Background color",
      "default": "#F0EDE6"
    },
    {
      "type": "header",
      "content": "Section Spacing – Desktop"
    },
    {
      "type": "range",
      "id": "padding_top",
      "label": "Padding top (px)",
      "min": 0,
      "max": 120,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "padding_bottom",
      "label": "Padding bottom (px)",
      "min": 0,
      "max": 120,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "content_padding_vertical",
      "label": "Content padding vertical (px)",
      "min": 16,
      "max": 120,
      "step": 4,
      "default": 60
    },
    {
      "type": "range",
      "id": "content_padding_horizontal",
      "label": "Content padding horizontal (px)",
      "min": 16,
      "max": 120,
      "step": 4,
      "default": 64
    },
    {
      "type": "header",
      "content": "Badge"
    },
    {
      "type": "checkbox",
      "id": "show_badge",
      "label": "Show badge",
      "default": true
    },
    {
      "type": "text",
      "id": "badge_text",
      "label": "Badge text",
      "default": "Best Value"
    },
    {
      "type": "text",
      "id": "badge_icon",
      "label": "Badge icon (Material Symbols name)",
      "default": "star",
      "info": "Browse icons at fonts.google.com/icons"
    },
    {
      "type": "color",
      "id": "badge_background_color",
      "label": "Badge background",
      "default": "#1B4D2E"
    },
    {
      "type": "color",
      "id": "badge_text_color",
      "label": "Badge text / icon color",
      "default": "#FFFFFF"
    },
    {
      "type": "range",
      "id": "badge_font_size",
      "label": "Badge font size (px)",
      "min": 10,
      "max": 20,
      "step": 1,
      "default": 12
    },
    {
      "type": "select",
      "id": "badge_font_weight",
      "label": "Badge font weight",
      "default": "700",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "600", "label": "Semi-bold" },
        { "value": "700", "label": "Bold" },
        { "value": "800", "label": "Extra-bold" }
      ]
    },
    {
      "type": "range",
      "id": "badge_letter_spacing",
      "label": "Badge letter spacing (px)",
      "min": 0,
      "max": 6,
      "step": 0.5,
      "default": 1
    },
    {
      "type": "range",
      "id": "badge_padding_v",
      "label": "Badge padding vertical (px)",
      "min": 2,
      "max": 20,
      "step": 1,
      "default": 6
    },
    {
      "type": "range",
      "id": "badge_padding_h",
      "label": "Badge padding horizontal (px)",
      "min": 4,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "range",
      "id": "badge_border_radius",
      "label": "Badge border radius (px)",
      "min": 0,
      "max": 50,
      "step": 2,
      "default": 50
    },
    {
      "type": "range",
      "id": "badge_margin_bottom",
      "label": "Badge bottom margin (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "range",
      "id": "badge_icon_size",
      "label": "Badge icon size (px)",
      "min": 12,
      "max": 24,
      "step": 1,
      "default": 14
    },
    {
      "type": "header",
      "content": "Heading"
    },
    {
      "type": "text",
      "id": "heading_line1",
      "label": "Heading – Line 1",
      "default": "Daily Vital"
    },
    {
      "type": "text",
      "id": "heading_line2",
      "label": "Heading – Line 2",
      "default": "Bundle"
    },
    {
      "type": "color",
      "id": "heading_color",
      "label": "Heading color",
      "default": "#1B4D2E"
    },
    {
      "type": "range",
      "id": "heading_font_size",
      "label": "Heading font size (px)",
      "min": 24,
      "max": 96,
      "step": 2,
      "default": 64
    },
    {
      "type": "select",
      "id": "heading_font_weight",
      "label": "Heading font weight",
      "default": "800",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "600", "label": "Semi-bold" },
        { "value": "700", "label": "Bold" },
        { "value": "800", "label": "Extra-bold" },
        { "value": "900", "label": "Black" }
      ]
    },
    {
      "type": "text",
      "id": "heading_line_height",
      "label": "Heading line-height",
      "default": "1.05"
    },
    {
      "type": "range",
      "id": "heading_letter_spacing",
      "label": "Heading letter spacing (px)",
      "min": -4,
      "max": 10,
      "step": 0.5,
      "default": -1
    },
    {
      "type": "select",
      "id": "heading_text_transform",
      "label": "Heading text transform",
      "default": "uppercase",
      "options": [
        { "value": "none", "label": "None" },
        { "value": "uppercase", "label": "Uppercase" },
        { "value": "capitalize", "label": "Capitalize" }
      ]
    },
    {
      "type": "range",
      "id": "heading_margin_bottom",
      "label": "Heading bottom margin (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "header",
      "content": "Divider"
    },
    {
      "type": "checkbox",
      "id": "show_divider",
      "label": "Show divider",
      "default": false
    },
    {
      "type": "color",
      "id": "divider_color",
      "label": "Divider color",
      "default": "#1B4D2E"
    },
    {
      "type": "range",
      "id": "divider_width",
      "label": "Divider width (px)",
      "min": 20,
      "max": 200,
      "step": 4,
      "default": 60
    },
    {
      "type": "range",
      "id": "divider_height",
      "label": "Divider height (px)",
      "min": 2,
      "max": 10,
      "step": 1,
      "default": 4
    },
    {
      "type": "range",
      "id": "divider_margin_bottom",
      "label": "Divider bottom margin (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "header",
      "content": "Subheading"
    },
    {
      "type": "textarea",
      "id": "subheading",
      "label": "Subheading",
      "default": "Sea Moss Gel + Mossade, Built for daily consistency."
    },
    {
      "type": "color",
      "id": "subheading_color",
      "label": "Subheading color",
      "default": "#1A1A1A"
    },
    {
      "type": "range",
      "id": "subheading_font_size",
      "label": "Subheading font size (px)",
      "min": 14,
      "max": 40,
      "step": 1,
      "default": 22
    },
    {
      "type": "select",
      "id": "subheading_font_weight",
      "label": "Subheading font weight",
      "default": "700",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "600", "label": "Semi-bold" },
        { "value": "700", "label": "Bold" }
      ]
    },
    {
      "type": "text",
      "id": "subheading_line_height",
      "label": "Subheading line-height",
      "default": "1.35"
    },
    {
      "type": "range",
      "id": "subheading_margin_bottom",
      "label": "Subheading bottom margin (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 12
    },
    {
      "type": "header",
      "content": "Body Text"
    },
    {
      "type": "textarea",
      "id": "body_text",
      "label": "Body text",
      "default": "Real minerals. Sugar-free hydration. One simple routine."
    },
    {
      "type": "color",
      "id": "body_color",
      "label": "Body text color",
      "default": "#444444"
    },
    {
      "type": "range",
      "id": "body_font_size",
      "label": "Body font size (px)",
      "min": 12,
      "max": 28,
      "step": 1,
      "default": 16
    },
    {
      "type": "select",
      "id": "body_font_weight",
      "label": "Body font weight",
      "default": "400",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "500", "label": "Medium" },
        { "value": "600", "label": "Semi-bold" }
      ]
    },
    {
      "type": "text",
      "id": "body_line_height",
      "label": "Body line-height",
      "default": "1.6"
    },
    {
      "type": "range",
      "id": "body_margin_bottom",
      "label": "Body bottom margin (px)",
      "min": 0,
      "max": 60,
      "step": 2,
      "default": 24
    },
    {
      "type": "header",
      "content": "Feature Pills"
    },
    {
      "type": "color",
      "id": "pill_bg_color",
      "label": "Pill background",
      "default": "#FFFFFF"
    },
    {
      "type": "color",
      "id": "pill_text_color",
      "label": "Pill text color",
      "default": "#1B4D2E"
    },
    {
      "type": "color",
      "id": "pill_icon_color",
      "label": "Pill icon color",
      "default": "#1B4D2E"
    },
    {
      "type": "color",
      "id": "pill_border_color",
      "label": "Pill border color",
      "default": "#D0E8D8"
    },
    {
      "type": "range",
      "id": "pill_border_width",
      "label": "Pill border width (px)",
      "min": 0,
      "max": 4,
      "step": 1,
      "default": 1
    },
    {
      "type": "range",
      "id": "pill_font_size",
      "label": "Pill font size (px)",
      "min": 10,
      "max": 18,
      "step": 1,
      "default": 13
    },
    {
      "type": "select",
      "id": "pill_font_weight",
      "label": "Pill font weight",
      "default": "600",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "600", "label": "Semi-bold" },
        { "value": "700", "label": "Bold" }
      ]
    },
    {
      "type": "range",
      "id": "pill_padding_v",
      "label": "Pill padding vertical (px)",
      "min": 2,
      "max": 16,
      "step": 1,
      "default": 6
    },
    {
      "type": "range",
      "id": "pill_padding_h",
      "label": "Pill padding horizontal (px)",
      "min": 6,
      "max": 32,
      "step": 2,
      "default": 14
    },
    {
      "type": "range",
      "id": "pill_border_radius",
      "label": "Pill border radius (px)",
      "min": 0,
      "max": 50,
      "step": 2,
      "default": 50
    },
    {
      "type": "range",
      "id": "pill_icon_size",
      "label": "Pill icon size (px)",
      "min": 12,
      "max": 22,
      "step": 1,
      "default": 16
    },
    {
      "type": "range",
      "id": "features_gap",
      "label": "Gap between pills (px)",
      "min": 4,
      "max": 24,
      "step": 2,
      "default": 10
    },
    {
      "type": "range",
      "id": "features_margin_bottom",
      "label": "Pills bottom margin (px)",
      "min": 0,
      "max": 60,
      "step": 2,
      "default": 32
    },
    {
      "type": "header",
      "content": "Button"
    },
    {
      "type": "text",
      "id": "button_text",
      "label": "Button text",
      "default": "Add to Cart"
    },
    {
      "type": "url",
      "id": "button_url",
      "label": "Button link"
    },
    {
      "type": "header",
      "content": "Add to Cart Mode"
    },
    {
      "type": "select",
      "id": "button_mode",
      "label": "Button action",
      "default": "atc",
      "info": "ATC mode: select a product below. Link mode: uses Button link above.",
      "options": [
        { "value": "atc", "label": "Add to Cart (AJAX)" },
        { "value": "link", "label": "Link only" }
      ]
    },
    {
      "type": "product",
      "id": "atc_product",
      "label": "Product to add to cart",
      "info": "Used when Button action is set to Add to Cart"
    },
    {
      "type": "color",
      "id": "button_success_color",
      "label": "Button success color (after add)",
      "default": "#2A7A4B"
    },
    {
      "type": "checkbox",
      "id": "button_open_new_tab",
      "label": "Open in new tab",
      "default": false
    },
    {
      "type": "text",
      "id": "button_icon",
      "label": "Button icon (Material Symbols name)",
      "default": "shopping_cart",
      "info": "Leave blank to hide icon"
    },
    {
      "type": "select",
      "id": "button_icon_position",
      "label": "Icon position",
      "default": "right",
      "options": [
        { "value": "left", "label": "Left" },
        { "value": "right", "label": "Right" }
      ]
    },
    {
      "type": "color",
      "id": "button_bg_color",
      "label": "Button background",
      "default": "#1B4D2E"
    },
    {
      "type": "color",
      "id": "button_hover_bg_color",
      "label": "Button hover background",
      "default": "#163D24"
    },
    {
      "type": "color",
      "id": "button_text_color",
      "label": "Button text color",
      "default": "#FFFFFF"
    },
    {
      "type": "color",
      "id": "button_border_color",
      "label": "Button border color",
      "default": "#1B4D2E"
    },
    {
      "type": "range",
      "id": "button_border_width",
      "label": "Button border width (px)",
      "min": 0,
      "max": 4,
      "step": 1,
      "default": 0
    },
    {
      "type": "range",
      "id": "button_font_size",
      "label": "Button font size (px)",
      "min": 12,
      "max": 24,
      "step": 1,
      "default": 16
    },
    {
      "type": "select",
      "id": "button_font_weight",
      "label": "Button font weight",
      "default": "700",
      "options": [
        { "value": "400", "label": "Regular" },
        { "value": "600", "label": "Semi-bold" },
        { "value": "700", "label": "Bold" },
        { "value": "800", "label": "Extra-bold" }
      ]
    },
    {
      "type": "range",
      "id": "button_letter_spacing",
      "label": "Button letter spacing (px)",
      "min": 0,
      "max": 6,
      "step": 0.5,
      "default": 0.5
    },
    {
      "type": "range",
      "id": "button_padding_v",
      "label": "Button padding vertical (px)",
      "min": 8,
      "max": 32,
      "step": 2,
      "default": 18
    },
    {
      "type": "range",
      "id": "button_padding_h",
      "label": "Button padding horizontal (px)",
      "min": 16,
      "max": 80,
      "step": 4,
      "default": 40
    },
    {
      "type": "range",
      "id": "button_border_radius",
      "label": "Button border radius (px)",
      "min": 0,
      "max": 50,
      "step": 2,
      "default": 8
    },
    {
      "type": "range",
      "id": "button_min_width",
      "label": "Button min-width (px)",
      "min": 0,
      "max": 400,
      "step": 10,
      "default": 200
    },
    {
      "type": "range",
      "id": "button_icon_size",
      "label": "Button icon size (px)",
      "min": 14,
      "max": 28,
      "step": 1,
      "default": 20
    },
    {
      "type": "header",
      "content": "Product Image"
    },
    {
      "type": "image_picker",
      "id": "product_image",
      "label": "Product image"
    },
    {
      "type": "text",
      "id": "image_alt",
      "label": "Image alt text",
      "default": "Daily Vital Bundle – Sea Moss Gel and Mossade products"
    },
    {
      "type": "range",
      "id": "image_min_height",
      "label": "Image min-height (px)",
      "min": 200,
      "max": 800,
      "step": 20,
      "default": 460
    },
    {
      "type": "range",
      "id": "image_border_radius",
      "label": "Image border radius (px)",
      "min": 0,
      "max": 40,
      "step": 2,
      "default": 16
    },
    {
      "type": "select",
      "id": "image_focal_point",
      "label": "Image focal point",
      "default": "center center",
      "options": [
        { "value": "center center", "label": "Center" },
        { "value": "top center", "label": "Top" },
        { "value": "bottom center", "label": "Bottom" },
        { "value": "center left", "label": "Left" },
        { "value": "center right", "label": "Right" }
      ]
    },
    {
      "type": "text",
      "id": "image_hover_zoom",
      "label": "Image hover zoom scale",
      "default": "1.04",
      "info": "e.g. 1.04 = slight zoom. Set to 1 to disable."
    },
    {
      "type": "color",
      "id": "image_overlay_color",
      "label": "Image overlay color",
      "default": "#000000"
    },
    {
  "type": "range",
  "id": "mobile_image_padding",
  "label": "Image padding on mobile (px)",
  "min": 0,
  "max": 32,
  "step": 4,
  "default": 16
},
{
  "type": "range",
  "id": "mobile_image_inner_radius",
  "label": "Image border radius on mobile (px)",
  "min": 0,
  "max": 24,
  "step": 2,
  "default": 12
},
    {
      "type": "range",
      "id": "image_overlay_opacity",
      "label": "Image overlay opacity (%)",
      "min": 0,
      "max": 70,
      "step": 5,
      "default": 0
    },
    {
      "type": "header",
      "content": "Tablet Settings"
    },
    {
      "type": "range",
      "id": "tablet_heading_font_size",
      "label": "Heading font size (px)",
      "min": 24,
      "max": 80,
      "step": 2,
      "default": 52
    },
    {
      "type": "range",
      "id": "tablet_subheading_font_size",
      "label": "Subheading font size (px)",
      "min": 14,
      "max": 32,
      "step": 1,
      "default": 18
    },
    {
      "type": "range",
      "id": "tablet_body_font_size",
      "label": "Body font size (px)",
      "min": 12,
      "max": 22,
      "step": 1,
      "default": 15
    },
    {
      "type": "range",
      "id": "tablet_column_gap",
      "label": "Column gap (px)",
      "min": 0,
      "max": 80,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "tablet_content_padding_v",
      "label": "Content padding vertical (px)",
      "min": 16,
      "max": 80,
      "step": 4,
      "default": 40
    },
    {
      "type": "range",
      "id": "tablet_content_padding_h",
      "label": "Content padding horizontal (px)",
      "min": 16,
      "max": 80,
      "step": 4,
      "default": 40
    },
    {
      "type": "range",
      "id": "tablet_image_min_height",
      "label": "Image min-height (px)",
      "min": 200,
      "max": 600,
      "step": 20,
      "default": 380
    },
    {
      "type": "header",
      "content": "Mobile Settings"
    },
    {
      "type": "range",
      "id": "mobile_padding_top",
      "label": "Section padding top (px)",
      "min": 0,
      "max": 80,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "mobile_padding_bottom",
      "label": "Section padding bottom (px)",
      "min": 0,
      "max": 80,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "mobile_side_padding",
      "label": "Side padding (px)",
      "min": 0,
      "max": 40,
      "step": 4,
      "default": 0
    },
    {
      "type": "range",
      "id": "mobile_content_padding_v",
      "label": "Content padding vertical (px)",
      "min": 16,
      "max": 60,
      "step": 4,
      "default": 32
    },
    {
      "type": "range",
      "id": "mobile_content_padding_h",
      "label": "Content padding horizontal (px)",
      "min": 12,
      "max": 48,
      "step": 4,
      "default": 24
    },
    {
      "type": "range",
      "id": "mobile_heading_font_size",
      "label": "Heading font size (px)",
      "min": 24,
      "max": 60,
      "step": 2,
      "default": 40
    },
    {
      "type": "range",
      "id": "mobile_subheading_font_size",
      "label": "Subheading font size (px)",
      "min": 14,
      "max": 28,
      "step": 1,
      "default": 17
    },
    {
      "type": "range",
      "id": "mobile_body_font_size",
      "label": "Body font size (px)",
      "min": 12,
      "max": 20,
      "step": 1,
      "default": 14
    },
    {
      "type": "select",
      "id": "mobile_text_align",
      "label": "Text alignment",
      "default": "left",
      "options": [
        { "value": "left", "label": "Left" },
        { "value": "center", "label": "Center" },
        { "value": "right", "label": "Right" }
      ]
    },
    {
      "type": "checkbox",
      "id": "mobile_content_first",
      "label": "Show text above image on mobile",
      "default": false
    },
    {
      "type": "range",
      "id": "mobile_image_height",
      "label": "Image height on mobile (px)",
      "min": 180,
      "max": 500,
      "step": 20,
      "default": 280
    },
    {
      "type": "range",
      "id": "mobile_button_font_size",
      "label": "Button font size (px)",
      "min": 12,
      "max": 20,
      "step": 1,
      "default": 15
    },
    {
      "type": "range",
      "id": "mobile_button_padding_v",
      "label": "Button padding vertical (px)",
      "min": 8,
      "max": 24,
      "step": 2,
      "default": 16
    },
    {
      "type": "range",
      "id": "mobile_button_padding_h",
      "label": "Button padding horizontal (px)",
      "min": 16,
      "max": 60,
      "step": 4,
      "default": 32
    },
    {
      "type": "checkbox",
      "id": "mobile_button_full_width",
      "label": "Full-width button on mobile",
      "default": true
    }
  ],
  "blocks": [
    {
      "type": "feature_pill",
      "name": "Feature Pill",
      "settings": [
        {
          "type": "text",
          "id": "pill_label",
          "label": "Pill text",
          "default": "Sugar Free"
        },
        {
          "type": "text",
          "id": "pill_icon",
          "label": "Icon (Material Symbols name)",
          "default": "check_circle",
          "info": "Browse at fonts.google.com/icons"
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Daily Vital Bundle Banner",
      "blocks": [
        {
          "type": "feature_pill",
          "settings": {
            "pill_label": "Real Minerals",
            "pill_icon": "diamond"
          }
        },
        {
          "type": "feature_pill",
          "settings": {
            "pill_label": "Sugar Free",
            "pill_icon": "no_food"
          }
        },
        {
          "type": "feature_pill",
          "settings": {
            "pill_label": "Eco Friendly",
            "pill_icon": "eco"
          }
        }
      ]
    }
  ]
}
{% endschema %}
```
