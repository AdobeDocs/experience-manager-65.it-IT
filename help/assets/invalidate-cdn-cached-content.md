---
title: Invalidazione del contenuto cache CDN
description: L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Invalidazione del contenuto cache CDN {#invalidating-your-cdn-cached-content}

Le risorse multimediali dinamiche vengono memorizzate nella cache dalla rete CDN per una distribuzione rapida. Tuttavia, quando apportate gli aggiornamenti a una risorsa, potreste desiderare che tali modifiche diventino effettive immediatamente. L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.

Consultate anche Panoramica della [cache in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Per annullare la validità del contenuto cache CDN:**

1. Accedete al vostro account Dynamic Media Classic (Scene7):

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Le credenziali e l&#39;accesso sono stati forniti da Adobe al momento del provisioning. Se non disponete di tali informazioni, contattate il supporto tecnico.

1. Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali.
1. Nella pagina Impostazioni generali applicazione, nella sezione Server del gruppo, individuate la casella di testo Modello **[!UICONTROL di annullamento validità]** CDN.

1. Specificate il modello utilizzato per invalidare la cache CDN (Content Delivery Network).

   Ad esempio, se immettete un URL immagine (con predefiniti per immagini o modificatori) che fa riferimento a un ID immagine specifico, `<ID>`anziché a un ID immagine specifico come nell’esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, Contenuti multimediali dinamici si `https://<server>/is/image` riempiono nel punto in cui `<server>` si trova il Nome server di pubblicazione definito in Impostazioni generali e &lt;ID> è la risorsa o le risorse selezionate per essere annullate.

1. Nell’angolo inferiore destro della pagina, fate clic su **[!UICONTROL Chiudi]**.
1. Nell’interfaccia utente di Dynamic Media Classic (Scene7), selezionate una o più risorse, quindi fate clic su **[!UICONTROL File > Annulla validità CDN]**. Vedrete un elenco di uno o più URL generati dal modello e dalle risorse selezionate. Utilizza l’URL del server elencato in &quot;Nome server pubblicato&quot; nelle Impostazioni generali applicazione.

   Ad esempio, con il modello di annullamento validità CDN impostato nel passaggio precedente, supponete di aver selezionato una singola immagine di risorsa immagine denominata `Backpack_B`. Quando fate clic su **[!UICONTROL File > Annulla validità CDN]** , nell’interfaccia utente di annullamento validità CDN viene generato il seguente URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL, fate clic su **[!UICONTROL Continua]** per cancellare la cache per ciascun URL specifico. Potete modificare un URL o aggiungere un URL digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare precedentemente CDN Annulla validità modello.

   Dopo aver fatto clic su **[!UICONTROL Continua]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se avete selezionato più risorse, fate clic su **[!UICONTROL File > Annulla validità CDN]**, a ciascuna risorsa viene fatto riferimento nell’URL **[!UICONTROL del]** modello salvato. Di conseguenza, potete definire un modello **[!UICONTROL di annullamento validità]** CDN facendo riferimento a ciascun predefinito per immagini URL a cui viene fatto riferimento nel sito Web (ad esempio dettagli del prodotto, risultati di ricerca e così via). Quindi, quando selezionate una o più immagini da annullare la validità della cache, gli URL compilano automaticamente l&#39;interfaccia.

   >[!NOTE]
   >
   >Quando selezionate le risorse e fate clic su **[!UICONTROL File > Annulla validità CDN]**, per creare automaticamente URL da annullare la validità dalla rete CDN (Content Delivery Network) vengono utilizzati i modelli CDN non validi per Contenuti multimediali dinamici. Se nella casella di testo **** CDN non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse; è basato su URL. Pertanto, è necessario conoscere gli URL completi presenti sul sito Web. Dopo aver determinato tali URL, potete aggiungerli alla casella di testo **[!UICONTROL Annulla validità modello]** CDN precedente nella procedura. Potete quindi selezionare tali risorse e annullare la validità degli URL in un unico passaggio.
   >
   >Un&#39;altra opzione consiste nell&#39;aggiungere URL completi all&#39;elenco **[!UICONTROL Annulla validità CDN]** . Se seguite questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare all’opzione **[!UICONTROL File > Annulla validità CDN]** .

