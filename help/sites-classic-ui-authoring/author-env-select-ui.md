---
title: Selezione dell’interfaccia
seo-title: Selecting your UI
description: Per agevolare il lavoro degli utenti che si occupano di authoring, l’interfaccia utente touch consente di passare all’interfaccia classica quando necessario.
seo-description: For convenience to authoring users, the touch-enabled UI does allow for switching to the classic UI when necessary.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 55%

---

# Selezione dell’interfaccia{#selecting-your-ui}

Poiché l’interfaccia touch sostituisce l’interfaccia classica, l’utente o l’amministratore dell’istanza di AEM deve prendere una decisione attiva per continuare a utilizzare l’interfaccia classica. Poiché l’interfaccia classica non viene più aggiornata, l’utente che si occupa dell’authoring non può semplicemente passare dall’interfaccia classica all’equivalente nell’interfaccia touch.

Per agevolare il lavoro degli utenti che si occupano di authoring, l’interfaccia utente touch consente di passare all’interfaccia classica quando necessario. Per ulteriori informazioni, consulta la sezione [Selezione dell’interfaccia](/help/sites-authoring/select-ui.md) nella documentazione di authoring standard.

>[!NOTE]
>
>Nelle istanze aggiornate da una versione precedente viene mantenuta l’interfaccia classica per la creazione e la modifica delle pagine.
>
>Dopo l’aggiornamento, l’authoring delle pagine non passa automaticamente all’interfaccia touch, ma è possibile configurarlo utilizzando l’[Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio). Vedi [Ignorare le impostazioni dell’interfaccia per l’editor](#uioverridesfortheeditor).

## Configurazione dell’interfaccia utente predefinita per la propria istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente utilizzata all’avvio e all’accesso utilizzando la [mappatura della directory principale](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Tale impostazione può essere ignorata e sostituita dalle impostazioni predefinite dell’utente o dalle impostazioni della sessione.
