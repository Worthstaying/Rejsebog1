[index.html](https://github.com/user-attachments/files/29465961/index.html)
<!DOCTYPE html>
<html lang="da">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Rejsedagbog</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.min.js"></script>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: -apple-system, sans-serif; background: #F4EFE4; min-height: 100vh; }
#root { max-width: 480px; margin: 0 auto; min-height: 100vh; }
.lock { display: flex; align-items: center; justify-content: center; min-height: 100vh; background: #3F5E55; }
.lockbox { background: rgba(255,255,255,0.15); border-radius: 16px; padding: 32px 24px; width: 280px; text-align: center; }
.lockbox h1 { font-size: 22px; color: #fff; margin: 10px 0 4px; }
.lockbox p { font-size: 13px; color: rgba(255,255,255,0.6); margin-bottom: 20px; }
.pwinp { width: 100%; padding: 12px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.3); background: rgba(255,255,255,0.1); color: #fff; font-size: 16px; text-align: center; margin-bottom: 10px; font-family: inherit; }
.pwbtn { width: 100%; padding: 12px; border-radius: 10px; border: none; background: #fff; color: #3F5E55; font-size: 15px; font-weight: 700; cursor: pointer; font-family: inherit; }
.pwerr { color: #ffb3a0; font-size: 13px; margin-top: 8px; }
.header { background: #3F5E55; padding: 13px 14px; display: flex; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 20; }
.htitle { flex: 1; text-align: center; }
.htitle h2 { font-size: 17px; color: #fff; }
.htitle p { font-size: 11px; color: rgba(255,255,255,0.55); }
.hbtn { background: rgba(255,255,255,0.15); border: none; border-radius: 9px; width: 38px; height: 38px; color: #fff; cursor: pointer; font-size: 18px; }
.tabs { display: flex; background: #fff; border-bottom: 1px solid #E0D5C0; position: sticky; top: 56px; z-index: 19; }
.tab { flex: 1; display: flex; flex-direction: column; align-items: center; padding: 9px 0 7px; background: none; border: none; cursor: pointer; font-size: 10px; color: #8A7A63; gap: 3px; position: relative; font-family: inherit; }
.tab.on { color: #B5532C; font-weight: 600; }
.tab.on::after { content: ''; position: absolute; bottom: 0; left: 20%; right: 20%; height: 2px; background: #B5532C; border-radius: 2px 2px 0 0; }
.tabicon { font-size: 19px; }
.body { padding: 16px; padding-bottom: 90px; }
.sec { font-size: 11px; letter-spacing: 0.15em; text-transform: uppercase; color: #8A7A63; font-weight: 700; margin: 20px 0 10px; display: flex; align-items: center; gap: 8px; }
.sec::after { content: ''; flex: 1; height: 1px; background: #E0D5C0; }
.sec:first-child { margin-top: 0; }
.card { background: #FFFDF7; border-radius: 12px; padding: 16px; margin-bottom: 12px; border: 1px solid #E0D5C0; }
.inp { width: 100%; padding: 11px 13px; border-radius: 10px; border: 1px solid #E0D5C0; background: #fff; font-size: 15px; color: #2F2A22; font-family: inherit; outline: none; }
.inpsm { flex: 1; padding: 9px 11px; border-radius: 9px; border: 1px solid #E0D5C0; background: #fff; font-size: 13px; color: #2F2A22; font-family: inherit; min-width: 0; outline: none; }
.lbl { display: block; font-size: 11px; color: #8A7A63; text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 5px; }
.row { display: flex; gap: 8px; }
.btnp { background: #B5532C; color: #fff; border: none; border-radius: 10px; padding: 11px 16px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: inherit; }
.btng { background: #3F5E55; color: #fff; border: none; border-radius: 10px; padding: 11px 16px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: inherit; }
.btns { background: #fff; color: #5A4A3A; border: 1px solid #E0D5C0; border-radius: 10px; padding: 11px 16px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: inherit; }
.btnw { width: 100%; }
.btnsm { padding: 8px 12px; font-size: 13px; border-radius: 9px; }
.ghost { background: none; border: 1.5px dashed #C9B896; border-radius: 12px; padding: 15px; color: #8A7A63; font-size: 14px; font-weight: 600; cursor: pointer; width: 100%; margin-bottom: 14px; font-family: inherit; display: flex; align-items: center; justify-content: center; gap: 8px; }
.trash { background: none; border: none; color: #B5A98F; cursor: pointer; font-size: 16px; padding: 4px; }
.tripcard { display: flex; align-items: center; gap: 14px; background: #FFFDF7; border-radius: 14px; padding: 16px; margin-bottom: 12px; border: 1px solid #E0D5C0; cursor: pointer; }
.stamp { width: 50px; height: 50px; border-radius: 10px; border: 2px solid #B5532C; color: #B5532C; display: flex; align-items: center; justify-content: center; font-family: monospace; font-weight: 700; font-size: 12px; flex-shrink: 0; }
.tname { font-size: 18px; color: #2F2A22; }
.tdest { font-size: 13px; color: #8A7A63; margin-top: 2px; }
.tdates { font-size: 12px; color: #B5A98F; margin-top: 4px; }
.plrow { display: flex; align-items: flex-start; background: #FFFDF7; border-radius: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid #E0D5C0; gap: 10px; }
.plinfo { flex: 1; min-width: 0; }
.plname { font-size: 16px; color: #2F2A22; }
.plnote { font-size: 13px; color: #8A7A63; margin-top: 3px; }
.plmeta { font-size: 11px; color: #B5A98F; margin-top: 4px; }
.wishbadge { display: inline-block; font-size: 10px; background: #FFF3CD; color: #8B6914; border-radius: 6px; padding: 2px 7px; font-weight: 600; margin-top: 4px; }
.visitbadge { display: inline-block; font-size: 10px; background: #E8F5E9; color: #2E7D32; border-radius: 6px; padding: 2px 7px; font-weight: 600; margin-top: 4px; }
.movebtn { font-size: 11px; background: #3F5E55; color: #fff; border: none; border-radius: 7px; padding: 4px 9px; cursor: pointer; margin-top: 6px; font-family: inherit; display: block; }
.catpills { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 4px; }
.catpill { border: 1.5px solid #E0D5C0; border-radius: 9px; padding: 6px 12px; font-size: 12px; font-weight: 600; cursor: pointer; background: #fff; color: #5A4A3A; font-family: inherit; }
.chip { display: inline-flex; align-items: center; background: #fff; border: 1px solid #E0D5C0; border-radius: 20px; padding: 6px 12px; font-size: 13px; color: #5A4A3A; margin: 0 6px 6px 0; }
.chipx { background: none; border: none; color: #B5A98F; cursor: pointer; margin-left: 6px; font-size: 14px; }
.herobox { background: #3F5E55; border-radius: 14px; padding: 18px; margin-bottom: 18px; }
.herolbl { font-size: 10px; letter-spacing: 0.15em; text-transform: uppercase; color: rgba(255,255,255,0.55); margin-bottom: 4px; }
.heroval { font-size: 24px; color: #fff; }
.herorow { display: flex; justify-content: space-between; margin-top: 14px; }
.progress { height: 6px; background: rgba(255,255,255,0.2); border-radius: 4px; margin-top: 12px; overflow: hidden; }
.progfill { height: 100%; border-radius: 4px; background: #fff; }
.exprow { display: flex; align-items: center; background: #FFFDF7; border-radius: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid #E0D5C0; gap: 10px; }
.expinfo { flex: 1; }
.expdesc { font-size: 15px; color: #2F2A22; }
.expcat { font-size: 12px; color: #B5A98F; margin-top: 2px; }
.expamt { font-family: monospace; font-size: 15px; color: #5A4A3A; white-space: nowrap; }
.photogrid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 14px; }
.photocard { background: #FFFDF7; border-radius: 10px; overflow: hidden; border: 1px solid #E0D5C0; }
.photowrap { position: relative; }
.photodel { position: absolute; top: 6px; right: 6px; background: rgba(0,0,0,0.55); border: none; border-radius: 6px; width: 26px; height: 26px; color: #fff; cursor: pointer; font-size: 13px; }
.photocap { width: 100%; border: none; padding: 8px 10px; font-size: 12px; color: #5A4A3A; font-family: inherit; background: transparent; }
.empty { text-align: center; padding: 30px 20px; color: #B5A98F; font-size: 13px; line-height: 1.7; }
.overlay { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.45); display: flex; align-items: flex-end; justify-content: center; z-index: 100; }
.modal { background: #FFFDF7; border-radius: 20px 20px 0 0; padding: 20px; width: 100%; max-width: 480px; max-height: 85vh; overflow-y: auto; }
.modaltitle { font-size: 18px; color: #2F2A22; margin-bottom: 4px; font-weight: 600; }
.modalsub { font-size: 13px; color: #8A7A63; margin-bottom: 14px; line-height: 1.5; }
.startbg { background: #3F5E55; padding: 40px 20px 40px; }
.starttitle { font-size: 32px; color: #fff; margin-bottom: 6px; }
.startsub { font-size: 14px; color: rgba(255,255,255,0.6); }
.statrow { display: flex; gap: 8px; margin-bottom: 14px; }
.statbox { flex: 1; background: #FFFDF7; border-radius: 12px; padding: 12px; border: 1px solid #E0D5C0; text-align: center; }
.statnum { font-size: 24px; color: #2F2A22; margin-top: 4px; }
.statlbl { font-size: 10px; color: #8A7A63; text-transform: uppercase; margin-top: 2px; }
.tkrow { display: flex; align-items: center; font-size: 13px; color: #5A4A3A; margin-bottom: 8px; gap: 8px; background: #F4EFE4; border-radius: 8px; padding: 9px 12px; }
.cardhead { display: flex; align-items: center; gap: 8px; margin-bottom: 12px; }
.cardlbl { font-size: 15px; color: #2F2A22; flex: 1; }
.field { margin-bottom: 12px; }
.btnrow { display: flex; gap: 10px; margin-top: 12px; }
</style>
</head>
<body>
<div id="root"></div>
<script>
var SURL = "https://wwugsvsznrsupkjqingw.supabase.co";
var SKEY = "sb_publishable_vpuARxHJiq-eWNeF5iVonQ_cMRwkgST";
var APASS = "cobisa2026";

var db = supabase.createClient(SURL, SKEY);
var saveTimer = null;

var CATS = {
  restaurant: { l: "Restaurant", e: "🍽", c: "#B5532C" },
  vinbar: { l: "Vinbar", e: "🍷", c: "#7A3B45" },
  sevaerdighed: { l: "Sevaerdighed", e: "🏛", c: "#3F5E55" },
  hotel: { l: "Hotel", e: "🏨", c: "#5A4A3A" },
  hus: { l: "Hus", e: "🏠", c: "#6B5B3E" },
  cafe: { l: "Cafe", e: "☕", c: "#8B6914" },
  andet: { l: "Andet", e: "★", c: "#9C8B6E" }
};

var TRANS = {
  fly: { l: "Flybillet", e: "✈" },
  tog: { l: "Togbillet", e: "🚂" }
};

var S = {
  unlocked: sessionStorage.getItem("rjb4") === APASS,
  trips: [],
  loaded: false,
  activeTrip: null,
  tab: "oversigt",
  bookMode: false
};

function uid() { return Math.random().toString(36).slice(2, 10); }

function fmtD(d) {
  if (!d) return "";
  return new Date(d + "T00:00:00").toLocaleDateString("da-DK", { weekday: "short", day: "numeric", month: "short" });
}

function fmtDL(d) {
  if (!d) return "";
  return new Date(d + "T00:00:00").toLocaleDateString("da-DK", { day: "numeric", month: "long", year: "numeric" });
}

function mk(tag, cls) {
  var el = document.createElement(tag);
  if (cls) el.className = cls;
  return el;
}

function div(cls) { return mk("div", cls); }

function btn(cls, text, fn) {
  var b = mk("button", cls);
  b.innerHTML = text;
  b.onclick = fn;
  return b;
}

function inp(cls, ph, val, fn, type) {
  var i = mk("input", cls);
  i.placeholder = ph || "";
  i.value = val || "";
  i.type = type || "text";
  i.oninput = function() { fn(i.value); };
  return i;
}

function field(labelText, child) {
  var w = div("field");
  var l = mk("label", "lbl");
  l.textContent = labelText;
  w.appendChild(l);
  w.appendChild(child);
  return w;
}

function root() { return document.getElementById("root"); }

async function loadTrips() {
  try {
    var res = await db.from("trips_data").select("data").eq("id", 1).single();
    if (res.data && res.data.data) S.trips = res.data.data;
  } catch(err) { console.log("Load error", err); }
  S.loaded = true;
  render();
}

function save() {
  clearTimeout(saveTimer);
  saveTimer = setTimeout(function() {
    db.from("trips_data").update({ data: S.trips, updated_at: new Date().toISOString() }).eq("id", 1);
  }, 2000);
}

function setupRT() {
  db.channel("rjb4rt").on("postgres_changes", { event: "UPDATE", schema: "public", table: "trips_data" }, function(p) {
    if (p.new && p.new.data) { S.trips = p.new.data; render(); }
  }).subscribe();
}

function mutateTrip(fn) {
  var i = S.trips.findIndex(function(t) { return t.id === S.activeTrip; });
  if (i < 0) return;
  fn(S.trips[i]);
  save();
}

function render() {
  root().innerHTML = "";
  if (!S.unlocked) { renderLock(); return; }
  if (!S.loaded) {
    var w = div("lock");
    w.innerHTML = '<div style="color:#fff;font-size:20px;font-family:sans-serif">Henter rejser...</div>';
    root().appendChild(w);
    return;
  }
  if (S.bookMode && S.activeTrip) { renderBook(); return; }
  if (!S.activeTrip) { renderHome(); return; }
  renderTrip();
}

function renderLock() {
  var pw = "";
  var err = div("pwerr");
  var pi = inp("pwinp", "Adgangskode", "", function(v) { pw = v; }, "password");
  pi.addEventListener("keydown", function(ev) { if (ev.key === "Enter") tryUnlock(); });
  var bx = div("lockbox");
  bx.innerHTML = '<div style="font-size:36px">🗺</div>';
  var h1 = mk("h1", ""); h1.textContent = "Rejsedagbog"; bx.appendChild(h1);
  var p = mk("p", ""); p.textContent = "Jeres fælles rejsedagbog"; bx.appendChild(p);
  bx.appendChild(pi);
  bx.appendChild(btn("pwbtn", "Åbn", tryUnlock));
  bx.appendChild(err);
  var lk = div("lock");
  lk.appendChild(bx);
  root().appendChild(lk);

  function tryUnlock() {
    if (pw === APASS) {
      sessionStorage.setItem("rjb4", APASS);
      S.unlocked = true;
      loadTrips();
      setupRT();
    } else {
      err.textContent = "Forkert kode – prøv igen";
    }
  }
}

function renderHome() {
  var wrap = div("");
  var bg = div("startbg");
  var ey = div(""); ey.style.fontSize = "11px"; ey.style.color = "rgba(255,255,255,0.5)"; ey.style.letterSpacing = "0.3em"; ey.style.textTransform = "uppercase"; ey.style.marginBottom = "8px"; ey.textContent = "Rejsedagbog";
  var ti = mk("h1", "starttitle"); ti.textContent = "Jeres rejser";
  var su = div("startsub"); su.textContent = "Billetter · Steder · Budget · Minder";
  bg.appendChild(ey); bg.appendChild(ti); bg.appendChild(su);
  wrap.appendChild(bg);

  var body = div("body");
  wrap.appendChild(body);

  var drow = div("row"); drow.style.marginBottom = "14px";
  var eb = btn("btns btnsm", "💾 Gem data", doExport); eb.style.flex = "1";
  var ib = btn("btns btnsm", "📂 Indlæs", doImport); ib.style.flex = "1";
  drow.appendChild(eb); drow.appendChild(ib);
  body.appendChild(drow);

  S.trips.forEach(function(t) {
    var tc = div("tripcard");
    var stamp = div("stamp"); stamp.textContent = (t.destination || "???").slice(0, 3).toUpperCase();
    var info = div("");
    var tn = div("tname"); tn.textContent = t.name || "Unavngiven rejse";
    var td = div("tdest"); td.textContent = t.destination || "";
    info.appendChild(tn); info.appendChild(td);
    if (t.start || t.end) {
      var dates = div("tdates"); dates.textContent = fmtD(t.start) + (t.end ? " → " + fmtD(t.end) : "");
      info.appendChild(dates);
    }
    var del = btn("trash", "🗑", function(ev) {
      ev.stopPropagation();
      if (confirm("Slet rejsen?")) { S.trips = S.trips.filter(function(x) { return x.id !== t.id; }); save(); render(); }
    });
    tc.appendChild(stamp); tc.appendChild(info); tc.appendChild(del);
    tc.onclick = function() { S.activeTrip = t.id; S.tab = "oversigt"; render(); };
    body.appendChild(tc);
  });

  var showNew = S.trips.length === 0;
  var nb = btn("ghost", "＋ Ny rejse", function() { showNew = true; refreshNew(); });
  var nf = div("");
  body.appendChild(nb); body.appendChild(nf);

  function refreshNew() {
    nb.style.display = showNew ? "none" : "flex";
    nf.innerHTML = "";
    if (!showNew) return;
    var name = "", dest = "", start = "", end = "";
    var ni = inp("inp", "Navn (f.eks. Vintur til Alsace)", "", function(v) { name = v; });
    ni.style.marginBottom = "10px";
    var di = inp("inp", "Destination (f.eks. Frankrig)", "", function(v) { dest = v; });
    di.style.marginBottom = "10px";
    var si = inp("inpsm", "", "", function(v) { start = v; }, "date");
    var ei = inp("inpsm", "", "", function(v) { end = v; }, "date");
    var dr = div("row"); dr.style.marginBottom = "12px";
    var sl = div(""); sl.style.flex = "1";
    var sll = mk("label", "lbl"); sll.textContent = "Fra"; sl.appendChild(sll); sl.appendChild(si);
    var el2 = div(""); el2.style.flex = "1";
    var ell = mk("label", "lbl"); ell.textContent = "Til"; el2.appendChild(ell); el2.appendChild(ei);
    dr.appendChild(sl); dr.appendChild(el2);
    var br = div("btnrow");
    var cb = btn("btns", "Annuller", function() { showNew = false; refreshNew(); }); cb.style.flex = "1";
    var ob = btn("btnp", "Opret rejse", function() {
      if (!name.trim() || !dest.trim()) return;
      var t = { id: uid(), name: name, destination: dest, start: start, end: end, budget: "", stops: [], travelers: [], tickets: [], places: [], expenses: [], photos: [] };
      S.trips.push(t); save(); S.activeTrip = t.id; S.tab = "oversigt"; render();
    }); ob.style.flex = "1";
    br.appendChild(cb); br.appendChild(ob);
    var card = div("card");
    var cardTitle = div(""); cardTitle.style.fontSize = "18px"; cardTitle.style.color = "#2F2A22"; cardTitle.style.marginBottom = "14px"; cardTitle.textContent = "Ny rejse";
    card.appendChild(cardTitle); card.appendChild(ni); card.appendChild(di); card.appendChild(dr); card.appendChild(br);
    nf.appendChild(card);
  }
  refreshNew();
  root().appendChild(wrap);

  function doExport() {
    var json = JSON.stringify(S.trips, null, 2);
    showModal("💾 Gem data", "Kopier teksten og gem i Notes. Brug Indlæs data næste gang.", function(body) {
      var ta = mk("textarea", "inp"); ta.style.height = "140px"; ta.style.fontFamily = "monospace"; ta.style.fontSize = "11px"; ta.readOnly = true; ta.value = json;
      body.appendChild(ta);
      var cb = btn("btng btnw", "Kopier", function() {
        navigator.clipboard.writeText(json).then(function() { alert("Kopieret!"); }).catch(function() { ta.select(); document.execCommand("copy"); alert("Kopieret!"); });
      }); cb.style.marginTop = "10px";
      body.appendChild(cb);
    });
  }

  function doImport() {
    showModal("📂 Indlæs data", "Indsæt den tekst du gemte.", function(body) {
      var ta = mk("textarea", "inp"); ta.style.height = "140px"; ta.style.fontFamily = "monospace"; ta.style.fontSize = "11px"; ta.placeholder = "Indsæt tekst her...";
      body.appendChild(ta);
      var ib2 = btn("btng btnw", "Indlæs", function() {
        try {
          var d2 = JSON.parse(ta.value);
          if (Array.isArray(d2)) { S.trips = d2; save(); closeModal(); render(); }
        } catch(err) { alert("Ugyldig data"); }
      }); ib2.style.marginTop = "10px";
      body.appendChild(ib2);
    });
  }
}

function showModal(title, sub, fn) {
  var ov = div("overlay");
  var mo = div("modal");
  var mt = div("modaltitle"); mt.textContent = title;
  var ms = div("modalsub"); ms.textContent = sub;
  mo.appendChild(mt); mo.appendChild(ms);
  fn(mo);
  var cl = btn("btns btnw", "Luk", function() { ov.remove(); }); cl.style.marginTop = "10px";
  mo.appendChild(cl);
  ov.appendChild(mo);
  ov.onclick = function(ev) { if (ev.target === ov) ov.remove(); };
  root().appendChild(ov);
}

function closeModal() { var ov = root().querySelector(".overlay"); if (ov) ov.remove(); }

function renderTrip() {
  var trip = S.trips.find(function(t) { return t.id === S.activeTrip; });
  if (!trip) return;
  var TABS = [{ id: "oversigt", l: "Oversigt", e: "✈" }, { id: "steder", l: "Steder", e: "📍" }, { id: "budget", l: "Budget", e: "💰" }, { id: "billeder", l: "Billeder", e: "📷" }];
  var wrap = div("");

  var hdr = div("header");
  var bb = btn("hbtn", "‹", function() { S.activeTrip = null; render(); });
  var ht = div("htitle");
  var hth = mk("h2", ""); hth.textContent = trip.name || "Rejse"; ht.appendChild(hth);
  var htp = mk("p", ""); htp.textContent = trip.destination || ""; ht.appendChild(htp);
  var bkb = btn("hbtn", "📖", function() { S.bookMode = true; render(); });
  hdr.appendChild(bb); hdr.appendChild(ht); hdr.appendChild(bkb);
  wrap.appendChild(hdr);

  var tabbar = div("tabs");
  var content = div("body");
  var tabBtns = [];

  TABS.forEach(function(t) {
    var tb = btn("tab" + (S.tab === t.id ? " on" : ""), '<span class="tabicon">' + t.e + '</span>' + t.l, function() {
      S.tab = t.id;
      tabBtns.forEach(function(b, i) { b.className = "tab" + (TABS[i].id === t.id ? " on" : ""); });
      renderContent();
    });
    tabBtns.push(tb);
    tabbar.appendChild(tb);
  });

  wrap.appendChild(tabbar);
  wrap.appendChild(content);
  root().appendChild(wrap);

  function renderContent() {
    content.innerHTML = "";
    if (S.tab === "oversigt") renderOversigt(trip, content);
    else if (S.tab === "steder") renderSteder(trip, content);
    else if (S.tab === "budget") renderBudget(trip, content);
    else if (S.tab === "billeder") renderBilleder(trip, content);
  }
  renderContent();
}

function renderOversigt(trip, content) {
  if (!trip.travelers) trip.travelers = [];
  if (!trip.stops) trip.stops = [];
  if (!trip.tickets) trip.tickets = [];

  var sec1 = div("sec"); sec1.textContent = "Rejsende"; content.appendChild(sec1);
  var chips = div(""); chips.style.marginBottom = "10px"; content.appendChild(chips);

  function refreshChips() {
    chips.innerHTML = "";
    trip.travelers.forEach(function(n) {
      var chip = div("chip");
      chip.appendChild(document.createTextNode(n));
      var x = btn("chipx", "✕", function() {
        trip.travelers = trip.travelers.filter(function(x2) { return x2 !== n; });
        mutateTrip(function() {}); refreshChips();
      });
      chip.appendChild(x); chips.appendChild(chip);
    });
  }
  refreshChips();

  var tn = "";
  var ti = inp("inp", "Tilføj rejsende (f.eks. Louise)", "", function(v) { tn = v; });
  ti.addEventListener("keydown", function(ev) { if (ev.key === "Enter") addT(); });
  var tr = div("row"); tr.style.marginBottom = "20px";
  var ab = btn("btng btnsm", "Tilføj", addT); ab.style.flexShrink = "0";
  tr.appendChild(ti); tr.appendChild(ab); content.appendChild(tr);

  function addT() {
    if (!tn.trim()) return;
    trip.travelers.push(tn.trim()); mutateTrip(function() {}); ti.value = ""; tn = ""; refreshChips();
  }

  var sec2 = div("sec"); sec2.textContent = "Datoer"; content.appendChild(sec2);
  var dc = div("card");
  var dr = div("row");
  var sl = div(""); sl.style.flex = "1";
  var sll = mk("label", "lbl"); sll.textContent = "Fra"; sl.appendChild(sll);
  sl.appendChild(inp("inpsm", "", trip.start, function(v) { trip.start = v; mutateTrip(function() {}); }, "date"));
  var el2 = div(""); el2.style.flex = "1";
  var ell = mk("label", "lbl"); ell.textContent = "Til"; el2.appendChild(ell);
  el2.appendChild(inp("inpsm", "", trip.end, function(v) { trip.end = v; mutateTrip(function() {}); }, "date"));
  dr.appendChild(sl); dr.appendChild(el2); dc.appendChild(dr); content.appendChild(dc);

  var sec3 = div("sec"); sec3.textContent = "Ophold"; content.appendChild(sec3);
  var stopsEl = div(""); content.appendChild(stopsEl);

  function refreshStops() {
    stopsEl.innerHTML = "";
    if (!trip.stops.length) { var em = div("empty"); em.textContent = "Tilføj opholdssteder – f.eks. 5 dage i Cobisa og 2 dage i Madrid."; stopsEl.appendChild(em); return; }
    trip.stops.forEach(function(s, i) {
      var card = div("card");
      var ch = div("cardhead");
      var ico = div(""); ico.textContent = "🏠"; ico.style.fontSize = "20px";
      var cl = div("cardlbl"); cl.textContent = "Stop " + (i + 1);
      var del = btn("trash", "🗑", function() { trip.stops.splice(i, 1); mutateTrip(function() {}); refreshStops(); });
      ch.appendChild(ico); ch.appendChild(cl); ch.appendChild(del); card.appendChild(ch);
      var pi = inp("inp", "Sted (f.eks. Cobisa)", s.place, function(v) { s.place = v; mutateTrip(function() {}); }); pi.style.marginBottom = "8px";
      var dr2 = div("row"); dr2.style.marginBottom = "8px";
      var s1 = div(""); s1.style.flex = "1"; var sl1 = mk("label", "lbl"); sl1.textContent = "Ankomst"; s1.appendChild(sl1); s1.appendChild(inp("inpsm", "", s.start, function(v) { s.start = v; mutateTrip(function() {}); }, "date"));
      var e1 = div(""); e1.style.flex = "1"; var el1 = mk("label", "lbl"); el1.textContent = "Afrejse"; e1.appendChild(el1); e1.appendChild(inp("inpsm", "", s.end, function(v) { s.end = v; mutateTrip(function() {}); }, "date"));
      dr2.appendChild(s1); dr2.appendChild(e1);
      var ai = inp("inp", "Bolig / hotel navn", s.accommodation, function(v) { s.accommodation = v; mutateTrip(function() {}); }); ai.style.marginBottom = "8px";
      var li = inp("inp", "Booking-link (Airbnb, Booking.com...)", s.link, function(v) { s.link = v; mutateTrip(function() {}); });
      card.appendChild(pi); card.appendChild(dr2); card.appendChild(ai); card.appendChild(li);
      stopsEl.appendChild(card);
    });
  }
  refreshStops();

  var addStopBtn = btn("btns btnsm", "+ Tilføj ophold", function() {
    trip.stops.push({ id: uid(), place: "", start: "", end: "", accommodation: "", link: "" });
    mutateTrip(function() {}); refreshStops();
  }); addStopBtn.style.marginBottom = "20px";
  content.appendChild(addStopBtn);

  var sec4 = div("sec"); sec4.textContent = "Billetter"; content.appendChild(sec4);
  var trow = div("row"); trow.style.marginBottom = "12px";
  trow.appendChild(btn("btns btnsm", "✈ Flybillet", function() { trip.tickets.push({ id: uid(), type: "fly", from: "", to: "", date: "", time: "", ref: "" }); mutateTrip(function() {}); refreshTickets(); }));
  trow.appendChild(btn("btns btnsm", "🚂 Togbillet", function() { trip.tickets.push({ id: uid(), type: "tog", from: "", to: "", date: "", time: "", ref: "" }); mutateTrip(function() {}); refreshTickets(); }));
  content.appendChild(trow);

  var ticketsEl = div(""); content.appendChild(ticketsEl);

  function refreshTickets() {
    ticketsEl.innerHTML = "";
    if (!trip.tickets.length) { var em = div("empty"); em.textContent = "Tilføj fly- og togbilletter her."; ticketsEl.appendChild(em); return; }
    trip.tickets.forEach(function(tk, i) {
      var card = div("card");
      var ch = div("cardhead");
      var ico = div(""); ico.textContent = TRANS[tk.type].e; ico.style.fontSize = "20px";
      var cl = div("cardlbl"); cl.textContent = TRANS[tk.type].l;
      var del = btn("trash", "🗑", function() { trip.tickets.splice(i, 1); mutateTrip(function() {}); refreshTickets(); });
      ch.appendChild(ico); ch.appendChild(cl); ch.appendChild(del); card.appendChild(ch);
      var r1 = div("row"); r1.style.marginBottom = "8px";
      r1.appendChild(inp("inpsm", "Fra", tk.from, function(v) { tk.from = v; mutateTrip(function() {}); }));
      r1.appendChild(inp("inpsm", "Til", tk.to, function(v) { tk.to = v; mutateTrip(function() {}); }));
      var r2 = div("row"); r2.style.marginBottom = "8px";
      r2.appendChild(inp("inpsm", "", tk.date, function(v) { tk.date = v; mutateTrip(function() {}); }, "date"));
      r2.appendChild(inp("inpsm", "", tk.time, function(v) { tk.time = v; mutateTrip(function() {}); }, "time"));
      var ri = inp("inp", "Bookingreference / saede", tk.ref, function(v) { tk.ref = v; mutateTrip(function() {}); });
      card.appendChild(r1); card.appendChild(r2); card.appendChild(ri);
      ticketsEl.appendChild(card);
    });
  }
  refreshTickets();
}

function renderSteder(trip, content) {
  if (!trip.places) trip.places = [];

  var visited = trip.places.filter(function(p) { return p.status === "visited"; });
  var wishes = trip.places.filter(function(p) { return p.status !== "visited"; });

  var sr = div("statrow");
  var vb = div("statbox"); vb.innerHTML = '<div style="font-size:24px">✅</div><div class="statnum">' + visited.length + '</div><div class="statlbl">Besøgt</div>';
  var wb = div("statbox"); wb.innerHTML = '<div style="font-size:24px">🔖</div><div class="statnum">' + wishes.length + '</div><div class="statlbl">Ønsker</div>';
  sr.appendChild(vb); sr.appendChild(wb); content.appendChild(sr);

  var showForm = false;
  var draft = { name: "", category: "restaurant", note: "", date: "", status: "wish", source: "", link: "" };
  var formEl = div(""); var listEl = div("");
  content.appendChild(formEl); content.appendChild(listEl);

  function refreshList() {
    listEl.innerHTML = "";
    var allItems = trip.places;
    if (!allItems.length) { var em = div("empty"); em.textContent = "Tilføj steder du vil besøge eller har besøgt."; listEl.appendChild(em); return; }

    ["wish", "visited"].forEach(function(status) {
      var items = trip.places.filter(function(p) { return status === "wish" ? p.status !== "visited" : p.status === "visited"; });
      if (!items.length) return;
      var sec = div("sec"); sec.textContent = status === "wish" ? "🔖 Ønsker at besøge" : "✅ Besøgt"; listEl.appendChild(sec);

      items.forEach(function(p) {
        var cat = CATS[p.category] || CATS.andet;
        var row = div("plrow");
        var emo = div(""); emo.textContent = cat.e; emo.style.fontSize = "20px"; emo.style.flexShrink = "0";
        var info = div("plinfo");
        var pn = div("plname"); pn.textContent = p.name; info.appendChild(pn);
        var badge = div(status === "wish" ? "wishbadge" : "visitbadge"); badge.textContent = status === "wish" ? "🔖 Ønsker" : "✅ Besøgt"; info.appendChild(badge);
        if (p.note) { var pnote = div("plnote"); pnote.textContent = p.note; info.appendChild(pnote); }
        var meta = div("plmeta");
        if (p.date) meta.textContent += fmtD(p.date) + " ";
        if (p.source) meta.textContent += "Kilde: " + p.source;
        info.appendChild(meta);
        if (p.link) { var a = mk("a", ""); a.href = p.link; a.target = "_blank"; a.textContent = "🔗 Link"; a.style.fontSize = "12px"; a.style.color = "#3F5E55"; a.style.display = "block"; a.style.marginTop = "4px"; info.appendChild(a); }
        if (status === "wish") {
          var mb = btn("movebtn", "✅ Marker som besøgt", function() {
            p.status = "visited"; if (!p.date) p.date = new Date().toISOString().slice(0, 10);
            mutateTrip(function() {}); refreshList();
          });
          info.appendChild(mb);
        }
        var del = btn("trash", "🗑", function() { trip.places = trip.places.filter(function(x) { return x.id !== p.id; }); mutateTrip(function() {}); refreshList(); });
        row.appendChild(emo); row.appendChild(info); row.appendChild(del);
        listEl.appendChild(row);
      });
    });
  }

  function refreshForm() {
    formEl.innerHTML = "";
    if (!showForm) {
      formEl.appendChild(btn("ghost", "+ Tilføj sted", function() { showForm = true; refreshForm(); }));
      return;
    }
    var card = div("card");
    var ni = inp("inp", "Navn (f.eks. Le Bistrot du Vin)", "", function(v) { draft.name = v; });
    var nta = mk("textarea", "inp"); nta.placeholder = "Note – hvad er det godt for?"; nta.oninput = function() { draft.note = nta.value; };
    var si = inp("inp", "Kilde (f.eks. Wine Spectator, ven)", "", function(v) { draft.source = v; });
    var li = inp("inp", "Link til hjemmeside / anmeldelse", "", function(v) { draft.link = v; });
    var di = inp("inp", "", draft.date, function(v) { draft.date = v; }, "date");

    var pills = div("catpills");
    Object.keys(CATS).forEach(function(key) {
      var cat = CATS[key];
      var p2 = btn("catpill", cat.e + " " + cat.l, function() { draft.category = key; refreshForm(); });
      if (draft.category === key) { p2.style.borderColor = cat.c; p2.style.background = cat.c + "20"; p2.style.color = cat.c; }
      pills.appendChild(p2);
    });

    var sr2 = div("row"); sr2.style.marginBottom = "12px";
    var wb2 = btn("btnsm", "🔖 Ønsker", function() { draft.status = "wish"; refreshForm(); }); wb2.style.flex = "1";
    var vb2 = btn("btnsm", "✅ Besøgt", function() { draft.status = "visited"; refreshForm(); }); vb2.style.flex = "1";
    if (draft.status === "wish") wb2.className = "btnp btnsm"; else vb2.className = "btng btnsm";
    sr2.appendChild(wb2); sr2.appendChild(vb2);

    card.appendChild(field("Navn", ni));
    card.appendChild(field("Kategori", pills));
    card.appendChild(sr2);
    card.appendChild(field("Note", nta));
    card.appendChild(field("Kilde", si));
    card.appendChild(field("Link", li));
    if (draft.status === "visited") card.appendChild(field("Dato", di));

    var br = div("btnrow");
    var can = btn("btns", "Annuller", function() { showForm = false; draft = { name: "", category: "restaurant", note: "", date: "", status: "wish", source: "", link: "" }; refreshForm(); }); can.style.flex = "1";
    var sv = btn("btnp", "Gem sted", function() {
      if (!draft.name.trim()) return;
      trip.places.push({ id: uid(), name: draft.name, category: draft.category, note: draft.note, date: draft.date, status: draft.status, source: draft.source, link: draft.link });
      mutateTrip(function() {}); showForm = false; draft = { name: "", category: "restaurant", note: "", date: "", status: "wish", source: "", link: "" };
      refreshForm(); refreshList();
    }); sv.style.flex = "1";
    br.appendChild(can); br.appendChild(sv);
    card.appendChild(br);
    formEl.appendChild(card);
  }

  refreshForm(); refreshList();
}

function renderBudget(trip, content) {
  if (!trip.expenses) trip.expenses = [];
  var hero = div("herobox"); content.appendChild(hero);

  function calcTotal() { return trip.expenses.reduce(function(s, e) { return s + (parseFloat(e.amount) || 0); }, 0); }

  function refreshHero() {
    hero.innerHTML = "";
    var total = calcTotal();
    var budget = parseFloat(trip.budget) || 0;
    var rem = budget - total;
    var pct = budget > 0 ? Math.min(100, (total / budget) * 100) : 0;
    var bi = inp("inp", "Budget (DKK)", trip.budget, function(v) { trip.budget = v; mutateTrip(function() {}); refreshHero(); }, "number");
    bi.style.background = "rgba(255,255,255,0.15)"; bi.style.border = "1px solid rgba(255,255,255,0.3)"; bi.style.color = "#fff";
    var fl = div("field"); var lbl2 = mk("label", "lbl"); lbl2.style.color = "rgba(255,255,255,.55)"; lbl2.textContent = "Samlet budget (DKK)"; fl.appendChild(lbl2); fl.appendChild(bi);
    hero.appendChild(fl);
    var hr = div("herorow");
    var left = div(""); var ll = div("herolbl"); ll.textContent = "Brugt"; var lv = div("heroval"); lv.textContent = total.toLocaleString("da-DK") + " kr"; left.appendChild(ll); left.appendChild(lv);
    var right = div(""); right.style.textAlign = "right"; var rl = div("herolbl"); rl.textContent = "Tilbage"; var rv = div("heroval"); rv.textContent = rem.toLocaleString("da-DK") + " kr"; if (rem < 0) rv.style.color = "#FFB74D"; right.appendChild(rl); right.appendChild(rv);
    hr.appendChild(left); hr.appendChild(right); hero.appendChild(hr);
    if (budget > 0) { var pg = div("progress"); var pf = div("progfill"); pf.style.width = pct + "%"; if (total > budget) pf.style.background = "#FF7043"; pg.appendChild(pf); hero.appendChild(pg); }
  }
  refreshHero();

  var sec = div("sec"); sec.textContent = "Registrer udgift"; content.appendChild(sec);
  var card = div("card");
  var draft = { desc: "", amount: "", category: "mad" };
  var di = inp("inp", "Hvad var det? (f.eks. Frokost i Beaune)", "", function(v) { draft.desc = v; }); di.style.marginBottom = "8px";
  var r = div("row"); r.style.marginBottom = "10px";
  var ai = inp("inpsm", "Beloeb (DKK)", "", function(v) { draft.amount = v; }, "number");
  var sel = mk("select", "inpsm");
  ["mad", "transport", "ophold", "oplevelser", "vin", "andet"].forEach(function(c) { var o = mk("option", ""); o.value = c; o.textContent = c.charAt(0).toUpperCase() + c.slice(1); sel.appendChild(o); });
  sel.onchange = function() { draft.category = sel.value; };
  r.appendChild(ai); r.appendChild(sel);
  var addbtn = btn("btnp btnw", "Tilføj udgift", function() {
    if (!draft.desc.trim() || !draft.amount) return;
    trip.expenses.push({ id: uid(), desc: draft.desc, amount: parseFloat(draft.amount), category: draft.category, paidBy: "" });
    mutateTrip(function() {}); di.value = ""; ai.value = ""; draft = { desc: "", amount: "", category: "mad" };
    refreshHero(); refreshExp();
  }); addbtn.style.marginTop = "10px";
  card.appendChild(di); card.appendChild(r); card.appendChild(addbtn);
  content.appendChild(card);

  var explist = div(""); content.appendChild(explist);

  function refreshExp() {
    explist.innerHTML = "";
    if (!trip.expenses.length) return;
    var sec2 = div("sec"); sec2.textContent = "Udgifter"; explist.appendChild(sec2);
    trip.expenses.slice().reverse().forEach(function(ex) {
      var row = div("exprow");
      var info = div("expinfo");
      var desc = div("expdesc"); desc.textContent = ex.desc; info.appendChild(desc);
      var cat = div("expcat"); cat.textContent = ex.category; info.appendChild(cat);
      var amt = div("expamt"); amt.textContent = ex.amount.toLocaleString("da-DK") + " kr";
      var del = btn("trash", "🗑", function() { trip.expenses = trip.expenses.filter(function(x) { return x.id !== ex.id; }); mutateTrip(function() {}); refreshHero(); refreshExp(); });
      row.appendChild(info); row.appendChild(amt); row.appendChild(del);
      explist.appendChild(row);
    });
  }
  refreshExp();
}

function renderBilleder(trip, content) {
  if (!trip.photos) trip.photos = [];
  var fi = mk("input", "");
  fi.type = "file"; fi.accept = "image/*"; fi.multiple = true; fi.style.display = "none";
  fi.onchange = function() {
    Array.from(fi.files).forEach(function(file) {
      var r = new FileReader();
      r.onload = function() {
        trip.photos.push({ id: uid(), src: r.result, caption: "", date: new Date().toISOString().slice(0, 10) });
        mutateTrip(function() {}); refreshPhotos();
      };
      r.readAsDataURL(file);
    });
  };
  content.appendChild(fi);
  content.appendChild(btn("ghost", "📷  Tilføj billeder", function() { fi.click(); }));
  var grid = div("photogrid"); content.appendChild(grid);

  function refreshPhotos() {
    grid.innerHTML = "";
    if (!trip.photos.length) { var em = div("empty"); em.style.gridColumn = "1/-1"; em.textContent = "Tilføj billeder undervejs – de bruges i rejsebogen."; grid.appendChild(em); return; }
    trip.photos.slice().reverse().forEach(function(p) {
      var card = div("photocard");
      var wrap = div("photowrap");
      var img = mk("img", ""); img.src = p.src; img.style.width = "100%"; img.style.height = "130px"; img.style.objectFit = "cover"; img.style.display = "block";
      var del = btn("photodel", "🗑", function() { trip.photos = trip.photos.filter(function(x) { return x.id !== p.id; }); mutateTrip(function() {}); refreshPhotos(); });
      wrap.appendChild(img); wrap.appendChild(del);
      var ci = mk("input", "photocap"); ci.placeholder = "Billedtekst..."; ci.value = p.caption || ""; ci.oninput = function() { p.caption = ci.value; mutateTrip(function() {}); };
      card.appendChild(wrap); card.appendChild(ci);
      grid.appendChild(card);
    });
  }
  refreshPhotos();
}

function renderBook() {
  var trip = S.trips.find(function(t) { return t.id === S.activeTrip; });
  if (!trip) return;

  var days = [];
  if (trip.start && trip.end) {
    var cur = new Date(trip.start + "T00:00:00");
    var end = new Date(trip.end + "T00:00:00");
    while (cur <= end) { days.push(cur.toISOString().slice(0, 10)); cur.setDate(cur.getDate() + 1); }
  }

  var total = (trip.expenses || []).reduce(function(s, ex) { return s + (parseFloat(ex.amount) || 0); }, 0);
  var byCat = {};
  (trip.expenses || []).forEach(function(ex) { byCat[ex.category] = (byCat[ex.category] || 0) + ex.amount; });
  var visited = (trip.places || []).filter(function(p) { return p.status === "visited"; });

  var wrap = div("");
  var hdr = div("header");
  hdr.appendChild(btn("hbtn", "‹", function() { S.bookMode = false; render(); }));
  var ht = div("htitle"); ht.innerHTML = "<h2>Rejsebog</h2>"; hdr.appendChild(ht);
  hdr.appendChild(btn("hbtn", "🖨", function() { window.print(); }));
  wrap.appendChild(hdr);

  var page = div(""); page.style.background = "#FFFDF7";

  var cov = div(""); cov.style.background = "#3F5E55"; cov.style.padding = "60px 28px 50px"; cov.style.textAlign = "center";
  var ct = mk("h1", ""); ct.style.fontFamily = "Georgia,serif"; ct.style.fontSize = "36px"; ct.style.color = "#fff"; ct.style.marginBottom = "8px"; ct.textContent = trip.name || "Rejse";
  var cd = div(""); cd.style.fontSize = "16px"; cd.style.color = "rgba(255,255,255,.7)"; cd.textContent = trip.destination || "";
  cov.appendChild(ct); cov.appendChild(cd);
  if (trip.start || trip.end) { var cdates = div(""); cdates.style.fontSize = "13px"; cdates.style.color = "rgba(255,255,255,.5)"; cdates.style.marginTop = "12px"; cdates.textContent = fmtDL(trip.start) + (trip.end ? " – " + fmtDL(trip.end) : ""); cov.appendChild(cdates); }
  if (trip.travelers && trip.travelers.length) { var ctrav = div(""); ctrav.style.fontSize = "13px"; ctrav.style.color = "rgba(255,255,255,.55)"; ctrav.style.marginTop = "8px"; ctrav.textContent = trip.travelers.join(" · "); cov.appendChild(ctrav); }
  page.appendChild(cov);

  function addSection(title) {
    var sec = div(""); sec.style.padding = "26px 24px"; sec.style.borderBottom = "1px solid #E0D5C0"; sec.style.background = "#FFFDF7";
    var hw = div(""); hw.style.display = "flex"; hw.style.alignItems = "center"; hw.style.gap = "12px"; hw.style.marginBottom = "16px";
    var h2 = mk("h2", ""); h2.style.fontFamily = "Georgia,serif"; h2.style.fontSize = "21px"; h2.style.color = "#2F2A22"; h2.style.whiteSpace = "nowrap"; h2.textContent = title;
    var line = div(""); line.style.flex = "1"; line.style.height = "1px"; line.style.background = "#E0D5C0";
    hw.appendChild(h2); hw.appendChild(line); sec.appendChild(hw);
    page.appendChild(sec);
    return sec;
  }

  var fs = addSection("Rejsefakta");
  var fg = div(""); fg.style.display = "grid"; fg.style.gridTemplateColumns = "1fr 1fr"; fg.style.gap = "16px 20px";
  [["Destination", trip.destination || "—"], ["Antal dage", days.length || "—"], ["Rejsende", (trip.travelers || []).join(", ") || "—"], ["Besogte steder", visited.length], ["Billeder", (trip.photos || []).length], ["Forbrug", total.toLocaleString("da-DK") + " kr"]].forEach(function(pair) {
    var item = div(""); item.innerHTML = '<div style="font-size:10px;letter-spacing:.12em;text-transform:uppercase;color:#8A7A63">' + pair[0] + '</div><div style="font-size:17px;color:#2F2A22;margin-top:2px">' + pair[1] + '</div>';
    fg.appendChild(item);
  });
  fs.appendChild(fg);

  days.forEach(function(day, i) {
    var photos = (trip.photos || []).filter(function(p) { return p.date === day; });
    var places = visited.filter(function(p) { return p.date === day; });
    var tickets = (trip.tickets || []).filter(function(tk) { return tk.date === day; });
    if (!photos.length && !places.length && !tickets.length) return;
    var sec = addSection("Dag " + (i + 1) + " — " + fmtDL(day));
    tickets.forEach(function(tk) { var r = div("tkrow"); r.textContent = TRANS[tk.type].e + " " + tk.from + " → " + tk.to + (tk.time ? " kl. " + tk.time : ""); sec.appendChild(r); });
    if (photos.length) {
      var pg = div(""); pg.style.display = "grid"; pg.style.gridTemplateColumns = "1fr 1fr"; pg.style.gap = "10px"; pg.style.margin = "12px 0";
      photos.forEach(function(p) {
        var fig = mk("figure", ""); fig.style.margin = "0";
        var img = mk("img", ""); img.src = p.src; img.style.width = "100%"; img.style.height = "140px"; img.style.objectFit = "cover"; img.style.borderRadius = "8px"; img.style.display = "block";
        fig.appendChild(img);
        if (p.caption) { var cap = mk("figcaption", ""); cap.style.fontSize = "11px"; cap.style.color = "#8A7A63"; cap.style.marginTop = "4px"; cap.style.fontStyle = "italic"; cap.textContent = p.caption; fig.appendChild(cap); }
        pg.appendChild(fig);
      });
      sec.appendChild(pg);
    }
    places.forEach(function(p) { var cat = CATS[p.category] || CATS.andet; var row = div(""); row.style.display = "flex"; row.style.gap = "10px"; row.style.marginTop = "10px"; var emo = div(""); emo.textContent = cat.e; emo.style.fontSize = "18px"; var info = div(""); var pn = div(""); pn.style.fontFamily = "Georgia,serif"; pn.style.fontSize = "15px"; pn.textContent = p.name; info.appendChild(pn); if (p.note) { var pnote = div(""); pnote.style.fontSize = "13px"; pnote.style.color = "#8A7A63"; pnote.textContent = p.note; info.appendChild(pnote); } row.appendChild(emo); row.appendChild(info); sec.appendChild(row); });
  });

  if (visited.filter(function(p) { return !p.date; }).length) {
    var up = addSection("Steder og oplevelser");
    visited.filter(function(p) { return !p.date; }).forEach(function(p) { var cat = CATS[p.category] || CATS.andet; var row = div(""); row.style.marginBottom = "10px"; row.innerHTML = '<div style="font-family:Georgia,serif;font-size:15px">' + cat.e + " " + p.name + '</div>' + (p.note ? '<div style="font-size:13px;color:#8A7A63">' + p.note + '</div>' : ""); up.appendChild(row); });
  }

  var bs = addSection("Budget");
  bs.innerHTML += '<div style="display:grid;grid-template-columns:1fr 1fr;gap:16px"><div><div style="font-size:10px;color:#8A7A63;text-transform:uppercase;letter-spacing:.1em">Budget</div><div style="font-size:17px;color:#2F2A22">' + (trip.budget ? parseFloat(trip.budget).toLocaleString("da-DK") + " kr" : "—") + '</div></div><div><div style="font-size:10px;color:#8A7A63;text-transform:uppercase;letter-spacing:.1em">Forbrug</div><div style="font-size:17px;color:#2F2A22">' + total.toLocaleString("da-DK") + " kr</div></div></div>";
  Object.entries(byCat).forEach(function(entry) { bs.innerHTML += '<div style="display:flex;justify-content:space-between;font-size:14px;padding:6px 0;border-bottom:1px solid #F0E9D8"><span>' + entry[0] + '</span><span style="font-family:monospace">' + entry[1].toLocaleString("da-DK") + " kr</span></div>"; });

  var footer = div(""); footer.style.textAlign = "center"; footer.style.padding = "30px 0 20px"; footer.style.color = "#B5A98F"; footer.style.fontSize = "12px"; footer.style.fontFamily = "monospace"; footer.style.background = "#FFFDF7"; footer.textContent = "— Lavet med jeres rejsedagbog —";
  page.appendChild(footer);
  wrap.appendChild(page);
  root().appendChild(wrap);
}

if (S.unlocked) { loadTrips(); setupRT(); }
render();
</script>
</body>
</html>
