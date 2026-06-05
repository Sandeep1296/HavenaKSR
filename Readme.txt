# Havena by KSR — Project Documentation
===============================================
Project : Havena by KSR
Type    : Real Estate Landing Page
Base    : GP Bootstrap Template (BootstrapMade)
Last Updated : June 2025
===============================================


## OVERVIEW
-----------
Single-page real estate marketing website for Havena by KSR, a 2BHK & 3BHK
residential project in Yelahanka, Bangalore. Built on the GP Bootstrap template
with extensive customisations for lead generation, brochure gating, and
performance optimisation.


## FILE STRUCTURE
-----------------
index.html              — Main (and only) page
assets/css/main.css     — All styles including custom overrides
assets/js/main.js       — Core JS (nav, scroll, AOS, Swiper)
assets/img/Reviva/      — Project images, videos, logos, PDF
forms/                  — Original PHP form files (unused, replaced by Google Apps Script)


## KEY ASSETS
-------------
assets/img/Reviva/Havena by KSR.pdf          — Brochure PDF (gated download)
assets/img/Reviva/Havena_Final-Broadband High.mp4   — Hero video (38MB, high quality)
assets/img/Reviva/Havena_Final-Cellular Low.mp4     — Hero video (3.8MB, low quality)
assets/img/Reviva/1.jpg                       — Hero fallback image (video timeout)
assets/img/Reviva/logo-gold-for-black.png     — Header/footer logo
assets/img/Reviva/by-ksr-gold.png             — Hero overlay logo (builder branding)
assets/img/Reviva/SSI_Bangloare_View_01–12.jpg — Gallery slideshow images


## CHANGES MADE
---------------

### 1. CONTACT FORM — Google Apps Script Integration
- Removed PHP form action (forms/contact.php) and method attributes
- Integrated fetch() POST to Google Apps Script endpoint:
  https://script.google.com/macros/s/AKfycbzVqsEr2BUfFzIZ2Dq9yc6NGQMN220YucfOyqJEdKIbMUJw74r3UBanS9LmS1FaPsxTeA/exec
- Form fields: name, email, phone, address, details, source (hidden)
- Removed vendor/php-email-form/validate.js which was causing
  "form action property is not set" error
- Success/error/loading states handled in JS without page reload

### 2. SOURCE TRACKING
- Hidden input <input type="hidden" name="source"> added to contact form
- Default value: "Contact Form" (covers direct/nav visits)
- Each section has a "Contact Us" / "Enquire Now" button with data-source attribute
- JS sets source value on click before form submission
- Sources tracked: Hero, About, Home, Amenities, Master Plan,
  Floor Plan, Gallery, Mobile Bar, Contact Form

### 3. NAVIGATION
- Replaced template dropdown nav with project-specific links:
  Home, About, Amenities, Master Plan, Floor Plan, Gallery, Contact
- "Get Started" button changed to "Enquire Now" linking to #contact
- Footer useful links updated to match section anchors

### 4. NEW SECTIONS ADDED
- #amenities  — 4 amenity cards (Pool, Gardens, Clubhouse, Security)
- #masterplan — Layout image + description
- #floorplan  — 2BHK & 3BHK cards
- #gallery    — Auto Swiper slideshow (SSI_Bangloare_View images)
All new sections include Download Brochure button

### 5. COMMENTED OUT SECTIONS
- First services section (S-Shaped, No Common Walls, RERA, Possession cards)
- Clients/swiper section
- Portfolio section (isotope filter grid)
- Stats section (animated counters)
- Testimonials section
- Team section
- Second services section (template placeholder content)
- Call To Action section (kept HTML for reference)

### 6. HERO SECTION
- Replaced static hero background image (slider-1.jpg) with adaptive video:
  * Broadband/WiFi → Havena_Final-Broadband High.mp4 (38MB)
  * Slow/cellular  → Havena_Final-Cellular Low.mp4 (3.8MB)
  * Detection via navigator.connection.effectiveType
- 3-second fallback: if video hasn't started playing within 3s,
  1.jpg is shown instead and video controls are hidden
- Video controls: play/pause and mute/unmute buttons (bottom-left)
- by-ksr-gold.png overlay (top-right) inside frosted dark pill
- Hero content: tagline (Pacifico font), heading, RERA number, CTA buttons
- "Live the Tropical Vibe" tagline uses Pacifico font

### 7. BROCHURE GATED DOWNLOAD
- All Download Brochure buttons now open a modal form instead of
  directly downloading the PDF
- Modal form fields: name, phone, email + hidden source
- On successful submission → data sent to Google Sheet → PDF auto-downloads
- sessionStorage flag (havena_brochure_unlocked) set after first submission
- Repeat clicks in same session skip modal and download directly
- Auto-pop modal schedule: 30s → 120s → 240s → doubles each time
- Auto-pop stops once user has submitted (sessionStorage check)
- Paired "Enquire Now" buttons removed from all brochure button groups

### 8. LOGO & BRANDING
- Header: replaced <h1>HAVENA</h1> with logo-gold-for-black.png (height: 44px)
- Footer: replaced logo-light.png with logo-gold-for-black.png
- Hero overlay: by-ksr-gold.png at height:40px inside rgba(0,0,0,0.5) pill
  with backdrop-filter blur for visibility on any video frame

### 9. WHATSAPP & MOBILE BAR
- WhatsApp floating button: fixed bottom-right, desktop only (d-none d-md-flex)
  Placeholder number: wa.me/XXXXXXXXXX — replace with actual number
- Sticky mobile bar (d-flex d-md-none): fixed bottom, 3 actions:
  Call Us (tel:+916366097854), WhatsApp, Enquire (→ #contact)
- Scroll-to-top button lifted to bottom:70px on mobile to clear the sticky bar

### 10. BUTTON SYSTEM
- Custom button classes added to main.css:
  .btn-theme-primary   — gold fill, dark text, gold border
  .btn-theme-outline   — transparent, gold border/text
  .btn-theme-dark      — dark fill, gold text/border (used in About section)
  .btn-theme-dark-outline — transparent, dark border/text
  button.brochure-trigger.cta-btn / a.cta-btn — matches hero CTA style
- All button variants include explicit i { color } and :hover i { color }
  rules to prevent icon colour merging on hover
- Features section Download button icon explicitly set to #111 (black)
  to contrast against gold button background

### 11. FEATURES SECTION
- Updated icons to contextually correct Bootstrap Icons:
  bi-telephone-fill, bi-envelope-fill, bi-geo-alt-fill,
  bi-file-earmark-arrow-down-fill
- Phone number wrapped in tel: link
- Email wrapped in mailto: link
- Buttons standardised to btn-theme-primary / btn-theme-outline

### 12. GALLERY SECTION
- Replaced static 6-image grid with Swiper auto-slideshow
- Images: SSI_Bangloare_View_01, 02, 05, 06, 09, 10, 11, 12
- Config: autoplay 3s, loop, 3 slides on desktop, prev/next arrows, pagination
- Swiper arrows and pagination dots styled with --accent-color

### 13. CONTACT SECTION
- Get Directions link added below Google Maps iframe
  Links to: maps/dir/?api=1&destination=Havena+by+KSR...
- Map loads with loading="lazy"

### 14. SEO & META
- Page title: "Havena by KSR | 2BHK & 3BHK Homes in Yelahanka, Bangalore"
- Meta description and keywords updated
- Favicon updated to assets/img/Reviva/favicon.png

### 15. PERFORMANCE OPTIMISATIONS
- Removed unused vendor scripts (total ~101KB saved):
  * glightbox.min.js (55KB) — portfolio section commented out
  * glightbox.min.css (~8KB)
  * isotope.pkgd.min.js (35KB) — portfolio section commented out
  * imagesloaded.pkgd.min.js (5.4KB) — isotope dependency
  * purecounter_vanilla.js (5.3KB) — stats section commented out
- Removed GLightbox, Isotope, imagesLoaded, PureCounter
  initialisers from main.js
- Google Fonts trimmed from all weight variants (~40 variants)
  to only used weights per font:
  Raleway 400/500/600/700, Roboto 300/400/500, Poppins 400/500/600
- Pacifico merged into single Google Fonts request (saves 1 HTTP round trip)
- AOS animation duration reduced to 400ms on mobile (was 600ms)


## GOOGLE APPS SCRIPT
---------------------
Endpoint : https://script.google.com/macros/s/AKfycbzVqsEr2BUfFzIZ2Dq9yc6NGQMN220YucfOyqJEdKIbMUJw74r3UBanS9LmS1FaPsxTeA/exec
Method   : POST (mode: no-cors)
Payload  : JSON { name, email, phone, address, details, source }
           Brochure modal: JSON { name, phone, email, source }
Both forms post to the same endpoint and log to the same Google Sheet.


## PENDING / PLACEHOLDERS
--------------------------
- WhatsApp number: replace XXXXXXXXXX with actual number in 2 places
  (floating button and mobile sticky bar)
- Master Plan image: currently using landscape.jpg as placeholder —
  replace with actual master plan image
- Floor Plan: 2BHK and 3BHK cards are text-only — add floor plan images
- Amenities: generic icons — update with project-specific amenity list
- CTA section (call-to-action): currently uses Play.jpg as background —
  section is visible, update content or comment out
- About section image: currently slider-1.jpg — replace with dedicated about image


## VENDOR LIBRARIES IN USE
---------------------------
Bootstrap 5.3.3     — Layout, modal, grid, utilities
Bootstrap Icons     — All icons throughout the page
AOS                 — Scroll animations (once: true, duration: 600ms)
Swiper              — Hero testimonials slideshow + gallery slideshow
