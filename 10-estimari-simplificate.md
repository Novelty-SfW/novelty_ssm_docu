# Estimări simplificate — MVP vs Platformă

Scop: prezentare pe scurt, fără detalii tehnice, a funcționalităților incluse în MVP și în Platformă, cu timpi totali de implementare (fără breakdown) și o vedere simplificată a costurilor operaționale lunare.

---

## MVP — ce intră și cât durează

Funcționalități incluse (pe scurt):
- Autentificare + roluri de bază (Admin SSM, Manager, Angajat)
- Companii, angajați, organigramă (import din Excel)
- Invitații utilizatori și notificări e‑mail de bază
- Pachete conformitate: training + test + documente
- Vizualizare training, susținere test (scoring), rapoarte de bază
- Template document (parametri+tabele) + generare PDF
- Semnare simplă (self‑sign) și bibliotecă documente
- Stocare S3 pentru documente curente + arhivare în Google Drive
- Inspector view (link read‑only cu expirare)
- CI/CD și securitate de bază, teste E2E critice

Timp total estimat implementare: ≈ 1,220 ore

Observație: MVP este single‑tenant (un SSM‑ist), fără plăți/abonamente și fără semnătură calificată.

---

## Platformă — ce adăugăm peste MVP și cât durează

Funcționalități suplimentare (pe scurt):
- Multi‑tenancy (un tenant per SSM‑ist) și rol „Platform Owner”
- Template avansat (condiționale, secțiuni dinamice, imagini)
- Notificări programabile + SMS
- Plăți și abonamente (ex. Stripe) 
- Semnătură calificată (QES)
- S3 multi‑region + failover (extensie)
- Observabilitate și securitate extinse, testare și hardening

Timp total estimat implementare (increment peste MVP, fără Site Public): ≈ 1,435 ore

Observație: aceste ore extind produsul din MVP într‑o platformă comercială multi‑tenant.

---

## Site Public — ce include și cât durează

Funcționalități (pe scurt):
- Landing (hero, features, testimonials, CTA)
- Blog (listă articole + pagină articol)
- Pagini legale (Privacy, Terms, Cookies)
- Contact + formular
- Elemente comune marketing (Header/Footer/Nav, SEO meta, OG image basic)
- SEO tehnic (sitemap.xml, robots.txt, canonical URLs)

Timp total estimat implementare: ≈ 94 ore

Note:
- Poate fi dezvoltat și livrat separat de MVP/Platformă.
- Integrarea cu backend este minimă (ex. formulare contact/newsletter) și nu afectează estimarea de mai sus.

---

## Costuri operaționale (EUR/lună) — vedere simplificată

1 SSM‑ist (MVP):
- Fără opționale (fără SMS/QES/Arhivare S3): ~€6 – €48/lună
- Cu opționale (SMS + arhivare S3): până la ~€60/lună

10 SSM‑iști (200 angajați/SSM, total ~2,000):
- Fără SMS/QES: ~€35 – €134/lună
- + SMS: ~€55 – €184/lună
- + QES: ~€125 – €404/lună
- + SMS + QES: ~€145 – €454/lună

50 SSM‑iști (200 angajați/SSM, total ~10,000):
- Fără SMS/QES: ~€71 – €312/lună
- + SMS: ~€171 – €562/lună
- + QES: ~€521 – €1,662/lună
- + SMS + QES: ~€621 – €1,912/lună

100 SSM‑iști (200 angajați/SSM, total ~20,000):
- Fără SMS/QES: ~€0.12k – €0.52k/lună
- + SMS: ~€0.32k – €1.02k/lună
- + QES: ~€1.02k – €3.22k/lună
- + SMS + QES: ~€1.22k – €3.72k/lună

Note rapide:
- Principalii driveri de cost la scară sunt QES și SMS; se pot optimiza prin politici „email‑first” și negocieri de volum.
- Stocarea în S3 acoperă doar documentele curente; istoric pe Google Drive (costuri S3 de arhivare rămân opționale).

---

## Exemple Servicii Externe
- QES
	- [Namirial](https://www.namirial.ro/) - nu au pret pe site
	- [Signius](https://signius.eu/) - (min 0.0575€ (1200) - max 0.4€ (10))
- SMS Provider
	- [Web2SMS](https://www.web2sms.ro/) - (0.0348€ (500) ->  0.0278€ (25000) per SMS) in functie de volum
	- [SMSAlert](https://smsalert.mobi/en) - (0.03€ (1000) ->  0.005€ (25000) per SMS) in functie de volum
- Payment Provider 
	- [Netopia](https://netopia-payments.com/) - 0.99% Din valoarea tranzactiei - sau negociabil la volum
	- [Stripe](https://stripe.com/en-ro) - 1 RON + 1.5% Din valoarea tranzactiei 
	- [EuPlatesc](https://www.euplatesc.ro/) - Nu apare cost pe site
	- [PayU](https://romania.payu.com/en/) - 0.3 RON + 0.99% Din valoarea tranzactiei 
- Facturare
	- [SmartBill](https://www.smartbill.ro/) - Asta sar putea face intern simplificat (?) 

---

## Asumții și calendar (orientativ)
- MVP: ~5 luni calendar până la produs stabil, in 3 milestone-uri majore.
- Platformă: ~6 luni calendar după MVP în 3 milestone‑uri majore.

