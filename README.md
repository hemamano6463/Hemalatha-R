<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Hemalatha R | Creative Designer</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html{
    scroll-behavior:smooth;
}

body{
    font-family:Arial, Helvetica, sans-serif;
    background:#f7f5f0;
    color:#171717;
    line-height:1.6;
}

a{
    text-decoration:none;
    color:inherit;
}

.container{
    width:90%;
    max-width:1200px;
    margin:auto;
}


/* ================= HEADER ================= */

header{
    position:sticky;
    top:0;
    z-index:1000;
    background:#f7f5f0;
    border-bottom:1px solid #ddd8ce;
}

.nav{
    height:80px;
    display:flex;
    align-items:center;
    justify-content:space-between;
}

.logo{
    font-size:25px;
    font-weight:800;
    letter-spacing:2px;
}

.logo span{
    color:#b58b42;
}

nav{
    display:flex;
    align-items:center;
    gap:35px;
}

nav a{
    font-size:14px;
    font-weight:600;
    transition:.3s;
}

nav a:hover{
    color:#b58b42;
}

.talk{
    background:#171717;
    color:white;
    padding:12px 22px;
    border-radius:30px;
}

.talk:hover{
    background:#b58b42;
    color:white;
}


/* ================= HERO ================= */

.hero{
    min-height:90vh;
    display:flex;
    align-items:center;
    border-bottom:1px solid #ddd8ce;
}

.hero-content{
    padding:80px 0;
}

.small-title{
    color:#b58b42;
    font-size:14px;
    font-weight:bold;
    letter-spacing:3px;
    margin-bottom:20px;
}

.hero h1{
    font-size:clamp(70px,12vw,170px);
    line-height:.78;
    letter-spacing:-7px;
    font-weight:900;
    margin-bottom:30px;
}

.hero h2{
    font-size:35px;
    margin-bottom:20px;
}

.hero-description{
    max-width:650px;
    font-size:18px;
    color:#555;
}

.tags{
    display:flex;
    flex-wrap:wrap;
    gap:10px;
    margin-top:30px;
}

.tags span{
    border:1px solid #bbb3a6;
    border-radius:30px;
    padding:8px 16px;
    font-size:13px;
}

.stats{
    display:flex;
    gap:70px;
    margin-top:60px;
}

.stat strong{
    display:block;
    font-size:35px;
}

.stat span{
    color:#777;
    font-size:13px;
}


/* ================= SECTIONS ================= */

section{
    padding:110px 0;
}

.section-top{
    display:flex;
    gap:20px;
    align-items:center;
    margin-bottom:15px;
}

.section-number{
    color:#b58b42;
    font-weight:bold;
}

.section-label{
    letter-spacing:3px;
    font-size:13px;
    font-weight:bold;
}

.section-title{
    font-size:clamp(40px,6vw,75px);
    line-height:1;
    margin-bottom:60px;
}

.section-subtitle{
    color:#777;
    font-size:14px;
}


/* ================= ABOUT ================= */

.about{
    background:#171717;
    color:white;
}

.about .section-title{
    color:white;
}

.about-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:80px;
}

.about-text h3{
    font-size:28px;
    margin-bottom:25px;
}

.about-text p{
    color:#c5c5c5;
    font-size:17px;
    margin-bottom:20px;
}

.quote{
    margin-top:35px;
    border-left:3px solid #b58b42;
    padding-left:20px;
    font-size:22px;
    font-style:italic;
}

.about-items{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:1px;
    background:#444;
}

.about-item{
    background:#171717;
    padding:35px 25px;
}

.about-item h4{
    color:#b58b42;
    margin-bottom:8px;
}

.about-item p{
    color:#aaa;
    font-size:14px;
}


/* ================= SERVICES ================= */

.services-grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:1px;
    background:#ccc5b9;
    border:1px solid #ccc5b9;
}

.service{
    background:#f7f5f0;
    padding:40px;
    min-height:210px;
    transition:.3s;
}

.service:hover{
    background:#171717;
    color:white;
}

.service-number{
    color:#b58b42;
    font-size:13px;
    font-weight:bold;
}

.service h3{
    font-size:24px;
    margin:25px 0 12px;
}

.service p{
    color:#777;
    font-size:14px;
}

.service:hover p{
    color:#bbb;
}


/* ================= TOOLS ================= */

.tools{
    background:#e9e5dc;
}

.tools-list{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:20px;
}

.tool{
    background:#171717;
    color:white;
    padding:35px;
    text-align:center;
    font-size:20px;
    font-weight:bold;
    border-radius:4px;
}


/* ================= WORK ================= */

.work-grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:30px;
}

.work-card{
    background:white;
    border:1px solid #ddd8ce;
    overflow:hidden;
    transition:.3s;
}

.work-card:hover{
    transform:translateY(-5px);
    box-shadow:0 15px 35px rgba(0,0,0,.08);
}

.work-image{
    height:300px;
    background:#e8e3da;
    display:flex;
    align-items:center;
    justify-content:center;
}

.work-image img{
    width:100%;
    height:100%;
    object-fit:cover;
}

.placeholder{
    color:#888;
    text-align:center;
    padding:20px;
}

.work-info{
    padding:25px;
    display:flex;
    gap:20px;
}

.work-info span{
    color:#b58b42;
    font-weight:bold;
}

.work-info h3{
    font-size:18px;
}


/* ================= CONTACT ================= */

.contact{
    background:#171717;
    color:white;
}

.contact-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:80px;
}

.contact h3{
    font-size:40px;
    margin-bottom:20px;
}

.contact-text p{
    color:#aaa;
    font-size:18px;
}

.contact-details{
    display:flex;
    flex-direction:column;
    gap:25px;
}

.contact-item span{
    display:block;
    color:#b58b42;
    font-size:12px;
    letter-spacing:2px;
    margin-bottom:5px;
}

.contact-item a{
    font-size:19px;
}

.contact-item a:hover{
    color:#b58b42;
}

.whatsapp{
    display:inline-block;
    margin-top:40px;
    background:#b58b42;
    color:white;
    padding:14px 28px;
    border-radius:30px;
    font-weight:bold;
}

.whatsapp:hover{
    background:white;
    color:#171717;
}


/* ================= FOOTER ================= */

footer{
    background:#111;
    color:#888;
    padding:35px 0;
    text-align:center;
    font-size:13px;
}

footer strong{
    color:white;
}


/* ================= MOBILE ================= */

@media(max-width:768px){

    .nav{
        height:auto;
        padding:20px 0;
        flex-direction:column;
        gap:20px;
    }

    nav{
        gap:15px;
        flex-wrap:wrap;
        justify-content:center;
    }

    nav a{
        font-size:12px;
    }

    .hero{
        min-height:auto;
    }

    .hero h1{
        font-size:75px;
        letter-spacing:-4px;
    }

    .hero h2{
        font-size:28px;
    }

    .stats{
        gap:25px;
        flex-wrap:wrap;
    }

    .about-grid,
    .contact-grid{
        grid-template-columns:1fr;
        gap:45px;
    }

    .services-grid{
        grid-template-columns:1fr;
    }

    .tools-list{
        grid-template-columns:1fr;
    }

    .work-grid{
        grid-template-columns:1fr;
    }

    .about-items{
        grid-template-columns:1fr;
    }

    section{
        padding:75px 0;
    }

    .section-title{
        margin-bottom:40px;
    }

}

</style>
</head>


<body>


<!-- ================= HEADER ================= -->

<header>

<div class="container nav">

<a href="#home" class="logo">
HEMALATHA<span>.</span>
</a>

<nav>

<a href="#about">About</a>

<a href="#services">Services</a>

<a href="#work">Work</a>

<a href="#contact">Contact</a>

<a href="#contact" class="talk">Let's Talk</a>

</nav>

</div>

</header>



<!-- ================= HERO ================= -->

<section id="home" class="hero">

<div class="container hero-content">

<div class="small-title">
CREATIVE DESIGNER
</div>

<h1>
PORT<br>
FOLIO
</h1>

<h2>
Hemalatha R
</h2>

<p class="hero-description">
I turn ideas into professional designs that leave a lasting
impression — logos, menus, brochures, packaging and social
media designs created with care and creativity.
</p>

<div class="tags">

<span>Logo Design</span>

<span>Print Design</span>

<span>Social Media</span>

<span>Brand Identity</span>

</div>


<div class="stats">

<div class="stat">

<strong>5+</strong>

<span>Years Experience</span>

</div>


<div class="stat">

<strong>10</strong>

<span>Design Services</span>

</div>


<div class="stat">

<strong>3</strong>

<span>Design Tools</span>

</div>

</div>

</div>

</section>



<!-- ================= ABOUT ================= -->

<section id="about" class="about">

<div class="container">

<div class="section-top">

<span class="section-number">01</span>

<span class="section-label">ABOUT</span>

</div>

<h2 class="section-title">
Creating What<br>
Others Imagine
</h2>


<div class="about-grid">

<div class="about-text">

<h3>
About Me
</h3>

<p>
I am Hemalatha R, a Creative Designer and
Administrative Professional with experience in
administration, coordination and digital design.
</p>

<p>
I transform ideas into professional designs that
leave a lasting impression, combining creativity
with a detail-oriented approach.
</p>

<div class="quote">
"Creating What Others Imagine"
</div>

</div>


<div class="about-items">

<div class="about-item">

<h4>Administration</h4>

<p>
Coordination & process
</p>

</div>


<div class="about-item">

<h4>Digital Design</h4>

<p>
Print, branding & social media
</p>

</div>


<div class="about-item">

<h4>Detail-Led</h4>

<p>
Every project, client-ready
</p>

</div>


<div class="about-item">

<h4>Full-Cycle</h4>

<p>
Concept through final delivery
</p>

</div>

</div>

</div>

</div>

</section>



<!-- ================= SERVICES ================= -->

<section id="services">

<div class="container">

<div class="section-top">

<span class="section-number">02</span>

<span class="section-label">SERVICES</span>

</div>

<h2 class="section-title">
What I Design
</h2>


<div class="services-grid">


<div class="service">

<span class="service-number">01</span>

<h3>Logo Design</h3>

<p>
Distinctive logos built around your brand story.
</p>

</div>


<div class="service">

<span class="service-number">02</span>

<h3>Flyer Design</h3>

<p>
Creative promotional flyers for offers and announcements.
</p>

</div>


<div class="service">

<span class="service-number">03</span>

<h3>Menu Card Design</h3>

<p>
Professional and attractive restaurant menu designs.
</p>

</div>


<div class="service">

<span class="service-number">04</span>

<h3>Brochure Design</h3>

<p>
Multi-page brochures for businesses and organisations.
</p>

</div>


<div class="service">

<span class="service-number">05</span>

<h3>Product Label & Packaging</h3>

<p>
Professional packaging and product label designs.
</p>

</div>


<div class="service">

<span class="service-number">06</span>

<h3>Invitation Design</h3>

<p>
Beautiful invitations for special occasions and events.
</p>

</div>


<div class="service">

<span class="service-number">07</span>

<h3>Business Card Design</h3>

<p>
Professional business cards that represent your brand.
</p>

</div>


<div class="service">

<span class="service-number">08</span>

<h3>Social Media Design</h3>

<p>
Eye-catching posts and promotional social media graphics.
</p>

</div>


<div class="service">

<span class="service-number">09</span>

<h3>Poster & Advertisement</h3>

<p>
Bold promotional posters designed to grab attention.
</p>

</div>


<div class="service">

<span class="service-number">10</span>

<h3>ID Card Design</h3>

<p>
Professional ID card designs for schools and organisations.
</p>

</div>


</div>

</div>

</section>



<!-- ================= TOOLS ================= -->

<section class="tools">

<div class="container">

<div class="section-top">

<span class="section-number">03</span>

<span class="section-label">TOOLS</span>

</div>

<h2 class="section-title">
Design Tools
</h2>

<div class="tools-list">

<div class="tool">
Canva
</div>

<div class="tool">
Adobe Photoshop
</div>

<div class="tool">
CorelDRAW
</div>

</div>

</div>

</section>



<!-- ================= WORK ================= -->

<section id="work">

<div class="container">

<div class="section-top">

<span class="section-number">04</span>

<span class="section-label">PORTFOLIO</span>

</div>

<h2 class="section-title">
Featured Work
</h2>


<div class="work-grid">


<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Logo Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>01</span>

<h3>
Logo Design
</h3>

</div>

</div>



<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Flyer Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>02</span>

<h3>
Flyer Design
</h3>

</div>

</div>



<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Menu Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>03</span>

<h3>
Menu Card Design
</h3>

</div>

</div>



<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Brochure Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>04</span>

<h3>
Brochure Design
</h3>

</div>

</div>



<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Packaging Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>05</span>

<h3>
Product Packaging
</h3>

</div>

</div>



<div class="work-card">

<div class="work-image">

<div class="placeholder">
Your Social Media Design<br>
Add your project image here
</div>

</div>

<div class="work-info">

<span>06</span>

<h3>
Social Media Design
</h3>

</div>

</div>


</div>

</div>

</section>



<!-- ================= CONTACT ================= -->

<section id="contact" class="contact">

<div class="container">

<div class="section-top">

<span class="section-number">05</span>

<span class="section-label">CONTACT</span>

</div>

<h2 class="section-title">
Let's Work Together
</h2>


<div class="contact-grid">


<div class="contact-text">

<h3>
Have a project in mind?
</h3>

<p>
I'd love to help bring your idea to life.
Let's create something professional
together.
</p>

<a
href="https://wa.me/918610578887"
target="_blank"
class="whatsapp"
>
Chat on WhatsApp
</a>

</div>


<div class="contact-details">


<div class="contact-item">

<span>EMAIL</span>

<a href="mailto:mayilwings26@gmail.com">
mayilwings26@gmail.com
</a>

</div>


<div class="contact-item">

<span>PHONE</span>

<a href="tel:+918610578887">
8610578887
</a>

</div>


<div class="contact-item">

<span>INSTAGRAM</span>

<a
href="https://instagram.com/mayil_wings"
target="_blank"
>
@mayil_wings
</a>

</div>


</div>

</div>

</div>

</section>



<!-- ================= FOOTER ================= -->

<footer>

<div class="container">

<p>
© 2026 <strong>Hemalatha R</strong> · Creative Designer
</p>

<p>
Creating What Others Imagine
</p>

</div>

</footer>


</body>
</html>
