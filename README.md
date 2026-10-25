<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Rintisa – Prototipe MVP</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Archivo+Black&family=Montserrat:wght@400;500;600;700&display=swap">
<style>
:root{--bg:#f3f5f8;--card:#fff;--ink:#14202e;--mut:#5a6978;--pri:#17406a;--yel:#f2b705;--line:#d9e0e8;--ok:#1b7f55;--bad:#bf3a2b;--soft:#e8f0f8;--onyel:#1a1a1a;color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0d1620;--card:#15222f;--ink:#e8eef5;--mut:#9db0c3;--pri:#3274b4;--line:#27394a;--ok:#4cc58f;--bad:#ef7b6c;--soft:#1b2f43;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#0d1620;--card:#15222f;--ink:#e8eef5;--mut:#9db0c3;--pri:#3274b4;--line:#27394a;--ok:#4cc58f;--bad:#ef7b6c;--soft:#1b2f43;color-scheme:dark}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:500 15px/1.55 Montserrat,system-ui,sans-serif}
header{background:#17406a;color:#fff;border-bottom:4px solid var(--yel);padding:10px 16px;display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between}
header::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);background:#17406a;z-index:10}
.logo{font:400 22px 'Archivo Black',Impact,sans-serif;letter-spacing:.5px}.logo i{color:var(--yel);font-style:normal}
.seg{display:flex;background:rgba(255,255,255,.14);border-radius:8px;padding:3px}
.seg button{border:0;background:none;color:#fff;font:600 13px Montserrat,sans-serif;padding:7px 12px;border-radius:6px;cursor:pointer}
.seg button.on{background:var(--yel);color:var(--onyel)}
.rs{border:1px solid rgba(255,255,255,.4);background:none;color:#fff;border-radius:6px;font:600 12px Montserrat,sans-serif;padding:6px 10px;cursor:pointer}
main{max-width:760px;margin:0 auto;padding:18px 14px 80px}
h1,h2{font-family:'Archivo Black',Impact,sans-serif;font-weight:400;color:var(--pri);margin:0 0 6px;line-height:1.15}
h1{font-size:26px}h2{font-size:19px}h3{margin:0 0 6px;font-size:15px}
.card{background:var(--card);border:1px solid var(--line);border-radius:10px;padding:18px;margin-bottom:14px}
.mut{color:var(--mut);font-size:13px}
label{display:block;font-weight:600;font-size:13px;margin:12px 0 4px}
input,select,textarea{width:100%;padding:10px;border:1px solid var(--line);border-radius:8px;background:var(--bg);color:var(--ink);font:500 14px Montserrat,sans-serif}
textarea{min-height:70px;resize:vertical}
input:focus-visible,select:focus-visible,textarea:focus-visible,button:focus-visible{outline:3px solid var(--yel);outline-offset:1px}
.btn{background:var(--pri);color:#fff;border:0;border-radius:8px;padding:11px 16px;font:700 14px Montserrat,sans-serif;cursor:pointer;margin-top:14px}
.btn.y{background:var(--yel);color:var(--onyel)}.btn.o{background:none;color:var(--pri);border:1.5px solid var(--pri)}.btn.r{background:none;color:var(--bad);border:1.5px solid var(--bad)}
.btn:disabled{opacity:.45;cursor:not-allowed}.row{display:flex;gap:8px;flex-wrap:wrap}
.chips{display:flex;flex-wrap:wrap;gap:6px}.chip{border:1.5px solid var(--line);background:var(--card);color:var(--ink);border-radius:99px;padding:6px 12px;font:600 12.5px Montserrat,sans-serif;cursor:pointer}
.chip.on{background:var(--pri);color:#fff;border-color:var(--pri)}
.mvp{display:inline-block;background:var(--yel);color:var(--onyel);font:700 11px Montserrat,sans-serif;padding:2px 8px;border-radius:4px;margin-left:8px;vertical-align:middle}
.steps{display:flex;gap:6px;margin-bottom:14px}.steps span{flex:1;height:5px;border-radius:3px;background:var(--line)}.steps span.on{background:var(--yel)}
.bar{height:12px;background:var(--soft);border-radius:6px;overflow:hidden}.bar b{display:block;height:100%;background:var(--pri)}.bar.t b{background:var(--yel)}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}.grid>div{background:var(--soft);border-radius:8px;padding:10px}
.grid small{display:block;color:var(--mut);font-size:11.5px}.grid strong{font-size:14px}
.pill{display:inline-block;border-radius:99px;padding:3px 10px;font:700 12px Montserrat,sans-serif;background:var(--soft);color:var(--pri)}
.pill.ok{background:var(--ok);color:#fff}.pill.bad{background:var(--bad);color:#fff}
.chat{max-height:240px;overflow:auto;display:flex;flex-direction:column;gap:6px;margin-bottom:8px}
.m{max-width:80%;padding:8px 12px;border-radius:12px;background:var(--soft);font-size:14px}.m.me{align-self:flex-end;background:var(--pri);color:#fff}.m.sys{align-self:center;background:none;color:var(--mut);font-size:12.5px;text-align:center;max-width:100%}
.log{display:flex;gap:10px;padding:10px 0;border-top:1px solid var(--line)}.log img{width:64px;height:64px;object-fit:cover;border-radius:8px}
.ph{width:64px;height:64px;border-radius:8px;background:var(--soft);display:grid;place-items:center;font-size:11px;color:var(--mut)}
.dots{display:flex;gap:6px;margin:6px 0}.dots i{width:22px;height:22px;border-radius:50%;border:2px solid var(--pri)}.dots i.u{background:var(--pri)}
.note{border-left:4px solid var(--yel);background:var(--soft);padding:10px 12px;border-radius:0 8px 8px 0;font-size:13.5px;margin:10px 0}
.modal{position:fixed;inset:0;background:rgba(5,12,20,.6);display:grid;place-items:center;padding:16px;z-index:20}
.modal .card{max-width:420px;width:100%;border-top:6px solid var(--yel);margin:0}
.pct{font:400 44px 'Archivo Black',Impact,sans-serif;color:var(--pri);line-height:1}
.toast{position:fixed;left:50%;bottom:calc(20px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--ink);color:var(--bg);padding:10px 16px;border-radius:8px;font-size:13.5px;z-index:30;max-width:90%}
table{width:100%;border-collapse:collapse;font-size:14px}td{padding:6px 0;border-bottom:1px solid var(--line)}td:last-child{text-align:right;font-weight:700}
@media(max-width:520px){.grid{grid-template-columns:1fr}}
:root{--sh:0 1px 2px rgba(10,25,45,.06),0 10px 28px rgba(10,25,45,.08)}
header{position:sticky;top:env(safe-area-inset-top,0px);z-index:15;padding:12px 20px;border-bottom:0;box-shadow:0 4px 0 var(--yel)}
.logo{padding-left:12px;border-left:7px solid var(--yel);font-size:24px}
.seg{padding:4px;border-radius:999px}.seg button{border-radius:999px;padding:8px 18px}
main{max-width:820px;padding:28px 16px 90px}
h1{font-size:clamp(28px,6vw,42px)}h2{font-size:21px}
.card{border-radius:16px;padding:22px;box-shadow:var(--sh)}
.card:has(.mvp){border-left:6px solid var(--yel)}
.mvp{border-radius:999px;padding:3px 10px}
input,select,textarea{border-radius:10px;border-width:1.5px;padding:12px;background:var(--card)}
input:focus,select:focus,textarea:focus{border-color:var(--pri);outline:none;box-shadow:0 0 0 4px var(--soft)}
.btn{border-radius:10px;padding:12px 22px;font-size:14.5px;transition:transform .12s,box-shadow .12s}
.btn:hover:not(:disabled){transform:translateY(-1px);box-shadow:0 6px 14px rgba(23,64,106,.28)}
.btn.y{box-shadow:0 3px 0 #b98a00}.btn.wide{width:100%}
.chip{padding:8px 15px}.chip.on::before{content:"✓ "}
.hero{display:grid;grid-template-columns:1.15fr 1fr;gap:28px;align-items:center;background:#17406a;color:#fff;border-radius:22px;padding:38px;margin-bottom:18px;position:relative;overflow:hidden}
.hero::after{content:"";position:absolute;right:-70px;bottom:-70px;width:230px;height:230px;background:var(--yel);transform:rotate(45deg)}
.hero h1{color:#fff;margin-bottom:12px}.hero p{margin:0;color:#dbe6f2}
.hl,.login{position:relative;z-index:1}.login{margin:0}
.vp{list-style:none;padding:0;margin:18px 0 0}.vp li{position:relative;padding:6px 0 6px 28px}.vp li::before{content:"✓";position:absolute;left:0;color:var(--yel);font-weight:700}
.steps{gap:10px;margin-bottom:18px}.steps span{height:auto;background:none;border-radius:0;border-top:5px solid var(--line);padding-top:6px}
.steps span.on{border-top-color:var(--yel)}.steps em{font:600 12.5px Montserrat,sans-serif;font-style:normal;color:var(--mut)}.steps span.on em{color:var(--ink)}
.grid>div{border-radius:12px;padding:14px}.grid strong{display:block;margin-top:2px;font:400 19px 'Archivo Black',Impact,sans-serif;color:var(--pri)}
.grid>div:first-child{background:var(--pri)}.grid>div:first-child small,.grid>div:first-child strong{color:#fff}
.grid>div:first-child small::before{content:"🔒 "}
.bar{height:14px;border-radius:99px}.bar b{border-radius:99px}
.chat{max-height:300px;padding:4px}.m{padding:10px 14px;border-radius:16px 16px 16px 4px}.m.me{border-radius:16px 16px 4px 16px}
.log{position:relative;margin-left:8px;padding:12px 0 12px 20px;border-top:0;border-left:2px solid var(--line)}
.log::before{content:"";position:absolute;left:-8px;top:18px;width:14px;height:14px;border-radius:50%;background:var(--yel);border:3px solid var(--card)}
.dots i{width:26px;height:26px}.dots i.u{display:grid;place-items:center}.dots i.u::after{content:"✓";color:#fff;font-size:13px;font-weight:700}
.note{border-radius:0 12px 12px 0;border-left-width:5px}
.pill{padding:4px 12px}
.ring{--p:80;width:112px;height:112px;border-radius:50%;margin:0 auto;display:grid;place-items:center;background:conic-gradient(var(--yel) calc(var(--p)*1%),var(--soft) 0)}
.ring b{width:86px;height:86px;border-radius:50%;background:var(--card);display:grid;place-items:center;font:400 26px 'Archivo Black',Impact,sans-serif;color:var(--pri)}
.modal{backdrop-filter:blur(3px)}.modal .card{border-radius:22px;border-top:0;box-shadow:0 24px 70px rgba(0,0,0,.4);animation:up .25s ease-out}
@keyframes up{from{transform:translateY(16px);opacity:0}}
@media(max-width:700px){.hero{grid-template-columns:1fr;padding:26px}}
@media(prefers-reduced-motion:reduce){.modal .card,.btn{animation:none;transition:none}}
</style>
</head>
<body>
<header>
  <div class="logo">RINTI<i>SA</i></div>
  <div class="row" style="align-items:center">
    <div class="seg" role="group" aria-label="Mode demo"><button data-r="worker" onclick="setRole('worker')">Pencari Kerja</button><button data-r="employer" onclick="setRole('employer')">Pemberi Kerja</button></div>
    <button class="rs" onclick="resetAll()">Reset demo</button>
  </div>
</header>
<main id="app"></main>
<div id="pop"></div><div id="tst"></div>
<script>
const $=s=>document.querySelector(s);
const esc=t=>String(t).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const rp=n=>'Rp '+Number(n).toLocaleString('id-ID');
const L={worker:'Pencari Kerja',employer:'Pemberi Kerja'};
const SK=['Canva','Desain Poster','Logo','CapCut / Video','Penulisan Konten','Input Data','Foto Produk','Admin Medsos'];
const fresh=()=>({role:'worker',ob:{worker:0,employer:0},w:{name:'',bidang:'Desain',skills:[],bisa:'',min:15000},e:{name:'',jenis:'',idv:false},
 jd:{title:'',desc:'',skills:[],budget:100000,dpPct:30,days:5,rev:2},job:null,popup:false,status:'none',chat:[],day:0,prog:0,log:[],revUsed:0,revOpen:null,report:false,img:null});
let S=fresh();

function setRole(r){S.role=r;R()}
function resetAll(){S=fresh();R()}
function go(n){S.ob[S.role]=n;R();scrollTo(0,0)}
function toast(t){$('#tst').innerHTML='<div class="toast" role="status">'+esc(t)+'</div>';setTimeout(()=>$('#tst').innerHTML='',2600)}
function tg(o,k){const a=o.skills,i=a.indexOf(k);i<0?a.push(k):a.splice(i,1);R()}
const chips=(o)=>'<div class="chips">'+SK.map(k=>`<button type="button" class="chip${o.skills.includes(k)?' on':''}" onclick='tg(${o===S.w?"S.w":"S.jd"},${JSON.stringify(k)})'>${k}</button>`).join('')+'</div>';

/* ---------- logika inti ---------- */
function matchPct(){
  if(!S.job)return 0;
  const m=S.job.skills.filter(k=>S.w.skills.includes(k)).length;
  if(!m||S.w.min>S.job.budget)return 0;
  return Math.round(60+40*m/S.job.skills.length);
}
const dpAmt=()=>Math.round(S.job.budget*S.job.dpPct/100/1000)*1000;
function say(from,t){S.chat.push({from,t})}

/* ---------- tampilan onboarding ---------- */
const stepsBar=n=>'<div class="steps">'+['Syarat','Profil','Mulai'].map((t,i)=>`<span class="${i<n?'on':''}"><em>${t}</em></span>`).join('')+'</div>';
function vLogin(){return `<div class="hero"><div class="hl"><h1>Kerja pertama, tanpa portofolio.</h1><p>Rintisa mencocokkan talenta pemula dengan pekerjaan kecil dari UMKM dan komunitas, dengan dana yang aman dan progres yang terlihat.</p><ul class="vp"><li>Dicocokkan lewat profil kemampuan, tanpa rebutan melamar</li><li>DP langsung cair untuk modal kerja</li><li>Revisi terkunci sesuai kontrak</li></ul></div><div class="card login"><h2>Masuk sebagai ${L[S.role]}</h2><p class="mut">Ganti peran lewat tombol di header.</p>
<label>Email</label><input value="demo@rintisa.id"><label>Kata sandi</label><input type="password" value="12345678">
<button class="btn y wide" onclick="go(1)">Masuk</button></div></div>`}
function vTnc(){
 const w=S.role==='worker';
 return `${stepsBar(1)}<div class="card"><h2>Syarat dan ketentuan</h2>
 <p class="mut">Baca dulu sebelum lanjut.</p>
 <ul>${w?`<li>Kamu boleh menerima pekerjaan tanpa portofolio.</li><li>Tarif di Rintisa tingkat pemula. Kerjakan sesuai kesepakatan lingkup, tenggat, dan jumlah revisi.</li><li>Dana ditahan di awal, jadi kamu terlindung dari gagal bayar.</li>`
 :`<li>Kamu bersedia memberi pekerjaan dengan bayaran di bawah tarif profesional (Rp 15.000 – Rp 300.000), dengan ekspektasi yang wajar untuk talenta pemula.</li><li>Seluruh dana ditahan (escrow) sejak proyek dimulai.</li><li>Pembatalan sepihak tidak mendapat pengembalian dana. Jika pekerja bermasalah, laporkan lewat tombol laporan.</li>`}</ul>
 <label style="display:flex;gap:8px;align-items:center;font-weight:600"><input type="checkbox" id="ag" style="width:auto" onchange="$('#nx').disabled=!this.checked"> Saya setuju dengan syarat dan ketentuan</label>
 <button class="btn" id="nx" disabled onclick="go(2)">Lanjut ke profil</button></div>`}
function vProfile(){
 if(S.role==='worker'){const w=S.w;return `${stepsBar(2)}<div class="card"><h2>Lengkapi profil</h2><p class="mut">Makin spesifik, makin tepat pencocokannya. Tidak perlu portofolio.</p>
 <label>Nama</label><input value="${esc(w.name)}" oninput="S.w.name=this.value">
 <label>Bidang utama</label><select onchange="S.w.bidang=this.value">${['Desain','Video','Penulisan','Data & Admin','Media Sosial'].map(b=>`<option${b===w.bidang?' selected':''}>${b}</option>`).join('')}</select>
 <label>Kemampuan yang bisa kamu kerjakan</label>${chips(w)}
 <label>Ceritakan apa saja yang bisa kamu lakukan</label><textarea oninput="S.w.bisa=this.value" placeholder="Contoh: bisa bikin poster acara dan feed Instagram pakai Canva">${esc(w.bisa)}</textarea>
 <label>Bayaran minimum per proyek (Rp)</label><input type="number" min="15000" step="5000" value="${w.min}" oninput="S.w.min=+this.value">
 <button class="btn" onclick="if(!S.w.name||!S.w.skills.length)return toast('Isi nama dan pilih minimal satu kemampuan.');go(3)">Simpan profil</button></div>`}
 const e=S.e;return `${stepsBar(2)}<div class="card"><h2>Lengkapi profil usaha</h2>
 <label>Nama usaha / organisasi</label><input value="${esc(e.name)}" oninput="S.e.name=this.value">
 <label>Jenis</label><input value="${esc(e.jenis)}" placeholder="UMKM, panitia, komunitas, individu" oninput="S.e.jenis=this.value">
 <label style="display:flex;gap:8px;align-items:center;font-weight:600"><input type="checkbox" style="width:auto" ${e.idv?'checked':''} onchange="S.e.idv=this.checked"> Verifikasi identitas (KTP/SIM) – simulasi</label>
 <button class="btn" onclick="if(!S.e.name||!S.e.idv)return toast('Isi nama usaha dan centang verifikasi identitas.');go(3)">Simpan profil</button></div>`}

/* ---------- MVP 1: pemberi kerja isi pekerjaan, pekerja dapat pop-up cocok ---------- */
function vJobForm(){const j=S.jd;return `<div class="card"><h2>Isi pekerjaan<span class="mvp">MVP 1</span></h2><p class="mut">Rintisa mencocokkan pekerjaan ini ke pekerja yang kemampuannya sesuai.</p>
<label>Judul pekerjaan</label><input value="${esc(j.title)}" oninput="S.jd.title=this.value" placeholder="Contoh: Banner promo Ramadan">
<label>Detail tugas</label><textarea oninput="S.jd.desc=this.value">${esc(j.desc)}</textarea>
<label>Kemampuan yang dibutuhkan</label>${chips(j)}
<div class="row"><div style="flex:1;min-width:140px"><label>Honor total (Rp 15.000 – 300.000)</label><input type="number" value="${j.budget}" oninput="S.jd.budget=+this.value"></div>
<div style="flex:1;min-width:140px"><label>DP untuk pekerja</label><select onchange="S.jd.dpPct=+this.value">${[20,30,50].map(p=>`<option value="${p}"${p===j.dpPct?' selected':''}>${p}%</option>`).join('')}</select></div></div>
<div class="row"><div style="flex:1;min-width:140px"><label>Tenggat (hari)</label><input type="number" min="1" value="${j.days}" oninput="S.jd.days=+this.value"></div>
<div style="flex:1;min-width:140px"><label>Maksimal revisi</label><input type="number" min="0" max="5" value="${j.rev}" oninput="S.jd.rev=+this.value"></div></div>
<button class="btn y" onclick="postJob()">Cari pekerja yang cocok</button></div>`}
function postJob(){const j=S.jd;
 if(!j.title||!j.skills.length)return toast('Isi judul dan pilih minimal satu kemampuan.');
 if(j.budget<15000||j.budget>300000)return toast('Honor harus antara Rp 15.000 dan Rp 300.000.');
 if(j.days<1)return toast('Tenggat minimal 1 hari.');
 S.job={title:j.title,desc:j.desc,skills:[...j.skills],budget:j.budget,dpPct:j.dpPct,days:j.days,maxRev:Math.max(0,Math.min(5,j.rev))};
 S.status='posted';S.popup=true;R();toast('Pekerjaan dikirim. Cek tampilan Pencari Kerja untuk notifikasinya.')}
function popup(){
 if(S.role!=='worker'||S.ob.worker<3||S.status!=='posted'||!S.popup)return '';
 const p=matchPct();if(!p)return '';
 return `<div class="modal" role="dialog" aria-modal="true"><div class="card"><div class="ring" style="--p:${p}"><b>${p}%</b></div><p class="mut" style="text-align:center;margin:8px 0 14px">cocok dengan profilmu</p>
 <h2>${esc(S.job.title)}</h2><p>${esc(S.job.desc||'Tanpa deskripsi tambahan.')}</p>
 <table><tr><td>Honor</td><td>${rp(S.job.budget)}</td></tr><tr><td>DP langsung cair</td><td>${rp(dpAmt())}</td></tr><tr><td>Tenggat</td><td>${S.job.days} hari</td></tr><tr><td>Revisi maks.</td><td>${S.job.maxRev}x</td></tr></table>
 <div class="row"><button class="btn y" onclick="apply()">Daftar &amp; buka chat</button><button class="btn o" onclick="S.popup=false;R()">Nanti</button></div>
 <p class="mut" style="margin:10px 0 0">Tanpa kirim portofolio.</p></div></div>`}
function apply(){S.popup=false;S.status='chat';say('sys','Pekerja mendaftar lewat pencocokan. Tidak ada portofolio yang diminta.');say('worker','Halo, saya '+S.w.name+'. Saya tertarik mengerjakan "'+S.job.title+'".');R()}

/* ---------- chat & kontrak ---------- */
function chatBox(){return `<div class="card"><h3>Ruang chat</h3><div class="chat" id="ch">${S.chat.map(m=>m.from==='sys'?`<div class="m sys">${esc(m.t)}</div>`:`<div class="m${m.from===S.role?' me':''}">${esc(m.t)}</div>`).join('')}</div>
<div class="row"><input id="ci" style="flex:1;min-width:0" placeholder="Tulis pesan" onkeydown="if(event.key==='Enter')send()"><button class="btn" style="margin:0" onclick="send()">Kirim</button></div></div>`}
function send(){const v=$('#ci').value.trim();if(!v)return;say(S.role,v);R()}
function contract(){const j=S.job;return `<div class="card"><h3>Surat perjanjian</h3><table><tr><td>Pekerjaan</td><td>${esc(j.title)}</td></tr><tr><td>Honor total</td><td>${rp(j.budget)}</td></tr><tr><td>DP untuk pekerja</td><td>${rp(dpAmt())}</td></tr><tr><td>Tenggat</td><td>${j.days} hari</td></tr><tr><td>Kuota revisi</td><td>${j.maxRev}x</td></tr></table></div>`}
function vChat(){
 const emp=S.role==='employer';
 return contract()+chatBox()+(emp?`<div class="card"><h2>Setujui &amp; tahan dana<span class="mvp">MVP 2</span></h2><p class="mut">Seluruh honor (${rp(S.job.budget)}) ditahan Rintisa. DP ${rp(dpAmt())} langsung cair ke pekerja untuk modal kerja, misalnya domain atau CapCut premium.</p><button class="btn y" onclick="pay()">Setuju &amp; bayar ke escrow</button></div>`
 :`<div class="note">Menunggu pemberi kerja menyetujui kontrak dan membayar ke escrow.</div>`)}
function pay(){S.status='working';say('sys','Kontrak disetujui. Dana '+rp(S.job.budget)+' ditahan, DP '+rp(dpAmt())+' cair ke pekerja.');R();toast('Dana masuk escrow. Ruang kerja dibuka.')}

/* ---------- MVP 2: ruang kerja terkontrol ---------- */
function setImg(inp){const f=inp.files[0];if(!f)return;const r=new FileReader();r.onload=()=>{S.img=r.result;$('#pv').textContent='Foto siap';};r.readAsDataURL(f)}
function upd(){const p=+$('#rg').value,n=$('#nt').value.trim();
 S.log.unshift({p,n,img:S.img,d:S.day});S.prog=p;S.img=null;
 if(p===100){S.status='submitted';say('sys','Pekerja mengirim hasil final.')}R();toast('Progres diperbarui.')}
function claimRev(){const n=$('#rv').value.trim();if(!n)return toast('Tulis apa yang perlu direvisi.');
 S.revUsed++;S.revOpen=n;S.status='working';say('sys','Revisi ke-'+S.revUsed+' diajukan: '+n);R()}
function revDone(){S.revOpen=null;S.status='submitted';say('sys','Pekerja menandai revisi selesai.');R()}
function accept(){S.status='done';say('sys','Hasil diterima. Sisa dana cair ke pekerja.');R()}
function cancelJob(){if(!confirm('Batalkan sepihak? Dana tidak dikembalikan.'))return;S.status='cancelled';say('sys','Pemberi kerja membatalkan sepihak.');R()}
function rep(){S.report=true;say('sys',L[S.role]+' mengirim laporan. Admin meninjau pekerjaan ini.');R();toast('Laporan terkirim.')}

function vWork(){
 const j=S.job,emp=S.role==='employer',st=S.status,over=S.day>j.days;
 const pill={working:['Dikerjakan',''],submitted:['Menunggu persetujuan',''],done:['Selesai','ok'],cancelled:['Dibatalkan','bad']}[st];
 const dp=dpAmt(),rest=j.budget-dp,fin=st==='done'||st==='cancelled';
 let h=`<div class="card"><div class="row" style="justify-content:space-between;align-items:center"><h2 style="margin:0">${esc(j.title)}</h2><span class="pill ${pill[1]}">${pill[0]}</span></div>
 <div class="grid" style="margin-top:12px"><div><small>Dana di escrow</small><strong>${rp(j.budget)}</strong></div><div><small>DP sudah cair</small><strong>${rp(dp)}</strong></div><div><small>${fin?'Sisa dana (cair ke pekerja)':'Sisa ditahan'}</small><strong>${rp(rest)}</strong></div></div></div>`;
 if(S.report)h+='<div class="note">Laporan sedang ditinjau admin. Dana tetap ditahan sampai ada keputusan.</div>';
 if(st==='done')h+='<div class="note"><b>Proyek selesai.</b> Hasil ini bisa jadi portofolio terverifikasi pertama pekerja.</div>';
 if(st==='cancelled')h+='<div class="note"><b>Dibatalkan sepihak.</b> Tidak ada pengembalian dana. Jika pembatalan dipicu pekerja yang tidak bertanggung jawab, laporan bisa diajukan.</div>';
 h+=`<div class="card"><h3>Progres kerja<span class="mvp">MVP 2</span></h3>
 <p class="mut" style="margin:0 0 4px">Waktu: hari ke-${S.day} dari ${j.days}${over?' <b style="color:var(--bad)">(lewat tenggat)</b>':''}</p><div class="bar t"><b style="width:${Math.min(100,S.day/j.days*100)}%"></b></div>
 <p class="mut" style="margin:10px 0 4px">Pekerjaan: ${S.prog}% selesai</p><div class="bar"><b style="width:${S.prog}%"></b></div>
 ${fin?'':'<button class="btn o" onclick="S.day++;R()">Simulasi: maju 1 hari</button>'}
 ${S.log.map(l=>`<div class="log">${l.img?`<img src="${l.img}" alt="Foto progres">`:'<div class="ph">tanpa foto</div>'}<div><b>${l.p}%</b> <span class="mut">· hari ke-${l.d}</span><br>${esc(l.n||'Tanpa catatan')}</div></div>`).join('')}</div>`;
 if(!emp&&st==='working')h+=`<div class="card"><h3>Perbarui progres</h3>${S.revOpen?`<div class="note"><b>Revisi ke-${S.revUsed}:</b> ${esc(S.revOpen)}<br><button class="btn y" onclick="revDone()">Tandai revisi selesai</button></div>`:''}
 <label>Selesai <output id="ro">${S.prog}</output>%</label><input id="rg" type="range" min="0" max="100" step="5" value="${S.prog}" oninput="$('#ro').textContent=this.value">
 <label>Catatan</label><input id="nt" placeholder="Apa yang sudah dikerjakan?"><label>Foto progres</label><input type="file" accept="image/*" onchange="setImg(this)"><span class="mut" id="pv"></span><br>
 <button class="btn" onclick="upd()">Kirim update</button></div>`;
 const left=j.maxRev-S.revUsed;
 h+=`<div class="card"><h3>Revisi<span class="mvp">MVP 2</span></h3><div class="dots" aria-label="Revisi terpakai ${S.revUsed} dari ${j.maxRev}">${Array.from({length:j.maxRev},(_,i)=>`<i class="${i<S.revUsed?'u':''}"></i>`).join('')}</div><p class="mut" style="margin:0">Terpakai ${S.revUsed} dari ${j.maxRev} sesuai kontrak.</p>`;
 if(emp&&!fin){const can=left>0&&S.prog>0&&!S.revOpen;h+=`<textarea id="rv" placeholder="Apa yang perlu direvisi?" ${can?'':'disabled'}></textarea><button class="btn" ${can?'':'disabled'} onclick="claimRev()">Klaim revisi</button>
 ${left<=0?'<p class="mut">Kuota habis, tombol revisi terkunci otomatis.</p>':S.revOpen?'<p class="mut">Menunggu pekerja menyelesaikan revisi sebelumnya.</p>':!S.prog?'<p class="mut">Revisi bisa diklaim setelah ada progres.</p>':''}`}
 h+='</div>';
 if(!fin)h+=`<div class="card"><h3>Aksi</h3><div class="row">${emp?`<button class="btn y" style="margin:0" ${st==='submitted'&&!S.revOpen?'':'disabled'} onclick="accept()">Terima hasil &amp; cairkan sisa dana</button><button class="btn r" style="margin:0" onclick="cancelJob()">Batalkan sepihak</button>`:''}<button class="btn o" style="margin:0" ${S.report?'disabled':''} onclick="rep()">${emp?'Laporkan pekerja':'Laporkan pemberi kerja'}</button></div>
 ${emp?'<p class="mut">Pelunasan baru bisa dicairkan setelah hasil final dikirim dan tidak ada revisi yang menggantung.</p>':''}</div>`;
 return h+chatBox()}

/* ---------- beranda ---------- */
function vHome(){
 const st=S.status,emp=S.role==='employer',mp=matchPct();
 if(emp){
  if(st==='none')return `<h1>Halo, ${esc(S.e.name)}</h1><p class="mut">Isi pekerjaan, Rintisa carikan pekerja yang cocok.</p>`+vJobForm();
  if(st==='posted')return `<div class="card"><h2>Mencari pekerja yang cocok</h2><p>${mp?'Satu pekerja cocok sudah diberi notifikasi. Beralih ke tampilan Pencari Kerja untuk mencoba mendaftar.':'Belum ada pekerja yang cocok dengan kebutuhan dan honor ini. Coba tambah honor atau ubah kemampuan yang dibutuhkan.'}</p><button class="btn o" onclick="S.status='none';R()">Ubah pekerjaan</button></div>`+contract();
  if(st==='chat')return vChat();return vWork()}
 if(st==='none'||st==='posted'){
  const has=st==='posted'&&mp;
  return `<h1>Halo, ${esc(S.w.name)}</h1><div class="card"><h2>${has?'Ada pekerjaan yang cocok':'Belum ada pencocokan'}</h2><p>${has?'Pemberi kerja mencari kemampuan seperti milikmu.':'Notifikasi muncul di sini saat ada pekerjaan yang cocok. Coba pindah ke tampilan Pemberi Kerja dan isi pekerjaan.'}</p>${has?'<button class="btn y" onclick="S.popup=true;R()">Lihat pencocokan</button>':''}</div>`}
 if(st==='chat')return vChat();return vWork()}

function R(){
 const o=S.ob[S.role];
 $('#app').innerHTML=[vLogin,vTnc,vProfile,vHome][o]();
 $('#pop').innerHTML=popup();
 document.querySelectorAll('.seg button').forEach(b=>b.classList.toggle('on',b.dataset.r===S.role));
 const c=$('#ch');if(c)c.scrollTop=c.scrollHeight;
}
R();
</script>
</body>
</html>
