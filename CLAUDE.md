# Projektkontext – Gastro App Website

## Ziel

Wir entwickeln eine moderne, SEO-optimierte Website für ein B2B-Produkt: individuelle Gastronomie-Apps mit KI-Integration.  
Die Seite dient als Landingpage und Conversion-Tool, um Gastronomen von unserem Angebot zu überzeugen und Leads zu generieren.  
Später wird die Seite um Blog, Case Studies und weitere Inhalte erweitert.

## Zielgruppe

- Restaurant-, Café- und Bar-Betreiber
- Lokale Betriebe, auch deutschlandweit
- Technikferne Zielgruppe, die klare Vorteile und einfache Bedienung braucht
- Entscheider: Restaurantinhaber oder Geschäftsführer

## Positionierung

- Keine Baukastenlösung → maßgeschneiderte Apps
- USP: Eigene Gastro-Erfahrung + moderner Techstack + KI
- Transparente Preise ab 4.900 €
- Wert: Zeitersparnis, weniger Anrufe, bessere Kundenbindung

## Techstack der Website

- Framework: Next.js 15 (App Router, SSR, SSG, ISR)
- Programmiersprache: TypeScript
- Frontend: React 19
- Styling: Tailwind CSS v4 + shadcn/ui
- Icons: lucide-react
- Content: MDX / Contentlayer (Blog, Case Studies)
- Terminbuchung: Cal.com (Embed)
- E-Mail Versand: Resend
- Formulare: react-hook-form + zod
- SEO: next-sitemap, next-seo, dynamische OG-Images
- Analytics: Plausible oder Umami
- Hosting: Vercel

## Seitenstruktur

### Pflicht (Phase 1 – Launch)

- Home (/)
  - Hero mit USP und CTA („Demo buchen“)
  - Probleme der Zielgruppe → Lösung
  - Features Überblick
  - Referenz-App (Fallstudie Vater)
  - Preistabelle (Pakete Basic bis Enterprise)
  - Über mich (Gastro-Hintergrund)
  - Call to Action (Cal.com)
  - FAQ
  - Footer mit Kontakt
- Preise (/preise)
  - Detaillierte Auflistung der Pakete (Basic, Standard, Premium, Enterprise)
  - Laufende Kosten (150–350 €/Monat)
  - Add-ons
- Kontakt (/kontakt)
  - Formular mit react-hook-form + Resend
  - Cal.com Embed für Terminbuchung
- Impressum (/impressum)
- Datenschutz (/datenschutz)

### Erweiterung (Phase 2 – SEO & Autorität)

- Features (/features)
  - Unterseiten: KI-Chat, Bestellungen, Reservierungen, Loyalty, Multi-Location
- Case Studies (/case-studies/[slug])
  - Detailberichte mit Screenshots, Ergebnissen, Zitaten
- Blog (/blog/[slug])
  - Content zu Gastronomie-Digitalisierung, KI, App-Entwicklung
- Über mich (/ueber-mich)
  - Persönlicher Hintergrund, Foto, Story

## Designprinzipien

- Modern, minimalistisch, mobile-first
- Viel Weißraum, klare Typografie
- Conversion-getrieben (CTAs klar sichtbar)
- Preistabelle prominent
- Testimonials und Referenzen als Social Proof (bereits erstellte App für Grill Partner-Maier, Gastronomie-Betrieb in Kiel-Dietrichsdorf 24149)
- Schnelle Ladezeiten, optimiert für SEO

## Content Guidelines

- Einfach und klar formuliert
- Keine technischen Details für Endkunden
- Fokus: Nutzen und Vorteile („weniger Telefonstress“, „eigene App wie große Ketten“)
- Preise transparent darstellen
- Klare Call-to-Actions

## Pakete (Preismodelle)

### Basic – ab 4.900 €

- Branding (Logo, Farben)
- Digitale Speisekarte
- Öffnungszeiten, Kontakt, Standort
- KI-Chat (Fragen zu Speisekarte, Allergenen, Öffnungszeiten)
- Veröffentlichung iOS + Android
- Basis-Support

### Standard – 7.500–9.500 €

- Alles aus Basic
- Online-Bestellungen + Payment
- Push-Notifications
- Reservierungsanfragen
- Admin-Panel
- Erweiterte KI (Empfehlungen, FAQs)

### Premium – 11.500–14.500 €

- Alles aus Standard
- Tischreservierung mit Kalender
- Loyalty-System
- Multi-Location
- Dashboard/Analytics
- Mehrsprachigkeit
- Premium-Support

### Enterprise – ab 20.000 €

- Alles aus Premium
- Kassensystem-Integration (POS)
- Lieferplattform-Anbindung
- Erweiterte Analytics
- White-Label Option
- SLA & dedizierte Weiterentwicklung

### Laufende Kosten

- 150–350 €/Monat (Hosting, KI-API, Updates, Support)

## Wichtig für Claude Code

- Verwende TypeScript
- Nutze Tailwind v4 und shadcn/ui für UI-Komponenten
- Nutze `app/` Directory (Next.js App Router)
- Implementiere Komponenten modular (Hero, PricingTable, FeatureCards, FAQAccordion, ContactForm)
- Stelle sicher: Responsive, SEO-optimiert, barrierefrei (ARIA)
