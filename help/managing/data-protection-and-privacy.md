---
title: Norme sulla protezione dei dati e sulla privacy dei dati - Adobe Experience Manager
seo-title: Preparazione Adobe Experience Manager per le normative sulla protezione dei dati e sulla privacy dei dati; come GDPR, CCPA, ecc.
description: 'Informazioni sul supporto Adobe Experience Manager per le varie normative sulla protezione dei dati e la privacy dei dati; incluso il Regolamento generale sulla protezione dei dati (GDPR) dell''UE, il California sulla privacy Act e le modalità per conformarsi all''implementazione di un nuovo progetto AEM. '
seo-description: 'Informazioni sul supporto Adobe Experience Manager per le varie normative sulla protezione dei dati e la privacy dei dati; incluso il Regolamento generale sulla protezione dei dati (GDPR) dell''UE, il California sulla privacy Act e le modalità per conformarsi all''implementazione di un nuovo progetto AEM. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---


# Preparazione Adobe Experience Manager per la protezione dei dati e le normative sulla privacy {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto del presente documento non costituisce consulenza giuridica e non è inteso come sostituto della consulenza legale.
>
>Consulta l&#39;ufficio legale della tua azienda per consigli in merito alle normative sulla protezione dei dati e sulla privacy dei dati.

>[!NOTE]
>
>Per ulteriori informazioni  Adobe  risposta ai problemi di privacy e ciò che ciò significa per voi in quanto clienti  Adobe, consultate [Adobe Centro](https://www.adobe.com/privacy.html)per la privacy.

 Adobe fornisce documentazione e procedure (con API quando disponibili), affinché l&#39;amministratore della privacy del cliente o l&#39;amministratore AEM possa gestire le richieste di protezione dei dati e privacy dei dati e aiutare i nostri clienti a rispettare queste normative. Le procedure documentate consentiranno ai clienti di eseguire le richieste normative manualmente o chiamando le API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati ad Adobe Experience Manager.
>
>I dati provenienti da un altro servizio on-demand  Adobe, insieme a tutte le relative richieste di privacy, richiederanno l&#39;adozione di misure per tale servizio.
>
>Per ulteriori informazioni, vedere [Adobe  Centro](https://www.adobe.com/privacy.html)per la privacy.

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager e le applicazioni che le utilizzano sono di proprietà e gestite dai nostri clienti.

Di conseguenza, le normative sulla protezione dei dati, come il GDPR, l&#39;CCPA e altri, sono in gran parte responsabilità dei clienti.

Per una breve introduzione, le norme sulla privacy e la protezione dei dati comprendono nuove regole da seguire per:

* Entità commerciali (CCPA) e/o controllori dati (GDPR)

* Fornitori di servizi (CCPA) e/o processori di dati (GDPR)

Le disposizioni principali di tali regolamenti sono:

1. Definizione estesa di dati personali per includere tutti gli ID univoci; come in dati direttamente e indirettamente identificabili.

2. Requisiti di consenso rafforzati.

3. Maggiore attenzione ai diritti di eliminazione (Data Erasure).

4. Rifiuto della vendita di dati.

Per Adobe Experience Manager:

* Le istanze e le applicazioni che vengono eseguite su di esse sono di proprietà e gestite dal cliente.

   * Ciò significa che il cliente gestisce efficacemente i ruoli normativi, tra cui Business Entities e Service Provider, Data Controller e Data Processor, tra gli altri.

   * L&#39;Adobe Experience Platform Privacy Service  non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l&#39;amministratore della privacy del cliente e/o l&#39;amministratore AEM per l&#39;esecuzione delle richieste relative alla normativa sulla privacy; manualmente o tramite API, se disponibili.

* Non è stato aggiunto alcun nuovo servizio o interfaccia utente.

   * Le procedure e le API sono invece documentate per l&#39;utilizzo da parte dell&#39;interfaccia utente/portali del cliente che gestisce le richieste di informativa sulla privacy.

* AEM non includerà alcuno strumento out-of-the-box per supportare il flusso di lavoro delle richieste di privacy.

   *  Adobe fornirà la documentazione e le procedure per l&#39;amministratore della privacy del cliente e/o l&#39;amministratore AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

 Adobe fornisce procedure per la gestione delle richieste di privacy relative a Accesso, Eliminazione e Rifiuto per Adobe Experience Manager. In alcuni casi, sono disponibili delle API che possono essere richiamate da un portale sviluppato dal cliente o da script per facilitare l&#39;automazione.

Nel diagramma seguente è illustrato l’aspetto di un flusso di lavoro per la richiesta di privacy (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e la conformità alle normative {#aem-and-regulatory-readiness}

Per la documentazione regolamentare relativa alle aree di prodotto di AEM, consultare le sezioni seguenti.

## AEM Foundation {#aem-foundation}

Consulta [Gestione delle richieste di protezione e privacy dei dati per AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Scelta Nell&#39;Insieme Di Statistiche Di Uso Aggregato {#aem-opting-into-aggregate-usage-statistics-collection}

Consulta Raccolta [di statistiche sull&#39;utilizzo](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)aggregato.

## AEM Sites {#aem-sites}

Consulta [AEM Sites - Protezione dei dati e privacy.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

Consulta [AEM Commerce - Data Protection and Privacy Readiness](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

Consulta [AEM Mobile - Protezione dei dati e privacy](/help/mobile/aem-mobile-gdpr-compliance.md).

## Integrazione AEM con  Adobe Target e  Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni Adobe Experience Manager si integrano con i servizi di protezione dei dati e privacy (ad esempio, GDPR o CCPA). Nessun dato personale  Adobe Target o  Adobe Analytics viene memorizzato in AEM in relazione alle integrazioni.
Per ulteriori informazioni, consulta:

* [Adobe Target - Panoramica sulla privacy](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics Data Privacy Workflow](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

 AEM Communities assegna agli interessati i diritti di portabilità dei dati, diritto di accesso e diritto di essere dimenticati tramite API [pronte all&#39;uso](/help/communities/user-ugc-management-service.md). Queste API consentono l&#39;eliminazione in blocco e l&#39;esportazione in blocco del contenuto generato dall&#39;utente e la disattivazione degli account utente identificati tramite i loro ID autorizzabili. Tuttavia, l&#39;eliminazione permanente dell&#39;account utente è realizzabile attraverso l&#39;eliminazione del nodo utente in CRXDE Lite, che risolve la necessità di un facile rifiuto dal sistema.

Inoltre,  AEM Communities offre la privacy per progettazione grazie alla console Moderazione di massa, che consente ai membri privilegiati di trovare ed eliminare i contributi e i dettagli degli utenti. La console di gestione dei membri consente di limitare l’accesso al punto da vietare un collaboratore. Inoltre, autorizza gli interessati a cancellare i contributi da essi creati.

## AEM Forms {#aem-forms}

 AEM Forms include componenti e flussi di lavoro che acquisiscono, elaborano e memorizzano i dati per orchestrare i processi aziendali e completare le transazioni digitali. Diversi componenti utilizzano archivi di dati diversi e consentono l&#39;integrazione anche con archivi di dati personalizzati. La seguente documentazione descrive procedure e linee guida per l’accesso e la gestione dei dati utente al fine di supportare flussi di lavoro per la protezione e la privacy (ad esempio, GDPR o CCPA) di un componente.

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [Gestione della corrispondenza](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrazione con  Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flussi di lavoro Forms incentrati su OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flussi di lavoro](/help/forms/using/forms-workflow-jee-handling-user-data.md) Forms JEE (solo  AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (solo  AEM Forms JEE)
* [Gestione](/help/forms/using/user-management-handling-user-data.md) utente (solo  AEM Forms JEE)
