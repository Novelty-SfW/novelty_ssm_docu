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
| Backend/API | Serverless mic / Edge | 0.00 | 0.00 | 25.00 |
| E‑mail | 500/1,000/2,000 × €0.10/1k | 0.05 | 0.10 | 0.20 |
| SMS (opțional) | 0/200/400 × €0.02 | 0.00 | 4.00 | 8.00 |
| Domeniu + DNS | anual ~€12–€20 | 1.00 | 1.50 | 2.00 |
| Arhivare S3 (opțional) | ex. 100 GB IA/Glacier | 1.00 | 2.00 | 4.00 |


#### Totaluri (EUR/lună)

| Scenariu | Low | Med | High |
|---|---:|---:|---:|
| Fără opționale (fără SMS/Arhivare) | ≈ 6.16 | ≈ 11.81 | ≈ 47.62 |
| Cu opționale (SMS + Arhivare) | ≈ 7.16 | ≈ 17.81 | ≈ 59.62 |


---

## 2) Platformă — ~100 SSM‑iști

Ipoteze rapide: 20k–50k angajați activi total; 20k–50k PDF/lună; DTO total ~350–1,050 GB/lună; stocare „curente” (documente + training) ~400–1,200 GB. Supabase pe plan plătit (DB + Auth), compute/queue/observabilitate moderate. QES/SMS pot deveni dominante.

### 2.1 Breakdown costuri (EUR/lună)

| Componentă | Ipoteză | Low | Med | High |
|---|---|---:|---:|---:|
| S3 (total: stocare+DTO+cereri) | curente + training | 40 | 100 | 170 |
| CDN (recomandat) | 300–1,000 GB cache‑abil | 30 | 50 | 90 |
| DB + Auth (Supabase, plan plătit) | ex. Pro/Team | 25 | 100 | 200 |
| E‑mail | 100k–300k/lună | 20 | 40 | 60 |
| SMS (opțional) | 10k–25k × €0.02 | 200| 350 | 500 |
| QES (opțional) | €0.1 × 9k to 27k | 900 | 1,800 | 2,700 |
| Domeniu + DNS |  | 1 | 1.5 | 2 |


#### Totaluri (EUR/lună)

| Scenariu | Low | Med | High |
|---|---:|---:|---:|
| Fără SMS/QES | ≈ 116 | ≈ 291.5 | ≈ 522 |
| + SMS | ≈ 316 | ≈ 641.5 | ≈ 1,022 |
| + QES | ≈ 1,016 | ≈ 2,091.5 | ≈ 3,222 |
| + SMS + QES | ≈ 1,216 | ≈ 2,441.5 | ≈ 3,722 |

Note:
- Valorile pentru DB+Auth depind de planul ales și de depășirile de utilizare (MAU, stocare, egress). Sumele de mai sus sunt orientative.
- QES și SMS pot domina rapid costul total; negociați volume‑tiers la QES și folosiți email‑first ca politică implicită.

---

## 3) Formule rapide (pentru recalcul)
- S3 Storage ≈ GB × €0.021/lună
- S3 DTO ≈ GB × €0.09 (fără CDN) sau × €0.05–€0.09 (cu CDN)
- E‑mail ≈ (emailuri/1,000) × €0.10
- SMS ≈ (număr SMS) × €0.02
- QES ≈ (număr semnături) × €0.1 

---

## 4) Rezumat 
- MVP (1 SSM‑ist): ~€6–€48/lună fără opționale; până la ~€60 cu SMS/Arhivare.
- Platformă (100 SSM‑iști):
	- Fără SMS/QES: ~€0.12k–€0.52k
	- +SMS: ~€0.32k–€1.02k
	- +QES: ~€1.02k–€3.22k
	- +SMS+QES: ~€1.22k–€3.72k
	(mediane aprox.: 0.29k / 0.64k / 2.09k / 2.44k)
- Principalii consumatori: QES, SMS, DTO video. Optimizați cu CDN, politici de comunicare email‑first, și păstrați în S3 doar documentele curente (arhivare pe GDrive).
