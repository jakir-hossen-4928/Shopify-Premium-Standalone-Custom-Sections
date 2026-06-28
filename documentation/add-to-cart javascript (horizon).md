{%- comment -%} ── ATC JAVASCRIPT(horizon) ── {%- endcomment -%}
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
