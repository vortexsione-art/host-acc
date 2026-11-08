
<html lang="id">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Host - Vortex</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
*{font-family:'Space Grotesk',sans-serif; box-sizing:border-box}
body{margin:0; min-height:100vh; background:radial-gradient(600px at 100% 0%, rgba(204,255,0,0.15) 0%, transparent 50%),radial-gradient(500px at 0% 100%, rgba(0,255,170,0.12) 0%, transparent 50%),#0a0a0a; display:flex; justify-content:center; align-items:center; padding:16px; color:#fff}
.card{width:100%; max-width:520px; height:88vh; max-height:760px; background:#141414; border:1px solid #262626; border-radius:22px; overflow:hidden; box-shadow:0 20px 60px rgba(0,0,0,0.5); display:flex; flex-direction:column}
.header{padding:16px; background:#0f0f0f; display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid #262626}
.header b{font-size:17px; letter-spacing:-0.5px}
.header b span{color:#ccff00}
#conn{font-size:10px; color:#ccff00}
.iconBtn{width:36px; height:36px; border-radius:10px; border:1px solid #333; background:#1f1f1f; color:#fff; cursor:pointer; display:grid; place-items:center}
#userList{display:flex; gap:8px; padding:10px 14px; overflow-x:auto; background:#0f0f0f; border-bottom:1px solid #262626; scrollbar-width:none}
#userList::-webkit-scrollbar{display:none}
.userTab{flex-shrink:0; padding:8px 10px 8px 14px; border-radius:20px; background:#1f1f1f; border:1px solid #333; font-size:12px; cursor:pointer; white-space:nowrap; display:flex; align-items:center; gap:6px}
.userTab.active{background:#ccff00; color:#000; font-weight:700; border-color:#ccff00}
.userTab .dot{color:#ff3b3b; font-weight:700}
.delKontak{width:18px; height:18px; border-radius:50%; background:rgba(255,255,255,0.15); color:#fff; display:grid; place-items:center; font-size:10px; line-height:1; flex-shrink:0}
.userTab.active .delKontak{background:rgba(0,0,0,0.2); color:#000}
#chat{flex:1; overflow-y:auto; padding:16px; display:flex; flex-direction:column; gap:12px}
.bubble{max-width:82%; padding:10px 14px; border-radius:18px; font-size:13.5px; word-wrap:break-word; animation:pop 0.25s ease; line-height:1.5}
@keyframes pop{from{transform:scale(0.8); opacity:0} to{transform:scale(1); opacity:1}}
.me{align-self:flex-end; background:#ccff00; color:#000; border-bottom-right-radius:6px; font-weight:500}
.you{align-self:flex-start; background:#1f1f1f; border:1px solid #2a2a2a; border-bottom-left-radius:6px}
.replyTag{font-size:10px; opacity:0.7; border-left:2px solid currentColor; padding-left:6px; margin-bottom:4px}
.meta{font-size:9px; opacity:0.6; margin-top:4px; text-align:right}
.system{align-self:center; background:rgba(204,255,0,0.12); border:1px solid rgba(204,255,0,0.35); color:#ccff00; font-size:11px; padding:6px 14px; border-radius:20px}
.footer{padding:10px; background:#0f0f0f; display:flex; flex-direction:column; gap:8px; border-top:1px solid #262626}
.row{display:flex; gap:8px; align-items:center}
.footer input{flex:1; background:#1f1f1f; border:1px solid #333; border-radius:12px; padding:12px; color:#fff; outline:none}
.footer input::placeholder{color:#666}
.btn{padding:12px 18px; border:none; border-radius:12px; background:#ccff00; color:#000; font-weight:700; cursor:pointer}
.emojiBox{position:absolute; bottom:90px; right:20px; background:#1f1f1f; border:1px solid #333; border-radius:14px; padding:8px; display:none; grid-template-columns:repeat(6,1fr); gap:6px; z-index:10}
.emojiBox.show{display:grid}
.toast{position:fixed; bottom:20px; left:50%; transform:translateX(-50%); background:#ccff00; color:#000; padding:10px 18px; border-radius:20px; font-size:12px; font-weight:700; display:none; z-index:99}
.toast.show{display:block}
#overlay{position:fixed; inset:0; background:rgba(0,0,0,0.6); display:none; align-items:center; justify-content:center; z-index:99}
#overlay.show{display:flex}
.modal{background:#1a1a1a; border:1px solid #333; border-radius:18px; padding:20px; width:90%; max-width:320px; text-align:center; color:#fff}
.avatar{width:42px; height:42px; border-radius:12px; background:#ccff00; color:#000; display:grid; place-items:center; font-weight:700; flex-shrink:0}
#lockScreen{position:fixed; inset:0; background:#0a0a0a; display:flex; align-items:center; justify-content:center; z-index:200; padding:20px}
.lockCard{background:#141414; border:1px solid #333; border-radius:22px; padding:30px 26px; width:100%; max-width:360px; text-align:center}
.lockCard h2{margin:0; font-size:24px}
.lockCard h2 span{color:#ccff00}
.lockCard p{font-size:13px; color:#a3a3a3; line-height:1.5; margin:10px 0 18px}
#inputPass{width:100%; background:#1f1f1f; border:1px solid #333; border-radius:14px; padding:14px; color:#fff; outline:none; font-size:16px; text-align:center; letter-spacing:2px}
#inputPass:focus{border-color:#ccff00}
.btnLock{width:100%; margin-top:12px; padding:15px; border:none; border-radius:14px; background:#ccff00; color:#000; font-weight:700; font-size:15px; cursor:pointer}
#passError{display:none; color:#ff5c5c; font-size:12px; margin-top:10px}
</style>
</head>
<body>
<div id="lockScreen"><div class="lockCard"><div style="font-size:48px; margin-bottom:12px">🔒</div><h2>HOST <span>VORTEX</span></h2><p>Halaman ini khusus Host.<br>Masukin password biar bisa balesin chat.</p><input id="inputPass" type="password" placeholder="••••••" autocomplete="off"><button class="btnLock" onclick="cekPassword()">MASUK SEBAGAI HOST →</button><div id="passError">Password salah cuy, coba lagi!</div><div style="margin-top:16px; font-size:11px; color:#666">Lupa password? Ya udah, tanya yang bikin web-nya 😅</div></div></div>
<div class="card">
  <div class="header"><div style="display:flex; gap:10px; align-items:center"><div class="avatar">H</div><div><b>HOST <span>Vortex</span></b><div id="conn" style="font-size:10px">● Menghubungkan...</div></div></div><div style="display:flex; gap:8px"><button class="iconBtn" onclick="clearAll()">🗑️</button><button class="iconBtn" onclick="kunciLagi()">🔒</button></div></div>
  <div id="userList"></div>
  <div id="chat"></div>
  <div class="footer">
    <div id="replyPreview" style="display:none; background:rgba(204,255,0,0.12); border-left:3px solid #ccff00; padding:6px 10px; border-radius:8px; font-size:11px"><span id="replyText"></span><span style="float:right; cursor:pointer" onclick="cancelReply()">✕</span></div>
    <div class="row"><button class="iconBtn" onclick="document.getElementById('fileInput').click()">📎</button><input id="pesan" placeholder="Balesin dia..."><button class="iconBtn" onclick="toggleEmoji()">😊</button><button class="btn" onclick="kirim()">➤</button></div>
    <div id="emojiBox" class="emojiBox"></div>
  </div>
</div>

<!-- MODAL HAPUS PESAN -->
<div id="overlay" onclick="this.classList.remove('show')"><div class="modal" onclick="event.stopPropagation()"><h3>Hapus Pesan?</h3><p style="font-size:11px; opacity:0.7">Akan dihapus untuk kamu</p><button class="btn" style="background:#ff3b3b; color:#fff; margin-top:10px" onclick="confirmDelete()">Hapus</button></div></div>

<!-- MODAL HAPUS KONTAK - BARU -->
<div id="overlayKontak" onclick="this.classList.remove('show')" style="position:fixed; inset:0; background:rgba(0,0,0,0.6); display:none; align-items:center; justify-content:center; z-index:99"><div class="modal" onclick="event.stopPropagation()"><div style="font-size:36px">🗑️</div><h3 id="judulHapusKontak" style="margin:10px 0 6px">Hapus Kontak?</h3><p id="descHapusKontak" style="font-size:12px; opacity:0.7; line-height:1.5">Semua chat orang ini bakal kehapus dari HP lu.</p><button class="btn" style="background:#ff3b3b; color:#fff; margin-top:14px; width:100%" onclick="confirmDeleteKontak()">YA, HAPUS KONTAK</button><button class="btn" style="background:#1f1f1f; color:#fff; border:1px solid #333; margin-top:8px; width:100%" onclick="document.getElementById('overlayKontak').classList.remove('show'); document.getElementById('overlayKontak').style.display='none'">Batal</button></div></div>

<div id="toast" class="toast"></div>
<input type="file" id="fileInput" hidden accept="image/*" onchange="kirimGambar(this)">
<script>
const TOPIC="vortexsione_chat_2026_host_user";
const PASSWORD_HOST = "maulana09";
const HOST_NAME = "Maulana";
let aktifUser = 'all';
let semuaPesan = JSON.parse(localStorage.getItem('pesan_'+TOPIC) || '[]');
let unread = {};
let deleteKey=null, es=null, replyTo=null;
let kontakToDelete = null;
function norm(s){ return (s||'').toString().trim().toLowerCase() }
function showToast(m){ let t=document.getElementById('toast'); t.innerText=m; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),2000) }
if(sessionStorage.getItem('vortex_host_login')==='ok'){ document.getElementById('lockScreen').style.display='none'; }
function cekPassword(){
  let v = document.getElementById('inputPass').value.trim();
  if(v === PASSWORD_HOST){ sessionStorage.setItem('vortex_host_login','ok'); document.getElementById('lockScreen').style.display='none'; showToast('Selamat datang Host!'); }
  else { document.getElementById('passError').style.display='block'; document.getElementById('inputPass').value=''; document.getElementById('inputPass').style.borderColor='#ff3b3b'; setTimeout(()=>document.getElementById('inputPass').style.borderColor='#333', 1000); }
}
function kunciLagi(){ sessionStorage.removeItem('vortex_host_login'); location.reload(); }
document.getElementById('inputPass').addEventListener('keydown', e=>{ if(e.key==='Enter') cekPassword(); });
function getUsers(){ let users = [...new Set(semuaPesan.filter(m=>m.from==='pengirim').map(m=>m.nama))]; return users; }
function tampilkanUsers(){
  let list = document.getElementById('userList');
  let users = getUsers();
  let html = `<div class="userTab ${aktifUser==='all'?'active':''}" onclick="pilihUser('all')">🌐 Semua</div>`;
  users.forEach(u=>{
    let dot = unread[norm(u)] ? ` <span class="dot">●${unread[norm(u)]}</span>` : '';
    let safe = u.replace(/'/g,"\\'");
    html += `<div class="userTab ${norm(aktifUser)===norm(u)?'active':''}" onclick="pilihUser('${safe}')"><span>${u}${dot}</span><span class="delKontak" onclick="event.stopPropagation(); tanyaHapusKontak('${safe}')">✕</span></div>`;
  });
  list.innerHTML = html;
}
function pilihUser(u){ aktifUser = u; if(unread[norm(u)]) delete unread[norm(u)]; tampilkanUsers(); tampilkan(); }

// FITUR HAPUS KONTAK - BARU
function tanyaHapusKontak(namaKontak){
  kontakToDelete = namaKontak;
  document.getElementById('judulHapusKontak').innerText = 'Hapus '+namaKontak+'?';
  document.getElementById('descHapusKontak').innerHTML = 'Semua chat <b>'+namaKontak+'</b> bakal kehapus dari HP lu.<br>Orangnya masih bisa chat lagi kok, nanti muncul kontak baru.';
  let ov = document.getElementById('overlayKontak');
  ov.classList.add('show'); ov.style.display='flex';
}
function confirmDeleteKontak(){
  if(!kontakToDelete) return;
  let target = norm(kontakToDelete);
  // 1. Hapus semua chat orang itu dari host
  semuaPesan = semuaPesan.filter(m => {
    if(m.from==='pengirim' && norm(m.nama)===target) return false;
    if(m.from==='penerima' && norm(m.to)===target) return false;
    return true;
  });
  // 2. Hapus notif
  if(unread[target]) delete unread[target];
  // 3. Kalo lagi buka kontak itu, balik ke Semua
  if(norm(aktifUser)===target) aktifUser='all';
  localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan));
  let ov = document.getElementById('overlayKontak');
  ov.classList.remove('show'); ov.style.display='none';
  showToast('Kontak '+kontakToDelete+' dihapus');
  kontakToDelete = null;
  tampilkan();
}

function isRelevant(msg){
  if(aktifUser==='all') return true;
  if(msg.from==='system') return norm(msg.oldNama)===norm(aktifUser) || norm(msg.newNama)===norm(aktifUser);
  if(msg.from==='pengirim') return norm(msg.nama)===norm(aktifUser);
  if(msg.from==='penerima') return norm(msg.to)===norm(aktifUser);
  return false;
}
function tampilkan(){
  tampilkanUsers();
  let box=document.getElementById('chat'); box.innerHTML='';
  let filtered = semuaPesan.filter(m=>{
    if(m.deletedBy && m.deletedBy.map(norm).includes('host')) return false;
    return isRelevant(m);
  }).sort((a,b)=>a.timestamp-b.timestamp);
  if(!filtered.length){ box.innerHTML=`<div style="text-align:center; opacity:0.5; margin-top:60px; font-size:13px; line-height:1.6">Belum ada chat cuy.<br>Tunggu ada yang curhat ya.</div>`; return; }
  filtered.forEach(item=>{
    if(item.from==='system'){ box.innerHTML+=`<div style="width:100%; display:flex; justify-content:center"><div class="system">🔄 ${item.pesan}</div></div>`; }
    else{
      let isMe = item.from==='penerima';
      let replyHtml = item.reply ? `<div class="replyTag">↪ ${item.reply}</div>` : '';
      let imgHtml = item.image ? `<img src="${item.image}" style="max-width:100%; border-radius:12px; margin-top:6px">` : '';
      let namaLabel = !isMe ? `<div style="font-size:10px; opacity:0.6; margin-bottom:3px">${item.nama}</div>` : '';
      box.innerHTML+=`<div style="width:100%; display:flex; ${isMe?'justify-content:flex-end':'justify-content:flex-start'}"><div class="bubble ${isMe?'me':'you'}" onclick="setReply('${item.id}','${(item.pesan||'').replace(/'/g,'')}')" oncontextmenu="openDel('${item.id}'); return false;">${namaLabel}${replyHtml}${item.pesan}${imgHtml}<div class="meta">${item.jam} ${isMe?'✓✓':''}</div></div></div>`;
    }
  });
  box.scrollTop = box.scrollHeight;
}
function publish(msg){
  msg.id = Date.now()+'_'+Math.random().toString(36).substr(2,6); msg.timestamp = Date.now();
  fetch('https://ntfy.sh/'+TOPIC,{method:'POST', body:JSON.stringify(msg)});
  semuaPesan.push(msg); localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan.slice(-500))); tampilkan();
}
function kirim(){
  let p=document.getElementById('pesan').value.trim(); if(!p) return;
  publish({nama:HOST_NAME, pesan:p, jam:new Date().toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'}), from:'penerima', to:aktifUser, reply:replyTo, deletedBy:[]});
  document.getElementById('pesan').value=''; cancelReply();
}
function kirimGambar(input){
  let file=input.files[0]; if(!file) return;
  let r=new FileReader(); r.onload=()=>{ publish({nama:HOST_NAME, pesan:'📷 Gambar', image:r.result, jam:new Date().toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'}), from:'penerima', to:aktifUser, deletedBy:[]}) }; r.readAsDataURL(file);
}
function clearAll(){
  if(!confirm('Hapus semua chat di layar host?')) return;
  semuaPesan.forEach(m=>{ if(!m.deletedBy) m.deletedBy=[]; if(!m.deletedBy.includes('host')) m.deletedBy.push('host'); });
  localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan)); tampilkan(); showToast('Dibersihkan');
}
function buildEmoji(){ let e=["😀","😂","❤️","🔥","👍","😭","😍","🙏","✨","💀","😎","🥺"]; let box=document.getElementById('emojiBox'); box.innerHTML=e.map(x=>`<span style="cursor:pointer; font-size:18px" onclick="addEmoji('${x}')">${x}</span>`).join(''); }
function toggleEmoji(){ document.getElementById('emojiBox').classList.toggle('show') }
function addEmoji(e){ document.getElementById('pesan').value+=e; toggleEmoji(); document.getElementById('pesan').focus() }
function setReply(id,text){ replyTo=text.slice(0,40); document.getElementById('replyText').innerText='Balas: '+replyTo; document.getElementById('replyPreview').style.display='block'; }
function cancelReply(){ replyTo=null; document.getElementById('replyPreview').style.display='none' }
function openDel(id){ deleteKey=id; document.getElementById('overlay').classList.add('show') }
function confirmDelete(){
  let idx=semuaPesan.findIndex(m=>m.id===deleteKey);
  if(idx>-1){ if(!semuaPesan[idx].deletedBy) semuaPesan[idx].deletedBy=[]; semuaPesan[idx].deletedBy.push('host');
  publish({nama:'system', from:'system', type:'delete', targetId:deleteKey, deleter:'host', pesan:'host menghapus', jam:new Date().toLocaleTimeString('id-ID'), deletedBy:[], timestamp:Date.now(), id:Date.now()+'_del'}) }
  localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan.slice(-500)));
  document.getElementById('overlay').classList.remove('show'); showToast('Dihapus'); tampilkan();
}
function connectNtfy(){
  if(es) es.close();
  es=new EventSource('https://ntfy.sh/'+TOPIC+'/sse');
  es.onopen=()=>document.getElementById('conn').innerText='● Terhubung';
  es.onmessage=(e)=>{
    try{
      let outer=JSON.parse(e.data); if(!outer.message) return;
      let msg=JSON.parse(outer.message);
      if(semuaPesan.find(m=>m.id===msg.id)) return;
      if(msg.type==='rename' && msg.from==='system'){
        let oldN = norm(msg.oldNama);
        semuaPesan = semuaPesan.filter(m => {
          if(m.from==='pengirim' && norm(m.nama)===oldN) return false;
          if(m.from==='penerima' && norm(m.to)===oldN) return false;
          return true;
        });
        if(unread[oldN]) delete unread[oldN];
        if(norm(aktifUser)===oldN) aktifUser='all';
        localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan));
        showToast(msg.oldNama+' ganti nama jadi '+msg.newNama+' - kontak lama dihapus');
        tampilkan();
        return;
      }
      if(msg.type==='delete'){ let t=semuaPesan.find(x=>x.id===msg.targetId); if(t){ if(!t.deletedBy) t.deletedBy=[]; t.deletedBy.push(msg.deleter); } }
      else{
        semuaPesan.push(msg);
        if(msg.from==='pengirim' && norm(msg.nama)!==norm(aktifUser) && aktifUser!=='all'){
          unread[norm(msg.nama)] = (unread[norm(msg.nama)]||0)+1;
        }
      }
      localStorage.setItem('pesan_'+TOPIC, JSON.stringify(semuaPesan.slice(-500)));
      tampilkan();
    }catch{}
  };
  es.onerror=()=>{ document.getElementById('conn').innerText='🔴 reconnect...'; setTimeout(connectNtfy,3000); }
}
document.getElementById('pesan').addEventListener('keydown',e=>{ if(e.key==='Enter') kirim() });
buildEmoji(); tampilkan(); connectNtfy();
</script>
</body>
</html>
