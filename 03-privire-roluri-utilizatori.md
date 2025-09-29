# Roluri in Aplicatie

## Cine Folosește Sistemul și Ce Fac

```mermaid
graph TD
    subgraph UtilizatoriSistem ["👥 Utilizatori Sistem"]
        A1[👨‍� Admin Tehnic<br/>Template-uri & Configurare]
        A2[👨‍🔧 Admin SSM<br/>Pachete & Conformitate]
        B[🔍 Inspector<br/>Auditor Extern]
        C[🏢 Utilizatori Companie<br/>Rol Dinamic Business]
    end
    
    subgraph RoluriDinamice ["🔄 Roluri Dinamice"]
        D[👷 Angajat de Bază<br/>Sarcini Personale]
        E[👔 Manager/Șef<br/>Angajat + Management Echipă]
    end
    
    subgraph Activitati ["⚡ Activități"]
        F1[⚙️ Setup Template-uri<br/>Configurare Tehnic]
        F2[📋 Pachete Conformitate<br/>Asignări & Notificări]
        G[🔎 Audit Independent<br/>Conformitate]
        H[📚 Training Personal<br/>& Semnare Documente]
        I[📊 Monitorizare Echipă<br/>+ Toate drepturile angajatului]
    end
    
    A1 --> F1
    A2 --> F2
    B --> G
    C --> D
    C --> E
    D --> H
    E --> H
    E --> I
```

## Niveluri de Acces

```mermaid
graph TD
    subgraph Platforma ["🌐 Nivel Platformă"]
        A1[👨‍💻 Admin Tehnic<br/>📊 Statistici Generale Platformă<br/>⚙️ Template-uri & Configurări<br/>🚫 NU vede date companii]
    end
    
    subgraph NivelCompanie ["🏢 Nivel Companie"]
        A2[👨‍🔧 Admin SSM<br/>📋 Doar companiile sale<br/>👥 Toți angajații companiei<br/>� Control documente]
        B[🔍 Inspector<br/>� Doar documente oferite<br/>de Admin SSM<br/>� NU acces direct]
    end
    
    subgraph RolBusiness ["👥 Utilizatori Companie"]
        C[👷 Angajat<br/>📱 Date personale<br/>📚 Training propriu]
        D[👔 Manager<br/>📊 Echipa + date personale<br/>👥 Subordinații săi]
    end
    
    A1 -.->|"Furnizează template-uri"| A2
    A2 -->|"Gestionează"| C
    A2 -->|"Gestionează"| D
    A2 -.->|"Pune la dispoziție<br/>documente selectate"| B
    D -->|"Supervizează"| C
    
    style A1 fill:#ff9800,color:#fff
    style A2 fill:#ff5722,color:#fff
    style B fill:#9c27b0,color:#fff
    style C fill:#2196f3,color:#fff
    style D fill:#4caf50,color:#fff
```

## Beneficii Cheie pentru Fiecare Rol

| Rol | Beneficii Cheie | Limitări |
|-----|----------------|----------|
| **👨‍💻 Admin Tehnic** | Template-uri globale, configurare sistem, statistici generale platformă | ❌ Nu vede date din companii specifice |
| **👨‍🔧 Admin SSM** | Gestionare companiile sale, pachete conformitate, control documente pentru inspector | ✅ Acces complet doar la companiile sale |
| **🔍 Inspector** | Audit bazat pe documente oferite de Admin SSM | ❌ Nu are acces direct, doar la materialele puse la dispoziție |
| **👔 Manager** | **Toate drepturile angajatului** + monitorizare echipă din compania sa | ✅ Acces complet la subordinații săi |
| **👷 Angajat** | Training personal, semnare documente, progres vizibil | ❌ Doar datele proprii |

## Ierarhia și Relațiile Cheie în Sistem

```mermaid
graph TD
    subgraph Companie ["🏢 Companie"]
        A[�‍🔧 Admin SSM<br/>📊 Overview Companie<br/>👥 Toți Managerii]
        
        subgraph Management ["👔 Manageri"]
            B1[Manager Departament 1]
            B2[Manager Departament 2]
            B3[Manager...]
        end
        
        subgraph Angajati ["👷 Angajați"]
            C1[Angajat 1]
            C2[Angajat 2]
            C3[Angajat 3]
            C4[Angajat...]
        end
    end
    
    A -.->|"Supervizează"| B1
    A -.->|"Supervizează"| B2
    A -.->|"Supervizează"| B3
    
    B1 -->|"Gestionează echipa"| C1
    B1 -->|"Gestionează echipa"| C2
    B2 -->|"Gestionează echipa"| C3
    B3 -->|"Gestionează echipa"| C4
    
    subgraph Drepturi ["🔑 Drepturi Cheie"]
        D1[� Manager: Date echipă + personale]
        D2[� Angajat: Doar date personale]
        D3[🏢 Admin SSM: Overview companie]
    end
    
    style A fill:#ff5722,color:#fff
    style B1 fill:#4caf50,color:#fff
    style B2 fill:#4caf50,color:#fff
    style B3 fill:#4caf50,color:#fff
    style C1 fill:#2196f3,color:#fff
    style C2 fill:#2196f3,color:#fff
    style C3 fill:#2196f3,color:#fff
    style C4 fill:#2196f3,color:#fff
```