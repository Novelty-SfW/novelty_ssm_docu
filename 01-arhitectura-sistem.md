# Arhitectură Sistem - Componente Tehnice

## Arhitectură Sistem de Nivel Înalt

```mermaid
graph TB
    subgraph "� Acces Multi-Device"
        A[💻 Desktop<br/>Browser Web - PC/Laptop]
        B[📱 Mobile<br/>Browser Web - Telefon/Tabletă]
        C[🔍 Inspector<br/>Portal Web Dedicat]
    end
    
    subgraph "☁️ Portal Web Central"
        D[🌐 Aplicație Web <br/>Un singur portal pentru toate device-urile]
        E[⚙️ Logică Business<br/>Motor Central]
    end
    
    subgraph "🔗 Backend & Servicii"
        F[🗄️ Bază de Date]
        G[✍️ Semnătură Digitală]
        H[📧 Comunicații<br/>Email & SMS]
        I[💾 Cloud Storage]
    end
    
    A -->|HTTPS| D
    B -->|HTTPS| D
    C -->|HTTPS| D
    
    D --> E
    E --> F
    
    E --> G
    E --> H
    E --> I
    
    style D fill:#2196f3,color:#fff
    style E fill:#4caf50,color:#fff
    style F fill:#ff9800,color:#fff
    style G fill:#9c27b0,color:#fff
```

## Accesul Aplicatie - Portal Web

```mermaid
graph LR
    subgraph "🏢 Birou"
        A[💻 Desktop<br/>Admin Tehnic & Admin SSM]
    end
    
    subgraph "🚧 Teren"
        B[📱 Telefon<br/>Muncitori în teren]
        C[📋 Tabletă<br/>Supervisori mobili]
    end
    
    subgraph "🌐 Același Portal Web"
        D[📱 Design Responsiv<br/>Se adaptează automat]
        E[⚡ Funcții Optimizate<br/>Touch & Mobile UI]
        F[📶 Funcționare Offline<br/>Cache local pentru date]
    end
    
    A --> D
    B --> D
    C --> D
    
    D --> E
    E --> F
    
    style D fill:#4caf50,color:#fff
    style E fill:#ff9800,color:#fff
    style F fill:#9c27b0,color:#fff
```

## Flux Date & Securitate

```mermaid
graph LR
    subgraph "Date Input"
        A[👤 Date Utilizator<br/>Protecție GDPR]
        B[🏢 Info Companie<br/>Admin SSM - Ierarhie & Profile]
        C[📋 Template-uri<br/>Admin Tehnic - Upload & Config]
        K[📚 Material Training<br/>Video, PDF, Text - Admin Tehnic]
        L[✅ Teste & Quiz-uri<br/>Întrebări & Răspunsuri - Admin Tehnic]
    end
    
    subgraph "Procesare"
        E[🔒 Strat Criptare<br/>Securitate Date]
        F[⚡ Motor Procesare<br/>Generare Documente]
        G[✅ Validare<br/>Reguli Business]
    end
    
    subgraph "Output"
        H[📄 Documente Generate<br/>Pregătite pentru Semnare]
        I[📊 Rapoarte & Analize<br/>Admin Tehnic - Toate Companiile]
        J[🔔 Notificări<br/>Admin SSM - Compania Proprie]
        M[⚙️ Pachete Conformitate<br/>Generate & Configurate]
    end
    
    A --> E
    B --> E
    C --> E
    K --> E
    L --> E
    
    E --> F
    F --> G
    
    G --> H
    G --> I
    G --> J
    G --> M
    
    style M fill:#f44336,color:#fff
    style E fill:#9c27b0,color:#fff
    style F fill:#607d8b,color:#fff
```

## Caracteristici Securitate & Conformitate

| Caracteristică | Beneficiu |
|----------------|-----------|
| **🔐 Semnături Digitale AES/QES** | Documente cu valoare legală |
| **🛡️ Protecție Date GDPR** | Confidențialitate & drepturi utilizator |
| **🔒 Stocare Criptată** | Securitate date în repaus |
| **📋 Jurnal Audit** | Înregistrare completă activități |
| **🌐 Comunicații Securizate** | Transmisie date protejată |