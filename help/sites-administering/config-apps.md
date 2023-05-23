---
title: Configurazione per le app AEM
seo-title: Configuring for AEM Apps
description: Scopri come configurare le app AEM.
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Configurazione per le app AEM{#configuring-for-aem-apps}

Le app Adobe Experience Manager consentono di aggiornare il contenuto dell’applicazione in diretta (OTA). Il contenuto aggiornato viene archiviato nell’istanza di pubblicazione. Per consentire all’app sul dispositivo di connettersi all’istanza Publish e verificare la disponibilità di aggiornamenti, l’istanza Publish deve essere configurata in modo da consentire l’utilizzo di un’intestazione referente vuota.

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
