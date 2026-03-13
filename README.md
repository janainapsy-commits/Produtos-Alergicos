<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#f8f6f2">
<title>AlérgiCheck</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&family=DM+Serif+Display&display=swap" rel="stylesheet">
<style>
  :root{--bg:#f8f6f2;--surface:#fff;--surface2:#f1ede6;--text:#1a1714;--text2:#6b6560;--text3:#a09a94;--border:rgba(26,23,20,0.1);--border2:rgba(26,23,20,0.18);--danger-bg:#fff2f2;--danger-text:#c0392b;--danger-border:#f5c0bb;--safe-bg:#f0faf4;--safe-text:#1e7e45;--safe-border:#b3e8c5;--warn-bg:#fffbf0;--warn-text:#b07d10;--warn-border:#f5dfa0;--info-bg:#f0f5ff;--info-text:#2c5fb3;--info-border:#b8ccf5;--accent:#c17f4a;--radius:14px;--radius-sm:8px}
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
  body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;padding-bottom:68px}
  header{background:var(--surface);border-bottom:0.5px solid var(--border);padding:16px 20px 12px;position:sticky;top:0;z-index:10}
  .hrow{max-width:520px;margin:0 auto;display:flex;align-items:center;gap:10px}
  .logo-icon{width:30px;height:30px;border-radius:8px;background:var(--accent);display:flex;align-items:center;justify-content:center;flex-shrink:0}
  .logo-icon svg{width:16px;height:16px;fill:white}
  .logo-title{font-family:'DM Serif Display',serif;font-size:18px;font-weight:400;color:var(--text)}
  .bottom-nav{position:fixed;bottom:0;left:0;right:0;background:var(--surface);border-top:0.5px solid var(--border);display:flex;z-index:20}
  .nav-btn{flex:1;padding:9px 4px 11px;background:none;border:none;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:3px;font-family:'DM Sans',sans-serif;font-size:10px;color:var(--text3);transition:color 0.15s}
  .nav-btn.active{color:var(--accent)}
  .nav-btn svg{width:21px;height:21px;fill:none;stroke:currentColor;stroke-width:1.6;stroke-linecap:round;stroke-linejoin:round}
  .page{display:none;max-width:520px;margin:0 auto;padding:16px 16px 0}
  .page.active{display:block}
  .card{background:var(--surface);border:0.5px solid var(--border);border-radius:var(--radius);padding:18px;margin-bottom:14px}
  .card-title{font-size:11px;font-weight:500;letter-spacing:0.08em;text-transform:uppercase;color:var(--text3);margin-bottom:12px}
  .field{margin-bottom:12px}
  .field label{display:block;font-size:12px;font-weight:500;color:var(--text2);margin-bottom:5px}
  .field input,.field textarea{width:100%;padding:11px 13px;border:0.5px solid var(--border2);border-radius:var(--radius-sm);font-size:15px;font-family:'DM Sans',sans-serif;color:var(--text);background:var(--bg);outline:none;transition:border-color 0.15s;-webkit-appearance:none}
  .field input:focus,.field textarea:focus{border-color:var(--accent);background:var(--surface)}
  .field textarea{resize:none;height:100px;line-height:1.5}
  .field-hint{font-size:11px;color:var(--text3);margin-top:4px;line-height:1.5}
  .field-hint a{color:var(--info-text)}
  .row2{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .divider{border:none;border-top:0.5px solid var(--border);margin:14px 0}
  .btn{width:100%;padding:12px;border-radius:var(--radius-sm);font-size:14px;font-weight:500;font-family:'DM Sans',sans-serif;cursor:pointer;transition:all 0.15s;border:0.5px solid var(--border2);background:var(--surface);color:var(--text)}
  .btn:active{transform:scale(0.98)}
  .btn-accent{background:var(--accent);color:white;border-color:var(--accent);margin-top:6px}
  .btn-outline{border-color:var(--accent);color:var(--accent)}
  .result{border-radius:var(--radius);padding:16px 18px;margin-bottom:14px;border:0.5px solid;animation:fadeIn 0.25s ease}
  @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
  .result-danger{background:var(--danger-bg);border-color:var(--danger-border)}
  .result-safe{background:var(--safe-bg);border-color:var(--safe-border)}
  .result-warn{background:var(--warn-bg);border-color:var(--warn-border)}
  .rh{display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
  .dot{width:9px;height:9px;border-radius:50%;flex-shrink:0;margin-top:5px}
  .dot-danger{background:var(--danger-text)}.dot-safe{background:var(--safe-text)}.dot-warn{background:var(--warn-text)}
  .rt{font-size:14px;font-weight:500;line-height:1.4}
  .rt.danger{color:var(--danger-text)}.rt.safe{color:var(--safe-text)}.rt.warn{color:var(--warn-text)}
  .rb{font-size:13px;color:var(--text2);line-height:1.6}
  .rn{font-size:11px;color:var(--text3);margin-top:8px;line-height:1.5}
  .alist{list-style:none;margin-top:10px;display:flex;flex-direction:column;gap:7px}
  .aitem{background:var(--surface);border-radius:var(--radius-sm);border:0.5px solid var(--border);padding:9px 12px}
  .aname{font-size:13px;font-weight:500;color:var(--danger-text)}
  .afound{font-size:11px;color:var(--text3);margin-top:2px}
  .hitem{background:var(--surface);border:0.5px solid var(--border);border-radius:var(--radius);padding:14px 16px;margin-bottom:10px;cursor:pointer}
  .hitem-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:4px}
  .hitem-name{font-size:14px;font-weight:500}
  .hitem-date{font-size:11px;color:var(--text3)}
  .badge{font-size:11px;padding:2px 9px;border-radius:20px;font-weight:500}
  .badge-safe{background:var(--safe-bg);color:var(--safe-text);border:0.5px solid var(--safe-border)}
  .badge-danger{background:var(--danger-bg);color:var(--danger-text);border:0.5px solid var(--danger-border)}
  .empty{text-align:center;padding:40px 20px;color:var(--text3);font-size:14px}
  .atags{display:flex;flex-wrap:wrap;gap:6px}
  .atag{font-size:12px;padding:4px 11px;background:var(--surface);border:0.5px solid var(--border2);border-radius:20px;color:var(--text2);display:flex;align-items:center;gap:5px}
  .atag-x{background:none;border:none;cursor:pointer;color:var(--text3);font-size:15px;line-height:1;padding:0}
  .atag-x:hover{color:var(--danger-text)}
  .asection{background:var(--surface2);border-radius:var(--radius);padding:16px 18px;margin-bottom:14px}
  .asection h3{font-size:11px;font-weight:500;letter-spacing:0.08em;text-transform:uppercase;color:var(--text3);margin-bottom:10px}
  /* WELCOME */
  .welcome{position:fixed;inset:0;background:var(--bg);z-index:100;overflow-y:auto;padding:32px 20px 60px;display:flex;flex-direction:column;align-items:center}
  .welcome-logo{width:52px;height:52px;border-radius:13px;background:var(--accent);display:flex;align-items:center;justify-content:center;margin-bottom:18px;margin-top:20px}
  .welcome-logo svg{width:26px;height:26px;fill:white}
  .welcome h2{font-family:'DM Serif Display',serif;font-size:24px;font-weight:400;color:var(--text);margin-bottom:8px;text-align:center}
  .welcome-sub{font-size:14px;color:var(--text2);text-align:center;line-height:1.7;margin-bottom:24px;max-width:340px}
  .welcome-card{background:var(--surface);border:0.5px solid var(--border);border-radius:var(--radius);padding:18px;width:100%;max-width:420px;margin-bottom:12px}
  .welcome-card h3{font-size:13px;font-weight:500;color:var(--text);margin-bottom:12px}
  .welcome-card p{font-size:12px;color:var(--text2);line-height:1.7;margin-bottom:10px}
  .tip{font-size:12px;color:var(--text3);display:flex;align-items:flex-start;gap:8px;margin-bottom:6px;line-height:1.5}
  .tip-num{width:18px;height:18px;border-radius:50%;background:var(--surface2);display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:500;color:var(--text2);flex-shrink:0;margin-top:1px}
</style>
</head>
<body>

<!-- WELCOME -->
<div class="welcome" id="welcome-screen">
  <div style="width:100%;max-width:420px;display:flex;flex-direction:column;align-items:center;">
    <div class="welcome-logo"><svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 14.5v-9l6 4.5-6 4.5z"/></svg></div>
    <h2>Bem-vindo ao AlérgiCheck</h2>
    <p class="welcome-sub">Verifique ingredientes de cosméticos e descubra se contêm substâncias às quais você é alérgico.</p>

    <div class="welcome-card">
      <h3>Cadastre seus alérgenos para começar</h3>
      <div id="welcome-tags" style="display:flex;flex-wrap:wrap;gap:6px;margin-bottom:12px;min-height:28px;"></div>
      <div style="display:flex;gap:8px;">
        <input type="text" id="welcome-input" placeholder="Nome do alérgeno" style="flex:1;padding:10px 12px;border:0.5px solid var(--border2);border-radius:var(--radius-sm);font-size:14px;font-family:'DM Sans',sans-serif;color:var(--text);background:var(--bg);outline:none;"/>
        <button onclick="addWelcomeTag()" style="padding:10px 14px;background:var(--accent);color:white;border:none;border-radius:var(--radius-sm);font-size:13px;font-weight:500;font-family:'DM Sans',sans-serif;cursor:pointer;">+ Add</button>
      </div>
      <div class="field-hint" style="margin-top:6px;">Ex: Parabenos, Níquel, Lanolina, Formaldeído...</div>
    </div>

    <div class="welcome-card">
      <h3>Como usar o app</h3>
      <div class="tip"><div class="tip-num">1</div>Pesquise o produto em <a href="https://incibeauty.com" target="_blank" style="color:var(--info-text)">incibeauty.com</a> ou <a href="https://cosdna.com" target="_blank" style="color:var(--info-text)">cosdna.com</a></div>
      <div class="tip"><div class="tip-num">2</div>Copie a lista de ingredientes encontrada</div>
      <div class="tip"><div class="tip-num">3</div>Cole no app e clique em Verificar alérgenos</div>
      <div class="tip"><div class="tip-num">4</div>O app indica se o produto é seguro para você</div>
    </div>

    <button class="btn btn-accent" style="width:100%;max-width:420px;padding:14px;font-size:15px;margin-bottom:10px;" onclick="finishWelcome()">Começar a usar</button>
    <button onclick="finishWelcome()" style="background:none;border:none;font-size:13px;color:var(--text3);cursor:pointer;font-family:'DM Sans',sans-serif;padding:6px;">Pular por agora</button>
  </div>
</div>

<header>
  <div class="hrow">
    <div class="logo-icon"><svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 14.5v-9l6 4.5-6 4.5z"/></svg></div>
    <span class="logo-title">AlérgiCheck</span>
  </div>
</header>

<!-- VERIFICAR -->
<div class="page active" id="page-verificar">
  <div class="card">
    <div class="card-title">Produto</div>
    <div class="row2">
      <div class="field"><label>Nome do produto</label><input type="text" id="product-name" placeholder="ex: Hidratante Milk" autocomplete="off"/></div>
      <div class="field"><label>Marca</label><input type="text" id="brand-name" placeholder="ex: Dove" autocomplete="off"/></div>
    </div>
    <hr class="divider">
    <div class="field">
      <label>Ingredientes</label>
      <textarea id="ingredients" placeholder="Cole aqui a lista de ingredientes da embalagem, incibeauty.com ou cosdna.com"></textarea>
      <div class="field-hint">Encontre os ingredientes em <a href="https://incibeauty.com" target="_blank">incibeauty.com</a> ou <a href="https://cosdna.com" target="_blank">cosdna.com</a></div>
    </div>
    <button class="btn btn-accent" onclick="checkIngredients()">Verificar alérgenos</button>
  </div>
  <div id="result-area"></div>
</div>

<!-- HISTÓRICO -->
<div class="page" id="page-historico">
  <div id="history-list"></div>
</div>

<!-- ALÉRGENOS -->
<div class="page" id="page-alergenos">
  <div class="card">
    <div class="card-title">Adicionar alérgeno</div>
    <div class="field"><label>Nome</label><input type="text" id="new-name" placeholder="ex: Formaldeído" autocomplete="off"/></div>
    <div class="field">
      <label>Nomes técnicos INCI (separados por vírgula)</label>
      <input type="text" id="new-variants" placeholder="ex: formaldehyde, formalin, methanal" autocomplete="off"/>
      <div class="field-hint">Pesquise em <a href="https://incibeauty.com" target="_blank">incibeauty.com</a> para mais precisão</div>
    </div>
    <button class="btn btn-accent" onclick="addAllergen()">Adicionar</button>
  </div>
  <div id="allergens-list"></div>
</div>

<nav class="bottom-nav">
  <button class="nav-btn active" id="nav-verificar" onclick="showPage('verificar')">
    <svg viewBox="0 0 24 24"><path d="M9 11l3 3L22 4"/><path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"/></svg>Verificar
  </button>
  <button class="nav-btn" id="nav-historico" onclick="showPage('historico')">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>Histórico
  </button>
  <button class="nav-btn" id="nav-alergenos" onclick="showPage('alergenos')">
    <svg viewBox="0 0 24 24"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>Alérgenos
  </button>
</nav>

<script>
const getAllergens=()=>{try{return JSON.parse(localStorage.getItem('allergens'))||[]}catch{return[]}};
const saveAllergens=a=>localStorage.setItem('allergens',JSON.stringify(a));
const getHistory=()=>{try{return JSON.parse(localStorage.getItem('history'))||[]}catch{return[]}};
const saveHistory=h=>localStorage.setItem('history',JSON.stringify(h));
const isFirstTime=()=>!localStorage.getItem('welcomed');

let welcomeTags=[];

function warn(t,m){return`<div class="result result-warn"><div class="rh"><div class="dot dot-warn"></div><div class="rt warn">${t}</div></div><p class="rb">${m}</p></div>`}

// WELCOME
function addWelcomeTag(){
  const input=document.getElementById('welcome-input');
  const name=input.value.trim();
  if(!name)return;
  welcomeTags.push({name,variants:[name.toLowerCase()]});
  input.value='';input.focus();
  renderWelcomeTags();
}

document.addEventListener('DOMContentLoaded',()=>{
  document.getElementById('welcome-input').addEventListener('keydown',e=>{if(e.key==='Enter')addWelcomeTag();});
  renderWelcomeTags();
  if(!isFirstTime())document.getElementById('welcome-screen').style.display='none';
});

function renderWelcomeTags(){
  const el=document.getElementById('welcome-tags');
  if(!welcomeTags.length){el.innerHTML='<span style="font-size:12px;color:var(--text3)">Nenhum adicionado ainda</span>';return;}
  el.innerHTML=welcomeTags.map((a,i)=>`<span class="atag">${a.name}<button class="atag-x" onclick="welcomeTags.splice(${i},1);renderWelcomeTags()">×</button></span>`).join('');
}

function finishWelcome(){
  if(welcomeTags.length>0)saveAllergens(welcomeTags);
  localStorage.setItem('welcomed','1');
  document.getElementById('welcome-screen').style.display='none';
}

function showPage(name){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+name).classList.add('active');
  document.getElementById('nav-'+name).classList.add('active');
  if(name==='historico')renderHistory();
  if(name==='alergenos')renderAllergens();
}

// VERIFICAR
function checkIngredients(){
  const productName=document.getElementById('product-name').value.trim();
  const brand=document.getElementById('brand-name').value.trim();
  const ingredients=document.getElementById('ingredients').value.trim();
  const resultArea=document.getElementById('result-area');
  if(!ingredients){resultArea.innerHTML=warn('Ingredientes não informados','Cole a lista de ingredientes do produto no campo acima.');return;}
  const allergens=getAllergens();
  if(!allergens.length){resultArea.innerHTML=warn('Nenhum alérgeno cadastrado','Vá para a aba Alérgenos e cadastre seus alérgenos primeiro.');return;}
  const low=ingredients.toLowerCase();const found=[];
  for(const al of allergens){
    const matches=[];
    for(const v of al.variants){
      if(low.includes(v.toLowerCase())){
        const m=ingredients.match(new RegExp(v.replace(/[.*+?^${}()|[\]\\]/g,'\\$&'),'gi'));
        if(m)matches.push(m[0]);
      }
    }
    if(matches.length>0)found.push({allergen:al.name,found:[...new Set(matches)]});
  }
  const label=[brand,productName].filter(Boolean).join(' — ')||'Produto analisado';
  const safe=found.length===0;
  const history=getHistory();
  history.unshift({id:Date.now(),product:productName,brand,ingredients,found,safe,date:new Date().toLocaleDateString('pt-BR')});
  saveHistory(history.slice(0,50));
  if(safe){
    resultArea.innerHTML=`<div class="result result-safe"><div class="rh"><div class="dot dot-safe"></div><div class="rt safe">${label}</div></div><p class="rb">Nenhum alérgeno identificado. O produto parece seguro para você.</p><p class="rn">Sempre confirme no rótulo original e consulte seu dermatologista.</p></div>`;
  }else{
    resultArea.innerHTML=`<div class="result result-danger"><div class="rh"><div class="dot dot-danger"></div><div class="rt danger">${label} — ${found.length} alérgeno${found.length>1?'s':''} detectado${found.length>1?'s':''}</div></div><p class="rb">Este produto contém ingredientes que podem causar reação. Evite e consulte seu dermatologista.</p><ul class="alist">${found.map(f=>`<li class="aitem"><div class="aname">${f.allergen}</div><div class="afound">Encontrado como: ${f.found.join(', ')}</div></li>`).join('')}</ul></div>`;
  }
  resultArea.scrollIntoView({behavior:'smooth',block:'nearest'});
}

// HISTÓRICO
function renderHistory(){
  const history=getHistory();const el=document.getElementById('history-list');
  if(!history.length){el.innerHTML=`<div class="empty">Nenhum produto verificado ainda.</div>`;return;}
  el.innerHTML=history.map(item=>`<div class="hitem" onclick="loadHistory(${item.id})"><div class="hitem-top"><span class="hitem-name">${[item.brand,item.product].filter(Boolean).join(' — ')||'Sem nome'}</span><span class="hitem-date">${item.date}</span></div>${item.safe?'<span class="badge badge-safe">✓ Seguro</span>':`<span class="badge badge-danger">⚠ ${item.found.length} alérgeno${item.found.length>1?'s':''}</span>`}</div>`).join('');
}

function loadHistory(id){
  const item=getHistory().find(h=>h.id===id);if(!item)return;
  document.getElementById('product-name').value=item.product||'';
  document.getElementById('brand-name').value=item.brand||'';
  document.getElementById('ingredients').value=item.ingredients||'';
  showPage('verificar');setTimeout(()=>checkIngredients(),100);
}

// ALÉRGENOS
function renderAllergens(){
  const allergens=getAllergens();
  document.getElementById('allergens-list').innerHTML=`<div class="asection"><h3>Cadastrados (${allergens.length})</h3><div class="atags">${allergens.length?allergens.map((a,i)=>`<span class="atag">${a.name}<button class="atag-x" onclick="removeAllergen(${i})">×</button></span>`).join(''):'<span style="font-size:12px;color:var(--text3)">Nenhum cadastrado ainda</span>'}</div></div>`;
}

function addAllergen(){
  const name=document.getElementById('new-name').value.trim();
  const variantsRaw=document.getElementById('new-variants').value.trim();
  if(!name){alert('Digite o nome do alérgeno.');return;}
  const variants=variantsRaw?variantsRaw.split(',').map(v=>v.trim().toLowerCase()).filter(Boolean):[name.toLowerCase()];
  const allergens=getAllergens();allergens.push({name,variants});saveAllergens(allergens);
  document.getElementById('new-name').value='';document.getElementById('new-variants').value='';
  renderAllergens();alert(`"${name}" adicionado!`);
}

function removeAllergen(i){
  if(!confirm('Remover este alérgeno?'))return;
  const allergens=getAllergens();allergens.splice(i,1);saveAllergens(allergens);renderAllergens();
}
</script>
</body>
</html>
