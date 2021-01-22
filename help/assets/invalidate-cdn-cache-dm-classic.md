---
title: Annullamento della validità della cache CDN tramite Dynamic Media Classic
description: L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media Classic, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: f786b35e77c6b862f7fc6e45d3d0af56a51e3e95
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 24%

---


# Annullamento della validità della cache CDN tramite Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Le risorse Dynamic Media vengono memorizzate nella cache dalla rete CDN per una distribuzione rapida. Tuttavia, quando apportate gli aggiornamenti a una risorsa, potreste desiderare che tali modifiche diventino effettive immediatamente. L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo ad Dynamic Media in AEM 6.5, Service Pack 5 (AEM 6.5.5) o versioni precedenti.<br>Se utilizzate Dynamic Media in AEM 6.5, Service Pack 6 (AEM 6.5.6) o versione successiva, seguite i passaggi descritti in  [Invalidazione della cache CDN tramite Dynamic Media.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

Vedere anche [Panoramica della cache in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Per annullare la validità della cache CDN tramite Dynamic Media Classic:**

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app), quindi accedi al tuo account.

   Le credenziali e l&#39;accesso sono stati forniti  Adobe al momento del provisioning. Se non disponete di tali informazioni, contattate il supporto tecnico.

1. Vicino all&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali.]**
1. Nella pagina Impostazioni generali applicazione, sotto l&#39;intestazione del gruppo Server, individuare la casella di testo **[!UICONTROL Modello di annullamento validità CDN]**.

1. Specificate il modello utilizzato per invalidare la cache CDN (Content Delivery Network).

   Ad esempio, se immettete un URL immagine (con predefiniti per immagini o modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell’esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<server>/is/image` dove `<server>` è il nome del server di pubblicazione definito in Impostazioni generali e &lt;ID> è la risorsa o le risorse selezionate per essere annullate.

1. Nell&#39;angolo inferiore destro della pagina, fare clic su **[!UICONTROL Chiudi.]**
1. Nell’interfaccia utente di Dynamic Media Classic, selezionate una o più risorse, quindi fate clic su **[!UICONTROL File > Annulla validità CDN.]** Vedrete un elenco di uno o più URL generati dal modello e dalle risorse selezionate. Utilizza l’URL del server elencato in &quot;Nome server pubblicato&quot; nelle Impostazioni generali applicazione.

   Ad esempio, con il modello di annullamento validità CDN impostato nel passaggio precedente, supponete di aver selezionato una singola immagine di risorsa immagine denominata `Backpack_B`. Quando si fa clic su **[!UICONTROL File > Annulla validità CDN]**, nell&#39;interfaccia utente di annullamento validità CDN viene generato il seguente URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL, fate clic su **[!UICONTROL Continue]** per cancellare la cache per ciascun URL specifico. Potete modificare un URL o aggiungere un URL digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare precedentemente CDN Annulla validità modello.

   Dopo aver fatto clic su **[!UICONTROL Continue]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se hai selezionato più risorse e poi hai selezionato **[!UICONTROL File > Annulla validità CDN]**, nell’**[!UICONTROL URL del modello salvato viene fatto riferimento a ciascuna risorsa.]** Di conseguenza, puoi definire un **[!UICONTROL Modello di annullamento validità CDN]** facendo riferimento a ciascun predefinito dell’URL immagine a cui viene fatto riferimento nel tuo sito web (ad esempio dettagli del prodotto, risultati di ricerca e così via). Quindi, quando selezioni una o più immagini della cache di cui annullare la validità, gli URL compilano automaticamente l’interfaccia.

   >[!NOTE]
   >
   >Quando selezioni le risorse e fai clic su **[!UICONTROL File > Annulla validità CDN]**, Dynamic Media utilizza un modello CDN non valido per creare automaticamente gli URL che consentano di annullare la validità dalla rete CDN (Content Delivery Network). Se nella casella di testo **[!UICONTROL Modello di annullamento validità CDN]** non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse, bensì su URL. Pertanto, è necessario conoscere gli URL completi presenti sul tuo sito web. Dopo aver determinato questi URL, puoi aggiungerli alla casella di testo **[!UICONTROL Invalidate CDN Template (Annulla validità modello CDN)]** descritta nei passaggi precedenti. A questo punto puoi selezionare queste risorse e annullare la validità degli URL, tutto in un unico passaggio.
   >
   >Un&#39;altra opzione consiste nell&#39;aggiungere URL completi all&#39;elenco **[!UICONTROL Annulla validità CDN]**. Se seguite questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare all&#39;opzione **[!UICONTROL File > Annulla validità CDN]**.

