---
title: Configurazione per le app AEM
seo-title: Configurazione per le app AEM
description: Scopri come configurare le app AEM.
seo-description: Scopri come configurare le app AEM.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Configurazione per le app AEM{#configuring-for-aem-apps}

Le app Adobe Experience Manager consentono di aggiornare i contenuti dell’applicazione in modalità aerea (OTA). Il contenuto aggiornato viene memorizzato nell’istanza di pubblicazione. Per consentire all’app sul dispositivo di connettersi all’istanza di pubblicazione e verificare la disponibilità di aggiornamenti, l’istanza di pubblicazione deve essere configurata per consentire un’intestazione del referente vuota.

## Configurazione dell&#39;intestazione del referente vuota {#configuring-empty-referrer-header}

Per configurare il servizio filtro di riferimento:

* Aprite la console Apache Felix (**Configurazioni**) in:
* https://&lt;server>:&lt;numero_porta>/system/console/configMgr
* Effettuate il login come amministratore.
* Nel menu **Configurazioni** , selezionare: Filtro di riferimento *Apache Sling*
* Selezionare il campo Consenti valori vuoti per consentire intestazioni referrer vuote o mancanti.
* Click **Save** to save your changes.

![chlimage_1-58](assets/chlimage_1-58a.png)

Per ulteriori informazioni, consultate Impostazioni [di configurazione](/help/sites-deploying/osgi-configuration-settings.md) OSGI e Elenco di controllo della [sicurezza - Problemi con il servizio di inoltro](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) delle richieste tra siti.
