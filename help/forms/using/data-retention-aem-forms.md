---
title: Conservazione dei dati in AEM Forms
description: Scopri in che modo Adobe Experience Manager (AEM) Forms, per impostazione predefinita, funge da server pass-through e non memorizza i dati degli utenti finali dei moduli, supportando la privacy dei dati.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%
---
# Conservazione dei dati in AEM Forms {#data-retention-in-aem-forms}

AEM Forms memorizza i dati dei moduli? Per impostazione predefinita, no. Adobe Experience Manager (AEM) Forms funge da server pass-through per i dati acquisiti tramite Adaptive Forms e non memorizza i dati degli utenti finali nell’archivio di AEM. Il server trasmette invece i dati inviati alla destinazione che possiedi e configuri. Questo comportamento predefinito consente di soddisfare gli obiettivi di privacy e conformità dei dati e si applica sia ad AEM Forms su OSGi che ad AEM Forms su JEE.

Poiché AEM Forms è una piattaforma estensibile, puoi personalizzare AEM per modificare questo comportamento predefinito. Se la personalizzazione memorizza i dati inviati tramite un modulo adattivo nell’archivio di AEM o li scrive nei registri di AEM, è necessario assicurarsi che tali dati non vengano conservati nei sistemi di produzione e di staging.

## Comportamento predefinito con funzionalità predefinite {#default-behavior}

Quando utilizzi funzionalità predefinite di Adaptive Forms, AEM Forms non memorizza i dati degli utenti finali. Il server trasmette direttamente i dati inviati alla destinazione che possiedi e configuri.

I meccanismi predefiniti che collegano un modulo a una destinazione di tua proprietà includono il Modello dati modulo (FDM), connettori predefiniti e azioni di invio. Ognuno di questi invia i dati a una posizione di tua proprietà e configurata, in modo che non vengano mantenuti nell’archivio di AEM. Un modulo può anche richiamare un servizio esterno o di terze parti, ad esempio un’API REST, da una regola o da un’azione di invio e inoltrare i dati a tale servizio senza renderli persistenti in AEM.

Se utilizzi flussi di lavoro di AEM con processi di lunga durata che richiedono una fase di approvazione, AEM Forms potrebbe conservare i dati in memoria e nell’archiviazione temporanea per completare l’operazione. Per informazioni su come impedire il salvataggio di questi dati in AEM, consulta la sezione [Dati nei processi del flusso di lavoro di lunga durata](#long-lived-workflow-processes).

L’azione di invio di Forms Portal mantiene i dati acquisiti o inviati tramite Adaptive Forms, ma i dati vengono salvati in una posizione di archiviazione fornita e di proprietà, non nell’archivio o nei registri di AEM. Per ulteriori informazioni, vedere [Dati protetti salvati dall&#39;azione di invio del portale dei moduli](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action).

## Dati in transito {#data-in-transit}

Sebbene AEM Forms non memorizzi i dati dell’utente finale per impostazione predefinita, i dati si spostano comunque tra l’utente finale, AEM Forms e la destinazione configurata. Proteggi questo traffico con Transport Layer Security (TLS) in modo che i dati vengano crittografati in transito.

Per proteggere la connessione tra il browser e AEM, abilita HTTPS nell’istanza di AEM. Per i passaggi, consulta [SSL/TLS per impostazione predefinita](/help/sites-administering/ssl-by-default.md).

Inoltre, assicurati che gli endpoint a cui AEM Forms invia i dati, come le configurazioni cloud, gli URL delle azioni di invio e le origini dati del modello dati modulo, utilizzino endpoint HTTPS sicuri. Poiché AEM Forms non memorizza i dati trasmessi, la crittografia a riposo non viene applicata a tali dati. Per ulteriori indicazioni sulla protezione della connessione, vedere [Livello di trasporto sicuro](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer).

## Modello dati modulo per archivi dati esterni {#form-data-model}

Per leggere e scrivere dati in un archivio dati, utilizzare un modello dati modulo (FDM). FDM è il meccanismo consigliato per collegare un modulo a un’origine dati di tua proprietà e da te gestita, ad esempio un database o un servizio web RESTful.

Per ulteriori informazioni, vedere [Introduzione all&#39;integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md). Per informazioni sulla protezione dei dati gestiti da un FDM, vedere [Dati protetti gestiti dal modello dati modulo (FDM)](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm).

## Dati in processi di workflow di lunga durata {#long-lived-workflow-processes}

Se utilizzi processi di flusso di lavoro di lunga durata, AEM può salvare temporaneamente i dati come parte del payload del flusso di lavoro. Le variabili del flusso di lavoro che trasportano questo payload sono memorizzate nei metadati dell’istanza del flusso di lavoro nell’archivio di AEM e possono contenere informazioni personali (PII) o dati personali sensibili (SPD) forniti dagli utenti finali durante la compilazione di un modulo adattivo.

Per mantenere questi dati in un archivio di tua proprietà e gestito, come l’archiviazione BLOB di Azure, anziché su AEM, utilizza la funzionalità di esternalizzazione dei dati di AEM. Quando esternalizzi le variabili, i dati non vengono salvati nel repository di AEM, ma vengono memorizzati nel tuo repository di dati.

Per i passaggi per l&#39;esternalizzazione dei dati, vedere [Impostare i parametri dei dati sensibili per le variabili del flusso di lavoro e archiviarli in archivi dati esterni](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## Personalizzazione e registrazione {#customization-and-logging}

AEM è una soluzione personalizzabile. Se personalizzi AEM, assicurati che la personalizzazione non memorizzi dati nell’archivio o nei registri di AEM.

Quando utilizzi le funzionalità predefinite, AEM Forms non scrive i dati dell’utente finale dal modulo ai registri.

Il codice personalizzato può scrivere i dati nei registri. Se aggiungi traccia o registrazione durante lo sviluppo, rimuovi le tracce e i dati inviati ai registri prima di distribuire il codice negli ambienti di staging e produzione.

## Domande frequenti sulla conservazione dei dati in AEM Forms {#faq}

**AEM Forms memorizza i dati del modulo?**

No. Per impostazione predefinita, Adobe Experience Manager (AEM) Forms funge da server pass-through per i dati acquisiti tramite Adaptive Forms e non memorizza i dati degli utenti finali nel repository di AEM. Il server trasmette i dati inviati alla destinazione di tua proprietà e configurata, ad esempio un’origine dati Modello dati modulo, una destinazione di invio-azione o un’API esterna. Questo comportamento predefinito si applica sia ad AEM Forms su OSGi che ad AEM Forms su JEE.

**Dove sono memorizzati i dati del modulo adattivo?**

I dati del modulo adattivo inviato vengono memorizzati nella destinazione di tua proprietà e configurata, non nell’archivio di Adobe Experience Manager (AEM). Meccanismi predefiniti come il Modello dati modulo (FDM), i connettori e le azioni di invio inviano i dati alla tua posizione. Un modulo può anche inoltrare i dati a un servizio esterno, come un’API REST, senza mantenerli in AEM. L&#39;azione di invio di Forms Portal consente inoltre di salvare i dati in una posizione di archiviazione di tua proprietà.

**I dati del modulo vengono archiviati nei flussi di lavoro di lunga durata?**

I processi di workflow a lunga durata in Adobe Experience Manager (AEM) Forms possono salvare temporaneamente i dati come parte del payload del flusso di lavoro, che viene memorizzato nei metadati dell’istanza del flusso di lavoro nell’archivio di AEM. Per conservare questi dati in un archivio di tua proprietà e da te gestito, ad esempio l&#39;archiviazione BLOB di Azure, anziché in AEM, utilizza la funzionalità di esternalizzazione dei dati di [AEM per le variabili del flusso di lavoro](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

**AEM Forms scrive i dati nei registri?**

No. Con le funzionalità predefinite, Adobe Experience Manager (AEM) Forms non scrive i dati dell’utente finale del modulo nei registri. Poiché AEM è una piattaforma personalizzabile, il codice personalizzato può scrivere i dati nei registri. Se aggiungi traccia o registrazione durante lo sviluppo, rimuovi tali tracce ed eventuali dati registrati prima di distribuirli negli ambienti di staging e produzione. Una personalizzazione non deve memorizzare i dati nell’archivio o nei registri di AEM.

**Protezione dei dati in transito**

I dati in transito sono protetti con Transport Layer Security (TLS) in Adobe Experience Manager (AEM) Forms. Abilita HTTPS nell’istanza di AEM per proteggere la connessione tra il browser e AEM. Inoltre, assicurati che gli endpoint a cui AEM Forms invia i dati, come le configurazioni cloud, gli URL di invio-azione e le origini dati del modello dati modulo, utilizzino endpoint HTTPS sicuri. Poiché AEM Forms non memorizza i dati trasmessi, la crittografia a riposo non viene applicata a tali dati.

## Risorse correlate {#related-resources}

* [Introduzione all’integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md)
* [Parametrizza i dati sensibili per le variabili del flusso di lavoro e memorizzali in archivi di dati esterni](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [Configurazione dell’azione di invio](/help/forms/using/configuring-submit-actions.md)
* [Protezione avanzata di AEM Forms nell’ambiente OSGi](/help/forms/using/hardening-securing-aem-forms-environment.md)
