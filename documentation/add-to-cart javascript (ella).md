{%- comment -%} ── ATC JAVASCRIPT(ella) ── {%- endcomment -%}
<script>
 (function() {

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

        btn.classList.remove('is-loading');
        textEl.innerHTML = '<span class="material-symbols-outlined" aria-hidden="true" style="font-size:{{ section.settings.button_icon_size }}px;line-height:1;">check_circle</span>';
        btn.classList.add('is-success');

        
        function onCartUpdate() {
          document.removeEventListener('cart-update', onCartUpdate);
          document.body.classList.add('cart-sidebar-show');
        }
        document.addEventListener('cart-update', onCartUpdate);

        // fallback 2s
        setTimeout(function() {
          document.removeEventListener('cart-update', onCartUpdate);
          document.body.classList.add('cart-sidebar-show');
        }, 2000);

        // window.sharedFunctions.updateSidebarCart — correct global
        if (window.sharedFunctions && typeof window.sharedFunctions.updateSidebarCart === 'function') {
          window.sharedFunctions.updateSidebarCart(cart);
        }

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
