# 🍽️ Gastro-App Website

**Marketing- & Landingpage** für individuell entwickelte **Gastronomie-Apps mit KI**  
Stack: **Next.js 15 · React 19 · TypeScript · Tailwind CSS v4 · shadcn/ui · Vercel**  
Add-ons: **Cal.com (Buchungen) · Resend (E-Mail) · Plausible (Analytics) · optional Supabase (Leads/DB)**

---

## Inhaltsverzeichnis

- [Überblick](#überblick)
- [Features](#features)
- [Tech-Stack](#tech-stack)
- [Projektstruktur](#projektstruktur)
- [Schnellstart](#schnellstart)
- [Umgebungsvariablen](#umgebungsvariablen)
- [Nützliche Scripts](#nützliche-scripts)
- [Integrationen](#integrationen)
  - [Resend (Kontaktformular)](#resend-kontaktformular)
  - [Cal.com (Terminbuchung)](#calcom-terminbuchung)
  - [Plausible (Analytics)](#plausible-analytics)
  - [Supabase (optional)](#supabase-optional)
- [SEO & Performance](#seo--performance)
- [Barrierefreiheit](#barrierefreiheit)
- [Entwicklungsrichtlinien](#entwicklungsrichtlinien)
- [Deployment](#deployment)
- [Roadmap](#roadmap)
- [Lizenz](#lizenz)

---

## Überblick

Diese Website dient als **Conversion-getriebene Landingpage** für dein B2B-Angebot: **maßgeschneiderte Gastro-Apps mit KI** (Speisekarte, Öffnungszeiten, Bestellungen, Reservierungen, Loyalty, KI-Chat/RAG).  
Ziel: **Leads generieren** (Kontaktformular + Terminbuchung), **Vertrauen aufbauen** (Referenz/Case Study) und **Preise transparent** zeigen.

---

## Features

- **Landingpage** mit Hero, Nutzenargumentation, Feature-Grid, Referenz/Fallstudie, Preistabelle, FAQ, CTAs
- **Preise**: vier Pakete (Basic / Standard / Premium / Enterprise) + laufende Kosten
- **Kontakt**: Formular (Server-Route), Versand via **Resend**
- **Terminbuchung**: **Cal.com** Link/Embed
- **SEO**: strukturierte Metadaten, Open Graph, `next-sitemap`
- **Analytics**: **Plausible** (datenschutzfreundlich)
- **Rechtliches**: Impressum, Datenschutz
- **Optional**: Blog, Case Studies, Features-Detailseiten
- **Optional**: **Supabase** für Lead-Persistenz/Admin

---

## Tech-Stack

- **Next.js 15** (App Router, SSR/SSG/ISR, RSC)
- **React 19** + **TypeScript**
- **Tailwind CSS v4** (Utility-First, ohne Config-Overhead)
- **shadcn/ui** (komponentenbasiert, design-system-freundlich)
- **lucide-react** (Icons)
- **Vercel** (Hosting/Preview Deploys)
- Add-ons: **Resend**, **Cal.com**, **Plausible**, optional **Supabase**

---

## Projektstruktur

```txt
app/
  (marketing)/
    page.tsx               # Landingpage
    components/
      Hero.tsx
      FeatureGrid.tsx
      PricingTable.tsx
      Testimonial.tsx
      FAQ.tsx
      CTA.tsx
  preise/
    page.tsx
  kontakt/
    page.tsx
  api/
    contact/route.ts       # POST -> Resend
  impressum/
    page.tsx
  datenschutz/
    page.tsx
components/
  ui/                      # shadcn/ui Komponenten
  layout/
    Navbar.tsx
    Footer.tsx
lib/
  validators/              # zod Schemata
  utils.ts
  plausible.ts             # optional Event-Helper
  supabase.ts              # optional Client
public/
  og-image.png
  favicon.ico
styles/
  globals.css
.env.example
README.md
```

Schnellstart

Voraussetzung: Node 20+ (empfohlen), npm oder pnpm

# 1) Repo klonen

git clone git@github.com:DEINUSERNAME/gastro-app-website.git
cd gastro-app-website

# 2) Dependencies installieren

npm install

# 3) Env-Datei anlegen

cp .env.example .env.local

# ...Werte eintragen (siehe unten)

# 4) Development-Server starten

npm run dev

# http://localhost:3000

# 5) Production Build (optional)

npm run build && npm run start

Umgebungsvariablen

Lege .env.local mit folgenden Schlüsseln an (Beispielwerte ersetzen):

# --- Resend (Server-only) ---

RESEND*API_KEY=re***************\*\*\*\***************
RESEND_FROM="Dein Name <kontakt@deinedomain.de>"

# --- Cal.com (Client) ---

NEXT_PUBLIC_CALCOM_LINK=deinname/demo

# --- Plausible (Client) ---

NEXT_PUBLIC_PLAUSIBLE_DOMAIN=deinedomain.de

# optional wenn Proxy/Custom Host

PLAUSIBLE_API_HOST=https://plausible.io

# --- Site URLs ---

SITE_URL=https://deinedomain.de
NEXT_PUBLIC_SITE_URL=https://deinedomain.de

# --- Supabase (optional) ---

NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

Hinweise
• Variablen ohne NEXT*PUBLIC* sind nur serverseitig zugänglich (z. B. RESEND_API_KEY).
• .env.local niemals committen. Eine .env.example mit leeren Keys liegt bei.

    Nützliche Scripts

    {

"scripts": {
"dev": "next dev",
"build": "next build",
"start": "next start",
"lint": "next lint",
"postbuild": "next-sitemap" // falls next-sitemap genutzt wird
}
}

Integrationen

Resend (Kontaktformular)

Route: app/api/contact/route.ts

import { Resend } from 'resend';

export async function POST(req: Request) {
try {
const { name, email, message } = await req.json();
if (!name || !email || !message) {
return Response.json({ error: 'Missing fields' }, { status: 400 });
}

    const resend = new Resend(process.env.RESEND_API_KEY);
    await resend.emails.send({
      from: process.env.RESEND_FROM ?? 'Kontakt <noreply@deinedomain.de>',
      to: ['you@deinedomain.de'],
      reply_to: email,
      subject: `Neue Anfrage von ${name}`,
      text: `Von: ${name} <${email}>\n\n${message}`,
    });

    return Response.json({ ok: true });

} catch (e) {
console.error(e);
return Response.json({ error: 'Send failed' }, { status: 500 });
}
}

E-Mail-Zustellbarkeit: SPF/DKIM für deine Domain einrichten.

Cal.com (Terminbuchung)

Einfacher Link/Button:

<a
className="btn"
href={`https://cal.com/${process.env.NEXT_PUBLIC_CALCOM_LINK}`}
target="\_blank" rel="noreferrer"

> Demo buchen
> </a>

Inline-Embed (optional):

'use client';
import { useEffect } from 'react';
import { getCalApi } from '@calcom/embed-react';

export default function BookingEmbed() {
useEffect(() => {
(async () => {
const cal = await getCalApi();
cal('ui', { theme: 'light' });
cal('inline', { elementOrSelector: '#cal-embed', calLink: process.env.NEXT_PUBLIC_CALCOM_LINK! });
})();
}, []);

return <div id="cal-embed" style={{ minHeight: 700 }} />;
}

Plausible (Analytics)

Script in app/layout.tsx vor </body> einfügen:

{process.env.NEXT_PUBLIC_PLAUSIBLE_DOMAIN ? (

  <script
    defer
    data-domain={process.env.NEXT_PUBLIC_PLAUSIBLE_DOMAIN}
    src="/js/script.js" // optional Proxy
  />
) : null}

Events (Beispiel):

// lib/plausible.ts
export const track = (event: string, props?: Record<string, string | number>) => {
  // @ts-ignore
  window.plausible?.(event, { props });
};

// onClick={() => track('Lead')}

Supabase (optional)

Client (nur wenn benötigt):

// lib/supabase.ts
import { createClient } from '@supabase/supabase-js';

export const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);

Beispiel: Lead persistieren + E-Mail senden

// app/api/contact/route.ts (Ausschnitt)
import { createClient } from '@supabase/supabase-js';
const supabase = createClient(process.env.NEXT_PUBLIC_SUPABASE_URL!, process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!);

await supabase.from('leads').insert({
  name, email, message, source: 'website'
});

Sicherheit: Für Tabellen mit sensiblen Daten Row Level Security (RLS) korrekt konfigurieren.

⸻

SEO & Performance
	•	Metadata pro Route (Title ≤ 60, Description ≤ 155)
	•	Open Graph & Twitter Cards (dynamische OG-Images möglich)
	•	Schema.org JSON-LD: Organization, Product, FAQPage, optional LocalBusiness
	•	Sitemap/Robots: next-sitemap verwenden
	•	Bilder: next/image, AVIF/WebP, korrekte Größen
	•	Fonts: next/font (kein FOUT/CLS)
	•	Lighthouse Ziele: Performance/SEO/Best-Practices/Accessibility ≥ 90

⸻

Barrierefreiheit
	•	Semantische HTML-Elemente
	•	ARIA-Labels für interaktive UI
	•	Kontrast & Fokuszustände sicherstellen
	•	Keyboard-Navigation unterstützt
	•	Bilder mit alt-Texten

⸻

Entwicklungsrichtlinien
	•	TypeScript strikt (keine any/Suppressions ohne Kommentar)
	•	ESLint + Prettier (CI optional)
	•	Conventional Commits:
	•	feat:, fix:, chore:, docs:, refactor:, test:, perf:, build:
	•	Branches: main (protected) + feature/*
	•	shadcn/ui:

npx shadcn@latest init
npx shadcn@latest add button card accordion

	•	Testing (optional): Vitest/RTL oder Playwright

⸻

Deployment
	•	Vercel empfohlen:
	•	Repo verbinden
	•	Environment Variables in Vercel setzen
	•	Production Domain konfigurieren
	•	Optional: Preview Deploys für PRs
	•	Build/Start:

    npm run build
npm run start

Roadmap
	•	PricingPage mit Toggle (monatlich/jährlich) + FAQs
	•	Case Study v1 (Referenz: Eltern-Restaurant)
	•	Blog v1 (2–3 Startartikel)
	•	JSON-LD (FAQPage, Product) + OG-Image Generator
	•	Lead-Persistenz (optional via Supabase)
	•	A/B-Tests (Hero-Varianten, CTA-Text)
	•	i18n (Deutsch/Englisch) bei Bedarf
