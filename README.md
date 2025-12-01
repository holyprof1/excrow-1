# excrow <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Film & Entertainment - Savvy Media Africa</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<!-- Global header/footer + nav styles -->
<link rel="stylesheet" href="/savvy.css">

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}

:root{
  --deep-navy:#001d3d;
  --navy:#002855;
  --bright-cyan:#00D4FF;
  --cyan:#00A8E8;
  --bright-green:#00FF88;
  --green:#00E676;
  --orange:#FF6B35;
  --yellow:#FFB800;
  --white:#FFFFFF;
}

body{
  font-family:'Sora',sans-serif;
  color:var(--white);
  background:var(--deep-navy);
  overflow-x:hidden;
  line-height:1.6;
  font-weight:400;
  cursor:none;
}

/* ===== Custom cursor ===== */
.cursor{
  position:fixed;
  width:8px;
  height:8px;
  border-radius:50%;
  background:var(--bright-cyan);
  pointer-events:none;
  z-index:99999;
  opacity:.8;
  transition:transform .1s ease;
  mix-blend-mode:screen;
  box-shadow:0 0 12px var(--bright-cyan),0 0 24px rgba(0,212,255,.5)
}
.cursor-follower{
  position:fixed;
  width:32px;
  height:32px;
  border-radius:50%;
  border:1.5px solid var(--bright-cyan);
  pointer-events:none;
  z-index:99998;
  opacity:.4;
  transition:all .25s ease;
  box-shadow:inset 0 0 8px rgba(0,212,255,.3)
}

/* ========== HERO ========== */
.hero{
  min-height:90vh;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  position:relative;
  padding:12rem 4rem 6rem;
  overflow:hidden;
  background:linear-gradient(135deg,var(--deep-navy) 0%,var(--navy) 100%);
}
.floating-shape{
  position:absolute;
  border-radius:50%;
  filter:blur(120px);
  opacity:.12;
  pointer-events:none;
  animation:float 20s ease-in-out infinite;
}
.shape-1{
  width:700px;
  height:700px;
  background:linear-gradient(135deg,var(--bright-cyan),var(--cyan));
  top:10%;
  left:5%;
}
.shape-2{
  width:600px;
  height:600px;
  background:linear-gradient(135deg,var(--orange),var(--yellow));
  bottom:6%;
  right:5%;
  animation-delay:-10s;
}
@keyframes float{
  0%,100%{transform:translate(0,0) scale(1)}
  25%{transform:translate(50px,-50px) scale(1.1)}
  50%{transform:translate(80px,-80px) scale(1.2)}
  75%{transform:translate(30px,-40px) scale(1.15)}
}
.hero-content{
  text-align:center;
  max-width:1600px;
  position:relative;
  z-index:2;
}
.hero-title{
  font-family:'Sora',sans-serif;
  font-size:clamp(2.8rem,9vw,7rem);
  font-weight:500;
  line-height:1.05;
  margin-bottom:2rem;
}
.title-line{display:block;margin-bottom:.8rem}
.word{
  display:inline-block;
  margin-right:.25em;
  position:relative;
  opacity:0;
  transform:translate3d(0,100px,0) scale(.9) rotate(4deg);
}
.word.cyan{color:var(--bright-cyan)}
.word.green{color:var(--bright-green)}
.hero-subtitle{
  font-size:clamp(1rem,2vw,1.3rem);
  color:rgba(255,255,255,.9);
  max-width:900px;
  margin:1.5rem auto 0;
  line-height:1.9;
  opacity:0;
  font-weight:400;
}

/* ========== FILTER ========== */
.filter-section{
  padding:2.5rem 4rem;
  text-align:center;
  background:var(--navy);
}
.filter-tabs{
  display:flex;
  gap:1rem;
  justify-content:center;
  flex-wrap:wrap;
  max-width:1200px;
  margin:0 auto;
}
.filter-btn{
  background:rgba(0,212,255,.1);
  border:1px solid rgba(0,212,255,.3);
  color:var(--white);
  padding:.8rem 1.6rem;
  border-radius:999px;
  cursor:pointer;
  font-weight:600;
  font-size:.9rem;
  text-transform:uppercase;
  letter-spacing:1.5px;
  transition:.3s;
  font-family:'Sora',sans-serif;
}
.filter-btn:hover,
.filter-btn.active{
  background:var(--bright-cyan);
  color:var(--deep-navy);
  border-color:var(--bright-cyan);
  transform:scale(1.05);
}

/* ========== PORTFOLIO GRID ========== */
.portfolio-section{
  padding:5rem 2rem;
  background:var(--deep-navy);
}
.section-label{
  display:inline-block;
  background:linear-gradient(135deg,var(--orange),var(--yellow));
  color:var(--deep-navy);
  padding:.8rem 1.8rem;
  border-radius:999px;
  font-size:.85rem;
  font-weight:600;
  text-transform:uppercase;
  letter-spacing:2px;
  margin-bottom:1.5rem;
}
.section-title{
  font-size:clamp(2.5rem,6vw,4.5rem);
  font-weight:600;
  margin-bottom:.8rem;
  text-align:center;
  line-height:1.1;
}
.section-subtitle{
  font-size:1.2rem;
  color:rgba(255,255,255,.85);
  text-align:center;
  max-width:900px;
  margin:0 auto 4rem;
  font-weight:400;
  line-height:1.8;
}

.portfolio-grid{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(360px,1fr));
  gap:2.5rem;
  max-width:1700px;
  margin:0 auto;
}
.portfolio-card{
  position:relative;
  border-radius:18px;
  overflow:hidden;
  background:rgba(255,255,255,.04);
  backdrop-filter:blur(10px);
  border:1px solid rgba(0,212,255,.15);
  transition:.45s;
  opacity:0;
  transform:translateY(50px);
  cursor:pointer;
  display:flex;
  flex-direction:column;
  height:100%;
}
.portfolio-card::before{
  content:'';
  position:absolute;
  inset:0;
  background:linear-gradient(135deg,rgba(0,212,255,.2) 0%,rgba(255,107,53,.2) 100%);
  opacity:0;
  transition:.45s;
  pointer-events:none;
  z-index:3;
}
.portfolio-card:hover{
  border-color:rgba(0,212,255,.4);
  transform:translateY(-15px);
  box-shadow:0 25px 70px rgba(0,212,255,.25);
}
.portfolio-card:hover::before{opacity:1}
.portfolio-image{
  width:100%;
  height:300px;
  overflow:hidden;
  position:relative;
  background:var(--navy);
  display:flex;
  align-items:center;
  justify-content:center;
  flex-shrink:0;
}
.portfolio-image::after{
  content:'';
  position:absolute;
  inset:0;
  background:linear-gradient(180deg,rgba(0,0,0,0) 0%,rgba(0,29,61,.4) 100%);
  z-index:2;
  pointer-events:none;
}
.portfolio-image img{
  width:100%;
  height:100%;
  object-fit:cover;
  object-position:center;
  transition:transform .6s;
  position:relative;
  z-index:1;
}
.portfolio-card:hover .portfolio-image img{transform:scale(1.1)}
.portfolio-info{
  padding:2.5rem;
  position:relative;
  z-index:2;
  flex:1;
  display:flex;
  flex-direction:column;
  justify-content:flex-end;
  background:linear-gradient(180deg,rgba(0,29,61,.3) 0%,rgba(0,29,61,.85) 100%);
}
.portfolio-category{
  font-size:.8rem;
  color:var(--bright-green);
  text-transform:uppercase;
  letter-spacing:2px;
  font-weight:700;
  margin-bottom:1rem;
  display:inline-block;
  background:rgba(0,255,136,.12);
  padding:.5rem 1rem;
  border-radius:999px;
  width:fit-content;
}
.portfolio-title{
  font-size:1.6rem;
  font-weight:700;
  margin-bottom:1rem;
  color:var(--white);
  line-height:1.2;
}
.portfolio-description{
  font-size:.95rem;
  color:rgba(255,255,255,.8);
  line-height:1.7;
}

/* ========== DETAIL SECTIONS ========== */
.detail-section{
  padding:6rem 2rem;
  background:var(--navy);
  display:none;
  opacity:0;
  border-top:2px solid rgba(0,212,255,.2);
}
.detail-section.active{
  display:block;
  animation:revealDetail .8s ease forwards;
}
@keyframes revealDetail{to{opacity:1}}

.detail-container{
  max-width:1400px;
  margin:0 auto;
}
.detail-header{
  display:grid;
  grid-template-columns:1.2fr 1fr;
  gap:4rem;
  align-items:start;
  margin-bottom:4rem;
}

.detail-images{
  display:grid;
  grid-template-columns:1fr;
  gap:2rem;
}
.detail-img-main{
  width:100%;
  border-radius:18px;
  overflow:hidden;
  box-shadow:0 30px 80px rgba(0,0,0,.5);
  height:500px;
}
.detail-img-main img{
  width:100%;
  height:100%;
  object-fit:cover;
  display:block;
}
.detail-imgs-small{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:2rem;
  margin-top:2rem;
}
.detail-img-small{
  width:100%;
  height:280px;
  border-radius:14px;
  overflow:hidden;
  box-shadow:0 20px 50px rgba(0,0,0,.4);
}
.detail-img-small img{
  width:100%;
  height:100%;
  object-fit:cover;
}

.detail-content h2{
  font-size:clamp(2.2rem,4vw,3.5rem);
  font-weight:700;
  margin-bottom:1.5rem;
  line-height:1.2;
  color:var(--white);
}
.detail-client{
  color:var(--bright-cyan);
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:2px;
  margin-bottom:2rem;
  font-size:.9rem;
  display:inline-block;
  background:rgba(0,212,255,.15);
  padding:.8rem 1.8rem;
  border-radius:999px;
  border:1px solid rgba(0,212,255,.3);
}

.detail-boxes{margin-top:3rem}
.detail-box{
  margin-bottom:2.5rem;
  padding:2rem;
  background:rgba(0,212,255,.08);
  border:1px solid rgba(0,212,255,.2);
  border-radius:14px;
  transition:.3s;
}
.detail-box:hover{
  background:rgba(0,212,255,.12);
  border-color:rgba(0,212,255,.4);
}
.detail-box-label{
  color:var(--bright-green);
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:2px;
  margin-bottom:1rem;
  font-size:.95rem;
  display:flex;
  align-items:center;
  gap:.6rem;
}
.detail-box-label::before{
  content:'→';
  font-size:1.3rem;
  color:var(--bright-cyan);
}
.detail-box-text{
  font-size:1.05rem;
  line-height:1.85;
  color:rgba(255,255,255,.85);
}

.detail-stats{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
  gap:2rem;
  margin-top:3rem;
  padding-top:3rem;
  border-top:1px solid rgba(0,212,255,.15);
}
.detail-stat{
  background:rgba(0,212,255,.1);
  border:1px solid rgba(0,212,255,.2);
  padding:2rem;
  border-radius:14px;
  text-align:center;
  transition:.3s;
}
.detail-stat:hover{
  background:rgba(0,212,255,.15);
  border-color:rgba(0,212,255,.4);
  transform:translateY(-5px);
}
.detail-stat-number{
  font-size:2.2rem;
  font-weight:700;
  color:var(--bright-cyan);
  margin-bottom:.6rem;
}
.detail-stat-label{
  font-size:.85rem;
  color:rgba(255,255,255,.7);
  text-transform:uppercase;
  letter-spacing:1.5px;
  font-weight:600;
}

/* ========== CTA ========== */
.cta-section{
  padding:8rem 4rem;
  text-align:center;
  background:linear-gradient(135deg,var(--bright-cyan),var(--orange));
  position:relative;
  overflow:hidden;
}
.cta-section::before{
  content:'';
  position:absolute;
  inset:0;
  background:radial-gradient(circle at 20% 80%,rgba(255,107,53,.3),transparent);
  pointer-events:none;
}
.cta-title{
  font-size:clamp(2.5rem,7vw,5rem);
  font-weight:700;
  margin-bottom:1.5rem;
  color:var(--deep-navy);
  position:relative;
  z-index:2;
  line-height:1.1;
}
.cta-subtitle{
  font-size:1.5rem;
  margin-bottom:2.5rem;
  opacity:.95;
  color:var(--deep-navy);
  font-weight:500;
  position:relative;
  z-index:2;
}
.btn-primary{
  background:var(--deep-navy);
  color:var(--bright-cyan);
  padding:1.3rem 3.2rem;
  border-radius:999px;
  text-decoration:none;
  font-weight:700;
  font-size:1.1rem;
  display:inline-flex;
  align-items:center;
  gap:.8rem;
  box-shadow:0 15px 50px rgba(0,0,0,.3);
  transition:.3s;
  border:none;
  cursor:pointer;
  position:relative;
  z-index:2;
}
.btn-primary:hover{
  transform:translateY(-4px);
  box-shadow:0 20px 60px rgba(0,0,0,.4);
}

/* ========== SCROLL TOP ========== */
.scroll-top{
  position:fixed;
  bottom:30px;
  right:30px;
  width:70px;
  height:70px;
  border-radius:50%;
  z-index:9000;
  display:grid;
  place-items:center;
  cursor:pointer;
  background:conic-gradient(var(--bright-cyan) calc(var(--scroll,0)*1%),rgba(0,212,255,.15) 0);
  box-shadow:0 12px 40px rgba(0,212,255,.4),inset 0 0 0 8px rgba(0,29,61,.6);
  transform:scale(.85);
  opacity:0;
  pointer-events:none;
  transition:.3s ease;
  border:none;
}
.scroll-top.visible{
  opacity:1;
  pointer-events:auto;
  transform:scale(1);
}
.scroll-top .inner{
  width:52px;
  height:52px;
  border-radius:50%;
  display:grid;
  place-items:center;
  background:var(--navy);
  color:#fff;
  font-weight:700;
}
.scroll-top .pct{font-size:.9rem}

/* ========== RESPONSIVE ========== */
@media (max-width:1200px){
  .portfolio-grid{grid-template-columns:repeat(2,1fr)}
  .detail-header{grid-template-columns:1fr}
}

@media (max-width:768px){
  body{cursor:default}
  .cursor,.cursor-follower{display:none}
  
  .hero{padding:8rem 2rem 4rem}
  .portfolio-section{padding:3rem 1.5rem}
  .portfolio-grid{grid-template-columns:1fr;gap:1.5rem}
  .portfolio-image{height:240px}
  
  .detail-section{padding:4rem 1.5rem}
  .detail-header{gap:2rem}
  .detail-img-main{height:300px}
  .detail-boxes{margin-top:2rem}
  .detail-box{padding:1.5rem;margin-bottom:1.5rem}
  .detail-stats{
    grid-template-columns:repeat(auto-fit,minmax(120px,1fr));
    gap:1.5rem;
    margin-top:2rem;
    padding-top:2rem;
  }
  
  .cta-section{padding:4rem 2rem}
}
</style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor"></div>
<div class="cursor-follower"></div>

<!-- Global header include -->
<div data-include="/header.html"></div>

<!-- ========== HERO ========== -->
<section class="hero">
  <div class="floating-shape shape-1" data-parallax="-12"></div>
  <div class="floating-shape shape-2" data-parallax="14"></div>
  <div class="hero-content">
    <div class="hero-title">
      <div class="title-line"><span class="word">Film &</span></div>
      <div class="title-line"><span class="word cyan">Entertainment</span></div>
      <div class="title-line"><span class="word green">Campaigns</span></div>
    </div>
    <p class="hero-subtitle">Iconic premieres, blockbuster launches, and culture-moving entertainment campaigns that shape the narrative.</p>
  </div>
</section>

<!-- ========== FILTER ========== -->
<section class="filter-section">
  <div class="filter-tabs">
    <button class="filter-btn active" data-filter="all">Show all</button>
    <button class="filter-btn" data-filter="Content Production">Content Production</button>
    <button class="filter-btn" data-filter="Events">Events</button>
    <button class="filter-btn" data-filter="PR">PR</button>
    <button class="filter-btn" data-filter="Reality">Reality</button>
  </div>
</section>

<!-- ========== PORTFOLIO ========== -->
<section class="portfolio-section">
  <div style="text-align:center">
    <span class="section-label">Featured Campaigns</span>
    <h2 class="section-title">Film & Entertainment Portfolio</h2>
    <p class="section-subtitle">Iconic premieres and entertainment campaigns that shaped culture and delivered results.</p>
  </div>
  <div class="portfolio-grid" id="portfolioGrid"></div>
</section>

<!-- ========== DETAILS (ON CARD CLICK) ========== -->
<div id="detailsContainer"></div>

<!-- ========== CTA ========== -->
<section class="cta-section">
  <h2 class="cta-title">Ready for Your Next <span style="color:rgba(0,29,61,.7);">Cultural</span> Moment?</h2>
  <p class="cta-subtitle">Let's create a campaign that moves culture and delivers results.</p>
  <a href="mailto:hello@savvymediaafrica.com" class="btn-primary">Start Your Project <i class="fas fa-arrow-right"></i></a>
</section>

<!-- Global footer include -->
<div data-include="/footer.html"></div>

<!-- SCROLL TOP BUTTON -->
<button class="scroll-top" id="scrollTopBtn" aria-label="Back to top">
  <div class="inner"><span class="pct" id="scrollPct">0%</span></div>
</button>

<script>
gsap.registerPlugin(ScrollTrigger);

const filmProjects = [
  {
    id:'aburo',
    title:'Aburo Premiere',
    category:'Events',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Aburo-Movie-Premiere-.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/black-panther.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Aburo-Movie-Premiere-.jpg?w=500',
    client:'Aburo Film',
    challenge:'Execute a high-profile film premiere that maximizes media coverage and creates memorable audience engagement.',
    solution:'Orchestrated every detail from guest logistics to red-carpet media coordination. Secured premium media partnerships and curated the guest experience to amplify brand visibility across traditional and digital channels. Managed VIP relations, press interviews, and post-event media coverage.',
    results:'Flawless execution with industry-wide recognition. Achieved extensive media coverage, premium attendance with A-list celebrities, and established premiere as cultural benchmark for film industry events in West Africa.',
    achievements:[
      {label:'Execution',value:'Flawless'},
      {label:'Coverage',value:'Extensive'},
      {label:'Attendance',value:'Premium'}
    ]
  },
  {
    id:'alls-fair',
    title:"All's Fair in Love",
    category:'Events',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Alls-Fair-In-Love_.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Alls-Fair-In-Love_.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/avatar.jpg?w=500',
    client:'Deyemi Okanlawon Films',
    challenge:'Drive both cultural impact and box office success for a major film release in competitive Nigerian market.',
    solution:'Comprehensive marketing spanning digital amplification, earned media, influencer partnerships, and strategic PR. Positioned film as cultural event through targeted audience engagement. Coordinated social media campaign with 26M+ reach, influencer previews, and strategic premiere timing.',
    results:'26M+ social reach achieved, ₦33.6M earned media value, ₦130.2M cinema gross. Film became highest-grossing Nollywood release of the year with strong audience retention and word-of-mouth momentum.',
    achievements:[
      {label:'Social Reach',value:'26M+'},
      {label:'Earned Media',value:'₦33.6M'},
      {label:'Box Office',value:'₦130.2M'}
    ]
  },
  {
    id:'bad-boys',
    title:'Bad Boys: Ride or Die',
    category:'Events',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Bad-Boys-Premiere_1.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Bad-Boys-Premiere_1.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Alls-Fair-In-Love_.jpg?w=500',
    client:'Sony Pictures',
    challenge:'Execute world-class premiere for major studio blockbuster release in West Africa.',
    solution:'Precision red-carpet coordination with premium media partnerships. Managed star-studded guest logistics, international press coordination, and comprehensive media coverage strategy. Secured partnerships with leading media outlets for live coverage and exclusive interviews.',
    results:'Premium execution achieved with star-studded attendance including international cast members. Extensive media coverage across all platforms. Film achieved strong box office performance in region with sustained audience interest.',
    achievements:[
      {label:'Red Carpet',value:'Premium'},
      {label:'Media',value:'Extensive'},
      {label:'Attendance',value:'Star-Studded'}
    ]
  },
  {
    id:'furiosa',
    title:'Furiosa Premiere',
    category:'Content Production',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Furiosa-Premiere_1.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Furiosa-Premiere_1.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Bad-Boys-Premiere_1.jpg?w=500',
    client:'Warner Bros',
    challenge:"Create premiere experience matching film's high-impact storytelling and action-packed narrative.",
    solution:'Immersive event production with thematic creative direction. Designed experience that resonated across audiences and media platforms. Created custom visual installations, coordinated stunt demonstrations, and developed experiential activations reflecting film’s action themes.',
    results:'High impact execution with explosive engagement across audiences. Massive audience reach with viral social media moments. Event became talking point in entertainment industry with strong sentiment and brand association.',
    achievements:[
      {label:'Impact',value:'High'},
      {label:'Engagement',value:'Explosive'},
      {label:'Reach',value:'Massive'}
    ]
  },
  {
    id:'criminal',
    title:'Criminal Movie Premiere',
    category:'Content Production',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Saving-Onome_.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Saving-Onome_.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/dark-october.jpg?w=500',
    client:'Criminal Film',
    challenge:'Execute secure, sophisticated premiere for exclusive thriller release maintaining high security and exclusivity.',
    solution:'Meticulous VIP logistics with comprehensive security protocols. Maintained exclusivity while generating significant media coverage. Coordinated private guest lists, security screening, and VIP parking. Managed media access carefully to protect exclusivity while enabling coverage.',
    results:'Secure execution achieved with flawless VIP management. Professional media coverage captured premium positioning. Premiere established film as exclusive event with strong word-of-mouth among industry insiders.',
    achievements:[
      {label:'Execution',value:'Secure'},
      {label:'Management',value:'Flawless'},
      {label:'Coverage',value:'Professional'}
    ]
  },
  {
    id:'avatar',
    title:'Avatar: The Way of Water',
    category:'Content Production',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/avatar.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/avatar.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Furiosa-Premiere_1.jpg?w=500',
    client:'20th Century Studios',
    challenge:'Translate global blockbuster into locally relevant cultural moment for Nigerian and West African audiences.',
    solution:"Original content production creating Nigeria's first Avatar-inspired cultural landmark. Commissioned iconic mural installation in Lagos combining global blockbuster themes with local artistic expression. Coordinated unveiling ceremony with artist interviews, community engagement, and media partnerships.",
    results:'Iconic landmark created becoming major tourist attraction and cultural talking point. Significant media attention across international and local outlets. Strong cultural resonance with positioning as proudly African artistic response to global phenomenon.',
    achievements:[
      {label:'Creation',value:'Iconic'},
      {label:'Reach',value:'Significant'},
      {label:'Culture',value:'Resonant'}
    ]
  },
  {
    id:'dark-october',
    title:'Dark October',
    category:'PR',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/dark-october.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/dark-october.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Aburo-Movie-Premiere-.jpg?w=500',
    client:'Linda Ikeji Films',
    challenge:'Drive comprehensive multi-platform media coverage for thriller film release with strong genre positioning.',
    solution:'Strategic guest curation including influencers, media personalities, and entertainment journalists. PR management coordinated exclusive interviews, behind-the-scenes content access, and feature opportunities across TV, radio, digital, and print.',
    results:'Multi-platform coverage achieved across all major media channels. Strong media reach with sustained audience interest throughout release period. Positive critical reception with prominent media features and interviews building strong pre-release momentum.',
    achievements:[
      {label:'Platforms',value:'Multi'},
      {label:'Reach',value:'Strong'},
      {label:'Interest',value:'Sustained'}
    ]
  },
  {
    id:'okaidi',
    title:'Okaidi Obaibi',
    category:'Reality',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Okaidi-Obaibi_.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Okaidi-Obaibi_.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Alls-Fair-In-Love_.jpg?w=500',
    client:'Okaidi Productions',
    challenge:'Build strong audience engagement for new reality series in crowded content landscape.',
    solution:'Developed multi-platform marketing strategy with social media teasers, exclusive clips, and influencer partnerships. Created community engagement opportunities through interactive content and viewer participation.',
    results:'Strong community engagement with active viewer participation. Consistent viewership maintained across episodes. Built loyal audience base with sustained return viewership and word-of-mouth recommendations.',
    achievements:[
      {label:'Engagement',value:'High'},
      {label:'Community',value:'Strong'},
      {label:'Viewership',value:'Consistent'}
    ]
  },
  {
    id:'accelerate',
    title:'Accelerate Filmmakers Project',
    category:'Events',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Accelerate-Filmmakers-Project_-scaled.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Accelerate-Filmmakers-Project_-scaled.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/avatar.jpg?w=500',
    client:'Accelerate Program',
    challenge:"Position the Accelerate Filmmakers Project as Africa's premier filmmaker development initiative.",
    solution:'Comprehensive marketing campaign with media partnerships highlighting program impact and filmmaker testimonials, plus launch events and showcases.',
    results:'Increased program visibility across industry and media. Attracted exceptional filmmaker applications from across Africa. Gained significant industry recognition and positioning as leading development platform.',
    achievements:[
      {label:'Visibility',value:'High'},
      {label:'Applications',value:'Increased'},
      {label:'Industry',value:'Recognition'}
    ]
  },
  {
    id:'diana',
    title:'Chief Diana Chen Foundation Scholarships',
    category:'PR',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Diana-Chen-Foundation.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Diana-Chen-Foundation.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Furiosa-Premiere_1.jpg?w=500',
    client:'Chief Diana Chen Foundation',
    challenge:"Elevate the foundation's scholarship program reach and impact across communities.",
    solution:'Strategic PR campaign with community engagement events and media partnerships. Coordinated scholarship announcements, beneficiary stories, and media features.',
    results:'Community-wide reach with strong awareness among target communities. Meaningful beneficiary engagement and elevated foundation visibility.',
    achievements:[
      {label:'Reach',value:'Community'},
      {label:'Beneficiaries',value:'Many'},
      {label:'Impact',value:'Significant'}
    ]
  },
  {
    id:'visa',
    title:'Visa on Arrival Season 5',
    category:'Reality',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Visa-On-Arrival-Watch-Party_5.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Visa-On-Arrival-Watch-Party_5.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/avatar.jpg?w=500',
    client:'Visa on Arrival',
    challenge:'Maintain viewership momentum while attracting new audiences for Season 5 launch.',
    solution:'Multi-platform launch strategy with behind-the-scenes content, exclusive fan events, influencer teasers, and watch parties.',
    results:'Strong audience engagement with high viewership from premiere, growing across the season with expanded viewer base.',
    achievements:[
      {label:'Audience',value:'Engaged'},
      {label:'Reach',value:'Strong'},
      {label:'Momentum',value:'Growing'}
    ]
  },
  {
    id:'mimmi',
    title:"Mimmi Kasu's New Collection – A Piece Of Me",
    category:'Events',
    image:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Media-Round-for-Mimmi-Kasu.jpg?w=650',
    img2:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Media-Round-for-Mimmi-Kasu.jpg?w=500',
    img3:'https://i0.wp.com/savvymediaafrica.com/wp-content/uploads/2024/08/Alls-Fair-In-Love_.jpg?w=500',
    client:'Mimmi Kasu',
    challenge:'Position designer collection as significant cultural moment in fashion industry.',
    solution:'High-production content storytelling combined with strategic media partnerships, fashion show, previews, and influencer collabs.',
    results:'Successful collection launch with extensive industry coverage, strong social engagement, and elevated designer profile.',
    achievements:[
      {label:'Launch',value:'Successful'},
      {label:'Coverage',value:'Extensive'},
      {label:'Buzz',value:'Viral'}
    ]
  }
];

function renderPortfolio(projects = filmProjects){
  const grid = document.getElementById('portfolioGrid');
  grid.innerHTML = projects.map(p => `
    <div class="portfolio-card" onclick="scrollToDetail('${p.id}')">
      <div class="portfolio-image">
        <img src="${p.image}" alt="${p.title}" loading="lazy">
      </div>
      <div class="portfolio-info">
        <span class="portfolio-category">${p.category}</span>
        <h3 class="portfolio-title">${p.title}</h3>
        <p class="portfolio-description" style="overflow:hidden;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical">${p.challenge}</p>
      </div>
    </div>
  `).join('');

  gsap.utils.toArray('.portfolio-card').forEach((card,i)=>{
    gsap.to(card,{
      scrollTrigger:{trigger:card,start:'top 90%'},
      y:0,
      opacity:1,
      duration:0.6,
      delay:i*0.05,
      ease:'back.out(1.5)'
    });
  });
}

function renderDetails(){
  const container = document.getElementById('detailsContainer');
  container.innerHTML = filmProjects.map(p => `
    <section class="detail-section" id="detail-${p.id}">
      <div class="detail-container">
        <div class="detail-header">
          <div class="detail-images">
            <div class="detail-img-main">
              <img src="${p.image}" alt="${p.title}">
            </div>
            <div class="detail-imgs-small">
              <div class="detail-img-small"><img src="${p.img2}" alt="${p.title}"></div>
              <div class="detail-img-small"><img src="${p.img3}" alt="${p.title}"></div>
            </div>
          </div>

          <div class="detail-content">
            <div class="detail-client">${p.client}</div>
            <h2>${p.title}</h2>

            <div class="detail-boxes">
              <div class="detail-box">
                <div class="detail-box-label">Challenge</div>
                <div class="detail-box-text">${p.challenge}</div>
              </div>
              <div class="detail-box">
                <div class="detail-box-label">Solution</div>
                <div class="detail-box-text">${p.solution}</div>
              </div>
              <div class="detail-box">
                <div class="detail-box-label">Results</div>
                <div class="detail-box-text">${p.results}</div>
              </div>
            </div>

            <div class="detail-stats">
              ${p.achievements.map(s => `
                <div class="detail-stat">
                  <div class="detail-stat-number">${s.value}</div>
                  <div class="detail-stat-label">${s.label}</div>
                </div>
              `).join('')}
            </div>
          </div>
        </div>
      </div>
    </section>
  `).join('');
}

function scrollToDetail(id){
  document.querySelectorAll('.detail-section').forEach(el => el.classList.remove('active'));
  const el = document.getElementById(`detail-${id}`);
  if(el){
    el.classList.add('active');
    setTimeout(()=>el.scrollIntoView({behavior:'smooth',block:'start'}),50);
  }
}

// Filters
document.querySelectorAll('.filter-btn').forEach(btn=>{
  btn.addEventListener('click',function(){
    document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
    this.classList.add('active');
    const filter = this.getAttribute('data-filter');
    renderPortfolio(filter === 'all' ? filmProjects : filmProjects.filter(p=>p.category===filter));
  });
});

// Custom cursor
const cursor = document.querySelector('.cursor');
const cursorFollower = document.querySelector('.cursor-follower');

document.addEventListener('mousemove',e=>{
  cursor.style.left = (e.clientX - 4) + 'px';
  cursor.style.top  = (e.clientY - 4) + 'px';
  setTimeout(()=>{
    cursorFollower.style.left = (e.clientX - 16) + 'px';
    cursorFollower.style.top  = (e.clientY - 16) + 'px';
  },60);
});

document.addEventListener('mouseover',e=>{
  if(e.target.closest('a, button, .portfolio-card')){
    cursor.style.transform = 'scale(1.6)';
    cursorFollower.style.transform = 'scale(2.2)';
  }
});

document.addEventListener('mouseout',e=>{
  if(e.target.closest('a, button, .portfolio-card')){
    cursor.style.transform = 'scale(1)';
    cursorFollower.style.transform = 'scale(1)';
  }
});

// Hero animations
gsap.to('.hero-title .word',{
  y:0,scale:1,rotation:0,opacity:1,
  duration:1,
  stagger:0.06,
  ease:'power4.out',
  delay:0.05
});
gsap.to('.hero-subtitle',{opacity:1,duration:0.8,delay:0.8});

gsap.utils.toArray('[data-parallax]').forEach(el=>{
  const amt = +el.getAttribute('data-parallax') || 10;
  gsap.to(el,{
    y:amt,
    scrollTrigger:{trigger:'.hero',start:'top top',end:'bottom top',scrub:1}
  });
});

// Scroll top
const scrollBtn = document.getElementById('scrollTopBtn');
const scrollPct = document.getElementById('scrollPct');

function setScrollProgress(){
  const st = window.scrollY;
  const h  = document.documentElement.scrollHeight - innerHeight;
  const p  = h>0 ? Math.round((st/h)*100) : 0;
  document.documentElement.style.setProperty('--scroll',p);
  scrollBtn.style.setProperty('--scroll',p);
  scrollPct.textContent = p + '%';
  scrollBtn.classList.toggle('visible',st>380);
}

setScrollProgress();
window.addEventListener('scroll',setScrollProgress,{passive:true});
scrollBtn.addEventListener('click',()=>window.scrollTo({top:0,behavior:'smooth'}));

// Init grid + details
renderPortfolio();
renderDetails();
</script>

<!-- load header/footer includes -->
<script src="/include.js"></script>

<!-- header scroll behaviour (waits until header.html is injected) -->
<script>
(function waitForNav(){
  const nav = document.getElementById('nav');
  if(!nav){
    requestAnimationFrame(waitForNav);
    return;
  }
  function handleNavScroll(){
    if(window.scrollY > 80){
      nav.classList.add('scrolled');
    }else{
      nav.classList.remove('scrolled');
    }
  }
  handleNavScroll();
  window.addEventListener('scroll',handleNavScroll,{passive:true});
})();
</script>

</body>
</html>
