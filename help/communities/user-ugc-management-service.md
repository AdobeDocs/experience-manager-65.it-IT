---
title: Servizio di gestione di utenti e UGC in  AEM Communities
seo-title: Servizio di gestione di utenti e UGC in  AEM Communities
description: Utilizzate le API per eliminare e esportare in massa il contenuto generato dall'utente e disattivare l'account utente.
seo-description: Utilizzate le API per eliminare e esportare in massa il contenuto generato dall'utente e disattivare l'account utente.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 18f401babef4cb2aad47e6e4cbb0500b0f8365e2
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Servizio di gestione di utenti e UGC in  AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Il GDPR è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come GDPR, CCPA ecc.


 AEM Communities espone le API pronte all&#39;uso per gestire i profili utente e gestire in massa il contenuto generato dall&#39;utente (UGC). Una volta attivato, il servizio **UserUgcManagement** consente agli utenti privilegiati (amministratori e moderatori della community) di disattivare i profili utente e di eliminare o esportare in blocco UGC per utenti specifici. Queste API consentono inoltre ai responsabili del trattamento e ai responsabili del trattamento dei dati dei clienti di rispettare le norme generali sulla protezione dei dati (General Data Protection Regulation, GDPR) dell&#39;Unione Europea e altri mandati sulla privacy ispirati al GDPR.

Per ulteriori informazioni, consulta la pagina [GDPR all’ Centro](https://www.adobe.com/privacy/general-data-protection-regulation.html)per la privacy del Adobe.

>[!NOTE]
>
>Se avete configurato [Adobe Analytics  sito AEM Communities](/help/communities/analytics.md) , i dati utente acquisiti vengono inviati  server Adobe Analytics.  Adobe Analytics fornisce API che consentono di accedere, esportare ed eliminare dati utente e che sono conformi al GDPR. Per ulteriori informazioni, vedere [Sottomettere richieste](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)di accesso ed eliminazione.


Per utilizzare queste API, è necessario abilitare l&#39; `/services/social/ugcmanagement` endpoint attivando il servizio UserUgcManagement. Per attivare questo servizio, installate il servlet [di](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) esempio disponibile su [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Quindi, toccate l’endpoint nell’istanza di pubblicazione del sito community con i parametri appropriati utilizzando una richiesta http, simile a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Tuttavia, potete anche creare un&#39;interfaccia utente (interfaccia utente) per gestire i profili utente e il contenuto generato dall&#39;utente nel sistema.

Queste API consentono di eseguire le seguenti funzioni.

## Recuperare l’UGC di un utente {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream)** consente di esportare tutti gli UGC di un utente dal sistema.

* **utente**: ID autorizzabile di un utente.
* **outputStream**: Il risultato viene restituito come flusso di output, ovvero un file zip che include il contenuto generato dall&#39;utente (come file json) e gli allegati (che includono immagini o video caricati dall&#39;utente).

Ad esempio, per esportare l’UGC di un utente denominato Weston McCall, che utilizza weston.mccall@dodgit.com come ID autorizzabile per accedere al sito delle community, potete inviare una richiesta di GET http simile a quella riportata di seguito:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminare l’UGC di un utente {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** consente di eliminare dal sistema tutti gli UGC per un utente.

* **utente**: ID autorizzabile dell’utente.

Ad esempio, per eliminare l’UGC di un utente con ID autorizzabile weston.mccall@dodgit.com tramite richiesta http-POST, utilizzate i seguenti parametri:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Eliminare UGC da  Adobe Analytics {#delete-ugc-from-adobe-analytics}

Per eliminare i dati utente dall&#39;Adobe Analytics , segui il flusso di lavoro [](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)GDPR Analytics; poiché l&#39;API non elimina i dati utente da  Adobe Analytics.

Per  mappature delle variabili Adobe Analytics utilizzate da  AEM Communities, fare riferimento alla seguente immagine:

![AEM mappatura delle variabili delle community per  Adobe Analytics](assets/analytics-communities-mapping.png)

## Disattivazione di un account utente {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** consente di disabilitare un account utente.

* **utente**: ID autorizzabile dell’utente.

>[!NOTE]
>
>La disattivazione di un utente elimina tutto il contenuto generato dall&#39;utente sul server.


Ad esempio, per eliminare il profilo di un utente con ID autorizzabile `weston.mccall@dodgit.com` tramite richiesta http-POST, utilizzate i seguenti parametri:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API disattiva solo un profilo utente nel sistema e rimuove l&#39;UGC. Tuttavia, per eliminare un profilo utente dal sistema, andate al **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), individuare il nodo utente ed eliminarlo.


