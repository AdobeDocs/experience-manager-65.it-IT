---
title: Normative sulla protezione dei dati e la privacy - Compatibilità di Adobe Experience Manager
description: Scopri il supporto di Adobe Experience Manager per le varie normative sulla protezione dei dati e la privacy. Questo include il Regolamento generale sulla Protezione dei Dati (GDPR) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi all’implementazione di un nuovo progetto AEM.
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '890'
ht-degree: 100%

---

# Compatibilità di Adobe Experience Manager per le normative sulla protezione dei dati e la privacy {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende esserne una sostituzione.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

Adobe fornisce documentazione e procedure (con API, se disponibili) per l’amministratore della privacy della clientela o di AEM per gestire le richieste di protezione dei dati e privacy. Può aiutarti a diventare conforme a queste normative. Le procedure documentate consentono alla clientela di eseguire le richieste normative manualmente o di effettuare chiamate API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati ad Adobe Experience Manager.
>
>I dati provenienti da un altro servizio Adobe on-demand, insieme a eventuali richieste di accesso a dati personali correlate, richiederanno azioni su tale servizio.
>
>Per ulteriori informazioni, consulta [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager e le applicazioni che le eseguono sono di proprietà e gestite dalla clientela Adobe.

Di conseguenza, le normative sulla protezione dei dati, come GDPR, CCPA e altri, sono in gran parte responsabilità dei clienti.

Come breve introduzione, le norme sulla privacy e la protezione dei dati includono nuove regole che devono essere seguite dai ruoli di:

* Business Entities (CCPA) e/o Data Controllers (GDPR)

* Service Providers (CCPA) e/o Data Processors (GDPR)

Le principali disposizioni di tali regolamenti sono le seguenti:

1. Definizione ampliata dei dati personali per includere tutti gli ID univoci; come nei dati direttamente e indirettamente identificabili.

2. Requisiti più severi in materia di consenso.

3. Maggiore attenzione ai diritti di eliminazione (Cancellazione dati).

4. Rinuncia alla vendita di dati.

Per Adobe Experience Manager:

* Le istanze, e le applicazioni che le eseguono, sono di proprietà e gestite dalla clientela.

   * La clientela gestisce i ruoli normativi, tra cui entità aziendali e fornitori di servizi, titolari e responsabili del trattamento dati, tra gli altri.

   * Adobe Experience Platform Privacy Service non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l’amministratore della privacy del cliente e/o l’amministratore AEM per eseguire le richieste relative alla normativa sulla privacy, manualmente o tramite API, se disponibili.

* Nessun nuovo servizio o interfaccia utente aggiunto.

   * Le procedure e le API sono invece documentate per l’utilizzo da parte dell’interfaccia utente/dei portali dei clienti che gestiscono le richieste di normativa sulla privacy.

* AEM non includerà alcuno strumento predefinito per supportare il flusso di lavoro delle richieste di privacy.

   * Adobe fornisce documentazione e procedure per l’amministratore della privacy della clientela e per l’amministratore di AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

Adobe fornisce procedure per la gestione delle richieste di privacy relative ad accesso, eliminazione e rinuncia per Adobe Experience Manager. In alcuni casi, sono disponibili API che possono essere richiamate da un portale sviluppato dalla clientela o da script per facilitare l’automazione.

Il diagramma seguente illustra l’aspetto di un flusso di lavoro per la richiesta di accesso a dati personali (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Compatibilità di Adobe Experience Manager e delle normative {#aem-and-regulatory-readiness}

Consulta le sezioni seguenti per la documentazione sulla normativa per le aree di prodotto di AEM.

## AEM Foundation {#aem-foundation}

Consulta [Gestione delle richieste di protezione dei dati e privacy per AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM: consenso alla raccolta di statistiche di utilizzo aggregate {#aem-opting-into-aggregate-usage-statistics-collection}

Consulta [raccolta di statistiche di utilizzo aggregate](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulta [AEM Sites: compatibilità della protezione dei dati e della privacy.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consulta [AEM Commerce: compatibilità della protezione dei dati e della privacy](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulta [AEM Mobile: compatibilità della protezione dei dati e della privacy](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integrazione di AEM con Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni di Adobe Experience Manager sono associate a servizi conformi alla protezione dei dati e alla privacy (ad esempio, GDPR). Nessun dato personale da Adobe Target o Adobe Analytics viene memorizzato in AEM in relazione alle integrazioni.

Per ulteriori informazioni, consulta:

* [Adobe Target - Panoramica sulla privacy](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=it)

* [Flusso di lavoro sulla privacy dei dati di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=it)

## Community AEM {#aem-communities}

AEM Communities conferisce alle persone interessate il diritto alla portabilità dei dati, il diritto di accesso e il diritto all’oblio tramite [API pronte all’uso](/help/communities/user-ugc-management-service.md). Queste API abilitano l’eliminazione e l’esportazione in blocco dei contenuti generati dagli utenti, nonché la disabilitazione degli account utente identificati tramite i loro ID autorizzabili. Tuttavia, l’eliminazione permanente di un account utente può essere realizzata tramite l’eliminazione del nodo utente in CRXDE Lite, soddisfacendo la necessità di una semplice rinuncia dal sistema.

Inoltre, AEM Communities offre privacy by design grazie alla console di moderazione in blocco, che consente ai membri privilegiati di trovare ed eliminare i contributi e i dettagli degli utenti. La console di gestione dei membri consente di porre dei limiti, fino al punto di escludere un collaboratore. Inoltre, autorizza le persone interessate a eliminare i contributi che hanno creato.

## AEM Forms {#aem-forms}

AEM Forms include componenti e flussi di lavoro che acquisiscono, elaborano e memorizzano dati per orchestrare i processi aziendali e completare le transazioni digitali. Componenti diversi utilizzano archivi di dati diversi e consentono l’integrazione anche con archivi di dati personalizzati. Nella documentazione seguente sono illustrate le procedure e le linee guida per l’accesso e la gestione dei dati utente per supportare i flussi di lavoro relativi alla privacy e alla protezione dei dati (ad esempio, GDPR o CCPA) per un componente.

* [Portale dei moduli](/help/forms/using/forms-portal-handling-user-data.md)
* [Gestione della corrispondenza](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrazione con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flussi di lavoro incentrati sui moduli su OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flussi di lavoro Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (solo AEM Forms JEE)
* [Protezione dei documenti](/help/forms/using/document-security-handling-user-data.md) (solo AEM Forms JEE)
* [Gestione utenti](/help/forms/using/user-management-handling-user-data.md) (solo AEM Forms JEE)
