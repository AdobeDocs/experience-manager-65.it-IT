---
title: Servizio di gestione utenti e UGC in AEM Communities
seo-title: Servizio di gestione utenti e UGC in AEM Communities
description: Utilizza le API per eliminare e esportare in blocco i contenuti generati dagli utenti e disabilitare l’account utente.
seo-description: Utilizza le API per eliminare e esportare in blocco i contenuti generati dagli utenti e disabilitare l’account utente.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# Servizio di gestione utenti e UGC in AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come RGPD, CCPA, ecc.

AEM Communities espone le API predefinite per la gestione dei profili utente e la gestione in blocco dei contenuti generati dagli utenti (UGC, User-Generated Content). Una volta attivato, il servizio **UserUgcManagement** consente agli utenti privilegiati (amministratori della community e moderatori) di disabilitare i profili utente e di eliminare o esportare in blocco i contenuti UGC per utenti specifici. Queste API consentono inoltre ai titolari del trattamento e ai responsabili del trattamento dei dati dei clienti di rispettare i requisiti del Regolamento generale sulla protezione dei dati (RGPD) dell’Unione Europea e altri mandati sulla privacy ispirati al RGPD.

Per ulteriori informazioni, consulta la pagina [RGPD nell&#39;Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Se hai configurato [Adobe Analytics nel sito AEM Communities](/help/communities/analytics.md), i dati utente acquisiti vengono inviati al server Adobe Analytics. Adobe Analytics fornisce API che ti consentono di accedere, esportare ed eliminare i dati utente e di rispettare i requisiti RGPD. Per ulteriori informazioni, consulta [Inviare richieste di accesso e cancellazione](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Per utilizzare queste API, devi abilitare l’endpoint `/services/social/ugcmanagement` attivando il servizio UserUgcManagement. Per attivare questo servizio, installa il [servlet di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponibile su [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Quindi, colpisci l&#39;endpoint nell&#39;istanza di pubblicazione del sito Communities con i parametri appropriati utilizzando una richiesta http, simile a:

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Tuttavia, puoi anche creare un’interfaccia utente (interfaccia utente) per gestire i profili utente e i contenuti generati dagli utenti nel sistema.

Queste API consentono di eseguire le seguenti funzioni.

## Recupera l&#39;UGC di un utente {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** aiuta a esportare tutti gli UGC di un utente dal sistema.

* **utente**: ID autorizzabile di un utente.
* **outputStream**: Il risultato viene restituito come flusso di output, che è un file zip contenente il contenuto generato dall’utente (come file json) e gli allegati (che includono immagini o video caricati dall’utente).

Ad esempio, per esportare l’UGC di un utente chiamato Weston McCall, che utilizza weston.mccall@dodgit.com come ID autorizzabile per accedere al sito Communities, puoi inviare una richiesta http GET simile alla seguente:

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Eliminare l&#39;UGC di un utente {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** aiuta a eliminare dal sistema tutti gli UGC per un utente.

* **utente**: ID autorizzabile dell&#39;utente.

Ad esempio, per eliminare l’UGC di un utente con ID autorizzabile weston.mccall@dodgit.com tramite la richiesta http-POST, utilizza i seguenti parametri:

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Elimina UGC da Adobe Analytics {#delete-ugc-from-adobe-analytics}

Per eliminare i dati utente da Adobe Analytics, segui il [flusso di lavoro di Analytics RGPD](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html); poiché l’API non elimina i dati utente da Adobe Analytics.

Per le mappature delle variabili Adobe Analytics utilizzate da AEM Communities, fai riferimento alla seguente immagine:

![Mappatura delle variabili AEM community per Adobe Analytics](assets/analytics-communities-mapping.png)

## Disattiva un account utente {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** aiuta a disabilitare un account utente.

* **utente**: ID autorizzabile dell&#39;utente.

>[!NOTE]
>
>La disattivazione di un utente elimina tutti i contenuti generati dall’utente sul server.

Ad esempio, per eliminare il profilo di un utente con ID autorizzabile `weston.mccall@dodgit.com` tramite la richiesta http-POST, utilizza i seguenti parametri:

* utente = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API disabilita solo un profilo utente nel sistema e rimuove l&#39;UGC. Tuttavia, per eliminare un profilo utente dal sistema, passa a **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), individua il nodo utente ed eliminalo.
