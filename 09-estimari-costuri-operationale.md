# Estimări costuri operationale (MVP & Platformă)

Scop: estimare lunară orientativă, în format tabelar, pentru:
- MVP (un singur SSM‑ist)
- Platformă (scalare la ~100 SSM‑iști)

Ipoteze generale și notițe:
- Monedă: EUR. Regiune tipică UE. Prețuri rotunjite: S3 Standard ~€0.021/GB‑lună; DTO internet ~€0.09/GB; Email (SES) ~€0.10/1k; SMS ~€0.03–€0.08/SMS; QES ~€1–€3/semnătură.
- S3 păstrează DOAR documentele „curente”. Arhivarea istorică se face individual pe Google Drive. Costurile S3 pentru arhivare sunt opționale (vezi rând dedicat).
- MVP: considerăm Supabase Free pentru DB + Auth (în limitele planului gratuit). Costurile de compute sunt minime dacă folosim Edge Functions/servicii serverless cu trafic redus.
- Valorile sunt ordine de mărime, nu oferte comerciale; depind de trafic, țări pentru SMS, furnizori QES etc.

---

## 1) MVP — un singur SSM‑ist

### 1.1 Ipoteze rapide (orientative)
- 50–150 angajați activi, 100–300 PDF/lună, 1–2 descărcări/document
- Dimensiune medie PDF: 0.3–0.7 MB; materiale training: 2–5 GB total
- Emailuri/lună: 500–2,000; SMS: 0–200 (opțional)

### 1.2 Breakdown costuri (EUR/lună)

| Componentă | Ipoteză / unitate | Low | Med | High |
|---|---|---:|---:|---:|
| S3 – stocare „curente” | 5/10/20 GB × €0.021 | 0.11 | 0.21 | 0.42 |
| S3 – trafic (DTO) | 50/100/200 GB × €0.09 | 4.50 | 9.00 | 18.00 |
| S3 – cereri | PUT/GET moderate | 0.50 | 1.00 | 2.00 |
| Backend/API | Serverless mic / Edge | 0.00 | 10.00 | 20.00 |
| DB + Auth (Supabase Free) | în limitele planului | 0.00 | 0.00 | 0.00 |
| Observabilitate/loguri | entry tier | 0.00 | 5.00 | 10.00 |
| E‑mail | 500/1,000/2,000 × €0.10/1k | 0.05 | 0.10 | 0.20 |
| SMS (opțional) | 0/200/400 × €0.05 | 0.00 | 10.00 | 20.00 |
| Domeniu + DNS | anual ~€12–€20 | 1.00 | 1.50 | 2.00 |
| TLS | Let’s Encrypt/ACM | 0.00 | 0.00 | 0.00 |
| CDN (opțional) | trafic redus | 0.00 | 5.00 | 10.00 |
| Arhivare S3 (opțional) | ex. 100 GB IA/Glacier | 1.00 | 2.00 | 4.00 |


#### Totaluri (EUR/lună)

| Scenariu | Low | Med | High |
|---|---:|---:|---:|
| Fără opționale (fără SMS/CDN/Arhivare) | ≈ 6 | ≈ 27 | ≈ 53 |
| Cu opționale (SMS + CDN + Arhivare) | ≈ 7 | ≈ 44 | ≈ 87 |

Note:
- „DB + Auth (Supabase Free)” este €0 cât timp rămânem în limitele planului gratuit (DB mică, trafic redus, MAU rezonabile). La depășire, trecem pe plan plătit.
- Dacă trainingul video crește, activați un CDN (rând opțional) și optimizați bitrate/codec.

Rezumat MVP (practic):
- De regulă, fără opționale, veți vedea ~€25–€60/lună (depinde de DTO și backend).
- Cu SMS/CDN/Arhivare: până la ~€90/lună pentru vârfuri moderate.

---

## 2) Platformă — ~100 SSM‑iști (versiune compactă)

Ipoteze rapide: 20k–50k angajați activi total; 20k–50k PDF/lună; DTO total ~350–1,050 GB/lună; stocare „curente” (documente + training) ~400–1,200 GB. Supabase pe plan plătit (DB + Auth), compute/queue/observabilitate moderate. QES/SMS pot deveni dominante.

### 2.1 Breakdown costuri (EUR/lună)

| Componentă | Ipoteză | Low | Med | High |
|---|---|---:|---:|---:|
| S3 (total: stocare+DTO+cereri) | curente + training | 40 | 100 | 170 |
| CDN (recomandat) | 300–1,000 GB cache‑abil | 30 | 50 | 90 |
| Compute/API/Workers | autoscaling moderat | 600 | 900 | 1,200 |
| DB + Auth (Supabase, plan plătit) | ex. Pro/Team | 25 | 75 | 150 |
| Cache/Queue | Redis/queue gestionat | 100 | 200 | 300 |
| Observabilitate/APM | logs+metrics | 150 | 200 | 300 |
| E‑mail | 100k–300k/lună | 10 | 20 | 30 |
| SMS (opțional) | 30k–100k × €0.03–€0.08 | 1,500 | 2,500 | 4,000 |
| QES (opțional) | €1–€3 × volum | 9,000 | 18,000 | 27,000 |
| Domeniu + DNS |  | 1 | 1.5 | 2 |


#### Totaluri (EUR/lună)

| Scenariu | Low | Med | High |
|---|---:|---:|---:|
| Fără SMS/QES | ≈ 1,100 | ≈ 1,550 | ≈ 2,240 |
| + SMS | ≈ 2,600 | ≈ 4,050 | ≈ 6,240 |
| + QES | ≈ 10,100 | ≈ 19,550 | ≈ 29,240 |
| + SMS + QES | ≈ 11,600 | ≈ 22,050 | ≈ 33,240 |

Note:
- Valorile pentru DB+Auth depind de planul ales și de depășirile de utilizare (MAU, stocare, egress). Sumele de mai sus sunt orientative.
- QES și SMS pot domina rapid costul total; negociați volume‑tiers la QES și folosiți email‑first ca politică implicită.

---

## 3) Formule rapide (pentru recalcul)
- S3 Storage ≈ GB × €0.021/lună
- S3 DTO ≈ GB × €0.09 (fără CDN) sau × €0.05–€0.09 (cu CDN)
- E‑mail ≈ (emailuri/1,000) × €0.10
- SMS ≈ (număr SMS) × €0.03–€0.08
- QES ≈ (număr semnături) × €1–€3

---

## 4) Rezumat 
- MVP (1 SSM‑ist): ~€25–€60/lună fără opționale; până la ~€90 cu SMS/CDN/Arhivare.
- Platformă (100 SSM‑iști): ~€1.1k–€2.2k fără SMS/QES; cu SMS mediu: ~€1.6k–€4.1k; cu QES mediu: ~€10k–€29k (dominat de cost per semnătură).
- Principalii consumatori: QES, SMS, DTO video. Optimizați cu CDN, politici de comunicare email‑first, și păstrați în S3 doar documentele curente (arhivare pe GDrive).
