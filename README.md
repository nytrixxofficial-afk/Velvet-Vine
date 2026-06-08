<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Velvet &amp; Vine — Luxury Cafe &amp; Lounge</title>
  <meta name="description" content="Velvet &amp; Vine — premium luxury cafe & lounge. Explore menu, book tables, reserve events, and enjoy cinematic ambience." />

  <style>
    /*
      Velvet & Vine — dark luxury single-file site
      Note: This is a static fallback because the workspace tools can only see portfolio.html.
    */

    *, *::before, *::after{ box-sizing:border-box; margin:0; padding:0; }
    :root{
      --bg:#060606;
      --bg2:#0a0a0a;
      --card:rgba(255,255,255,.04);
      --card2:rgba(255,255,255,.06);
      --glass:rgba(255,255,255,.04);
      --glass-border:rgba(255,215,0,.18);
      --text:#f3f3f3;
      --muted:rgba(243,243,243,.7);
      --muted2:rgba(243,243,243,.55);
      --gold:#d7b15b;
      --gold2:#f2d27a;
      --char:#171717;
      --accent:#c89b3d;
      --accent2:#8b5a2b;
      --danger:#ff3b3b;
      --ring:rgba(215,177,91,.35);
      --shadow: 0 20px 60px rgba(0,0,0,.55);
      --shadow2: 0 10px 40px rgba(0,0,0,.35);
      --radius:18px;
      --radius2:26px;
      --max:1200px;
      --ease: cubic-bezier(.2,.8,.2,1);
    }

    html{ scroll-behavior:smooth; }
    body{
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      background: radial-gradient(1200px 600px at 20% -10%, rgba(215,177,91,.14), transparent 55%),
                  radial-gradient(900px 500px at 85% 10%, rgba(215,177,91,.08), transparent 55%),
                  linear-gradient(180deg, var(--bg), #050505 40%, #040404);
      color:var(--text);
      overflow-x:hidden;
      line-height:1.45;
    }

    a{ color:inherit; text-decoration:none; }
    img{ max-width:100%; display:block; }

    /* Subtle cinematic grain */
    .grain{
      pointer-events:none;
      position:fixed; inset:-40%;
      background-image:url('data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" width="140" height="140"%3E%3Cfilter id="n"%3E%3CfeTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="3" stitchTiles="stitch"/%3E%3C/filter%3E%3Crect width="140" height="140" filter="url(%23n)" opacity="0.35"/%3E%3C/svg%3E');
      opacity:.08;
      mix-blend-mode:overlay;
      transform: translateZ(0);
      animation: grainMove 10s steps(10) infinite;
      z-index: 0;
    }
    @keyframes grainMove{
      0%{ transform:translate(-2%, -1%); }
      10%{ transform:translate(-1%, -2%); }
      20%{ transform:translate(-3%, 0%); }
      30%{ transform:translate(0%, -3%); }
      40%{ transform:translate(-2%, -1%); }
      50%{ transform:translate(-1%, 0%); }
      60%{ transform:translate(-3%, -2%); }
      70%{ transform:translate(0%, -1%); }
      80%{ transform:translate(-2%, -3%); }
      90%{ transform:translate(-1%, -2%); }
      100%{ transform:translate(-2%, -1%); }
    }

    .wrap{ position:relative; z-index:1; }

    /* Scroll animations */
    .reveal{ opacity:0; transform: translateY(18px) scale(.98); filter: blur(6px); transition: opacity .9s var(--ease), transform .9s var(--ease), filter .9s var(--ease); }
    .reveal.on{ opacity:1; transform: translateY(0) scale(1); filter: blur(0); }

    /* Glass helpers */
    .glass{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid rgba(215,177,91,.18);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      box-shadow: var(--shadow2);
      border-radius: var(--radius);
    }

    /* Navbar */
    .nav{
      position:fixed; top:0; left:0; right:0;
      z-index:50;
      padding: 14px 16px;
      transition: background .3s var(--ease), border-color .3s var(--ease), transform .3s var(--ease);
    }
    .nav .bar{
      margin:0 auto;
      max-width: var(--max);
      display:flex; align-items:center; justify-content:space-between;
      padding: 12px 14px;
      border-radius: 999px;
      background: rgba(10,10,10,.35);
      border:1px solid rgba(215,177,91,.16);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      box-shadow: 0 10px 40px rgba(0,0,0,.35);
    }
    .nav.scrolled .bar{
      background: rgba(8,8,8,.65);
      border-color: rgba(215,177,91,.22);
    }
    .brand{
      display:flex; align-items:center; gap:10px;
      font-weight: 800;
      letter-spacing: .12em;
      text-transform: uppercase;
    }
    .brand .mark{
      width:34px; height:34px;
      border-radius: 50%;
      background: radial-gradient(circle at 30% 30%, rgba(242,210,122,.9), rgba(215,177,91,.35) 40%, rgba(0,0,0,.3) 70%);
      border: 1px solid rgba(242,210,122,.4);
      box-shadow: 0 0 0 4px rgba(215,177,91,.10), 0 0 30px rgba(215,177,91,.22);
      position:relative;
      overflow:hidden;
    }
    .brand .mark:after{
      content:"";
      position:absolute; inset:-30px;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,.22), transparent);
      transform: rotate(25deg) translateX(-40%);
      animation: sheen 4.5s var(--ease) infinite;
    }
    @keyframes sheen{
      0%{ transform: rotate(25deg) translateX(-60%); opacity:0; }
      25%{ opacity:1; }
      50%{ transform: rotate(25deg) translateX(60%); opacity:.8; }
      100%{ transform: rotate(25deg) translateX(60%); opacity:0; }
    }

    .links{ display:flex; gap: 18px; align-items:center; }
    .links a{
      font-size: 12px;
      letter-spacing: .16em;
      text-transform: uppercase;
      color: rgba(243,243,243,.78);
      padding: 8px 10px;
      border-radius: 999px;
      transition: background .2s var(--ease), color .2s var(--ease), transform .2s var(--ease);
      position:relative;
    }
    .links a:hover{
      color: rgba(242,210,122,.95);
      background: rgba(215,177,91,.12);
      transform: translateY(-1px);
    }

    .nav .right{ display:flex; gap:10px; align-items:center; }
    .pill{
      border-radius: 999px;
      padding: 10px 14px;
      border:1px solid rgba(215,177,91,.22);
      background: rgba(255,255,255,.04);
      color: rgba(242,210,122,.95);
      font-size: 12px;
      letter-spacing: .12em;
      text-transform: uppercase;
      cursor:pointer;
      transition: transform .2s var(--ease), background .2s var(--ease), box-shadow .2s var(--ease);
      display:inline-flex; align-items:center; gap:10px;
    }
    .pill:hover{
      transform: translateY(-1px);
      background: rgba(215,177,91,.10);
      box-shadow: 0 0 0 4px rgba(215,177,91,.10);
    }

    .icon-btn{ width:40px; height:40px; border-radius: 50%; border:1px solid rgba(215,177,91,.18); background: rgba(255,255,255,.04); cursor:pointer; display:grid; place-items:center; transition: transform .2s var(--ease), background .2s var(--ease); }
    .icon-btn:hover{ transform: translateY(-1px); background: rgba(215,177,91,.10); }

    .hamb{ display:none; }

    @media (max-width: 860px){
      .links{ display:none; }
      .hamb{ display:inline-grid; }
    }

    /* Mobile drawer */
    .drawer{
      position:fixed; inset:0; z-index:80;
      background: rgba(0,0,0,.58);
      display:none;
    }
    .drawer.open{ display:block; }
    .drawer .panel{
      position:absolute; top:12px; left:12px; right:12px;
      border-radius: var(--radius2);
      padding: 16px;
    }
    .drawer .panel .head{ display:flex; justify-content:space-between; align-items:center; margin-bottom: 12px; }
    .drawer .panel .head .title{ font-weight:800; letter-spacing:.12em; text-transform:uppercase; color: rgba(242,210,122,.95); }
    .drawer .menu{ display:flex; flex-direction:column; gap:10px; }
    .drawer .menu a{
      padding: 14px 14px;
      border-radius: 14px;
      border:1px solid rgba(215,177,91,.18);
      background: rgba(255,255,255,.03);
      color: rgba(243,243,243,.86);
      letter-spacing:.12em; text-transform:uppercase; font-size:12px;
    }

    /* Hero */
    .hero{ min-height: 100svh; padding-top: 98px; display:grid; place-items:center; position:relative; overflow:hidden; }
    .hero .bg{
      position:absolute; inset:-2px;
      background:
        radial-gradient(900px 520px at 22% 14%, rgba(215,177,91,.22), transparent 60%),
        radial-gradient(800px 460px at 78% 18%, rgba(215,177,91,.14), transparent 65%),
        linear-gradient(180deg, rgba(0,0,0,.0) 0%, rgba(0,0,0,.65) 70%, rgba(0,0,0,.85) 100%),
        url('https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?auto=format&fit=crop&w=2400&q=70');
      background-size: cover; background-position:center;
      filter: saturate(1.1) contrast(1.05);
      transform: scale(1.03);
    }
    .hero .vignette{ position:absolute; inset:0; background: radial-gradient(circle at 50% 30%, transparent 0%, rgba(0,0,0,.35) 55%, rgba(0,0,0,.8) 100%); }
    .hero .content{ position:relative; z-index:2; width:min(var(--max), 100%); padding: 24px 16px 38px; }

    .kicker{
      display:inline-flex; align-items:center; gap:10px;
      padding: 10px 14px;
      border-radius: 999px;
      border:1px solid rgba(215,177,91,.22);
      background: rgba(255,255,255,.05);
      color: rgba(242,210,122,.95);
      letter-spacing:.2em;
      text-transform:uppercase;
      font-size:12px;
      margin-bottom: 18px;
    }

    .hero h1{
      font-size: clamp(38px, 6vw, 72px);
      line-height: 1.02;
      font-weight: 900;
      letter-spacing: .04em;
      margin-bottom: 18px;
      text-shadow: 0 18px 60px rgba(0,0,0,.65);
    }
    .hero h1 .grad{
      background: linear-gradient(90deg, var(--gold2), rgba(255,255,255,.92) 22%, var(--gold));
      -webkit-background-clip:text; background-clip:text; color:transparent;
    }
    .hero p{
      max-width: 720px;
      color: rgba(243,243,243,.78);
      font-size: 16px;
      margin-bottom: 26px;
    }

    .hero .ctaRow{ display:flex; flex-wrap:wrap; gap:12px; align-items:center; }

    .btn{
      border-radius: 999px;
      border:1px solid rgba(215,177,91,.28);
      background: rgba(255,255,255,.04);
      color: rgba(242,210,122,.95);
      padding: 12px 16px;
      font-weight: 700;
      letter-spacing: .14em;
      text-transform: uppercase;
      font-size: 12px;
      cursor:pointer;
      transition: transform .25s var(--ease), background .25s var(--ease), box-shadow .25s var(--ease), border-color .25s var(--ease);
      display:inline-flex; align-items:center; gap:10px;
      user-select:none;
    }
    .btn:hover{ transform: translateY(-2px); background: rgba(215,177,91,.10); box-shadow: 0 0 0 6px rgba(215,177,91,.10); }

    .btn.primary{
      background: linear-gradient(180deg, rgba(215,177,91,.22), rgba(215,177,91,.10));
      border-color: rgba(215,177,91,.42);
      color: rgba(10,10,10,.95);
      box-shadow: 0 20px 60px rgba(215,177,91,.10);
    }
    .btn.primary span{ color: rgba(10,10,10,.95); }
    .btn.primary:hover{ background: linear-gradient(180deg, rgba(242,210,122,.30), rgba(215,177,91,.16)); }

    .hero .statsStrip{
      margin-top: 26px;
      display:grid;
      grid-template-columns: repeat(3, minmax(0,1fr));
      gap: 12px;
    }
    @media (max-width: 720px){ .hero .statsStrip{ grid-template-columns: 1fr; } }

    .stat{
      padding: 14px 14px;
      border-radius: 16px;
      border:1px solid rgba(215,177,91,.18);
      background: rgba(255,255,255,.03);
      backdrop-filter: blur(10px);
    }
    .stat .n{ font-size: 22px; font-weight: 900; letter-spacing:.06em; color: rgba(242,210,122,.95); }
    .stat .l{ margin-top: 6px; font-size: 12px; letter-spacing:.16em; text-transform:uppercase; color: rgba(243,243,243,.65); }

    /* Sections */
    section{ padding: 84px 16px; }
    .container{ width:min(var(--max), 100%); margin: 0 auto; }
    .secHead{ display:flex; align-items:flex-end; justify-content:space-between; gap: 18px; margin-bottom: 28px; flex-wrap:wrap; }
    .secHead .left{ max-width: 720px; }
    .secLabel{ color: rgba(242,210,122,.95); letter-spacing:.2em; text-transform:uppercase; font-size:12px; margin-bottom: 10px; }
    .secTitle{ font-size: clamp(26px, 3.4vw, 40px); font-weight: 900; letter-spacing:.04em; }
    .secSub{ margin-top: 10px; color: rgba(243,243,243,.7); }

    .grid3{ display:grid; grid-template-columns: repeat(3, minmax(0,1fr)); gap: 14px; }
    @media (max-width: 980px){ .grid3{ grid-template-columns: 1fr; } }
    .grid2{ display:grid; grid-template-columns: repeat(2, minmax(0,1fr)); gap: 14px; }
    @media (max-width: 980px){ .grid2{ grid-template-columns: 1fr; } }

    .card{
      border-radius: var(--radius);
      padding: 18px;
      background: rgba(255,255,255,.03);
      border:1px solid rgba(215,177,91,.16);
      backdrop-filter: blur(12px);
      box-shadow: 0 14px 50px rgba(0,0,0,.35);
      transition: transform .25s var(--ease), border-color .25s var(--ease), background .25s var(--ease);
      position:relative;
      overflow:hidden;
    }
    .card::after{
      content:"";
      position:absolute; inset:-2px;
      background: linear-gradient(120deg, transparent 0%, rgba(242,210,122,.22) 22%, transparent 45%);
      transform: translateX(-60%);
      transition: transform .65s var(--ease);
      opacity:.7;
      pointer-events:none;
    }
    .card:hover{ transform: translateY(-4px); border-color: rgba(215,177,91,.30); background: rgba(255,255,255,.04); }
    .card:hover::after{ transform: translateX(40%); }

    .media{
      border-radius: 16px;
      height: 168px;
      background:
        radial-gradient(700px 240px at 20% 10%, rgba(215,177,91,.22), transparent 55%),
        linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02)),
        url('https://images.unsplash.com/photo-1544145945-f90425340c7e?auto=format&fit=crop&w=1600&q=70');
      background-size: cover; background-position:center;
      border: 1px solid rgba(215,177,91,.18);
      overflow:hidden;
      position:relative;
    }
    .media::before{
      content:"";
      position:absolute; inset:0;
      background: linear-gradient(90deg, rgba(0,0,0,.55), transparent 45%),
                  linear-gradient(180deg, transparent 0%, rgba(0,0,0,.6) 100%);
    }

    /* Menu filter */
    .toolbar{ display:flex; flex-wrap:wrap; gap:10px; align-items:center; justify-content:space-between; margin-bottom: 18px; }
    .chips{ display:flex; flex-wrap:wrap; gap:10px; }
    .chip{
      padding: 10px 14px;
      border-radius: 999px;
      border:1px solid rgba(215,177,91,.18);
      background: rgba(255,255,255,.03);
      color: rgba(243,243,243,.78);
      cursor:pointer;
      font-size:12px;
      letter-spacing:.12em;
      text-transform:uppercase;
      transition: transform .2s var(--ease), background .2s var(--ease), color .2s var(--ease), border-color .2s var(--ease);
      user-select:none;
    }
    .chip:hover{ transform: translateY(-1px); background: rgba(215,177,91,.10); border-color: rgba(215,177,91,.28); color: rgba(242,210,122,.95); }
    .chip.on{ background: rgba(215,177,91,.14); border-color: rgba(215,177,91,.35); color: rgba(242,210,122,.98); }

    .search{
      display:flex; gap:10px; align-items:center;
      flex: 1;
      justify-content:flex-end;
    }
    .search input{
      width: min(420px, 100%);
      padding: 12px 14px;
      border-radius: 14px;
      border:1px solid rgba(215,177,91,.18);
      background: rgba(0,0,0,.18);
      color: rgba(243,243,243,.92);
      outline:none;
    }
    .search input::placeholder{ color: rgba(243,243,243,.45); }

    .menuGrid{ display:grid; grid-template-columns: repeat(3, minmax(0,1fr)); gap: 14px; }
    @media (max-width: 980px){ .menuGrid{ grid-template-columns: 1fr; } }

    .itemHead{ display:flex; justify-content:space-between; align-items:flex-start; gap: 10px; }
    .itemName{ font-weight: 900; letter-spacing:.03em; }
    .price{ color: rgba(242,210,122,.95); font-weight: 900; }
    .desc{ margin-top: 10px; color: rgba(243,243,243,.68); font-size: 13.5px; }
    .tagRow{ display:flex; flex-wrap:wrap; gap: 8px; margin-top: 12px; }
    .tag{
      font-size: 11px;
      padding: 8px 10px;
      border-radius: 999px;
      border:1px solid rgba(215,177,91,.16);
      color: rgba(243,243,243,.72);
      background: rgba(255,255,255,.03);
      letter-spacing:.08em;
      text-transform:uppercase;
    }

    /* Reviews slider */
    .slider{
      position:relative;
      overflow:hidden;
      border-radius: var(--radius2);
      border:1px solid rgba(215,177,91,.16);
      background: rgba(255,255,255,.03);
      backdrop-filter: blur(12px);
      box-shadow: 0 14px 50px rgba(0,0,0,.35);
      padding: 20px;
    }
    .slides{ display:flex; transition: transform .6s var(--ease); }
    .slide{ min-width:100%; padding: 10px; }
    .quote{ font-size: 18px; font-weight: 700; color: rgba(243,243,243,.9); }
    .by{ margin-top: 12px; color: rgba(242,210,122,.95); letter-spacing:.12em; text-transform:uppercase; font-size:12px; }
    .slider .controls{ display:flex; justify-content:space-between; margin-top: 14px; }

    /* Gallery */
    .masonry{ column-count: 3; column-gap: 14px; }
    @media (max-width: 1000px){ .masonry{ column-count: 2; } }
    @media (max-width: 680px){ .masonry{ column-count: 1; } }
    .gItem{ break-inside:avoid; margin-bottom: 14px; border-radius: 18px; overflow:hidden; border:1px solid rgba(215,177,91,.16); background: rgba(255,255,255,.03); }
    .gItem button{ width:100%; padding:0; border:0; background:transparent; cursor:pointer; display:block; }
    .gItem .img{
      height: 220px;
      background-size: cover;
      background-position:center;
      position:relative;
    }
    .gItem .img:after{
      content:""; position:absolute; inset:0;
      background: linear-gradient(180deg, transparent 30%, rgba(0,0,0,.55) 100%);
      opacity:.85;
      transition: opacity .25s var(--ease);
    }
    .gItem:hover .img:after{ opacity:.65; }
    .gItem .cap{ padding: 12px 14px; display:flex; justify-content:space-between; align-items:center; gap:10px; }
    .gItem .cap .t{ font-weight: 800; letter-spacing:.04em; color: rgba(243,243,243,.88); }
    .gItem .cap .c{ font-size: 12px; color: rgba(242,210,122,.95); letter-spacing:.12em; text-transform:uppercase; }

    /* Lightbox */
    .lightbox{ position:fixed; inset:0; z-index:120; background: rgba(0,0,0,.75); display:none; padding: 18px; }
    .lightbox.open{ display:block; }
    .lightbox .box{
      margin: 4vh auto 0;
      width: min(1100px, 100%);
      border-radius: 22px;
      overflow:hidden;
      border:1px solid rgba(215,177,91,.22);
      background: rgba(255,255,255,.03);
      backdrop-filter: blur(12px);
    }
    .lightbox img{ width:100%; height: auto; max-height: 70vh; object-fit:cover; }
    .lightbox .top{
      display:flex; justify-content:space-between; align-items:center;
      padding: 12px 14px;
      border-bottom: 1px solid rgba(215,177,91,.18);
    }
    .lightbox .top .title{ color: rgba(242,210,122,.95); letter-spacing:.12em; text-transform:uppercase; font-size:12px; font-weight:900; }
    .xbtn{ width:40px; height:40px; border-radius: 50%; border:1px solid rgba(215,177,91,.18); background: rgba(255,255,255,.04); cursor:pointer; color: rgba(243,243,243,.9); }

    /* Floating buttons */
    .float{
      position:fixed;
      right: 16px;
      bottom: 16px;
      z-index: 90;
      display:flex;
      flex-direction:column;
      gap: 12px;
    }
    .fab{
      border-radius: 999px;
      padding: 12px 14px;
      border:1px solid rgba(215,177,91,.26);
      background: rgba(8,8,8,.65);
      color: rgba(242,210,122,.95);
      cursor:pointer;
      display:flex; align-items:center; gap:10px;
      box-shadow: 0 18px 50px rgba(0,0,0,.45);
      backdrop-filter: blur(14px);
      transition: transform .25s var(--ease), background .25s var(--ease);
      user-select:none;
    }
    .fab:hover{ transform: translateY(-3px); background: rgba(215,177,91,.10); }

    /* Footer */
    footer{ padding: 46px 16px; border-top: 1px solid rgba(215,177,91,.14); background: rgba(0,0,0,.25); }
    .footerGrid{ display:grid; grid-template-columns: 1.4fr 1fr 1fr; gap: 14px; align-items:start; }
    @media (max-width: 900px){ .footerGrid{ grid-template-columns:1fr; } }
    .footTitle{ font-weight: 900; letter-spacing:.12em; text-transform:uppercase; color: rgba(242,210,122,.95); margin-bottom: 12px; }
    .footText{ color: rgba(243,243,243,.68); }
    .footLinks{ display:flex; flex-direction:column; gap:10px; }
    .footLinks a{ color: rgba(243,243,243,.7); }
    .footLinks a:hover{ color: rgba(242,210,122,.95); }
    .hours{ display:flex; flex-direction:column; gap:8px; }
    .row{ display:flex; justify-content:space-between; gap: 14px; color: rgba(243,243,243,.72); }
    .copyright{ margin-top: 24px; color: rgba(243,243,243,.45); font-size: 12px; letter-spacing:.12em; text-transform:uppercase; }

    /* Reduced motion */
    @media (prefers-reduced-motion: reduce){
      *{ animation: none !important; transition: none !important; scroll-behavior: auto !important; }
      .reveal{ opacity:1; transform:none; filter:none; }
    }

  </style>
</head>
<body>
  <div class="grain"></div>

  <div class="wrap">
    <!-- NAV -->
    <header class="nav" id="topNav">
      <div class="bar">
        <a class="brand" href="#home" aria-label="Velvet & Vine Home">
          <span class="mark" aria-hidden="true"></span>
          <span>Velvet &amp; Vine</span>
        </a>

        <nav class="links" aria-label="Primary">
          <a href="#home">Home</a>
          <a href="#about">About</a>
          <a href="#menu">Menu</a>
          <a href="#events">Events</a>
          <a href="#gallery">Gallery</a>
          <a href="#reservations">Reservations</a>
          <a href="#contact">Contact</a>
        </nav>

        <div class="right">
          <button class="icon-btn hamb" id="hambBtn" aria-label="Open menu">☰</button>
          <button class="pill" id="modeBtn" aria-label="Toggle dark/light">Dark Mode</button>
          <a class="pill" href="#reservations" style="text-decoration:none;" aria-label="Book table">Book Table</a>
        </div>
      </div>
    </header>

    <!-- Mobile drawer -->
    <div class="drawer" id="drawer" role="dialog" aria-modal="true" aria-label="Mobile menu">
      <div class="panel glass">
        <div class="head">
          <div class="title">Velvet &amp; Vine</div>
          <button class="xbtn" id="drawerClose" aria-label="Close">✕</button>
        </div>
        <div class="menu">
          <a href="#home">Home</a>
          <a href="#about">About Us</a>
          <a href="#menu">Menu</a>
          <a href="#events">Events</a>
          <a href="#gallery">Gallery</a>
          <a href="#reservations">Reservations</a>
          <a href="#contact">Contact</a>
        </div>
      </div>
    </div>

    <!-- HERO -->
    <main>
      <section class="hero" id="home">
        <div class="bg" aria-hidden="true"></div>
        <div class="vignette" aria-hidden="true"></div>

        <div class="content">
          <div class="kicker reveal">Luxury Cafe • Lounge • Live Nights</div>

          <div class="reveal" style="transition-delay:.1s;">
            <h1><span class="grad">Cinematic comfort</span>,
              crafted in velvet &amp; served with gold.</h1>
            <p>
              Velvet &amp; Vine is where espresso rituals meet late-night lounge energy—premium bites,
              signature drinks, and ambience that feels like a private screening.
            </p>
            <div class="ctaRow">
              <a class="btn primary" href="#reservations"><span>Book Table</span> →</a>
              <a class="btn" href="#menu">Explore Menu</a>
              <a class="btn" href="#events">See Events</a>
            </div>
          </div>

          <div class="hero statsStrip reveal" style="transition-delay:.25s;">
            <div class="stat">
              <div class="n" data-count="120">0</div>
              <div class="l">Signature Dishes</div>
            </div>
            <div class="stat">
              <div class="n" data-count="48">0</div>
              <div class="l">Avg. Reviews Rate</div>
            </div>
            <div class="stat">
              <div class="n" data-count="7">0</div>
              <div class="l">Events / Week</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Featured dishes -->
      <section id="featured">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Featured</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">Premium plates, designed to linger</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Handpicked highlights from our kitchen—rich, balanced, and unmistakably Velvet &amp; Vine.</div>
            </div>
          </div>

          <div class="grid3">
            <article class="card reveal">
              <div class="media" style="background-image:url('https://images.unsplash.com/photo-1541544741938-0af808871cc0?auto=format&fit=crop&w=1600&q=70');"></div>
              <div class="itemHead" style="margin-top:14px;">
                <div>
                  <div class="itemName">Truffle Noir Risotto</div>
                  <div class="desc">Creamy arborio, truffle essence, parmesan veil, and golden oil finish.</div>
                </div>
                <div class="price">₹ 699</div>
              </div>
              <div class="tagRow"><span class="tag">Signature</span><span class="tag">Vegetarian</span></div>
            </article>

            <article class="card reveal" style="transition-delay:.08s;">
              <div class="media" style="background-image:url('https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=1600&q=70');"></div>
              <div class="itemHead" style="margin-top:14px;">
                <div>
                  <div class="itemName">Velvet Spiced Chicken</div>
                  <div class="desc">Charcoal-seared chicken, warm spices, citrus glaze, and herb couture.</div>
                </div>
                <div class="price">₹ 749</div>
              </div>
              <div class="tagRow"><span class="tag">Best Seller</span><span class="tag">Non-Veg</span></div>
            </article>

            <article class="card reveal" style="transition-delay:.16s;">
              <div class="media" style="background-image:url('https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&w=1600&q=70');"></div>
              <div class="itemHead" style="margin-top:14px;">
                <div>
                  <div class="itemName">Goldleaf Chocolate Cake</div>
                  <div class="desc">Dense cocoa crumb, silky ganache, and a shimmer of edible gold.</div>
                </div>
                <div class="price">₹ 399</div>
              </div>
              <div class="tagRow"><span class="tag">Dessert</span><span class="tag">Premium</span></div>
            </article>
          </div>
        </div>
      </section>

      <!-- About -->
      <section id="about" style="padding-top:40px;">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">About Us</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">A lounge built like a cinematic set</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Our story is simple: craft beauty in every course, every pour, every moment.</div>
            </div>
          </div>

          <div class="grid2">
            <div class="card reveal" style="padding:22px;">
              <h3 style="font-size:18px; letter-spacing:.06em;">The Velvet Tale</h3>
              <p class="footText" style="margin-top:10px; font-size:14.5px; line-height:1.8;">
                Velvet &amp; Vine began as a late-night idea: a cafe where the lighting is soft,
                the service is precise, and the sound feels like velvet against glass.
                From the first espresso to the final dessert—everything is designed for elegance.
              </p>
              <div class="tagRow" style="margin-top:14px;">
                <span class="tag">Dark Luxury</span>
                <span class="tag">Glassmorphism</span>
                <span class="tag">Cinematic Ambience</span>
              </div>
            </div>

            <div class="card reveal" style="padding:22px; transition-delay:.1s;">
              <h3 style="font-size:18px; letter-spacing:.06em;">Founder Spotlight</h3>
              <p class="footText" style="margin-top:10px; font-size:14.5px; line-height:1.8;">
                Our founder believes hospitality should feel personal—like you’ve been invited.
                Every menu item is developed with a lounge mindset: rich textures, clean finishes,
                and signature moments.
              </p>
              <div class="tagRow" style="margin-top:14px;">
                <span class="tag">Craft-first</span>
                <span class="tag">Premium sourcing</span>
                <span class="tag">Service precision</span>
              </div>
            </div>
          </div>

          <div class="grid3" style="margin-top:14px;">
            <div class="card reveal" style="transition-delay:.08s;">
              <div class="secLabel" style="margin:0 0 8px;">Interior Showcase</div>
              <div class="footText">Dark wood, golden reflections, smooth glass panels, and quiet corners.</div>
            </div>
            <div class="card reveal" style="transition-delay:.14s;">
              <div class="secLabel" style="margin:0 0 8px;">Team Energy</div>
              <div class="footText">From bar to floor, we keep it calm, attentive, and flawless.</div>
            </div>
            <div class="card reveal" style="transition-delay:.2s;">
              <div class="secLabel" style="margin:0 0 8px;">Premium Lighting</div>
              <div class="footText">Cinematic contrast built for photos and late conversations.</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Menu -->
      <section id="menu">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Menu</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">Interactive categories + search</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Filter by food/drinks and find your mood instantly.</div>
            </div>
          </div>

          <div class="toolbar reveal">
            <div class="chips" id="chips">
              <div class="chip on" data-filter="all">All</div>
              <div class="chip" data-filter="food">Food</div>
              <div class="chip" data-filter="drinks">Drinks</div>
              <div class="chip" data-filter="signature">Signature</div>
            </div>
            <div class="search">
              <input id="menuSearch" placeholder="Search dishes, drinks, flavors…" />
            </div>
          </div>

          <div class="menuGrid" id="menuGrid">
            <!-- Items injected by JS -->
          </div>
        </div>
      </section>

      <!-- Events -->
      <section id="events">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Events</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">DJ nights • Live music • Sufi nights</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Book your vibe. Reserve your seats.</div>
            </div>
          </div>

          <div class="grid3">
            <article class="card reveal">
              <div class="itemName">DJ Nights</div>
              <div class="desc">Deep house, disco overlays, and late-night lounge remixes.</div>
              <div class="tagRow"><span class="tag">Fri • 10PM</span><span class="tag">Limited Seats</span></div>
            </article>
            <article class="card reveal" style="transition-delay:.1s;">
              <div class="itemName">Live Music</div>
              <div class="desc">Acoustic sets + modern covers—soft, premium, memorable.</div>
              <div class="tagRow"><span class="tag">Sat • 8:30PM</span><span class="tag">Reservations</span></div>
            </article>
            <article class="card reveal" style="transition-delay:.2s;">
              <div class="itemName">Sufi Nights</div>
              <div class="desc">Qawwali-inspired ambience and soulful evenings of velvet sound.</div>
              <div class="tagRow"><span class="tag">Sun • 7PM</span><span class="tag">Cultural Lounge</span></div>
            </article>
          </div>

          <div class="grid2" style="margin-top:14px;">
            <div class="card reveal" style="transition-delay:.08s;">
              <div class="itemName">Sports Screening</div>
              <div class="desc">Premium screens, curated snacks, and big-match energy.</div>
              <div class="tagRow"><span class="tag">Match Days</span><span class="tag">Group Bookings</span></div>
            </div>

            <div class="card reveal" style="transition-delay:.16s;">
              <div class="itemName">Event Booking Form</div>
              <div class="desc">Tell us your date, seats, and vibe. We’ll confirm quickly.</div>
              <form id="eventForm" style="margin-top:14px; display:grid; gap:10px;">
                <input required name="name" placeholder="Full Name" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <input required name="phone" placeholder="Phone / WhatsApp" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <input required type="date" name="date" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <select name="event" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);">
                  <option>DJ Nights</option>
                  <option>Live Music</option>
                  <option>Sufi Nights</option>
                  <option>Sports Screening</option>
                </select>
                <input required type="number" min="1" max="20" name="seats" placeholder="Seats (1-20)" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <textarea name="note" placeholder="Special request (optional)" rows="3" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);"></textarea>

                <button class="btn primary" type="submit" style="justify-content:center;">Submit Booking</button>
                <div id="eventMsg" style="color: rgba(242,210,122,.95); font-size:12px; letter-spacing:.12em; text-transform:uppercase; min-height:18px;"></div>
              </form>
            </div>
          </div>
        </div>
      </section>

      <!-- Gallery -->
      <section id="gallery">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Gallery</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">Masonry layout + lightbox</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Explore Food, Drinks, and Ambience categories.</div>
            </div>
          </div>

          <div class="toolbar reveal">
            <div class="chips" id="gChips">
              <div class="chip on" data-g="all">All</div>
              <div class="chip" data-g="food">Food</div>
              <div class="chip" data-g="drinks">Drinks</div>
              <div class="chip" data-g="ambience">Ambience</div>
            </div>
          </div>

          <div class="masonry" id="masonry">
            <!-- JS -->
          </div>
        </div>
      </section>

      <!-- Reservations -->
      <section id="reservations">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Reservations</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">Online table booking</div>
              <div class="secSub reveal" style="transition-delay:.15s;">Guest count, date &amp; time, special requests—premium and fast.</div>
            </div>
          </div>

          <div class="grid2">
            <div class="card reveal">
              <div class="itemName">Quick Booking</div>
              <div class="desc">This static demo simulates booking submission.</div>

              <form id="reserveForm" style="margin-top:14px; display:grid; gap:10px;">
                <input required name="name" placeholder="Full Name" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <input required name="phone" placeholder="Phone / WhatsApp" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />

                <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px;">
                  <div>
                    <div style="font-size:12px; letter-spacing:.12em; text-transform:uppercase; color: rgba(242,210,122,.95); margin-bottom:6px;">Guests</div>
                    <input required type="number" min="1" max="12" name="guests" value="2" style="width:100%; padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                  </div>
                  <div>
                    <div style="font-size:12px; letter-spacing:.12em; text-transform:uppercase; color: rgba(242,210,122,.95); margin-bottom:6px;">Time</div>
                    <input required type="time" name="time" value="19:30" style="width:100%; padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                  </div>
                </div>

                <div>
                  <div style="font-size:12px; letter-spacing:.12em; text-transform:uppercase; color: rgba(242,210,122,.95); margin-bottom:6px;">Date</div>
                  <input required type="date" name="date" style="width:100%; padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                </div>

                <textarea name="request" rows="3" placeholder="Special request (allergies, occasion, seating)" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);"></textarea>

                <button class="btn primary" type="submit" style="justify-content:center;">Confirm Reservation</button>
                <div id="reserveMsg" style="color: rgba(242,210,122,.95); font-size:12px; letter-spacing:.12em; text-transform:uppercase; min-height:18px;"></div>
              </form>
            </div>

            <div class="card reveal" style="transition-delay:.1s;">
              <div class="itemName">Customer Reviews</div>
              <div class="desc">Premium service, consistent taste, and the kind of ambience people remember.</div>
              <div class="slider" style="margin-top:14px;">
                <div class="slides" id="slides" style="transform: translateX(0%);">
                  <div class="slide">
                    <div class="quote">“Gold-level hospitality. The ambience is pure luxury.”</div>
                    <div class="by">— Anaya R.</div>
                  </div>
                  <div class="slide">
                    <div class="quote">“Every dish felt curated—like a tasting show.”</div>
                    <div class="by">— Kabir S.</div>
                  </div>
                  <div class="slide">
                    <div class="quote">“Booked for friends; ended up staying for the lounge set.”</div>
                    <div class="by">— Farah K.</div>
                  </div>
                </div>
                <div class="controls">
                  <button class="pill" id="prevBtn" style="padding:10px 12px;">← Prev</button>
                  <button class="pill" id="nextBtn" style="padding:10px 12px;">Next →</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact -->
      <section id="contact" style="padding-top:40px;">
        <div class="container">
          <div class="secHead">
            <div class="left">
              <div class="secLabel reveal">Contact</div>
              <div class="secTitle reveal" style="transition-delay:.08s;">Google Maps, message, hours</div>
              <div class="secSub reveal" style="transition-delay:.15s;">We respond quickly. For urgent bookings—use WhatsApp.</div>
            </div>
          </div>

          <div class="grid2">
            <div class="card reveal">
              <div class="itemName">Find us</div>
              <div class="desc">Map placeholder (replace with real embed link).</div>
              <div style="margin-top:12px; border-radius:16px; overflow:hidden; border:1px solid rgba(215,177,91,.16); background:rgba(0,0,0,.2);">
                <iframe title="Map" style="width:100%; height:320px; border:0; filter:saturate(1.05) contrast(1.05);" loading="lazy" referrerpolicy="no-referrer-when-downgrade"
                  src="https://www.google.com/maps?q=London&output=embed"></iframe>
              </div>
            </div>

            <div class="card reveal" style="transition-delay:.1s;">
              <div class="itemName">Contact form</div>
              <div class="desc">This demo simulates sending.</div>
              <form id="contactForm" style="margin-top:14px; display:grid; gap:10px;">
                <input required name="name" placeholder="Your Name" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <input required type="email" name="email" placeholder="Email" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);" />
                <textarea required name="msg" rows="3" placeholder="How can we help?" style="padding:12px 14px; border-radius:14px; border:1px solid rgba(215,177,91,.18); background: rgba(0,0,0,.18); color:rgba(243,243,243,.92);"></textarea>
                <button class="btn primary" type="submit" style="justify-content:center;">Send Message</button>
                <div id="contactMsg" style="color: rgba(242,210,122,.95); font-size:12px; letter-spacing:.12em; text-transform:uppercase; min-height:18px;"></div>
              </form>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer -->
      <footer>
        <div class="container">
          <div class="footerGrid">
            <div>
              <div class="footTitle">Velvet &amp; Vine</div>
              <div class="footText">Premium cafe &amp; lounge with cinematic ambience—made for reservations, celebrations, and late-night calm.</div>
              <div class="copyright">© 2026 Velvet &amp; Vine</div>
            </div>
            <div>
              <div class="footTitle">Contact</div>
              <div class="footLinks">
                <a href="mailto:hello@velvetandvine.com">hello@velvetandvine.com</a>
                <a href="tel:+910000000000">+91 00000 00000</a>
                <a href="#reservations">Reservations</a>
              </div>
            </div>
            <div>
              <div class="footTitle">Hours</div>
              <div class="hours">
                <div class="row"><span>Mon–Thu</span><span>12:00 PM – 1:00 AM</span></div>
                <div class="row"><span>Fri</span><span>12:00 PM – 2:00 AM</span></div>
                <div class="row"><span>Sat</span><span>11:00 AM – 2:30 AM</span></div>
                <div class="row"><span>Sun</span><span>11:00 AM – 1:00 AM</span></div>
              </div>
            </div>
          </div>
        </div>
      </footer>
    </main>

    <!-- Floating buttons -->
    <div class="float" aria-label="Quick actions">
      <a class="fab" href="#reservations"><span>Reserve</span> ✦</a>
      <a class="fab" href="https://wa.me/910000000000" target="_blank" rel="noopener noreferrer"><span>WhatsApp</span> ♡</a>
    </div>

    <!-- Lightbox -->
    <div class="lightbox" id="lightbox" role="dialog" aria-modal="true" aria-label="Image preview">
      <div class="box">
        <div class="top">
          <div class="title" id="lbTitle">Preview</div>
          <button class="xbtn" id="lbClose" aria-label="Close preview">✕</button>
        </div>
        <div>
          <img id="lbImg" alt="Gallery preview" src="" />
        </div>
      </div>
    </div>
  </div>

  <script>
    // Reveal on scroll (fast)
    const revealEls = Array.from(document.querySelectorAll('.reveal'));
    const obs = new IntersectionObserver((entries)=>{
      for(const e of entries){
        if(e.isIntersecting){ e.target.classList.add('on'); obs.unobserve(e.target); }
      }
    }, { threshold: 0.14 });
    revealEls.forEach(el=>obs.observe(el));

    // Navbar scroll effect
    const nav = document.getElementById('topNav');
    const onScroll = ()=>{
      if(window.scrollY > 14) nav.classList.add('scrolled'); else nav.classList.remove('scrolled');
    };
    window.addEventListener('scroll', onScroll, { passive:true });
    onScroll();

    // Mobile drawer
    const drawer = document.getElementById('drawer');
    const hambBtn = document.getElementById('hambBtn');
    const drawerClose = document.getElementById('drawerClose');
    hambBtn?.addEventListener('click', ()=>drawer.classList.add('open'));
    drawerClose?.addEventListener('click', ()=>drawer.classList.remove('open'));
    drawer?.addEventListener('click', (e)=>{ if(e.target===drawer) drawer.classList.remove('open'); });
    document.querySelectorAll('.drawer a')?.forEach(a=>a.addEventListener('click', ()=>drawer.classList.remove('open')));

    // Dark/Light mode toggle (luxury minimal)
    const modeBtn = document.getElementById('modeBtn');
    let isLight = false;
    modeBtn?.addEventListener('click', ()=>{
      isLight = !isLight;
      if(isLight){
        document.documentElement.style.setProperty('--bg', '#f7f3ea');
        document.documentElement.style.setProperty('--bg2', '#ffffff');
        document.documentElement.style.setProperty('--text', '#111');
        modeBtn.textContent = 'Light Mode';
        document.body.style.background = 'radial-gradient(1200px 600px at 20% -10%, rgba(215,177,91,.28), transparent 55%), radial-gradient(900px 500px at 85% 10%, rgba(215,177,91,.15), transparent 55%), linear-gradient(180deg, #f7f3ea, #f2ead8 40%, #efe5cf)';
      } else {
        document.documentElement.style.setProperty('--bg', '#060606');
        document.documentElement.style.setProperty('--bg2', '#0a0a0a');
        document.documentElement.style.setProperty('--text', '#f3f3f3');
        modeBtn.textContent = 'Dark Mode';
        document.body.style.background = '';
      }
    });

    // Count-up
    const counts = Array.from(document.querySelectorAll('[data-count]'));
    const countObs = new IntersectionObserver((entries)=>{
      for(const e of entries){
        if(!e.isIntersecting) continue;
        const el = e.target;
        const target = Number(el.getAttribute('data-count'));
        const start = 0;
        const dur = 900;
        const t0 = performance.now();
        const tick = (t)=>{
          const p = Math.min(1, (t - t0) / dur);
          const eased = 1 - Math.pow(1 - p, 3);
          el.textContent = String(Math.round(start + (target - start) * eased));
          if(p < 1) requestAnimationFrame(tick);
        };
        requestAnimationFrame(tick);
        countObs.unobserve(el);
      }
    }, { threshold: 0.3 });
    counts.forEach(el=>countObs.observe(el));

    // Menu data
    const menuItems = [
      { id:1, name:'Truffle Noir Risotto', price:'₹ 699', cat:['food','signature'], desc:'Creamy arborio, truffle essence, parmesan veil, and golden oil finish.', tags:['Signature','Vegetarian'], img:'https://images.unsplash.com/photo-1541544741938-0af808871cc0?auto=format&fit=crop&w=1600&q=70' },
      { id:2, name:'Velvet Spiced Chicken', price:'₹ 749', cat:['food'], desc:'Charcoal-seared chicken, warm spices, citrus glaze, and herb couture.', tags:['Best Seller','Non-Veg'], img:'https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=1600&q=70' },
      { id:3, name:'Goldleaf Chocolate Cake', price:'₹ 399', cat:['food','signature'], desc:'Dense cocoa crumb, silky ganache, and a shimmer of edible gold.', tags:['Dessert','Premium'], img:'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&w=1600&q=70' },
      { id:4, name:'Saffron Smoke Latte', price:'₹ 349', cat:['drinks','signature'], desc:'Saffron infused espresso with smoked milk foam and gold dust top.', tags:['Signature','Hot'], img:'https://images.unsplash.com/photo-1511920170033-f8396924c348?auto=format&fit=crop&w=1600&q=70' },
      { id:5, name:'Vineyard Iced Tea', price:'₹ 299', cat:['drinks'], desc:'Black tea, berry notes, citrus lift, and a clean premium finish.', tags:['Cold','Refreshing'], img:'https://images.unsplash.com/photo-1527169402691-a3fbfda1f582?auto=format&fit=crop&w=1600&q=70' },
      { id:6, name:'Citrus Velvet Mocktail', price:'₹ 399', cat:['drinks','signature'], desc:'Fresh citrus, herb whisper, and lounge-ready sparkle (non-alcoholic).', tags:['Signature','Zero Proof'], img:'https://images.unsplash.com/photo-1527169402691-a3fbfda1f582?auto=format&fit=crop&w=1600&q=70' },
    ];

    const grid = document.getElementById('menuGrid');
    const chips = Array.from(document.querySelectorAll('#chips .chip'));
    const search = document.getElementById('menuSearch');

    let active = 'all';
    const render = ()=>{
      const q = (search.value||'').trim().toLowerCase();
      const filtered = menuItems.filter(it=>{
        const okCat = (active==='all') ? true : it.cat.includes(active);
        const okQ = q ? (it.name.toLowerCase().includes(q) || it.desc.toLowerCase().includes(q) || it.tags.join(' ').toLowerCase().includes(q)) : true;
        return okCat && okQ;
      });
      grid.innerHTML = filtered.map(it=>{
        return `
          <article class="card reveal">
            <div class="media" style="height:150px; background-image:url('${it.img}'); background-position:center;"></div>
            <div class="itemHead" style="margin-top:14px;">
              <div>
                <div class="itemName">${it.name}</div>
                <div class="desc">${it.desc}</div>
              </div>
              <div class="price">${it.price}</div>
            </div>
            <div class="tagRow">${it.tags.map(t=>`<span class="tag">${t}</span>`).join('')}</div>
          </article>
        `;
      }).join('');

      // Re-bind reveal for newly injected items
      grid.querySelectorAll('.reveal').forEach(el=>{
        el.classList.remove('on');
      });
      // quick re-observe
      grid.querySelectorAll('.reveal').forEach(el=>{
        obs.observe(el);
      });
    };

    chips.forEach(ch=>ch.addEventListener('click', ()=>{
      chips.forEach(c=>c.classList.remove('on'));
      ch.classList.add('on');
      active = ch.getAttribute('data-filter');
      render();
    }));

    search?.addEventListener('input', ()=>render());
    render();

    // Reviews slider
    let idx = 0;
    const slides = document.getElementById('slides');
    const slideCount = 3;
    const nextBtn = document.getElementById('nextBtn');
    const prevBtn = document.getElementById('prevBtn');
    const go = (n)=>{
      idx = (n + slideCount) % slideCount;
      slides.style.transform = `translateX(-${idx*100}%)`;
    };
    nextBtn?.addEventListener('click', ()=>go(idx+1));
    prevBtn?.addEventListener('click', ()=>go(idx-1));
    setInterval(()=>go(idx+1), 6500);

    // Events form (demo)
    const eventForm = document.getElementById('eventForm');
    const eventMsg = document.getElementById('eventMsg');
    eventForm?.addEventListener('submit', (e)=>{
      e.preventDefault();
      eventMsg.textContent = 'Request received — we will confirm shortly.';
      setTimeout(()=>eventMsg.textContent = '', 4500);
      eventForm.reset();
    });

    // Reservations form (demo)
    const reserveForm = document.getElementById('reserveForm');
    const reserveMsg = document.getElementById('reserveMsg');
    reserveForm?.addEventListener('submit', (e)=>{
      e.preventDefault();
      reserveMsg.textContent = 'Reservation confirmed (demo). See you soon ✦';
      setTimeout(()=>reserveMsg.textContent='', 4500);
      reserveForm.reset();
    });

    // Contact form (demo)
    const contactForm = document.getElementById('contactForm');
    const contactMsg = document.getElementById('contactMsg');
    contactForm?.addEventListener('submit', (e)=>{
      e.preventDefault();
      contactMsg.textContent = 'Message sent (demo). We’ll reply fast.';
      setTimeout(()=>contactMsg.textContent='', 4500);
      contactForm.reset();
    });

    // Gallery
    const gallery = [
      { id:1, cat:'food', title:'Truffle Risotto', src:'https://images.unsplash.com/photo-1541544741938-0af808871cc0?auto=format&fit=crop&w=1600&q=70' },
      { id:2, cat:'drinks', title:'Gold Saffron Latte', src:'https://images.unsplash.com/photo-1511920170033-f8396924c348?auto=format&fit=crop&w=1600&q=70' },
      { id:3, cat:'ambience', title:'Cinematic Lounge', src:'https://images.unsplash.com/photo-1514933651103-005eec06c04b?auto=format&fit=crop&w=1600&q=70' },
      { id:4, cat:'food', title:'Velvet Chicken', src:'https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=1600&q=70' },
      { id:5, cat:'drinks', title:'Vineyard Iced Tea', src:'https://images.unsplash.com/photo-1527169402691-a3fbfda1f582?auto=format&fit=crop&w=1600&q=70' },
      { id:6, cat:'ambience', title:'Glassmorphism Details', src:'https://images.unsplash.com/photo-1525268323446-0505b6fe7778?auto=format&fit=crop&w=1600&q=70' },
      { id:7, cat:'food', title:'Chocolate Goldleaf', src:'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&w=1600&q=70' },
      { id:8, cat:'ambience', title:'Velvet Lighting', src:'https://images.unsplash.com/photo-1521737604893-d14cc237f11d?auto=format&fit=crop&w=1600&q=70' },
    ];

    const masonry = document.getElementById('masonry');
    const gChips = Array.from(document.querySelectorAll('#gChips .chip'));
    let gFilter = 'all';

    const renderGallery = ()=>{
      const list = gallery.filter(g=> gFilter==='all' ? true : g.cat===gFilter);
      masonry.innerHTML = list.map(g=>{
        return `
          <div class="gItem">
            <button type="button" data-id="${g.id}" data-cat="${g.cat}" data-title="${g.title}" data-src="${g.src}" aria-label="Open ${g.title}">
              <div class="img" style="background-image:url('${g.src}')"></div>
              <div class="cap">
                <div class="t">${g.title}</div>
                <div class="c">${g.cat}</div>
              </div>
            </button>
          </div>
        `;
      }).join('');

      masonry.querySelectorAll('button[data-src]').forEach(btn=>{
        btn.addEventListener('click', ()=>{
          document.getElementById('lbTitle').textContent = btn.getAttribute('data-title');
          document.getElementById('lbImg').src = btn.getAttribute('data-src');
          document.getElementById('lightbox').classList.add('open');
        });
      });
    };

    gChips.forEach(ch=>ch.addEventListener('click', ()=>{
      gChips.forEach(c=>c.classList.remove('on'));
      ch.classList.add('on');
      gFilter = ch.getAttribute('data-g');
      renderGallery();
    }));

    // Lightbox controls
    const lightbox = document.getElementById('lightbox');
    document.getElementById('lbClose').addEventListener('click', ()=>lightbox.classList.remove('open'));
    lightbox.addEventListener('click', (e)=>{ if(e.target===lightbox) lightbox.classList.remove('open'); });
    document.addEventListener('keydown', (e)=>{ if(e.key==='Escape') lightbox.classList.remove('open'); });

    renderGallery();

  </script>
</body>
</html>

