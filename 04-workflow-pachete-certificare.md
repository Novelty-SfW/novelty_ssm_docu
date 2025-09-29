# Workflow Pachete Certificare - Inima Sistemului

## Ce Este un Pachet de Certificare?

```mermaid
graph TD
    A[📦 Pachet Certificare<br/>Bundle Complet Conformitate] --> B[📚 Componentă Training<br/>Video-uri, PDF-uri, Text]
    A --> C[✅ Componentă Testare<br/>Quiz-uri & Evaluări]  
    A --> D[📄 Componentă Documente<br/>Contracte & Certificate]
    
    B --> E{Training Complet?}
    C --> F{Test Promovat?}
    D --> G{Documente Semnate?}
    
    E -->|Da| F
    F -->|Da| G
    G -->|Da| H[✅ Pachet Complet<br/>Complet Conform]
    
    E -->|Nu| I[🔄 Continuare Training]
    F -->|Nu| J[🔄 Reluare Test]
    G -->|Nu| K[🔄 Semnare Documente]
    
    I --> B
    J --> C
    K --> D
    
    %% Stiluri pentru Componente
    style A fill:#e1f5fe,color:#000
    style B fill:#e8f5e8,color:#000
    style C fill:#fff3e0,color:#000
    style D fill:#fce4ec,color:#000
    style H fill:#c8e6c9,color:#000
    style I fill:#e8f5e8,color:#000
    style J fill:#fff3e0,color:#000
    style K fill:#fce4ec,color:#000
    
    %% Stiluri pentru Decizii
    style E fill:#ffeb3b,color:#000
    style F fill:#ffeb3b,color:#000
    style G fill:#ffeb3b,color:#000
```

## Opțiuni Configurare Pachete

```mermaid
graph LR
    subgraph "Tipuri Pachete Flexibile"
        A[📚 Doar Training<br/>Învățare & Dezvoltare]
        B[📝 Doar Documente<br/>Necesită semnare obligatorie]
        C[🧪 Doar Testare<br/>Validare Cunoștințe]
        D[🔄 Pachet Complet<br/>Training → Test → Documente]
    end
    
    subgraph "Workflow-uri Semnare Documente"
        E[🚫 Fără Semnare<br/>Pachete fără documente]
        F[👤 Semnare Simplă<br/>Doar angajatul]
        G[👥 Semnare Secvențială<br/>Angajat + Șefi]
        H[🔗 Semnare în Lanț<br/>Șefi multipli]
    end
    
    A --> E
    C --> E
    B --> F
    B --> G
    D --> H
    
    style D fill:#4caf50,color:#fff
    style H fill:#ff9800,color:#fff
    style E fill:#9e9e9e,color:#fff
```

## Strategii Asignare Pachete

| Tip Asignare | Cel Mai Bun Pentru | Exemplu Caz de Utilizare |
|-------------|-------------------|------------------------|
| **👤 Individual** | Roluri specifice/angajări noi | Pachet onboarding CEO |
| **👥 Grup** | Training la nivel departament | Securitate IT pentru echipa tech |
| **🏢 La nivel companie** | Conformitate universală | Certificare anuală securitate |
| **📋 Bazat pe rol** | Nevoi specifice poziție | Training leadership manageri |

## Dashboard Urmărire Progres

```mermaid
graph TB
    subgraph "Privire Generală Status Pachete"
        A[📊 Vizualizare Dashboard]
        A --> B[🟢 Completate: 45 angajați]
        A --> C[🟡 În Progres: 23 angajați]
        A --> D[🔴 Întârziate: 7 angajați]
        A --> E[⚪ Neînceput: 12 angajați]
    end
    
    subgraph "Detaliere"
        B --> F[✅ Toate componentele finalizate]
        C --> G[📚 Momentan în faza training]
        C --> H[📝 Așteptare semnare documente]
        D --> I[⚠️ Trecut de termen - necesită atenție]
        E --> J[📬 Notificări asignare trimise]
    end
```

## Beneficii pentru Stakeholderi Diferiți

| Stakeholder | Beneficii Cheie | Valoare Livrată |
|------------|----------------|-----------------|
| **👨‍� Admin Tehnic** | Template-uri centralizate, rapoarte detaliate | Control tehnic & analitică |
| **👨‍🔧 Admin SSM** | Asignări facile, notificări automate, lanț semnături | Management conformitate eficient |
| **👔 Șef** | Vizibilitate progres echipă | Management proactiv activat |
| **👷 Angajat** | Cale clară pentru finalizare | Confuzie & întârzieri reduse |
| **🔍 Inspector** | Documentație pregătită audit | Verificare conformitate mai rapidă |