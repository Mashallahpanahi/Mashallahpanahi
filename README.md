<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mashallah panhi · full stack dev</title>
  <!-- Font Awesome 6 (free icons) -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(145deg, #0c0f1e 0%, #141b2b 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      padding: 2rem 1.5rem;
    }

    /* main card – glassmorphism + soft glow */
    .profile-card {
      max-width: 1000px;
      width: 100%;
      background: rgba(20, 30, 48, 0.7);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: 3.5rem;
      padding: 2.8rem 3rem;
      box-shadow: 0 30px 50px rgba(0, 0, 0, 0.7), 0 0 0 1px rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.04);
      transition: all 0.2s ease;
    }

    /* header: name + title */
    .header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 2.8rem;
      border-bottom: 1px solid rgba(255, 255, 255, 0.05);
      padding-bottom: 1.8rem;
    }

    .name-title h1 {
      font-size: 3.2rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      background: linear-gradient(to right, #f0f4ff, #b7cbff);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 0.2rem;
      line-height: 1.1;
    }

    .name-title .badge {
      display: inline-block;
      background: rgba(255, 215, 100, 0.12);
      border: 1px solid rgba(255, 215, 100, 0.15);
      padding: 0.4rem 1.4rem;
      border-radius: 60px;
      font-size: 1rem;
      font-weight: 500;
      color: #f5d78c;
      letter-spacing: 0.3px;
      backdrop-filter: blur(4px);
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }

    .profile-icon {
      font-size: 2.8rem;
      color: rgba(255, 255, 255, 0.08);
      background: rgba(255, 255, 255, 0.02);
      padding: 0.6rem 1.2rem;
      border-radius: 80px;
      border: 1px solid rgba(255, 255, 255, 0.02);
      backdrop-filter: blur(4px);
    }

    /* section titles */
    .section-title {
      font-size: 1.1rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: rgba(255, 255, 255, 0.25);
      margin-bottom: 1.5rem;
      font-weight: 500;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .section-title i {
      font-size: 1rem;
      color: rgba(255, 215, 100, 0.5);
    }

    .skill-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
      gap: 0.9rem 1.2rem;
      margin-bottom: 2.8rem;
    }

    /* skill pill – each skill with icon */
    .skill-pill {
      display: flex;
      align-items: center;
      gap: 10px;
      background: rgba(255, 255, 255, 0.02);
      border: 1px solid rgba(255, 255, 255, 0.03);
      padding: 0.7rem 1.2rem 0.7rem 1rem;
      border-radius: 60px;
      backdrop-filter: blur(4px);
      transition: all 0.15s ease;
      box-shadow: 0 2px 4px rgba(0,0,0,0.2);
    }

    .skill-pill:hover {
      background: rgba(255, 255, 255, 0.06);
      border-color: rgba(255, 215, 100, 0.15);
      transform: translateY(-2px);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    }

    .skill-pill i {
      font-size: 1.6rem;
      width: 2rem;
      text-align: center;
      color: #d6e2ff;
    }

    /* specific brand colors for icons (optional) */
    .skill-pill .fa-react { color: #61dbfb; }
    .skill-pill .fa-node-js { color: #68a063; }
    .skill-pill .fa-js { color: #f7df1e; }
    .skill-pill .fa-css3-alt { color: #2965f1; }
    .skill-pill .fa-html5 { color: #e34f26; }
    .skill-pill .fa-php { color: #777bb4; }
    .skill-pill .fa-database { color: #00758f; } /* sql / postgres */
    .skill-pill .fa-nestjs { 
      color: #e0234e; 
    }
    /* custom nestjs icon via text fallback (fontawesome doesn't have official) */
    .skill-pill .fa-nestjs-custom {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-size: 1rem;
      background: #e0234e;
      color: white;
      width: 1.9rem;
      height: 1.9rem;
      border-radius: 40px;
      font-family: 'Inter', sans-serif;
      letter-spacing: -0.5px;
      box-shadow: 0 2px 8px rgba(224, 35, 78, 0.3);
    }
    .skill-pill .fa-nestjs-custom small {
      font-size: 0.8rem;
      font-weight: 800;
    }

    /* backend & pro block */
    .backend-highlight {
      background: rgba(255, 255, 255, 0.01);
      border-radius: 2.5rem;
      padding: 1.8rem 2rem;
      margin-top: 1.2rem;
      border: 1px solid rgba(255, 255, 255, 0.02);
      backdrop-filter: blur(4px);
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }

    .backend-stack {
      display: flex;
      flex-wrap: wrap;
      gap: 0.9rem 1.8rem;
    }

    .backend-item {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 1.1rem;
      font-weight: 400;
      color: rgba(255, 255, 255, 0.7);
    }
    .backend-item i {
      font-size: 1.6rem;
      width: 2rem;
      text-align: center;
    }
    .backend-item .fa-node-js { color: #68a063; }
    .backend-item .fa-nestjs-custom { 
      background: #e0234e; 
      color: white;
      width: 2rem;
      height: 2rem;
      font-size: 0.9rem;
      border-radius: 40px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
    }
    .backend-item .fa-php { color: #777bb4; }
    .backend-item .fa-database { color: #00758f; }

    .pro-badge {
      background: rgba(224, 35, 78, 0.12);
      border: 1px solid rgba(224, 35, 78, 0.2);
      padding: 0.4rem 1.8rem;
      border-radius: 60px;
      font-size: 0.95rem;
      font-weight: 500;
      color: #ff8ba7;
      letter-spacing: 0.3px;
      white-space: nowrap;
      backdrop-filter: blur(4px);
      box-shadow: 0 2px 8px rgba(224, 35, 78, 0.05);
    }
    .pro-badge i {
      margin-right: 8px;
      color: #e0234e;
    }

    /* footer / small */
    .footnote {
      margin-top: 2.4rem;
      font-size: 0.85rem;
      color: rgba(255, 255, 255, 0.12);
      text-align: right;
      letter-spacing: 0.2px;
      border-top: 1px solid rgba(255, 255, 255, 0.02);
      padding-top: 1.8rem;
    }

    /* responsive */
    @media (max-width: 700px) {
      .profile-card { padding: 2rem 1.5rem; }
      .name-title h1 { font-size: 2.4rem; }
      .header { flex-direction: column; align-items: flex-start; gap: 0.8rem; }
      .profile-icon { align-self: flex-start; }
      .skill-grid { grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); }
      .backend-highlight { flex-direction: column; align-items: flex-start; gap: 1.2rem; }
      .pro-badge { white-space: normal; }
    }

    @media (max-width: 460px) {
      .skill-grid { grid-template-columns: 1fr 1fr; }
      .backend-stack { gap: 0.6rem 1rem; }
    }

    /* small tweaks */
    .text-glow {
      text-shadow: 0 2px 12px rgba(255, 215, 100, 0.08);
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <!-- header: name + full stack -->
    <div class="header">
      <div class="name-title">
        <h1><i class="fas fa-code" style="color: rgba(255,215,100,0.2); margin-right: 10px;"></i>Mashallah panhi</h1>
        <span class="badge"><i class="fas fa-layer-group" style="margin-right: 8px;"></i>full stuck developer</span>
      </div>
      <div class="profile-icon">
        <i class="fas fa-terminal"></i>
      </div>
    </div>

    <!-- frontend skills -->
    <div class="section-title">
      <i class="fas fa-paint-brush"></i> frontend · react ecosystem
    </div>
    <div class="skill-grid">
      <div class="skill-pill"><i class="fab fa-react fa-react"></i> React</div>
      <div class="skill-pill"><i class="fab fa-js"></i> JavaScript</div>
      <div class="skill-pill"><i class="fab fa-node-js"></i> Next.js</div>
      <div class="skill-pill"><i class="fab fa-css3-alt"></i> TailwindCSS</div>
      <div class="skill-pill"><i class="fab fa-css3-alt"></i> CSS</div>
      <div class="skill-pill"><i class="fab fa-html5"></i> HTML</div>
    </div>

    <!-- backend skills -->
    <div class="section-title" style="margin-top: 0.8rem;">
      <i class="fas fa-server"></i> backend · api & databases
    </div>
    <div class="skill-grid">
      <div class="skill-pill"><i class="fab fa-node-js"></i> Node.js</div>
      <div class="skill-pill">
        <!-- custom nestjs icon: using a small badge-like element -->
        <span class="fa-nestjs-custom"><small>N</small></span>
        NestJS
      </div>
      <div class="skill-pill"><i class="fab fa-php"></i> PHP</div>
      <div class="skill-pill"><i class="fas fa-database"></i> SQL</div>
      <div class="skill-pill"><i class="fas fa-database" style="color: #00758f;"></i> PostgreSQL</div>
    </div>

    <!-- professional highlight: NestJS + Postgres -->
    <div class="backend-highlight">
      <div class="backend-stack">
        <span class="backend-item">
          <span class="fa-nestjs-custom" style="background: #e0234e; color: white; width: 2.2rem; height: 2.2rem; font-size: 1rem; border-radius: 40px; display: inline-flex; align-items: center; justify-content: center; font-weight: 700;">N</span>
          <span style="font-weight: 500; color: white;">NestJS</span>
        </span>
        <span class="backend-item">
          <i class="fas fa-database" style="color: #00758f;"></i>
          <span style="font-weight: 500; color: white;">PostgreSQL</span>
        </span>
        <span class="backend-item" style="opacity: 0.6;">
          <i class="fas fa-plug"></i> 
          <span>TypeORM · Prisma</span>
        </span>
      </div>
      <div class="pro-badge">
        <i class="fas fa-star"></i> professional in nestjs + postgres
      </div>
    </div>

    <!-- extra: full stack vibe -->
    <div style="display: flex; flex-wrap: wrap; gap: 0.8rem 1.5rem; margin-top: 2rem; padding-top: 0.8rem; border-top: 1px solid rgba(255,255,255,0.02);">
      <span style="color: rgba(255,255,255,0.2); font-size: 0.85rem; display: flex; align-items: center; gap: 6px;">
        <i class="fas fa-check-circle" style="color: rgba(100, 200, 100, 0.3);"></i> REST · GraphQL
      </span>
      <span style="color: rgba(255,255,255,0.2); font-size: 0.85rem; display: flex; align-items: center; gap: 6px;">
        <i class="fas fa-check-circle" style="color: rgba(100, 200, 100, 0.3);"></i> Docker · AWS
      </span>
      <span style="color: rgba(255,255,255,0.2); font-size: 0.85rem; display: flex; align-items: center; gap: 6px;">
        <i class="fas fa-check-circle" style="color: rgba(100, 200, 100, 0.3);"></i> microservices
      </span>
    </div>

    <div class="footnote">
      <i class="fas fa-arrow-right" style="margin-right: 6px;"></i> full stuck · mashallah panhi
    </div>
  </div>
</body>
</html>
