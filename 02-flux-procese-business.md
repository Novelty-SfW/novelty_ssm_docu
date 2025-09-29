# Business Process - Cum se Desfășoară Munca

## Procesul Complet de Certificare

```mermaid
graph TD
    A[🏢 Configurare Companie<br/>Admin SSM încarcă ierarhia]
    B1[📋 Pachete Predefinite<br/>Admin Tehnic - Template-uri]
    B2[📋 Pachete Personalizate<br/>Admin SSM - Configurare specifică]
    
    A --> B1
    A --> B2
    B1 --> C[👥 Asignare la Angajați<br/>Admin SSM - Individual sau pe Grup]
    B2 --> C
    C --> D(Angajatul Primește Asignarea)
    
    D --> E[📚 Completare Training<br/>Module Video/PDF/Text]
    E --> F[✅ Susținere Test<br/>Quiz sau checklist]
    F --> G{Test Promovat?}
    
    G -->|Da| H[📝 Semnare Documente<br/>Semnătură digitală]
    G -->|Nu| I[🔄 Reluare Training<br/>& Test]
    I --> F
    
    H --> J{Semnătură Șef<br/>Necesară?}
    J -->|Da| K[👔 Revizuire Șef<br/>& Semnătură]
    J -->|Nu| L[✅ Proces Finalizat]
    K --> L
    
    L --> M[📊 Rapoarte Disponibile<br/>Admin, Șef, Inspector]
```

## Ciclul Lunar de Business

```mermaid
gantt
    title Ciclul Lunar de Conformitate
    dateFormat  YYYY-MM-DD
    section Faza de Configurare
    Admin Tehnic - Template-uri :done, setup, 2024-01-01, 2d
    Admin SSM - Config pachete  :done, config, after setup, 2d
    Admin SSM - Asignare        :done, assign, after config, 2d
    
    section Faza de Execuție
    Training angajați        :active, training, after assign, 10d
    Semnare documente       :signing, after training, 5d
    
    section Faza de Revizuire
    Revizuire șef           :review, after signing, 3d
    Audit inspector         :audit, after review, 2d
    
    section Raportare
    Generare rapoarte       :report, after audit, 2d
    Arhivare documente      :archive, after report, 1d
```

## Metrici Cheie Monitorizate

| Metrică | Scop | Responsabil |
|---------|------|------------|
| **📊 Rata de Finalizare** | Urmărește progresul training-ului | Șefi |
| **⏱️ Timp de Completare** | Identifică blocajele | Admin Tehnic (toate companiile)<br/>Admin SSM (compania proprie) |
| **✅ Rate Promovare/Respingere** | Eficiența training-ului | Admin Tehnic (toate companiile)<br/>Admin SSM (compania proprie) |
| **📄 Status Documente** | Pregătire pentru conformitate | Inspector |
| **🔔 Elemente Întârziate** | Managementul riscurilor | Toate rolurile |