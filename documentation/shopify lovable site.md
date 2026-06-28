**shopify lovable site:**

Each UI section must be built as a completely separate module. All sections should be placed inside a dedicated `sections` folder, with one section per folder/file. The styles for each section must be defined within that same section file—no centralized or global styling is allowed.

Every section must be fully responsive across mobile and desktop devices. The UI design and styling should follow a modern, visually polished, and production-quality standard.

All generated images must be high-resolution, optimized, and responsive across different screen sizes.

Additionally, each section must follow a styling approach similar to the provided example—where styles are scoped locally (e.g., using a `styles` constant inside the component), ensuring complete isolation and no dependency on shared/global CSS.



this is the example: 
```css
import heroImg from "@/assets/hero-serum.jpg";

const styles = `
.vd-hero { background: #F9F8F4; color: #2D3A31; font-family: 'Source Sans 3', system-ui, sans-serif; }
.vd-hero-inner { max-width: 1280px; margin: 0 auto; padding: 24px 24px 64px; }
.vd-nav { display: flex; align-items: center; justify-content: space-between; padding: 8px 0 64px; }
.vd-logo { font-family: 'Playfair Display', serif; font-size: 1.6rem; font-weight: 600; letter-spacing: -0.01em; color: #2D3A31; }
.vd-logo em { font-style: italic; color: #8C9A84; }
.vd-nav-links { display: none; gap: 36px; font-size: 0.85rem; letter-spacing: 0.12em; text-transform: uppercase; color: #2D3A31; }
.vd-nav-links a { color: inherit; text-decoration: none; transition: color .3s ease; }
.vd-nav-links a:hover { color: #C27B66; }
.vd-nav-cta { display: inline-flex; align-items: center; gap: 8px; padding: 12px 22px; border-radius: 999px; background: #2D3A31; color: #F9F8F4; font-size: 0.78rem; letter-spacing: 0.18em; text-transform: uppercase; text-decoration: none; transition: background .3s ease; }
.vd-nav-cta:hover { background: #C27B66; }

.vd-grid { display: grid; grid-template-columns: 1fr; gap: 56px; align-items: center; }
.vd-eyebrow { display: inline-flex; align-items: center; gap: 12px; font-size: 0.78rem; letter-spacing: 0.22em; text-transform: uppercase; color: #8C9A84; margin-bottom: 28px; }
.vd-eyebrow::before { content: ""; width: 36px; height: 1px; background: #8C9A84; display: inline-block; }
.vd-headline { font-family: 'Playfair Display', serif; font-weight: 600; font-size: clamp(2.8rem, 7vw, 5.5rem); line-height: 1.02; letter-spacing: -0.02em; color: #2D3A31; margin: 0 0 28px; }
.vd-headline em { font-style: italic; color: #8C9A84; font-weight: 500; }
.vd-sub { font-size: 1.05rem; line-height: 1.7; color: #4a5a50; max-width: 480px; margin: 0 0 40px; }
.vd-cta-row { display: flex; gap: 16px; flex-wrap: wrap; align-items: center; }
.vd-btn-primary { display: inline-flex; align-items: center; gap: 10px; padding: 16px 32px; border-radius: 999px; background: #2D3A31; color: #F9F8F4; font-size: 0.82rem; letter-spacing: 0.18em; text-transform: uppercase; text-decoration: none; border: none; cursor: pointer; transition: all .3s ease; }
.vd-btn-primary:hover { background: #C27B66; transform: translateY(-1px); }
.vd-btn-ghost { display: inline-flex; align-items: center; gap: 10px; padding: 16px 28px; border-radius: 999px; background: transparent; color: #2D3A31; font-size: 0.82rem; letter-spacing: 0.18em; text-transform: uppercase; text-decoration: none; border: 1px solid #8C9A84; cursor: pointer; transition: all .3s ease; }
.vd-btn-ghost:hover { background: #8C9A84; color: #F9F8F4; }

.vd-img-wrap { position: relative; }
.vd-arch { position: relative; width: 100%; aspect-ratio: 3/4; border-top-left-radius: 9999px; border-top-right-radius: 9999px; overflow: hidden; box-shadow: 0 25px 50px -12px rgba(45,58,49,0.18); animation: vd-float 7s ease-in-out infinite; background: #DCCFC2; }
.vd-arch img { width: 100%; height: 100%; object-fit: cover; display: block; }
.vd-quote { position: absolute; bottom: 28px; left: 50%; transform: translateX(-50%); width: calc(100% - 48px); max-width: 360px; background: rgba(249,248,244,0.85); backdrop-filter: blur(10px); border-radius: 24px; padding: 20px 24px; box-shadow: 0 10px 30px -10px rgba(45,58,49,0.15); }
.vd-quote p { font-family: 'Playfair Display', serif; font-style: italic; font-size: 1.05rem; line-height: 1.4; margin: 0 0 8px; color: #2D3A31; }
.vd-quote span { font-size: 0.72rem; letter-spacing: 0.2em; text-transform: uppercase; color: #8C9A84; }

.vd-stats { display: flex; gap: 40px; margin-top: 48px; padding-top: 32px; border-top: 1px solid #E6E2DA; }
.vd-stat-num { font-family: 'Playfair Display', serif; font-size: 2rem; font-weight: 600; color: #2D3A31; line-height: 1; }
.vd-stat-lbl { font-size: 0.72rem; letter-spacing: 0.18em; text-transform: uppercase; color: #8C9A84; margin-top: 8px; }

@keyframes vd-float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-12px); } }

@media (min-width: 768px) {
  .vd-hero-inner { padding: 32px 48px 96px; }
  .vd-nav-links { display: flex; }
  .vd-grid { grid-template-columns: 1.05fr 1fr; gap: 80px; }
}
`;

const Hero = () => (
  <section className="vd-hero">
    <style>{styles}</style>
    <div className="vd-hero-inner">
      <nav className="vd-nav">
        <div className="vd-logo">Verd<em>é</em></div>
        <div className="vd-nav-links">
          <a href="#collections">Collections</a>
          <a href="#bestsellers">Best Sellers</a>
          <a href="#story">Our Story</a>
          <a href="#journal">Journal</a>
        </div>
        <a href="#shop" className="vd-nav-cta">Shop</a>
      </nav>

      <div className="vd-grid">
        <div>
          <div className="vd-eyebrow">Botanical Skincare · Est. 2018</div>
          <h1 className="vd-headline">
            Nurture your <em>natural</em><br />
            glow, daily.
          </h1>
          <p className="vd-sub">
            Clean, dermatologist-tested formulas crafted from cold-pressed botanicals
            and skin-loving actives. Quiet rituals for radiant, resilient skin.
          </p>
          <div className="vd-cta-row">
            <a href="#collections" className="vd-btn-primary">Shop the Collection</a>
            <a href="#story" className="vd-btn-ghost">Our Ingredients</a>
          </div>
          <div className="vd-stats">
            <div>
              <div className="vd-stat-num">98%</div>
              <div className="vd-stat-lbl">Natural Origin</div>
            </div>
            <div>
              <div className="vd-stat-num">24k+</div>
              <div className="vd-stat-lbl">Glowing Reviews</div>
            </div>
            <div>
              <div className="vd-stat-num">100%</div>
              <div className="vd-stat-lbl">Cruelty Free</div>
            </div>
          </div>
        </div>

        <div className="vd-img-wrap">
          <div className="vd-arch">
            <img src={heroImg} alt="Amber glass botanical serum surrounded by eucalyptus and olive leaves" width={1024} height={1280} />
            <div className="vd-quote">
              <p>"Skin remembers what nature gives it."</p>
              <span>— Verdé Apothecary</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
);

export default Hero;
```
