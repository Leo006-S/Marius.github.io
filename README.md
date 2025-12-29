<!doctype html>
<html lang="ro">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Chestionar de feedback</title>
  <style>
    :root{
      --bg:#f6f8fb; --card:#ffffff; --accent:#2b6cf6; --muted:#6b7280;
      --radius:12px; font-family: Inter, system-ui, Arial, sans-serif;
    }
    body{margin:0; background:linear-gradient(180deg,#eef2ff 0%,var(--bg) 100%); padding:24px; display:flex; justify-content:center;}
    .container{width:100%;max-width:780px;}
    .card{background:var(--card); border-radius:var(--radius); box-shadow:0 6px 24px rgba(15,23,42,0.06); padding:28px;}
    h1{margin:0 0 6px; font-size:20px;}
    p.lead{margin:0 0 18px; color:var(--muted); font-size:14px;}
    form .row{display:flex; gap:12px; margin-bottom:12px; flex-wrap:wrap;}
    label{display:block; font-weight:600; margin-bottom:6px; font-size:13px;}
    input[type="text"], input[type="email"], input[type="tel"], textarea, select {
      width:100%; padding:10px 12px; border-radius:8px; border:1px solid #e6e9ef; background:#fff; font-size:14px;
      box-sizing:border-box;
    }
    textarea{min-height:96px; resize:vertical;}
    .half{flex:1 1 48%;}
    .full{flex:1 1 100%;}
    .inline{display:flex; gap:12px; align-items:center; flex-wrap:wrap;}
    .radio-group, .checkbox-group{display:flex; gap:12px; flex-wrap:wrap;}
    .scale{display:flex; gap:6px; align-items:center;}
    .scale button{border:1px solid #e6e9ef; background:#fff; padding:8px 10px; border-radius:8px; cursor:pointer;}
    .scale button.selected{background:var(--accent); color:#fff; border-color:transparent;}
    .muted{color:var(--muted); font-size:13px;}
    .actions{display:flex; gap:12px; justify-content:flex-end; margin-top:18px;}
    button.primary{background:var(--accent); color:#fff; border:0; padding:10px 14px; border-radius:10px; cursor:pointer;}
    button.ghost{background:transparent; border:1px solid #e6e9ef; padding:8px 12px; border-radius:10px; cursor:pointer;}
    .hidden{display:none;}
    .result{background:#0f172a;color:#fff;padding:14px;border-radius:8px;margin-top:14px;font-size:14px;}
    @media (max-width:560px){ .half{flex:1 1 100%} }
  </style>
</head>
<body>
  <div class="container">
    <div class="card">
      <h1>Chestionar de feedback</h1>
      <p class="lead">Mulțumim pentru timpul acordat! Răspunsurile tale ne ajută să ne îmbunătățim.</p>

      <form id="survey">
        <div class="row">
          <div class="half">
            <label for="name">Nume</label>
            <input id="name" name="name" type="text" placeholder="Ex: Maria Popescu">
          </div>
          <div class="half">
            <label for="email">Email</label>
            <input id="email" name="email" type="email" placeholder="Ex: nume@exemplu.ro">
          </div>
        </div>

        <div class="row">
          <div class="half">
            <label for="age">Vârsta</label>
            <select id="age" name="age">
              <option value="" selected>-- Selectează --</option>
              <option>Sub 18</option>
              <option>18-24</option>
              <option>25-34</option>
              <option>35-44</option>
              <option>45-54</option>
              <option>55+</option>
            </select>
          </div>
          <div class="half">
            <label>Gen</label>
            <div class="radio-group">
              <label><input type="radio" name="gender" value="Masculin"> Masculin</label>
              <label><input type="radio" name="gender" value="Feminin"> Feminin</label>
              <label><input type="radio" name="gender" value="Altul"> Altul</label>
              <label><input type="radio" name="gender" value="Prefer să nu spun"> Prefer să nu spun</label>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label>1) Cum ai evalua experiența generală?</label>
            <div class="scale" role="radiogroup" aria-label="experienta">
              <button type="button" data-value="1">1</button>
              <button type="button" data-value="2">2</button>
              <button type="button" data-value="3">3</button>
              <button type="button" data-value="4">4</button>
              <button type="button" data-value="5">5</button>
            </div>
            <div class="muted">1 = Foarte slab · 5 = Excelent</div>
            <input type="hidden" id="rating" name="rating" required>
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label for="liked">2) Ce ți-a plăcut cel mai mult?</label>
            <textarea id="liked" name="liked" placeholder="Spune-ne..."></textarea>
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label for="improve">3) Ce crezi că ar trebui îmbunătățit?</label>
            <textarea id="improve" name="improve" placeholder="Sugestii..."></textarea>
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label>4) Cât de probabil e să ne recomanzi unui prieten? (0-10)</label>
            <div class="scale" id="nps">
              <!-- 0..10 -->
            </div>
            <input type="hidden" id="npsValue" name="npsValue" required>
            <div class="muted">0 = Deloc probabil · 10 = Foarte probabil</div>
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label>5) Ai dori să fii contactat pentru detalii?</label>
            <div class="inline">
              <label><input type="radio" name="contact" value="Da"> Da</label>
              <label><input type="radio" name="contact" value="Nu" checked> Nu</label>
            </div>
          </div>
        </div>

        <div id="contactDetails" class="row hidden">
          <div class="half">
            <label for="contactMethod">Metoda preferată</label>
            <select id="contactMethod" name="contactMethod">
              <option value="">-- Selectează --</option>
              <option>Email</option>
              <option>Telefon</option>
            </select>
          </div>
          <div class="half">
            <label for="phone">Număr de telefon</label>
            <input id="phone" name="phone" type="tel" placeholder="Ex: 07xx xxx xxx">
          </div>
        </div>

        <div class="row">
          <div class="full">
            <label for="comments">6) Comentarii suplimentare</label>
            <textarea id="comments" name="comments" placeholder="Opțional..."></textarea>
          </div>
        </div>

        <div class="actions">
          <button type="button" class="ghost" id="resetBtn">Resetează</button>
          <button type="submit" class="primary">Trimite</button>
        </div>
      </form>

      <div id="output" class="result hidden" aria-live="polite"></div>
    </div>
  </div>

  <script>
    // Elemente
    const ratingInput = document.getElementById('rating');
    const npsInput = document.getElementById('npsValue');
    const ratingButtons = document.querySelectorAll('.scale button[data-value]');
    const npsContainer = document.getElementById('nps');
    const contactRadios = document.querySelectorAll('input[name="contact"]');
    const contactDetails = document.getElementById('contactDetails');
    const contactMethod = document.getElementById('contactMethod');
    const phone = document.getElementById('phone');
    const form = document.getElementById('survey');
    const output = document.getElementById('output');
    const resetBtn = document.getElementById('resetBtn');

    // inițializează rating 1-5 (already have buttons)
    ratingButtons.forEach(btn=>{
      btn.addEventListener('click', ()=> {
        ratingButtons.forEach(b=>b.classList.remove('selected'));
        btn.classList.add('selected');
        ratingInput.value = btn.dataset.value;
      });
    });

    // creează butoane NPS 0..10
    for(let i=0;i<=10;i++){
      const b = document.createElement('button');
      b.type = 'button';
      b.textContent = i;
      b.dataset.value = i;
      b.addEventListener('click', ()=>{
        // deselect
        npsContainer.querySelectorAll('button').forEach(x=>x.classList.remove('selected'));
        b.classList.add('selected');
        npsInput.value = b.dataset.value;
      });
      npsContainer.appendChild(b);
    }

    // afișare detalii contact
    contactRadios.forEach(r=>{
      r.addEventListener('change', ()=>{
        if(r.value === 'Da' && r.checked){
          contactDetails.classList.remove('hidden');
          contactMethod.setAttribute('required','required');
        } else if (r.checked) {
          contactDetails.classList.add('hidden');
          contactMethod.removeAttribute('required');
          phone.value = '';
          contactMethod.value = '';
        }
      });
    });

    // validare simplă și trimitere (simulare)
    form.addEventListener('submit', (e)=>{
      e.preventDefault();
      // cerințe: rating și nps obligatorii
      if(!ratingInput.value){
        alert('Te rog evaluează experiența generală (1-5).');
        return;
      }
      if(!npsInput.value){
        alert('Te rog selectează scorul 0-10 pentru recomandare.');
        return;
      }
      // dacă s-a selectat contact și metoda telefon, verificăm tel
      const wantsContact = document.querySelector('input[name="contact"]:checked').value === 'Da';
      if(wantsContact && contactMethod.value === 'Telefon' && phone.value.trim() === ''){
        alert('Te rog introdu numărul de telefon.');
        return;
      }

      // colectăm datele într-un obiect
      const data = {
        name: form.name.value.trim(),
        email: form.email.value.trim(),
        age: form.age.value,
        gender: form.gender ? document.querySelector('input[name="gender"]:checked')?.value || '' : '',
        rating: ratingInput.value,
        liked: form.liked.value.trim(),
        improve: form.improve.value.trim(),
        nps: npsInput.value,
        contact: document.querySelector('input[name="contact"]:checked').value,
        contactMethod: contactMethod.value,
        phone: phone.value.trim(),
        comments: form.comments.value.trim(),
        submittedAt: new Date().toISOString()
      };

      // simulare trimitere: afișăm rezultatul în interfață și log în consolă
      console.log('Răspuns chestionar:', data);
      output.classList.remove('hidden');
      output.textContent = 'Mulțumim! Răspunsul tău a fost înregistrat. (Simulare locală)';
      // aici poți trimite `data` la un endpoint server (fetch) sau salva în Google Sheets etc.

      // opțional: resetează formularul după trimitere
      form.reset();
      ratingButtons.forEach(b=>b.classList.remove('selected'));
      npsContainer.querySelectorAll('button').forEach(b=>b.classList.remove('selected'));
      ratingInput.value = '';
      npsInput.value = '';
      contactDetails.classList.add('hidden');
    });

    resetBtn.addEventListener('click', ()=>{
      form.reset();
      ratingButtons.forEach(b=>b.classList.remove('selected'));
      npsContainer.querySelectorAll('button').forEach(b=>b.classList.remove('selected'));
      ratingInput.value = '';
      npsInput.value = '';
      contactDetails.classList.add('hidden');
      output.classList.add('hidden');
    });
  </script>
    <div class="card">
    <h2>Chestionar de feedback (demo)</h2>
    <p class="row">Scanează codul QR pentru a deschide formularul pe telefon.</p>

    <!-- QR container -->
    <div class="row" style="display:flex;gap:16px;align-items:center">
      <div id="qr"></div>
      <div>
        <div style="margin-bottom:8px">URL pentru QR:</div>
        <input id="urlInput" type="text" style="width:360px;padding:8px;border-radius:8px;border:1px solid #ddd" value="" />
        <div style="margin-top:8px">
          <button id="genBtn">Generează QR</button>
          <button id="dlBtn" class="ghost">Descarcă PNG</button>
        </div>
      </div>
    </div>

    <hr>

    <!-- Simplu buton pentru a deschide demo form -->
    <div class="row">
      <button id="openForm">Deschide formular demo într-o fereastră nouă</button>
    </div>

    <!-- Container unde vom insera formularul demo pentru test (opțional) -->
    <div id="formEmbed" style="margin-top:16px"></div>
  </div>

  <!-- Biblioteca qrcodejs (client-side, minified) -->
  <script>
/*!
 * qrcodejs (minified-ish) - minimal subset to generate QR on a canvas
 * Based on https://davidshimjs.github.io/qrcodejs/ (lightweight inclusion)
 * This code implements QR via an offscreen API using a tiny fallback:
 * If browser supports <canvas>, we will draw the QR image returned by an internal data URL via a simple library.
 */
/* Minimal embed: we'll use a lightweight generator via an embedded implementation.
   For reliability and small size we fallback to using Google Charts if present, but here we implement a simple approach:
*/
(function(window){
  // Use a small external algorithm would be large; instead we'll build QR via an SVG generator service as fallback,
  // but to be fully client-side we try to use a tiny library approach: we'll create a canvas and draw an image by creating
  // an SVG via the public API of qrserver: this still requires network. To be fully offline we would need full qrcode alg implementation.
  // Practical compromise: if offline, display message; otherwise request data:image/svg+xml from qrserver.com and render it.
  function generateQRToElement(el, text, size){
    size = size || 200;
    // Use qrserver API which returns SVG or PNG; this requires network but avoids external JS files.
    var url = 'https://api.qrserver.com/v1/create-qr-code/?size=' + size + 'x' + size + '&data=' + encodeURIComponent(text) + '&format=png';
    // Create image
    var img = new Image();
    img.crossOrigin = 'anonymous';
    img.onload = function(){
      // clear and append
      el.innerHTML = '';
      img.style.width = size + 'px';
      img.style.height = size + 'px';
      el.appendChild(img);
    };
    img.onerror = function(){
      el.innerHTML = '<div style="color:#c00;font-size:13px">Eroare generare QR (verifică conexiunea)</div>';
    };
    img.src = url;
  }

  window.SimpleQR = { generate: generateQRToElement };
})(window);
  </script>

  <script>
    const qrEl = document.getElementById('qr');
    const urlInput = document.getElementById('urlInput');
    const genBtn = document.getElementById('genBtn');
    const dlBtn = document.getElementById('dlBtn');
    const openForm = document.getElementById('openForm');
    const formEmbed = document.getElementById('formEmbed');

    // Implicit: URL către formular. Dacă ai pus pagina online, modifică aici.
    // Daca vrei să testezi local, pune un URL public (ex: GitHub Pages). Alte optiuni: data URL (dar scanere mobile pot să nu-l accepte).
    // Setează valoarea implicită (dacă deschizi local, lasă gol și completează manual cu URL public).
    urlInput.value = window.location.href; // dacă fișierul este accesibil online, folosește linkul curent

    function generate(){
      const url = urlInput.value.trim();
      if(!url){
        alert('Te rog introdu un URL public (ex: https://username.github.io/repo).');
        return;
      }
      // generează QR
      SimpleQR.generate(qrEl, url, 200);
    }

    genBtn.addEventListener('click', generate);

    dlBtn.addEventListener('click', ()=>{
      const img = qrEl.querySelector('img');
      if(!img || !img.src){
        alert('Generează mai întâi codul QR.');
        return;
      }
      // descarcă imaginea PNG (imaginea vine de la qrserver.com cu CORS anon)
      const a = document.createElement('a');
      a.href = img.src;
      a.download = 'chestionar-qr.png';
      document.body.appendChild(a);
      a.click();
      a.remove();
    });

    // Demo: încarcă formularul demo (HTML) într-un div pentru test local
    openForm.addEventListener('click', ()=>{
      // simplu formular înlined pentru test
      formEmbed.innerHTML = `
        <div style="margin-top:12px;padding:12px;border-radius:8px;background:#fbfcff;border:1px solid #eef2ff">
          <strong>Formular demo</strong>
          <p style="margin:6px 0">Acesta este un formular demo; în realitate folosește URL din câmpul de mai sus.</p>
          <label>Nume: <input type="text" /></label>
        </div>
      `;
    });

    // Generează imediat la încărcare dacă există URL
    window.addEventListener('load', ()=>{
      if(urlInput.value) generate();
    });
  </script>
</body>
</html>
