# Estimări Platformă (Recalibrare Post-MVP – Scope extins)

Scop: definim extensiile necesare transformării produsului MVP (single SSM-ist) într-o Platformă multi-tenant completă operată de un Platform Owner, având ca clienți principali SSM-iștii (fiecare SSM-ist = tenant izolat logic). Conform noii decizii, toate elementele marcate anterior ca „out-of-scope” (Plăți, QES, Site Public, SMS, S3 add-on) intră în scope de bază.

---

## Asumări Platformă
- Multi-tenancy logic (un tenant per SSM-ist) cu separare clară a datelor și garduri de securitate (row-level & service-level checks).
- Rol Platform Owner (operațional) cu vizibilitate la nivel de sănătate sistem (status job-uri, erori agregate) fără acces la conținut documente.
- Extindere engine documente: versiuni, template condițional avansat
- Notificări programabile cu SMS inclus (email + SMS reminders) – chain & ferestre orare simple.
- Plăți & Subscription (Stripe) 
- Semnatura Avansata 
- Site Public (landing + pricing + blog simplu) 
- S3 multi‑region & failover (extensie peste S3 din MVP)

---

## Reutilizare din MVP (NU se mai estimează)
Acoperit deja (1,210h): Auth & RBAC minim, CRUD companii & organigramă (import Excel), invitații, pachete de bază (training+test+doc), training viewer, test runner (scoring), template & generare simplă (parametri+tabele), storage S3 + arhivare GDrive, self-sign, notificări de bază, rapoarte de bază, inspector link read-only, audit minimal, CI/CD simplu, teste E2E critice inițiale, securitate de bază.

---

## Structură Estimări Extensii
Reorganizăm segmentarea Frontend pentru claritate operațională și ownership:
- FE User (reused din MVP) – include fluxurile deja livrate pentru SSM-ist și ierarhia companiilor (nu se mai estimează aici; doar eventuale adaptări minore absorbite în sinergie).
- FE Core Shared – componente transversale noi sau adaptate (tenant switching, elemente comune template/versioning, notificări UI extinsă, integrare QES/Payments în shell comun, elemente site public generice).
- FE Business (nou) – capabilitățile comerciale și avansate adăugate în această fază: UI Payments, QES wizard, Versioning & Retention views, Template advanced controls, Notifications & SMS scheduling.
- Site Public (nou pachet) – pagini marketing (landing, pricing, blog), pagini legale, contact & newsletter, SEO/OG, analytics & consent.

---

## 1. Pachet Core Extins (Backend)
Obiectiv: multi-tenancy robust, lifecycle document avansat, motor template extins, plăți, QES, notificări programabile cu SMS, versiuni & retention și hardening securitate.

| Componentă | Descriere | Estimare (h) |
|------------|-----------|---------------|
| Multi-Tenancy Layer | 85 |
| Platform Owner Tools | 30 |
| Document Versioning & Retention | 90 |
| Advanced Template Engine | Condiționale, bucle nested, imagini, secțiuni dinamice | 150 |
| Notifications Scheduler + SMS | Chain reminders, ferestre orare, gateway SMS | 75 |
| Payments (Stripe) Backend | 85 |
| QES Integration | Integrare furnizor | 180 |
| S3 multi‑region & failover (add‑on peste MVP) | 55 |
| Site Public Backend Support | Endpoint content (blog/posts, pricing static) | 25 |
| Security Hardening extins | Rate limit per tenant, WAF/CDN , secret rotation | 40 |
| Observabilitate minimă | Log agregat structurat + metrici bază (latency, error rate) | 30 |
| SLA & Queue Hardening | Retry, dead-letter, metrici queue | 40 |

Subtotal Core: 885h

## 2. FE Core 
| Componentă | Descriere | Estimare (h) |
|------------|-----------|---------------|
| Tenant Switching & Context Banner | Componente context tenant reutilizabile | 20 |
| Platform Owner Health | Dashboard erori/job lag, stocare sumar | 20 |
| Shell Integrări (Payments/QES hooks) | Adaptări layout, stări globale abonament/QES | 15 |
| Template / Versioning Shared Components | Liste, diff view minimalist reutilizat | 25 |
| Notifications Shared Panel | Extindere panou existent pentru scheduling & SMS toggle | 20 |

Subtotal FE Core Shared: 100h

## 3. FE Business (nou)
| Componentă | Descriere | Estimare (h) |
|------------|-----------|---------------|
| Payments (Stripe) UI | Checkout, abonament, status plan | 50 |
| QES Signing Wizard | Identitate + progres semnare calificată | 40 |
| Document Versioning & Retention Views | Istoric, restore, filtru retenție | 40 |
| Advanced Template Controls UI | Condiționale, secțiuni dinamice, imagini | 35 |
| Notifications & SMS Scheduling UI | Creare/reminder chain, ferestre orare | 30 |

Subtotal FE Business: 195h

FE Total (Core Shared + Business): 295h

## 4. Site Public / Landing Page
| Componentă | Descriere | Estimare (h) |
|------------|-----------|---------------|
| Common Marketing Elements | Header/Footer/Nav, SEO meta generator, OG image basic | 20 |
| Landing Page | Hero, features, testimonials, CTA | 24 |
| Pricing Page | Planuri, comparație, FAQ, CTA | 16 |
| Blog List | Listare articole, filtre de bază | 10 |
| Blog Article Template | Layout articol, navigare, share | 12 |
| Legal Pages | Privacy, Terms, Cookies | 8 |
| Contact Page & Form | Validări, integrare backend | 14 |
| SEO Tehnic | Sitemap.xml, robots.txt, canonical URLs | 6 |

Subtotal Site Public: 110h

## 5. DevOps / QA / Securitate Extins
| Componentă | Descriere | Estimare (h) |
|------------|-----------|---------------|
| Multi-tenant, versioning, payments, QES, SMS | 90 |
| Backup & DR formal | Snapshots, restore drills, rotație chei, runbooks | 45 |
| Performance & Load | Profiling, caching, concurrency test | 40 |
| Compliance & Security review QES/Payments | Politici chei, rotație, checklist audit | 25 |
| Documentation | User Manual, Platform Owner Manual, Other User tutorials | 80 |

Subtotal DevOps/QA: 280h

---

## 6. Total Increment Estimat (Bază)
- Core Backend: 885h
- FE Core Shared: 100h
- FE Business: 195h
- Site Public: 110h
- DevOps/QA: 280h

Total (bază): 1,570h

---

## 7. Milestone-uri și Timeline Platformă
Ipoteză: start fază Platformă 01 Jun 2026, imediat după finalul MVP (31 May 2026). Durată: ~6 luni (o fereastră de 3 luni urmată de două ferestre de 1.5 luni).

### Milestone 1 — 3 luni (Iun 2026 – Aug 2026): Multi-tenancy & Fundament Comercial
- Multi-tenancy layer + tenant switching UI
- Payments Stripe (backend + UI) flux abonament funcțional (fără rapoarte avansate)
- Notifications scheduler (email) + SMS gateway integrat (trimitere simplă)
- Observabilitate minimă + security hardening inițial
- Site Public variantă landing/pricing skeleton
- Advanced Template Engine 
Rezultat: onboarding primii SSM-iști plătitori (fără QES încă).

### Milestone 2 — 1.5 luni (Sep 2026 – Mid Oct 2026): Document Lifecycle & Semnătură Calificată
- Document Versioning & Retention
- QES integrare completă + UI
- Site Public complet (blog, SEO/OG, sitemap/robots, contact + newsletter, analytics + consent, accesibilitate & performance) + S3 replică/failover
- Notifications chain + SMS ferestre orare
Rezultat: ofertă diferențiatoare conformitate & semnare avansată.

### Milestone 3 — 1.5 luni (Mid Oct 2026 – Nov 2026): Stabilizare & Reziliență
- SLA & Queue hardening, Performance tests
- DR & Backup drill, secret rotation
- Optimizări UX template/versioning
- Hardening final securitate & metrici p95 stabile
Rezultat: platformă pregătită pentru scalare controlată (10+ SSM-iști) cu QES și plăți stabile.

---

## 8. Diagrama Gantt (Mermaid) — Platformă (01 Jun 2026 – 30 Nov 2026)
```mermaid
gantt
  title Platform Timeline (01 Jun 2026 - 30 Nov 2026)
  dateFormat YYYY-MM-DD

  section Ferestre
  M1 (3 luni)      :m1win, 2026-06-01, 92d
  M2 (1.5 luni)    :m2win, 2026-09-01, 45d
  M3 (1.5 luni)    :m3win, 2026-10-16, 45d

  section Milestone-uri
  M1 complet     :milestone, m1, 2026-08-31, 0d
  M2 complet     :milestone, m2, 2026-10-15, 0d
  M3 complet     :milestone, m3, 2026-11-30, 0d
```
