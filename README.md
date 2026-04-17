<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shalev Dev</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600&family=Outfit:wght@300;400;500&display=swap" rel="stylesheet">
<style>
* { margin:0; padding:0; box-sizing:border-box; }
:root {
  --black:#0a0a0a; --white:#fafafa; --accent:#7F77DD; --accent-light:#EEEDFE;
  --gray:#888780; --border:rgba(0,0,0,0.08); --card-bg:#ffffff;
}
body { font-family:'Outfit',sans-serif; background:var(--white); color:var(--black); direction:rtl; overflow-x:hidden; }
 
/* AUTH OVERLAY */
#auth-overlay {
  position:fixed; inset:0; background:var(--white); z-index:1000;
  display:flex; align-items:center; justify-content:center;
}
.auth-box {
  background:#fff; border:1px solid var(--border); border-radius:24px;
  padding:2.5rem 2rem; width:100%; max-width:380px; text-align:center;
  box-shadow:0 8px 40px rgba(0,0,0,0.06);
}
.auth-logo { font-family:'Space Grotesk',sans-serif; font-size:1.5rem; font-weight:600; margin-bottom:0.3rem; }
.auth-logo span { color:var(--accent); }
.auth-sub { font-size:0.85rem; color:var(--gray); margin-bottom:2rem; font-weight:300; }
.auth-tabs { display:flex; background:#f5f4f2; border-radius:12px; padding:4px; margin-bottom:1.5rem; gap:4px; }
.auth-tab {
  flex:1; padding:0.5rem; border:none; background:transparent; border-radius:9px;
  font-size:0.85rem; cursor:pointer; font-family:'Outfit',sans-serif; color:var(--gray); transition:all 0.2s;
}
.auth-tab.active { background:#fff; color:var(--black); font-weight:500; box-shadow:0 1px 4px rgba(0,0,0,0.08); }
.auth-input {
  width:100%; padding:0.75rem 1rem; border:1px solid var(--border); border-radius:12px;
  font-size:0.9rem; font-family:'Outfit',sans-serif; background:#fafafa; margin-bottom:0.75rem;
  outline:none; transition:border-color 0.2s; direction:ltr; text-align:right;
}
.auth-input:focus { border-color:var(--accent); }
.auth-btn {
  width:100%; padding:0.85rem; background:var(--black); color:#fff; border:none;
  border-radius:50px; font-size:0.9rem; font-weight:500; cursor:pointer;
  font-family:'Outfit',sans-serif; transition:background 0.2s; margin-top:0.5rem;
}
.auth-btn:hover { background:var(--accent); }
.auth-error { font-size:0.82rem; color:#E24B4A; margin-top:0.5rem; min-height:1.2rem; }
.auth-success { font-size:0.82rem; color:#1D9E75; margin-top:0.5rem; }
 
/* ADMIN PANEL */
#admin-panel {
  display:none; position:fixed; inset:0; background:var(--white); z-index:999; overflow-y:auto; padding:2rem;
}
.admin-header {
  display:flex; justify-content:space-between; align-items:center;
  margin-bottom:2rem; padding-bottom:1rem; border-bottom:1px solid var(--border);
}
.admin-title { font-family:'Space Grotesk',sans-serif; font-size:1.4rem; font-weight:600; }
.admin-logout {
  background:transparent; border:1px solid var(--border); padding:0.4rem 1rem;
  border-radius:50px; cursor:pointer; font-size:0.82rem; font-family:'Outfit',sans-serif;
  color:var(--gray); transition:all 0.2s;
}
.admin-logout:hover { border-color:var(--black); color:var(--black); }
.orders-grid { display:grid; gap:1rem; }
.order-card {
  background:#fff; border:1px solid var(--border); border-radius:16px; padding:1.2rem 1.5rem;
}
.order-top { display:flex; justify-content:space-between; align-items:flex-start; margin-bottom:0.75rem; }
.order-name { font-weight:500; font-size:0.95rem; }
.order-date { font-size:0.75rem; color:var(--gray); }
.order-type {
  display:inline-block; background:var(--accent-light); color:var(--accent);
  font-size:0.75rem; padding:0.25rem 0.75rem; border-radius:50px; margin-bottom:0.5rem;
}
.order-desc { font-size:0.85rem; color:var(--gray); line-height:1.5; font-weight:300; }
.order-contact { font-size:0.8rem; color:var(--gray); margin-top:0.5rem; }
.no-orders { text-align:center; color:var(--gray); padding:3rem; font-weight:300; }
.orders-count { font-size:0.85rem; color:var(--gray); margin-bottom:1rem; font-weight:300; }
.delete-order {
  background:transparent; border:none; color:#E24B4A; cursor:pointer;
  font-size:0.78rem; margin-top:0.5rem; font-family:'Outfit',sans-serif;
}
 
/* NAV */
nav {
  display:flex; justify-content:space-between; align-items:center;
  padding:1.2rem 2.5rem; border-bottom:1px solid var(--border);
  position:sticky; top:0; background:rgba(250,250,250,0.95);
  backdrop-filter:blur(8px); z-index:100;
}
.logo { font-family:'Space Grotesk',sans-serif; font-size:1.3rem; font-weight:600; letter-spacing:-0.5px; }
.logo span { color:var(--accent); }
.nav-links { display:flex; gap:2rem; list-style:none; }
.nav-links a { text-decoration:none; color:var(--gray); font-size:0.9rem; transition:color 0.2s; }
.nav-links a:hover { color:var(--black); }
.nav-user { display:flex; align-items:center; gap:0.75rem; }
.nav-user-name { font-size:0.85rem; color:var(--gray); }
.nav-signout {
  background:transparent; border:1px solid var(--border); padding:0.4rem 1rem;
  border-radius:50px; cursor:pointer; font-size:0.8rem; font-family:'Outfit',sans-serif;
  color:var(--gray); transition:all 0.2s;
}
.nav-signout:hover { color:var(--black); border-color:var(--black); }
 
/* HERO */
.hero {
  min-height:88vh; display:flex; flex-direction:column;
  align-items:center; justify-content:center; text-align:center; padding:4rem 2rem;
}
.hero-tag {
  display:inline-block; background:var(--accent-light); color:var(--accent);
  font-size:0.78rem; font-weight:500; padding:0.35rem 1rem; border-radius:50px;
  margin-bottom:1.5rem; letter-spacing:0.5px;
}
.hero h1 {
  font-family:'Space Grotesk',sans-serif; font-size:clamp(2.5rem,6vw,5rem);
  font-weight:600; line-height:1.1; letter-spacing:-2px; max-width:700px; margin-bottom:1.2rem;
}
.hero h1 em { font-style:normal; color:var(--accent); }
.hero p { font-size:1.05rem; color:var(--gray); max-width:440px; line-height:1.7; margin-bottom:2.5rem; font-weight:300; }
.hero-btns { display:flex; gap:1rem; justify-content:center; flex-wrap:wrap; }
.btn-primary {
  background:var(--black); color:var(--white); padding:0.85rem 2rem; border-radius:50px;
  font-size:0.9rem; font-weight:500; border:none; cursor:pointer; transition:background 0.2s,transform 0.15s;
  font-family:'Outfit',sans-serif;
}
.btn-primary:hover { background:var(--accent); transform:translateY(-1px); }
.btn-secondary {
  background:transparent; color:var(--black); padding:0.85rem 2rem; border-radius:50px;
  font-size:0.9rem; font-weight:500; border:1px solid rgba(0,0,0,0.15); cursor:pointer;
  transition:border-color 0.2s,transform 0.15s; font-family:'Outfit',sans-serif;
}
.btn-secondary:hover { border-color:var(--black); transform:translateY(-1px); }
 
/* STATS */
.stats-bar {
  display:flex; justify-content:center; gap:3rem; padding:2rem;
  border-top:1px solid var(--border); border-bottom:1px solid var(--border); flex-wrap:wrap;
}
.stat { text-align:center; }
.stat-num { font-family:'Space Grotesk',sans-serif; font-size:1.8rem; font-weight:600; letter-spacing:-1px; }
.stat-label { font-size:0.78rem; color:var(--gray); margin-top:2px; font-weight:300; }
 
/* SERVICES */
.section { padding:5rem 2.5rem; max-width:1100px; margin:0 auto; }
.section-label { font-size:0.75rem; font-weight:500; letter-spacing:2px; color:var(--accent); text-transform:uppercase; margin-bottom:0.75rem; }
.section-title { font-family:'Space Grotesk',sans-serif; font-size:clamp(1.8rem,3vw,2.5rem); font-weight:600; letter-spacing:-1px; margin-bottom:0.75rem; }
.section-sub { font-size:0.95rem; color:var(--gray); font-weight:300; margin-bottom:3rem; max-width:480px; line-height:1.7; }
.cards-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr)); gap:1.5rem; }
.service-card {
  background:var(--card-bg); border:1px solid var(--border); border-radius:20px;
  padding:2rem; transition:transform 0.2s,box-shadow 0.2s; cursor:pointer;
}
.service-card:hover { transform:translateY(-4px); box-shadow:0 12px 40px rgba(0,0,0,0.08); }
.card-icon { width:48px; height:48px; border-radius:14px; display:flex; align-items:center; justify-content:center; margin-bottom:1.2rem; font-size:1.3rem; }
.icon-purple { background:var(--accent-light); }
.icon-teal { background:#E1F5EE; }
.card-title { font-family:'Space Grotesk',sans-serif; font-size:1.1rem; font-weight:600; margin-bottom:0.5rem; letter-spacing:-0.3px; }
.card-desc { font-size:0.88rem; color:var(--gray); line-height:1.6; font-weight:300; }
.card-price { margin-top:1.2rem; display:flex; align-items:center; justify-content:space-between; }
.price-tag { font-family:'Space Grotesk',sans-serif; font-size:1.1rem; font-weight:600; }
.price-tag span { font-size:0.75rem; color:var(--gray); font-weight:400; }
.card-btn {
  background:var(--black); color:var(--white); border:none; padding:0.5rem 1.1rem;
  border-radius:50px; font-size:0.8rem; cursor:pointer; font-family:'Outfit',sans-serif; transition:background 0.2s;
}
.card-btn:hover { background:var(--accent); }
 
/* ORDER MODAL */
#order-modal {
  display:none; position:fixed; inset:0; background:rgba(0,0,0,0.4); z-index:500;
  align-items:center; justify-content:center;
}
#order-modal.open { display:flex; }
.modal-box {
  background:#fff; border-radius:24px; padding:2rem; width:100%; max-width:440px;
  max-height:90vh; overflow-y:auto;
}
.modal-title { font-family:'Space Grotesk',sans-serif; font-size:1.2rem; font-weight:600; margin-bottom:0.3rem; }
.modal-sub { font-size:0.83rem; color:var(--gray); margin-bottom:1.5rem; font-weight:300; }
.modal-label { font-size:0.82rem; color:var(--gray); margin-bottom:0.3rem; display:block; }
.modal-select, .modal-textarea, .modal-input {
  width:100%; padding:0.75rem 1rem; border:1px solid var(--border); border-radius:12px;
  font-size:0.9rem; font-family:'Outfit',sans-serif; background:#fafafa; margin-bottom:1rem;
  outline:none; transition:border-color 0.2s;
}
.modal-select:focus, .modal-textarea:focus, .modal-input:focus { border-color:var(--accent); }
.modal-textarea { resize:vertical; min-height:100px; }
.modal-btns { display:flex; gap:0.75rem; margin-top:0.5rem; }
.modal-submit {
  flex:1; background:var(--black); color:#fff; border:none; padding:0.85rem;
  border-radius:50px; font-size:0.9rem; font-weight:500; cursor:pointer;
  font-family:'Outfit',sans-serif; transition:background 0.2s;
}
.modal-submit:hover { background:var(--accent); }
.modal-cancel {
  background:transparent; color:var(--gray); border:1px solid var(--border);
  padding:0.85rem 1.5rem; border-radius:50px; font-size:0.9rem; cursor:pointer;
  font-family:'Outfit',sans-serif;
}
.modal-ok { color:#1D9E75; font-size:0.9rem; margin-top:0.5rem; display:none; }
 
/* HOW */
.how-section { background:#f5f4f2; padding:5rem 2.5rem; }
.how-inner { max-width:1100px; margin:0 auto; }
.steps { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:2rem; margin-top:3rem; }
.step { display:flex; flex-direction:column; gap:0.75rem; }
.step-num { font-family:'Space Grotesk',sans-serif; font-size:2.5rem; font-weight:600; color:rgba(0,0,0,0.07); line-height:1; letter-spacing:-2px; }
.step-title { font-family:'Space Grotesk',sans-serif; font-size:1rem; font-weight:600; letter-spacing:-0.3px; }
.step-desc { font-size:0.85rem; color:var(--gray); line-height:1.6; font-weight:300; }
 
/* CTA */
.cta-banner { background:var(--black); color:var(--white); text-align:center; padding:5rem 2rem; }
.cta-banner h2 { font-family:'Space Grotesk',sans-serif; font-size:clamp(1.8rem,3.5vw,3rem); font-weight:600; letter-spacing:-1px; margin-bottom:0.75rem; }
.cta-banner h2 em { font-style:normal; color:#AFA9EC; }
.cta-banner p { color:rgba(255,255,255,0.5); font-size:0.95rem; font-weight:300; margin-bottom:2rem; }
.btn-white {
  background:var(--white); color:var(--black); padding:0.9rem 2.2rem; border-radius:50px;
  font-size:0.9rem; font-weight:500; border:none; cursor:pointer;
  font-family:'Outfit',sans-serif; transition:background 0.2s;
}
.btn-white:hover { background:var(--accent-light); }
 
/* FOOTER */
footer {
  padding:2rem 2.5rem; border-top:1px solid var(--border);
  display:flex; justify-content:space-between; align-items:center;
  flex-wrap:wrap; gap:1rem; font-size:0.82rem; color:var(--gray);
}
footer a { color:var(--gray); text-decoration:none; transition:color 0.2s; }
footer a:hover { color:var(--black); }
.social-links { display:flex; gap:1.2rem; }
 
@media(max-width:600px){
  nav { padding:1rem 1.2rem; }
  .nav-links { display:none; }
  .section { padding:3.5rem 1.2rem; }
  .hero { padding:3rem 1.2rem; min-height:auto; }
}
</style>
</head>
<body>
 
<!-- AUTH OVERLAY -->
<div id="auth-overlay">
  <div class="auth-box">
    <div class="auth-logo">Shalev<span>.</span>Dev</div>
    <div class="auth-sub">ברוך הבא — התחבר או הירשם כדי להמשיך</div>
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchTab('login')">התחברות</button>
      <button class="auth-tab" onclick="switchTab('register')">הרשמה</button>
    </div>
    <div id="login-form">
      <input class="auth-input" type="email" id="login-email" placeholder="כתובת מייל" />
      <input class="auth-input" type="password" id="login-pass" placeholder="סיסמה" />
      <button class="auth-btn" onclick="doLogin()">התחבר</button>
      <div class="auth-error" id="login-error"></div>
    </div>
    <div id="register-form" style="display:none">
      <input class="auth-input" type="text" id="reg-name" placeholder="שם מלא" />
      <input class="auth-input" type="email" id="reg-email" placeholder="כתובת מייל" />
      <input class="auth-input" type="password" id="reg-pass" placeholder="סיסמה (לפחות 6 תווים)" />
      <button class="auth-btn" onclick="doRegister()">הרשמה</button>
      <div class="auth-error" id="reg-error"></div>
      <div class="auth-success" id="reg-success" style="display:none">נרשמת בהצלחה! מתחבר...</div>
    </div>
  </div>
</div>
 
<!-- ADMIN PANEL -->
<div id="admin-panel">
  <div class="admin-header">
    <div class="admin-title">פאנל ניהול — הזמנות</div>
    <button class="admin-logout" onclick="adminLogout()">יציאה</button>
  </div>
  <div class="orders-count" id="orders-count"></div>
  <div class="orders-grid" id="orders-list"></div>
</div>
 
<!-- ORDER MODAL -->
<div id="order-modal">
  <div class="modal-box">
    <div class="modal-title">שליחת הזמנה</div>
    <div class="modal-sub">מלא את הפרטים ונחזור אליך בהקדם</div>
    <label class="modal-label">סוג המוצר</label>
    <select class="modal-select" id="order-type">
      <option>GIF מותאם אישית</option>
      <option>בוט מותאם אישית</option>
      <option>חבילת פרימיום (GIF + בוט)</option>
    </select>
    <label class="modal-label">פרטי הבקשה</label>
    <textarea class="modal-textarea" id="order-desc" placeholder="תאר מה אתה צריך — סגנון, שימוש, פלטפורמה..."></textarea>
    <label class="modal-label">איך לחזור אליך? (  מייל / דיסקורד)</label>
    <input class="modal-input" type="text" id="order-contact" placeholder="@username / email" />
    <div class="modal-btns">
      <button class="modal-cancel" onclick="closeModal()">ביטול</button>
      <button class="modal-submit" onclick="submitOrder()">שלח הזמנה</button>
    </div>
    <div class="modal-ok" id="modal-ok">ההזמנה נשלחה בהצלחה!</div>
  </div>
</div>
 
<!-- MAIN SITE -->
<div id="main-site" style="display:none">
 
<nav>
  <div class="logo">Shalev<span>.</span>Dev</div>
  <ul class="nav-links">
    <li><a href="#">שירותים</a></li>
    <li><a href="#">תהליך</a></li>
    <li><a href="#">צור קשר</a></li>
  </ul>
  <div class="nav-user">
    <span class="nav-user-name" id="nav-username"></span>
    <button class="nav-signout" onclick="signOut()">התנתק</button>
  </div>
</nav>
 
<section class="hero">
  <div class="hero-tag">✦ GIF-ים ובוטים בהזמנה אישית</div>
  <h1>תוכן דיגיטלי<br><em>בדיוק כמו שרצית</em></h1>
  <p>אנימציות GIF מותאמות אישית ובוטים חכמים שנבנים במיוחד בשבילך — מהר, מקצועי, ובמחיר שמשתלם.</p>
  <div class="hero-btns">
    <button class="btn-primary" onclick="openModal()">הזמן עכשיו</button>
    <button class="btn-secondary" onclick="document.querySelector('.section').scrollIntoView({behavior:'smooth'})">ראה שירותים</button>
  </div>
</section>
 
<div class="stats-bar">
  <div class="stat"><div class="stat-num">150+</div><div class="stat-label">לקוחות מרוצים</div></div>
  <div class="stat"><div class="stat-num">48h</div><div class="stat-label">זמן אספקה ממוצע</div></div>
  <div class="stat"><div class="stat-num">100%</div><div class="stat-label">מותאם אישית</div></div>
  <div class="stat"><div class="stat-num">∞</div><div class="stat-label">תיקונים עד שמושלם</div></div>
</div>
 
<div class="section">
  <div class="section-label">שירותים</div>
  <h2 class="section-title">מה אנחנו מציעים</h2>
  <p class="section-sub">כל מוצר נבנה מאפס לפי הדרישות שלך — אין תבניות, אין קיצורי דרך.</p>
  <div class="cards-grid">
    <div class="service-card">
      <div class="card-icon icon-purple">🎞</div>
      <div class="card-title">GIF מותאם אישית</div>
      <p class="card-desc">אנימציות GIF ייחודיות לשימוש בסושיאל, אתרים, מסרים ומצגות.</p>
      <div class="card-price">
        <div class="price-tag">₪5 <span>/ GIF</span></div>
        <button class="card-btn" onclick="openModal('GIF מותאם אישית')">הזמן</button>
      </div>
    </div>
    <div class="service-card">
      <div class="card-icon icon-teal">🤖</div>
      <div class="card-title">בוט מותאם אישית</div>
      <p class="card-desc"> בוטים לדיסקורד</p>
      <div class="card-price">
        <div class="price-tag">₪8 <span>/ בוט</span></div>
        <button class="card-btn" onclick="openModal('בוט מותאם אישית')">הזמן</button>
      </div>
    </div>
    <div class="service-card">
      <div class="card-icon icon-purple">⚡</div>
      <div class="card-title">חבילת פרימיום</div>
      <p class="card-desc">GIF + בוט ביחד עם עדיפות בתור ותמיכה מלאה לחודש שלם.</p>
      <div class="card-price">
        <div class="price-tag">17 <span>/ חבילה</span></div>
        <button class="card-btn" onclick="openModal('חבילת פרימיום (GIF + בוט)')">הזמן</button>
      </div>
    </div>
  </div>
</div>
 
<div class="how-section">
  <div class="how-inner">
    <div class="section-label">תהליך</div>
    <h2 class="section-title">איך זה עובד?</h2>
    <div class="steps">
      <div class="step">
        <div class="step-num">01</div>
        <div class="step-title">ספר לנו מה אתה צריך</div>
        <p class="step-desc">שלח הזמנה עם הפרטים — מה המוצר, לאיזה פלטפורמה, ומה הסגנון.</p>
      </div>
      <div class="step">
        <div class="step-num">02</div>
        <div class="step-title">אנחנו מאשרים ומתחילים</div>
        <p class="step-desc">נחזור אליך תוך שעות עם הצעת מחיר וציר זמן.</p>
      </div>
      <div class="step">
        <div class="step-num">03</div>
        <div class="step-title">גרסה ראשונה לבדיקה</div>
        <p class="step-desc">תקבל את המוצר לבדיקה — ניתן לתיקונים עד שאתה מרוצה.</p>
      </div>
      <div class="step">
        <div class="step-num">04</div>
        <div class="step-title">מוצר מוכן אצלך</div>
        <p class="step-desc">מסירה מלאה עם כל הקבצים, הקוד ותיעוד שימוש.</p>
      </div>
    </div>
  </div>
</div>
 
<div class="cta-banner">
  <h2>מוכן להתחיל?<br><em>בוא נבנה משהו יחד.</em></h2>
  <p>הגע עם רעיון — אנחנו נהפוך אותו למוצר.</p>
  <button class="btn-white" onclick="openModal()">שלח הזמנה עכשיו</button>
</div>
 
<footer>
  <div class="logo">Shalev<span style="color:var(--accent)">.</span>Dev</div>
  <div>GIF-ים ובוטים בהזמנה אישית</div>
  <div class="social-links">
    <a href="https://discord.com/users/1461853510877577271" target="_blank">Discord</a>
    <a href="#" target="_blank">Instagram</a>
    <a href="#" target="_blank">Telegram</a>
  </div>
</footer>
 
</div>
 
<script>
const ADMIN_EMAIL = 'shalevaaqaz13@gmail.com';
const USERS_KEY = 'shalev_users';
const ORDERS_KEY = 'shalev_orders';
const SESSION_KEY = 'shalev_session';
 
function getUsers() { try { return JSON.parse(localStorage.getItem(USERS_KEY)) || {}; } catch(e) { return {}; } }
function saveUsers(u) { localStorage.setItem(USERS_KEY, JSON.stringify(u)); }
function getOrders() { try { return JSON.parse(localStorage.getItem(ORDERS_KEY)) || []; } catch(e) { return []; } }
function saveOrders(o) { localStorage.setItem(ORDERS_KEY, JSON.stringify(o)); }
function getSession() { try { return JSON.parse(localStorage.getItem(SESSION_KEY)); } catch(e) { return null; } }
function saveSession(s) { localStorage.setItem(SESSION_KEY, JSON.stringify(s)); }
function clearSession() { localStorage.removeItem(SESSION_KEY); }
 
function switchTab(tab) {
  document.querySelectorAll('.auth-tab').forEach((t,i) => t.classList.toggle('active', (tab==='login'&&i===0)||(tab==='register'&&i===1)));
  document.getElementById('login-form').style.display = tab==='login'?'block':'none';
  document.getElementById('register-form').style.display = tab==='register'?'block':'none';
}
 
function doLogin() {
  const email = document.getElementById('login-email').value.trim().toLowerCase();
  const pass = document.getElementById('login-pass').value;
  const err = document.getElementById('login-error');
  if (!email || !pass) { err.textContent = 'נא למלא את כל השדות'; return; }
  const users = getUsers();
  if (email === ADMIN_EMAIL) {
    if (!users[email]) { err.textContent = 'מייל לא רשום'; return; }
    if (users[email].pass !== btoa(pass)) { err.textContent = 'סיסמה שגויה'; return; }
    saveSession({ email, name: 'Admin' });
    showSite(email, 'Admin');
    return;
  }
  if (!users[email]) { err.textContent = 'מייל לא רשום במערכת'; return; }
  if (users[email].pass !== btoa(pass)) { err.textContent = 'סיסמה שגויה'; return; }
  err.textContent = '';
  saveSession({ email, name: users[email].name });
  showSite(email, users[email].name);
}
 
function doRegister() {
  const name = document.getElementById('reg-name').value.trim();
  const email = document.getElementById('reg-email').value.trim().toLowerCase();
  const pass = document.getElementById('reg-pass').value;
  const err = document.getElementById('reg-error');
  const ok = document.getElementById('reg-success');
  if (!name || !email || !pass) { err.textContent = 'נא למלא את כל השדות'; return; }
  if (pass.length < 6) { err.textContent = 'סיסמה חייבת להיות לפחות 6 תווים'; return; }
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) { err.textContent = 'כתובת מייל לא תקינה'; return; }
  const users = getUsers();
  if (users[email]) { err.textContent = 'מייל זה כבר רשום'; return; }
  users[email] = { name, pass: btoa(pass) };
  saveUsers(users);
  err.textContent = '';
  ok.style.display = 'block';
  saveSession({ email, name });
  setTimeout(() => showSite(email, name), 1200);
}
 
function showSite(email, name) {
  document.getElementById('auth-overlay').style.display = 'none';
  if (email === ADMIN_EMAIL) { showAdmin(); }
  else {
    document.getElementById('main-site').style.display = 'block';
    document.getElementById('nav-username').textContent = name;
  }
}
 
function showAdmin() {
  document.getElementById('admin-panel').style.display = 'block';
  renderOrders();
}
 
function renderOrders() {
  const orders = getOrders();
  const list = document.getElementById('orders-list');
  const count = document.getElementById('orders-count');
  count.textContent = orders.length === 0 ? 'אין הזמנות עדיין' : 'סה"כ ' + orders.length + ' הזמנות';
  if (orders.length === 0) { list.innerHTML = '<div class="no-orders">אין הזמנות עדיין 🎉</div>'; return; }
  list.innerHTML = orders.slice().reverse().map((o, ri) => {
    const i = orders.length - 1 - ri;
    return '<div class="order-card"><div class="order-top"><div class="order-name">' + o.name + ' <span style="color:var(--gray);font-weight:300;font-size:0.82rem">' + o.email + '</span></div><div class="order-date">' + o.date + '</div></div><div class="order-type">' + o.type + '</div><div class="order-desc">' + o.desc + '</div><div class="order-contact">יצירת קשר: ' + o.contact + '</div><button class="delete-order" onclick="deleteOrder(' + i + ')">מחק הזמנה</button></div>';
  }).join('');
}
 
function deleteOrder(i) {
  const orders = getOrders(); orders.splice(i, 1); saveOrders(orders); renderOrders();
}
 
function adminLogout() {
  clearSession();
  document.getElementById('admin-panel').style.display = 'none';
  document.getElementById('auth-overlay').style.display = 'flex';
}
 
function signOut() {
  clearSession();
  document.getElementById('main-site').style.display = 'none';
  document.getElementById('auth-overlay').style.display = 'flex';
}
 
function openModal(type) {
  document.getElementById('order-modal').classList.add('open');
  document.getElementById('modal-ok').style.display = 'none';
  if (type) document.getElementById('order-type').value = type;
}
function closeModal() {
  document.getElementById('order-modal').classList.remove('open');
  document.getElementById('order-desc').value = '';
  document.getElementById('order-contact').value = '';
  document.getElementById('modal-ok').style.display = 'none';
}
 
function submitOrder() {
  const type = document.getElementById('order-type').value;
  const desc = document.getElementById('order-desc').value.trim();
  const contact = document.getElementById('order-contact').value.trim();
  if (!desc || !contact) { alert('נא למלא את כל השדות'); return; }
  const session = getSession();
  const orders = getOrders();
  orders.push({ name: session.name, email: session.email, type, desc, contact,
    date: new Date().toLocaleDateString('he-IL', { day:'2-digit', month:'2-digit', year:'numeric', hour:'2-digit', minute:'2-digit' }) });
  saveOrders(orders);
  document.getElementById('modal-ok').style.display = 'block';
  setTimeout(closeModal, 2000);
}
 
(function() {
  const s = getSession();
  if (s && s.email) {
    const users = getUsers();
    if (users[s.email] || s.email === ADMIN_EMAIL) showSite(s.email, s.name);
  }
})();
</script>
</body>
</html>
