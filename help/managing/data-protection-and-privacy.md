---
title: Normative sulla protezione dei dati e la privacy dei dati - Preparazione di Adobe Experience Manager
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: Scopri il supporto di Adobe Experience Manager per le varie normative su privacy e protezione dei dati, incluso il Regolamento generale sulla protezione dei dati (RGPD) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi all’implementazione di un nuovo progetto AEM.
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 60%

---

# Preparazione di Adobe Experience Manager per le normative su privacy e protezione dei dati {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende sostituirsi a una consulenza legale.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro privacy di Adobe](https://www.adobe.com/it/privacy.html).

Adobe fornisce documentazione e procedure (con API se disponibili) per l’amministratore della privacy del cliente o AEM per gestire le richieste di protezione dei dati e privacy dei dati e aiutare i nostri clienti a rispettare queste normative. Le procedure documentate consentiranno ai clienti di eseguire le richieste normative manualmente o chiamando nelle API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati ad Adobe Experience Manager.
>
>I dati provenienti da un altro servizio Adobe on-demand, insieme a eventuali richieste di accesso a dati personali correlate, richiederanno azioni su tale servizio.
>
>Per ulteriori informazioni consulta [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager e le applicazioni che vengono eseguite su di esse sono di proprietà e gestite dai nostri clienti.

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

* Le istanze, e le applicazioni che le eseguono, sono di proprietà e gestite dal cliente.

   * Ciò significa di fatto che il cliente gestisce i ruoli normativi, tra cui Business Entities e Service Provider, Data Controller e Data Processor, tra gli altri.

   * Adobe Experience Platform Privacy Service non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l’amministratore della privacy del cliente e/o l’amministratore AEM per eseguire le richieste relative alla normativa sulla privacy, manualmente o tramite API, se disponibili.

* Nessun nuovo servizio o interfaccia utente aggiunto.

   * Le procedure e le API sono invece documentate per l’utilizzo da parte dell’interfaccia utente/dei portali dei clienti che gestiscono le richieste di normativa sulla privacy.

* AEM non includerà alcuno strumento predefinito per supportare il flusso di lavoro delle richieste di privacy.

   * Adobe fornisce documentazione e procedure per l’amministratore della privacy del cliente e/o per l’amministratore AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

Adobe fornisce procedure per la gestione delle richieste di accesso, cancellazione e rinuncia alla privacy relative ad Adobe Experience Manager. In alcuni casi, sono disponibili API che possono essere richiamate da un portale sviluppato dal cliente o da script per facilitare l’automazione.

Il diagramma seguente illustra l’aspetto di un flusso di lavoro per la richiesta di accesso a dati personali (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e preparazione alle normative {#aem-and-regulatory-readiness}

Consulta le sezioni seguenti per la documentazione regolamentare per le aree di prodotto di AEM.

## AEM Foundation {#aem-foundation}

Vedi [Gestione delle richieste di protezione e privacy dei dati per AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Optare Per Aggregare La Raccolta Di Statistiche Di Utilizzo {#aem-opting-into-aggregate-usage-statistics-collection}

Vedi [Raccolta di statistiche di utilizzo aggregato](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Vedi [AEM Sites - Preparazione per privacy e protezione dei dati.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Vedi [AEM Commerce - Preparazione per privacy e protezione dei dati](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Vedi [AEM Mobile - Preparazione per privacy e protezione dei dati](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integrazione AEM con Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni di Adobe Experience Manager si basano sulla protezione dei dati e la privacy (ad esempio, RGPD o CCPA) dei servizi pronti. Nessun dato personale da Adobe Target o Adobe Analytics viene memorizzato in AEM in relazione alle integrazioni.
Per ulteriori informazioni, consulta:

* [Adobe Target - Panoramica sulla privacy](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html?lang=it)

* [Flusso di lavoro sulla privacy dei dati di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=it)

## AEM Communities {#aem-communities}

AEM Communities conferisce alle persone interessate il diritto alla portabilità dei dati, al diritto di accesso e al diritto di essere dimenticate tramite [API predefinite](/help/communities/user-ugc-management-service.md). Queste API consentono l’eliminazione in blocco e l’esportazione in blocco di contenuti generati dagli utenti e la disattivazione degli account utente identificati tramite i loro ID autorizzabili. Tuttavia, l’eliminazione permanente dell’account utente è realizzabile tramite l’eliminazione del nodo utente in CRXDE Lite, che risponde alla necessità di una facile rinuncia dal sistema.

Inoltre, AEM Communities offre privacy by design grazie alla console di moderazione di gruppo, che consente ai membri con privilegi di trovare ed eliminare i contributi e i dettagli degli utenti. La console di gestione dei membri consente di limitare il limite al punto di vietare un collaboratore. Inoltre, autorizza le persone interessate a cancellare i contributi da esse creati.

## AEM Forms {#aem-forms}

AEM Forms include componenti e flussi di lavoro che acquisiscono, elaborano e memorizzano dati per orchestrare i processi aziendali e completare le transazioni digitali. Componenti diversi utilizzano archivi di dati diversi e consentono l’integrazione anche con archivi di dati personalizzati. La seguente documentazione spiega procedure e linee guida per l’accesso e la gestione dei dati utente al fine di supportare la protezione e la privacy dei dati (ad esempio, RGPD o CCPA) nei flussi di lavoro per un componente.

* [Portale Forms](/help/forms/using/forms-portal-handling-user-data.md)
* [Gestione della corrispondenza](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrazione con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flussi di lavoro incentrati su Forms su OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flussi di lavoro JEE Forms](/help/forms/using/forms-workflow-jee-handling-user-data.md) (Solo JEE per AEM Forms)
* [Sicurezza dei documenti](/help/forms/using/document-security-handling-user-data.md) (Solo JEE per AEM Forms)
* [Gestione utente](/help/forms/using/user-management-handling-user-data.md) (Solo JEE per AEM Forms)
