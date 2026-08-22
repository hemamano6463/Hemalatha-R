src/routes/index.tsx (main page component)
import { createFileRoute } from "@tanstack/react-router";
import { useEffect } from "react";
import { portfolioHtml } from "../portfolioHtml";
import "../portfolio.css";

export const Route = createFileRoute("/")({
  head: () => ({
    meta: [
      { title: "Hemalatha R — Creative Designer Portfolio" },
      {
        name: "description",
        content:
          "Portfolio of Hemalatha R, a creative designer crafting bold brand identities, visual systems and digital experiences.",
      },
      { property: "og:title", content: "Hemalatha R — Creative Designer Portfolio" },
      {
        property: "og:description",
        content:
          "Bold brand identities, visual systems and digital design work by Hemalatha R.",
      },
      { property: "og:type", content: "website" },
      { name: "twitter:card", content: "summary_large_image" },
    ],
  }),
  component: Portfolio,
});

function Portfolio() {
  useEffect(() => {
    const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

    // Hero letter split
    const splitLetters = (id: string, startDelay: number, step: number) => {
      const el = document.getElementById(id);
      if (!el) return;
      const text = el.textContent || "";
      el.textContent = "";
      text.split("").forEach((ch, i) => {
        const span = document.createElement("span");
        span.className = "ch";
        span.style.setProperty("--cd", startDelay + i * step + "s");
        span.textContent = ch;
        el.appendChild(span);
      });
    };
    if (reduceMotion) {
      document
        .querySelectorAll<HTMLElement>(".hero h1 span")
        .forEach((s) => (s.style.opacity = "1"));
    } else {
      splitLetters("fillWord", 0.05, 0.045);
      splitLetters("outlineWord", 0.05 + 4 * 0.045 + 0.03, 0.045);
    }

    // Stagger delays within grids
    const applyStagger = (selector: string, step: number) => {
      document.querySelectorAll(selector).forEach((group) => {
        group.querySelectorAll<HTMLElement>(".reveal-pop").forEach((el, i) => {
          el.style.setProperty("--d", i * step + "s");
        });
      });
    };
    applyStagger(".svc-grid", 0.07);
    applyStagger(".work-grid", 0.06);
    applyStagger(".tools-row", 0.08);

    let io: IntersectionObserver | null = null;
    if (reduceMotion) {
      document
        .querySelectorAll(".reveal, .reveal-pop")
        .forEach((el) => el.classList.add("in"));
    } else {
      io = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              entry.target.classList.add("in");
              io?.unobserve(entry.target);
            }
          });
        },
        { threshold: 0.15, rootMargin: "0px 0px -40px 0px" },
      );
      document.querySelectorAll(".reveal, .reveal-pop").forEach((el) => io!.observe(el));
    }

    // Count-up stats
    let counted = false;
    const countUp = () => {
      if (counted) return;
      counted = true;
      document.querySelectorAll<HTMLElement>(".count").forEach((el) => {
        const target = parseInt(el.getAttribute("data-target") || "0", 10);
        const suffix = el.getAttribute("data-suffix") || "";
        if (reduceMotion) {
          el.textContent = target + suffix;
          return;
        }
        let start: number | null = null;
        const dur = 900;
        const step = (ts: number) => {
          if (!start) start = ts;
          const progress = Math.min((ts - start) / dur, 1);
          const eased = 1 - Math.pow(1 - progress, 3);
          el.textContent = Math.round(eased * target) + suffix;
          if (progress < 1) requestAnimationFrame(step);
        };
        requestAnimationFrame(step);
      });
    };
    const statsEl = document.querySelector(".hero-stats");
    let statsIO: IntersectionObserver | null = null;
    if (statsEl) {
      statsIO = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              countUp();
              statsIO?.disconnect();
            }
          });
        },
        { threshold: 0.4 },
      );
      statsIO.observe(statsEl);
    }

    // Mobile menu
    const burger = document.getElementById("burgerBtn");
    const mobileMenu = document.getElementById("mobileMenu");
    const overlay = document.getElementById("menuOverlay");
    const closeMenu = () => {
      burger?.classList.remove("open");
      mobileMenu?.classList.remove("open");
      overlay?.classList.remove("open");
      burger?.setAttribute("aria-expanded", "false");
      document.body.style.overflow = "";
    };
    const openMenu = () => {
      burger?.classList.add("open");
      mobileMenu?.classList.add("open");
      overlay?.classList.add("open");
      burger?.setAttribute("aria-expanded", "true");
      document.body.style.overflow = "hidden";
    };
    const onBurger = () => {
      if (mobileMenu?.classList.contains("open")) closeMenu();
      else openMenu();
    };
    const onResize = () => {
      if (window.innerWidth > 920) closeMenu();
    };
    const links = mobileMenu ? Array.from(mobileMenu.querySelectorAll("a")) : [];
    if (burger && mobileMenu && overlay) {
      burger.addEventListener("click", onBurger);
      overlay.addEventListener("click", closeMenu);
      links.forEach((a) => a.addEventListener("click", closeMenu));
      window.addEventListener("resize", onResize);
    }
    return () => {
      io?.disconnect();
      statsIO?.disconnect();
      burger?.removeEventListener("click", onBurger);
      overlay?.removeEventListener("click", closeMenu);
      links.forEach((a) => a.removeEventListener("click", closeMenu));
      window.removeEventListener("resize", onResize);
      document.body.style.overflow = "";
    };
  }, []);

  return <div dangerouslySetInnerHTML={{ __html: portfolioHtml }} />;
}

2. src/portfolio.css (styles)


:root{
  --red:#F0303B;
  --red-dark:#C71F29;
  --ink:#161414;
  --cream:#FBF8F3;
  --paper:#FFFFFF;
  --line:#EAE3D8;
  --grey:#6B6560;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;scroll-padding-top:90px;}

/* ---------- Animation keyframes ---------- */
@keyframes fadeUp{
  from{opacity:0;transform:translateY(26px);}
  to{opacity:1;transform:translateY(0);}
}
@keyframes fadeIn{
  from{opacity:0;}
  to{opacity:1;}
}
@keyframes popIn{
  from{opacity:0;transform:scale(.92);}
  to{opacity:1;transform:scale(1);}
}
@keyframes floatY{
  0%,100%{transform:translateY(0);}
  50%{transform:translateY(-8px);}
}
@keyframes spinSlow{
  from{transform:rotate(0deg);}
  to{transform:rotate(360deg);}
}
@keyframes drawLine{
  from{width:0;}
  to{width:34px;}
}

.hero-anim{opacity:0;animation:fadeUp .8s cubic-bezier(.22,.8,.32,1) forwards;}
.hero-anim.d1{animation-delay:.05s;}
.hero-anim.d2{animation-delay:.18s;}
.hero-anim.d3{animation-delay:.34s;}
.hero-anim.d4{animation-delay:.5s;}
.hero-anim.d5{animation-delay:.64s;}

.reveal{opacity:0;transition:opacity .8s ease;}
.reveal.in{opacity:1;}
.reveal-pop{opacity:0;transition:opacity .6s ease;}
.reveal-pop.in{opacity:1;}
.svc-grid .reveal-pop.in,.work-grid .reveal-pop.in,.tools-row .reveal-pop.in{transition-delay:var(--d,0s);}

.pinwheel{animation:spinSlow 40s linear infinite;}
@media (prefers-reduced-motion: reduce){
  .pinwheel{animation:none;}
}
body{
  background:var(--cream);
  color:var(--ink);
  font-family:'Archivo',sans-serif;
  overflow-x:hidden;
  position:relative;
}
body:before{
  content:'';position:fixed;inset:0;pointer-events:none;z-index:1;opacity:.045;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='140' height='140'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  mix-blend-mode:multiply;
}
::selection{background:var(--red);color:#fff;}

.wrap{max-width:1180px;margin:0 auto;padding:0 32px;}

/* ---------- Background blobs ---------- */
.bg-blob{position:absolute;border-radius:50%;filter:blur(70px);pointer-events:none;z-index:0;}
@keyframes blobDriftA{
  0%,100%{transform:translate(0,0) scale(1);}
  50%{transform:translate(30px,-24px) scale(1.08);}
}
@keyframes blobDriftB{
  0%,100%{transform:translate(0,0) scale(1);}
  50%{transform:translate(-26px,22px) scale(1.06);}
}
@media (prefers-reduced-motion: reduce){
  .bg-blob{animation:none !important;}
}

/* ---------- Texture: dot grid & pinwheel triangles ---------- */
.dots{
  display:grid;grid-template-columns:repeat(4,14px);gap:12px;
}
.dots span{width:14px;height:14px;border-radius:50%;background:var(--red);display:block;}

.pinwheel{width:96px;height:96px;position:relative;flex-shrink:0;}
.pinwheel svg{width:100%;height:100%;display:block;}

/* ---------- Nav ---------- */
header{
  position:fixed;top:0;left:0;right:0;z-index:60;
  background:rgba(251,248,243,.88);backdrop-filter:blur(8px);
  border-bottom:1px solid var(--line);
}
.nav{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;padding:18px 32px;max-width:1180px;margin:0 auto;}
.nav .mark{justify-self:start;grid-column:1;}
.nav ul{justify-self:center;grid-column:2;}
.nav .cta{justify-self:end;grid-column:3;}
.nav .burger{justify-self:end;grid-column:3;}
.nav .mark{font-family:'Anton',sans-serif;font-size:22px;letter-spacing:.5px;}
.nav .mark span{color:var(--red);}
.nav ul{display:flex;gap:34px;list-style:none;}
.nav a{color:var(--ink);text-decoration:none;font-weight:600;font-size:14px;letter-spacing:.03em;text-transform:uppercase;position:relative;}
.nav a:after{content:'';position:absolute;left:0;bottom:-6px;width:0;height:2px;background:var(--red);transition:width .25s ease;}
.nav a:hover:after{width:100%;}
.nav .cta{
  background:var(--ink);color:#fff;padding:10px 20px;border-radius:2px;
  text-transform:uppercase;font-weight:700;font-size:13px;letter-spacing:.04em;
}
.nav .cta:after{display:none;}
.nav .cta:hover{background:var(--red);}
.burger{
  display:none;background:none;border:none;cursor:pointer;
  width:34px;height:26px;position:relative;z-index:60;flex-shrink:0;
}
.burger span{
  position:absolute;left:0;width:100%;height:2.4px;background:var(--ink);
  border-radius:2px;transition:transform .3s ease,opacity .3s ease,top .3s ease;
}
.burger span:nth-child(1){top:2px;}
.burger span:nth-child(2){top:12px;}
.burger span:nth-child(3){top:22px;}
.burger.open span:nth-child(1){top:12px;transform:rotate(45deg);}
.burger.open span:nth-child(2){opacity:0;}
.burger.open span:nth-child(3){top:12px;transform:rotate(-45deg);}

.mobile-menu{
  display:none;
  position:fixed;top:0;right:0;height:100vh;width:min(78vw,320px);
  background:var(--ink);z-index:55;
  flex-direction:column;justify-content:center;gap:6px;padding:40px;
  transform:translateX(100%);transition:transform .35s cubic-bezier(.22,.8,.32,1);
}
.mobile-menu.open{transform:translateX(0);}
.mobile-menu a{
  color:#fff;text-decoration:none;font-family:'Anton',sans-serif;font-size:28px;
  padding:14px 0;border-bottom:1px solid #33302e;letter-spacing:.01em;
}
.mobile-menu a.cta-mobile{color:var(--red);}
.menu-overlay{
  display:none;position:fixed;inset:0;background:rgba(22,20,20,.5);z-index:54;
  opacity:0;transition:opacity .3s ease;pointer-events:none;
}
.menu-overlay.open{opacity:1;pointer-events:auto;}

/* ---------- Hero ---------- */
.hero{
  position:relative;
  padding:170px 0 90px;
  overflow:hidden;
}
.hero .wrap{position:relative;z-index:2;}
.corner-tl, .corner-br{position:absolute;opacity:.9;}
.corner-tl{top:24px;left:24px;}
.corner-br{bottom:24px;right:24px;transform:rotate(180deg);}

.hero .eyebrow{
  display:flex;align-items:center;gap:10px;
  font-size:13px;letter-spacing:.14em;text-transform:uppercase;font-weight:700;color:var(--red-dark);
  margin-bottom:22px;
}
.hero .eyebrow:before{content:'';width:34px;height:2px;background:var(--red);display:inline-block;}

.hero h1{
  font-family:'Anton',sans-serif;
  font-weight:400;
  line-height:.9;
  font-size:clamp(64px,12vw,176px);
  letter-spacing:-.01em;
}
.hero h1 .fill{color:var(--red);-webkit-text-stroke:1px var(--red);}
.hero h1 .outline{
  color:transparent;-webkit-text-stroke:1.6px var(--ink);
}
.hero h1 .ch{display:inline-block;opacity:0;transform:translateY(60px) rotate(6deg);animation:letterIn .7s cubic-bezier(.2,.9,.25,1.2) forwards;animation-delay:var(--cd,0s);}
@keyframes letterIn{
  to{opacity:1;transform:translateY(0) rotate(0deg);}
}
.hero .signature{
  font-family:'Caveat',cursive;
  font-weight:700;
  font-size:clamp(46px,7.5vw,96px);
  color:var(--ink);
  margin-top:4px;
  filter:drop-shadow(2px 3px 0 var(--cream));
  display:inline-block;
  opacity:0;
  transform:scale(.6) rotate(-4deg);
  animation:sigPop .8s cubic-bezier(.34,1.56,.64,1) forwards;
  animation-delay:1.05s;
  transform-origin:left bottom;
}
@keyframes sigPop{
  60%{opacity:1;transform:scale(1.08) rotate(1deg);}
  to{opacity:1;transform:scale(1) rotate(0deg);}
}
.hero-sub{
  display:flex;gap:60px;align-items:flex-end;flex-wrap:wrap;
  margin-top:46px;
}
.hero-copy{max-width:430px;}
.hero-copy p{font-size:17px;line-height:1.65;color:#3a3634;}
.hero-tags{display:flex;flex-wrap:wrap;gap:10px;margin-top:22px;}
.hero-tags span{
  border:1.4px solid var(--ink);padding:7px 14px;font-size:12.5px;font-weight:700;
  text-transform:uppercase;letter-spacing:.04em;border-radius:999px;
}
.hero-stats{display:flex;gap:38px;}
.hero-stats div b{
  font-family:'Anton',sans-serif;font-size:44px;color:var(--red);display:block;line-height:1;
}
.hero-stats div span{font-size:12.5px;text-transform:uppercase;letter-spacing:.05em;color:var(--grey);font-weight:700;}

/* ---------- Section heading pattern ---------- */
.heading{display:flex;align-items:baseline;gap:16px;margin-bottom:44px;}
.heading h2{
  font-family:'Anton',sans-serif;font-weight:400;font-size:clamp(34px,5vw,54px);
}
.heading h2 .out{color:transparent;-webkit-text-stroke:1.3px var(--ink);}
.heading .num{font-family:'Caveat',cursive;font-weight:700;color:var(--red);font-size:26px;}
section{padding:100px 0;position:relative;}
.section-line{border-top:1px solid var(--line);}

/* ---------- About ---------- */
.about{display:grid;grid-template-columns:.85fr 1.15fr;gap:70px;align-items:center;}
.about-portrait{position:relative;animation:portraitFloat 5.5s ease-in-out infinite;}
.about-portrait .frame{
  position:relative;border:2px solid var(--ink);padding:14px;background:var(--paper);
  transition:transform .5s cubic-bezier(.22,.8,.32,1),box-shadow .5s ease;
  transform-style:preserve-3d;
}
.about-portrait .frame:before{
  content:'';position:absolute;inset:-2px;border:2px solid var(--red);opacity:0;
  transition:opacity .4s ease,transform .5s ease;transform:scale(.96);pointer-events:none;
}
.about-portrait:hover .frame{transform:rotate(-1.5deg) scale(1.02);box-shadow:14px 14px 0 rgba(240,48,59,.18);}
.about-portrait:hover .frame:before{opacity:1;transform:scale(1.035);}
.about-portrait img{width:100%;display:block;filter:grayscale(6%);transition:filter .5s ease;}
.about-portrait:hover img{filter:grayscale(0%);}
.about-portrait .tag{
  position:absolute;bottom:-22px;left:-22px;background:var(--red);color:#fff;
  padding:14px 20px;font-family:'Anton',sans-serif;font-size:15px;letter-spacing:.02em;
  box-shadow:6px 6px 0 var(--ink);transition:transform .35s ease;
}
.about-portrait:hover .tag{transform:translate(-3px,3px);}
@keyframes portraitFloat{
  0%,100%{transform:translateY(0);}
  50%{transform:translateY(-12px);}
}
@media (prefers-reduced-motion: reduce){
  .about-portrait{animation:none;}
}
.about-text p{font-size:17px;line-height:1.75;color:#3a3634;margin-bottom:18px;}
.about-text .credo{
  font-family:'Caveat',cursive;font-size:34px;color:var(--red-dark);font-weight:700;margin:22px 0 26px;
}
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-top:28px;}
.about-grid .item{border-left:3px solid var(--red);padding-left:14px;}
.about-grid .item b{display:block;font-size:14px;text-transform:uppercase;letter-spacing:.04em;margin-bottom:4px;}
.about-grid .item span{font-size:13.5px;color:var(--grey);}

/* ---------- Services ---------- */
.services{background:var(--ink);color:var(--cream);}
.services .heading h2{color:var(--cream);}
.services .heading h2 .out{color:transparent;-webkit-text-stroke:1.3px var(--cream);}
.services .heading .num{color:var(--red);}
.svc-grid{display:grid;grid-template-columns:repeat(2,1fr);grid-auto-flow:column;grid-template-rows:repeat(5,auto);gap:1px;background:#33302e;border:1px solid #33302e;}
.svc-card{background:var(--ink);padding:34px 28px;transition:background .25s ease;}
.svc-card:hover{background:#221f1e;}
.svc-card .idx{font-family:'Caveat',cursive;color:var(--red);font-size:24px;font-weight:700;}
.svc-card h3{font-family:'Archivo',sans-serif;font-weight:800;font-size:19px;margin:10px 0 8px;letter-spacing:-.01em;}
.svc-card p{font-size:13.5px;color:#B9B2AC;line-height:1.55;}

/* ---------- Tools ---------- */
.tools .heading{margin-bottom:36px;}
.tools-row{display:flex;gap:20px;flex-wrap:wrap;}
.tool-chip{
  display:flex;align-items:center;gap:12px;border:1.4px solid var(--ink);padding:16px 22px;
  font-weight:800;font-size:15px;letter-spacing:.01em;background:var(--paper);
}
.tool-chip .dot{width:9px;height:9px;background:var(--red);border-radius:50%;}

/* ---------- Work Gallery ---------- */
.work-grid{
  display:grid;grid-template-columns:repeat(3,1fr);gap:26px;
}
.work-card{
  position:relative;overflow:hidden;background:var(--paper);border:1px solid var(--line);
  break-inside:avoid;
}
.work-card img{width:100%;display:block;transition:transform .5s ease;}
.work-card:hover img{transform:scale(1.045);}
.work-card .cap{
  position:absolute;left:0;right:0;bottom:0;padding:16px 18px;
  background:linear-gradient(0deg,rgba(22,20,20,.88),transparent);
  color:#fff;opacity:0;transform:translateY(8px);transition:all .3s ease;
}
.work-card:hover .cap{opacity:1;transform:translateY(0);}
.work-card .cap b{display:block;font-size:14.5px;font-weight:800;}
.work-card .cap span{font-size:11.5px;color:#e7dfd6;text-transform:uppercase;letter-spacing:.05em;}
.work-card.wide{grid-column:span 2;display:flex;align-items:center;justify-content:center;}
.work-card.wide img{width:100%;height:auto;object-fit:contain;align-self:center;}

/* ---------- Contact ---------- */
.contact{
  background:var(--red);color:#fff;position:relative;overflow:hidden;
}
.contact .wrap{position:relative;z-index:2;}
.contact .heading h2{color:#fff;}
.contact .heading h2 .out{color:transparent;-webkit-text-stroke:1.3px #fff;}
.contact .heading .num{color:var(--ink);}
.contact-grid{display:grid;grid-template-columns:1.2fr .8fr;gap:60px;align-items:end;}
.contact-lead{font-family:'Anton',sans-serif;font-size:clamp(30px,4.6vw,50px);line-height:1.08;max-width:640px;}
.contact-list{display:flex;flex-direction:column;gap:22px;margin-top:14px;}
.contact-list a{
  color:#fff;text-decoration:none;font-size:19px;font-weight:700;
  display:flex;justify-content:space-between;align-items:baseline;gap:18px;flex-wrap:wrap;
  border-bottom:1.4px solid rgba(255,255,255,.4);padding-bottom:14px;
}
.contact-list a span:first-child{color:#FFE3E1;font-size:12px;text-transform:uppercase;letter-spacing:.08em;font-weight:800;flex-shrink:0;}
.contact-list a span:last-child{text-align:right;}
.contact-list a:hover{border-color:#fff;}
.contact .bigsig{
  font-family:'Caveat',cursive;font-weight:700;font-size:clamp(40px,7vw,92px);
  text-align:right;opacity:.95;white-space:nowrap;
}
.contact-tri{position:absolute;opacity:.18;}

footer{
  background:var(--ink);color:#B9B2AC;padding:26px 0;font-size:12.5px;
  display:flex;justify-content:space-between;align-items:center;
}
footer b{color:#fff;}

@media(max-width:920px){
  .about{grid-template-columns:1fr;}
  .svc-grid{grid-template-columns:repeat(2,1fr);}
  .work-grid{grid-template-columns:repeat(2,1fr);}
  .work-card.wide{grid-column:span 1;}
  .contact-grid{grid-template-columns:1fr;gap:36px;}
  .contact .bigsig{text-align:left;}
  .nav ul{display:none;}
  .nav .cta{display:none;}
  .burger{display:block;}
  .mobile-menu{display:flex;}
  .menu-overlay{display:block;}
}
@media(max-width:600px){
  .svc-grid{grid-template-columns:1fr;grid-auto-flow:row;grid-template-rows:none;}
  .work-grid{grid-template-columns:1fr;}
  .hero-sub{gap:30px;}
  .wrap{padding:0 20px;}
  .hero h1{font-size:15vw;line-height:.95;}
  .hero .signature{font-size:11vw;}
}

@media (prefers-reduced-motion: reduce){
  *{transition:none !important;animation:none !important;}
}



3. src/portfolioHtml.ts



This file contains the HTML markup as a JavaScript string, including your images (embedded as base64). It is very large because of the image data. You can view it in the project editor under src/portfolioHtml.ts.



4. src/routes/__root.tsx (root layout with fonts)


import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import {
  Outlet,
  Link,
  createRootRouteWithContext,
  useRouter,
  HeadContent,
  Scripts,
} from "@tanstack/react-router";
import { useEffect, type ReactNode } from "react";

import appCss from "../styles.css?url";
import { reportLovableError } from "../lib/lovable-error-reporting";

function NotFoundComponent() {
  return (
    <div className="flex min-h-screen items-center justify-center bg-background px-4">
      <div className="max-w-md text-center">
        <h1 className="text-7xl font-bold text-foreground">404</h1>
        <h2 className="mt-4 text-xl font-semibold text-foreground">Page not found</h2>
        <p className="mt-2 text-sm text-muted-foreground">
          The page you're looking for doesn't exist or has been moved.
        </p>
        <div className="mt-6">
          <Link
            to="/"
            className="inline-flex items-center justify-center rounded-md bg-primary px-4 py-2 text-sm font-medium text-primary-foreground transition-colors hover:bg-primary/90"
          >
            Go home
          </Link>
        </div>
      </div>
    </div>
  );
}

function ErrorComponent({ error, reset }: { error: Error; reset: () => void }) {
  console.error(error);
  const router = useRouter();
  useEffect(() => {
    reportLovableError(error, { boundary: "tanstack_root_error_component" });
  }, [error]);

  return (
    <div className="flex min-h-screen items-center justify-center bg-background px-4">
      <div className="max-w-md text-center">
        <h1 className="text-xl font-semibold tracking-tight text-foreground">
          This page didn't load
        </h1>
        <p className="mt-2 text-sm text-muted-foreground">
          Something went wrong on our end. You can try refreshing or head back home.
        </p>
        <div className="mt-6 flex flex-wrap justify-center gap-2">
          <button
            onClick={() => {
              router.invalidate();
              reset();
            }}
            className="inline-flex items-center justify-center rounded-md bg-primary px-4 py-2 text-sm font-medium text-primary-foreground transition-colors hover:bg-primary/90"
          >
            Try again
          </button>
          <a
            href="/"
            className="inline-flex items-center justify-center rounded-md border border-input bg-background px-4 py-2 text-sm font-medium text-foreground transition-colors hover:bg-accent"
          >
            Go home
          </a>
        </div>
      </div>
    </div>
  );
}

export const Route = createRootRouteWithContext<{ queryClient: QueryClient }>()({
  head: () => ({
    meta: [
      { charSet: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      { title: "Lovable App" },
      { name: "description", content: "Lovable Generated Project" },
      { name: "author", content: "Lovable" },
      { property: "og:title", content: "Lovable App" },
      { property: "og:description", content: "Lovable Generated Project" },
      { property: "og:type", content: "website" },
      { name: "twitter:card", content: "summary_large_image" },
      { name: "twitter:site", content: "@Lovable" },
    ],
    links: [
      {
        rel: "stylesheet",
        href: appCss,
      },
      { rel: "icon", href: "/favicon.ico", type: "image/x-icon" },
      { rel: "preconnect", href: "https://fonts.googleapis.com" },
      { rel: "preconnect", href: "https://fonts.gstatic.com", crossOrigin: "anonymous" },
      {
        rel: "stylesheet",
        href: "https://fonts.googleapis.com/css2?family=Anton&family=Caveat:wght@500;700&family=Archivo:wght@400;500;600;700;800;900&display=swap",
      },
    ],
  }),
  shellComponent: RootShell,
  component: RootComponent,
  notFoundComponent: NotFoundComponent,
  errorComponent: ErrorComponent,
});

function RootShell({ children }: { children: ReactNode }) {
  return (
    <html lang="en">
      <head>
        <HeadContent />
      </head>
      <body>
        {children}
        <Scripts />
      </body>
    </html>
  );
}

function RootComponent() {
  const { queryClient } = Route.useRouteContext();

  return (
    <QueryClientProvider client={queryClient}>
      <Outlet />
    </QueryClientProvider>
  );
}
