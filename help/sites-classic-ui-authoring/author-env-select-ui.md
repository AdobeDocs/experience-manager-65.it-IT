---
title: Selezione dell’interfaccia utente
description: Per semplificare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Selezione dell’interfaccia utente{#selecting-your-ui}

Poiché l’interfaccia touch sostituisce l’interfaccia classica, l’utente o l’amministratore dell’istanza AEM deve prendere una decisione attiva per continuare a utilizzare l’interfaccia classica. Poiché l’interfaccia classica non viene più mantenuta, non è possibile per l’utente che esegue l’authoring passare semplicemente dall’interfaccia classica all’equivalente nell’interfaccia touch.

Per semplificare l’authoring degli utenti, l’interfaccia touch consente di passare all’interfaccia classica quando necessario. Consulta la [Selezione dell’interfaccia utente](/help/sites-authoring/select-ui.md) per informazioni dettagliate, consulta la documentazione standard sull’authoring.

>[!NOTE]
>
>Le istanze aggiornate da una versione precedente manterranno l’interfaccia utente classica per l’authoring delle pagine.
>
>Dopo l’aggiornamento, l’authoring delle pagine non passerà automaticamente all’interfaccia touch, ma puoi configurarlo utilizzando la[Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio). Consulta [Sostituzioni dell’interfaccia utente per l’editor](#uioverridesfortheeditor).

## Configurazione dell’interfaccia utente predefinita per l’istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente visualizzata all’avvio e all’accesso utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Questo può essere ignorato dai valori predefiniti dell&#39;utente o dalle impostazioni di sessione.
