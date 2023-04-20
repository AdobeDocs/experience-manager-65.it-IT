---
title: Selezione dell’interfaccia utente
description: Per agevolare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Selezione dell’interfaccia utente{#selecting-your-ui}

Poiché l’interfaccia touch sostituisce l’interfaccia classica, l’utente o l’amministratore dell’istanza di AEM deve prendere una decisione attiva per continuare a utilizzare l’interfaccia classica. Poiché l’interfaccia classica non viene più aggiornata, l’utente che si occupa dell’authoring non può semplicemente passare dall’interfaccia classica all’equivalente nell’interfaccia touch.

Per agevolare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario. Consulta la sezione [Selezione dell’interfaccia utente](/help/sites-authoring/select-ui.md) per ulteriori informazioni, consulta la documentazione standard sull’authoring .

>[!NOTE]
>
>Le istanze aggiornate da una versione precedente manterranno l’interfaccia classica per la creazione delle pagine.
>
>Dopo l’aggiornamento, l’authoring delle pagine non passa automaticamente all’interfaccia touch, ma è possibile configurarlo utilizzando l’[Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio). Vedi [Ignorare le impostazioni dell’interfaccia per l’editor](#uioverridesfortheeditor).

## Configurazione dell’interfaccia utente predefinita per la tua istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente visualizzata all’avvio e all’accesso utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Questo valore può essere ignorato dalle impostazioni predefinite dell’utente o dalle impostazioni della sessione.
