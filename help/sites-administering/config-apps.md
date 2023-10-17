---
title: Configurazione per le app AEM
description: Scopri come utilizzare le app Adobe Experience Manager per aggiornare il contenuto dell’OTA dell’applicazione (over the air).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Configurazione per le app AEM{#configuring-for-aem-apps}

Le app Adobe Experience Manager ti consentono di aggiornare il contenuto dell’OTA dell’applicazione (via etere). Il contenuto aggiornato viene archiviato nell’istanza di pubblicazione. Per consentire all’app sul dispositivo di connettersi all’istanza Publish e di verificare la disponibilità di aggiornamenti, l’istanza Publish deve essere configurata in modo da consentire l’utilizzo di un’intestazione referente vuota.

## Configurazione di un’intestazione di riferimento vuota {#configuring-empty-referrer-header}

Per configurare il servizio filtro referenti:

* Apri la console Apache Felix (**Configurazioni**) in:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Accedi come amministratore.
* In **Configurazioni** , selezionare: *Filtro referrer Apache Sling*
* Seleziona il campo Consenti vuoto per consentire intestazioni referente vuote/mancanti.
* Clic **Salva** per salvare le modifiche.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulta la [Impostazioni configurazione OSGI](/help/sites-deploying/osgi-configuration-settings.md) e [Elenco di controllo della sicurezza: problemi relativi alla falsificazione di richieste tra siti diversi](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) per ulteriori dettagli.
