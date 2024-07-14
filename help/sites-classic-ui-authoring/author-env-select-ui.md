---
title: Selezione dell’interfaccia utente
description: Per semplificare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Selezione dell’interfaccia utente{#selecting-your-ui}

Poiché l’interfaccia touch sostituisce l’interfaccia classica, l’utente o l’amministratore dell’istanza AEM deve prendere una decisione attiva per continuare a utilizzare l’interfaccia classica. Poiché l’interfaccia classica non viene più mantenuta, non è possibile per l’utente che esegue l’authoring passare semplicemente dall’interfaccia classica all’equivalente nell’interfaccia touch.

Per semplificare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario. Per informazioni dettagliate, consulta la sezione [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md) nella documentazione standard per l&#39;authoring.

>[!NOTE]
>
>Le istanze aggiornate da una versione precedente manterranno l’interfaccia utente classica per l’authoring delle pagine.
>
>Dopo l&#39;aggiornamento, l&#39;authoring delle pagine non passerà automaticamente all&#39;interfaccia touch, ma puoi configurarlo utilizzando la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **servizio modalità interfaccia utente di authoring WCM** (servizio `AuthoringUIMode`). Consulta [Sostituzioni interfaccia utente per l&#39;editor](#uioverridesfortheeditor).

## Configurazione dell’interfaccia utente predefinita per l’istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l&#39;interfaccia utente visualizzata all&#39;avvio e all&#39;accesso utilizzando [Root Mapping](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Questo può essere ignorato dai valori predefiniti dell&#39;utente o dalle impostazioni di sessione.
