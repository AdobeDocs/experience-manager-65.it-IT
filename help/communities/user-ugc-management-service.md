---
title: Servizio di gestione utenti e contenuti generati dagli utenti in AEM Communities
seo-title: User and UGC Management Service in AEM Communities
description: Utilizza le API per eliminare e esportare in blocco i contenuti generati dagli utenti e disabilitare l’account utente.
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# Servizio di gestione utenti e contenuti generati dagli utenti in AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come RGPD, CCPA, ecc.

AEM Communities espone le API pronte all’uso per gestire i profili utente e i contenuti generati dagli utenti (UGC, User Generated Content) in blocco. Una volta abilitata, la funzione **UserUgcManagement** Il servizio consente agli utenti privilegiati (amministratori di community e moderatori) di disabilitare i profili utente e di eliminare in blocco o esportare in blocco contenuti generati dall&#39;utente (UGC, User-Generated Content) per utenti specifici. Queste API consentono inoltre ai titolari del trattamento e ai responsabili del trattamento dei dati dei clienti di conformarsi alle normative generali sulla protezione dei dati (RGPD) dell’Unione Europea e ad altri mandati sulla privacy ispirati al RGPD.

Per ulteriori informazioni, consulta [Pagina RGPD nel Centro per la privacy di Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Se hai configurato [Adobe Analytics in AEM Communities](/help/communities/analytics.md) sito, i dati utente acquisiti vengono inviati al server Adobe Analytics. Adobe Analytics fornisce API che ti consentono di accedere, esportare ed eliminare dati utente in conformità con il RGPD. Per ulteriori informazioni, consulta [Inviare richieste di accesso e cancellazione](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Per utilizzare queste API, devi abilitare `/services/social/ugcmanagement` attivando il servizio UserUgcManagement. Per attivare questo servizio, installare [servlet di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponibile su [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Quindi, premi l’endpoint sull’istanza di pubblicazione del sito community con i parametri appropriati utilizzando una richiesta http simile alla seguente:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Tuttavia, puoi anche creare un’interfaccia utente (interfaccia utente) per gestire i profili utente e i contenuti generati dagli utenti nel sistema.

Queste API consentono di eseguire le seguenti funzioni.

## Recuperare l’UGC di un utente {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** consente di esportare tutti i contenuti generati dagli utenti (UGC, User-Generated Content) di un utente dal sistema.

* **utente**: ID autorizzabile di un utente.
* **outputStream**: il risultato viene restituito come flusso di output, che è un file zip contenente il contenuto generato dall’utente (come file json) e gli allegati (che includono immagini o video caricati dall’utente).

Ad esempio, per esportare l&#39;UGC di un utente di nome Weston McCall, che utilizza weston.mccall@dodgit.com come ID autorizzabile per accedere al sito Communities, puoi inviare una richiesta HTTP GET simile alla seguente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminare l’UGC di un utente {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, utente stringa)** consente di eliminare dal sistema tutti i contenuti generati dagli utenti (UGC).

* **utente**: ID autorizzabile dell’utente.

Ad esempio, per eliminare l’UGC di un utente con ID autorizzabile weston.mccall@dodgit.com tramite richiesta http-POST, utilizza i seguenti parametri:

* utente = `weston.mccall@dodgit.com`
* operazione = `deleteUgc`

### Elimina UGC da Adobe Analytics {#delete-ugc-from-adobe-analytics}

Per eliminare i dati utente da Adobe Analytics, segui la [Flusso di lavoro di analisi del RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=it); poiché l’API non elimina i dati utente da Adobe Analytics.

Per le mappature delle variabili di Adobe Analytics utilizzate da AEM Communities, fai riferimento alla seguente immagine:

![Mappatura delle variabili delle community AEM per Adobe Analytics](assets/analytics-communities-mapping.png)

## Disattivare un account utente {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, utente stringa)** consente di disabilitare un account utente.

* **utente**: ID autorizzabile dell’utente.

>[!NOTE]
>
>La disabilitazione di un utente comporta l’eliminazione di tutto il contenuto generato dall’utente che si trova sul server.

Ad esempio, per eliminare il profilo di un utente con ID autorizzabile `weston.mccall@dodgit.com` tramite la richiesta http-POST, utilizza i seguenti parametri:

* utente = `weston.mccall@dodgit.com`
* operazione = `deleteUser`

>[!NOTE]
>
>L’API deleteUserAccount() disabilita solo un profilo utente nel sistema e rimuove l’UGC. Tuttavia, per eliminare un profilo utente dal sistema, vai a **CRXDE Liti**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), individua il nodo utente ed eliminalo.
