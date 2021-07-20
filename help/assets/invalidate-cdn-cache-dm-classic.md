---
title: Annullare la validità della cache della rete di distribuzione dei contenuti tramite Dynamic Media Classic
description: L’annullamento della validità della rete CDN (Content Delivery Network) memorizzata nella cache consente di aggiornare rapidamente le risorse consegnate da Dynamic Media Classic, anziché attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Cache CDN, Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 12%

---

# Annullare la validità della cache della rete di distribuzione dei contenuti tramite Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Le risorse Dynamic Media sono memorizzate nella cache della rete CDN (Content Delivery Network) per velocizzarne la distribuzione. Tuttavia, quando apporti aggiornamenti a una risorsa, vuoi che tali modifiche abbiano effetto immediato. L’annullamento della validità del contenuto CDN memorizzato nella cache consente di aggiornare rapidamente le risorse consegnate da Dynamic Media, anziché attendere la scadenza della cache.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo a Dynamic Media in Adobe Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versioni precedenti.<br>Se utilizzi Dynamic Media in Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o versione successiva, segui i passaggi descritti in  [Invalidate the CDN cache (Invalida la cache CDN) tramite Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

Vedi anche [Panoramica sulla cache in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Per annullare la validità della cache CDN tramite Dynamic Media Classic:**

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app), quindi accedi al tuo account.

   Le credenziali e l&#39;accesso sono stati forniti da Adobe al momento del provisioning. Se non si dispone di tali informazioni, contattare il supporto tecnico.

1. Vicino all&#39;angolo superiore destro della pagina, passa a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**.
1. Nella pagina Impostazioni generali applicazione, sotto l&#39;intestazione del gruppo Server, individuare la casella di testo **[!UICONTROL Modello di invalidazione CDN]**.

1. Specifica il modello utilizzato per annullare la validità della cache CDN (Content Delivery Network).

   Ad esempio, supponiamo di inserire un URL immagine (inclusi predefiniti immagine o modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<server>/is/image` dove `<server>` è il nome del server di pubblicazione definito in Impostazioni generali e &lt;ID> sono le risorse selezionate da annullare.

1. Nell&#39;angolo in basso a destra della pagina, seleziona **[!UICONTROL Chiudi]**.
1. Nell’interfaccia utente di Dynamic Media Classic, seleziona una o più risorse, quindi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**. Viene visualizzato un elenco di uno o più URL generati dal modello creato e dalle risorse selezionate. Utilizza l&#39;URL del server elencato in &quot;Nome server pubblicato&quot; nelle Impostazioni generali dell&#39;applicazione.

   Ad esempio, con il modello di annullamento validità CDN impostato nel passaggio precedente, supponi di aver selezionato una singola immagine di risorsa immagine denominata `Backpack_B`. Quando si passa a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, si ottiene il seguente URL generato nell&#39;interfaccia utente di annullamento validità CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL, seleziona **[!UICONTROL Continua]** per cancellare la cache per ogni URL specifico. È possibile modificare un URL o aggiungere un URL digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare prima il modello di annullamento validità CDN.

   Dopo aver selezionato **[!UICONTROL Continua]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se hai selezionato più risorse, vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, a ciascuna risorsa viene fatto riferimento nell&#39; **[!UICONTROL URL modello]** salvato. Pertanto, puoi definire un **[!UICONTROL Modello di annullamento validità CDN]** facendo riferimento a ciascun predefinito immagine URL a cui viene fatto riferimento sul tuo sito web (ad esempio dettagli del prodotto e risultati della ricerca). Quindi, quando selezioni una o più immagini della cache di cui annullare la validità, gli URL compilano automaticamente l’interfaccia.

   >[!NOTE]
   >
   >Quando selezioni le risorse e vai su **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, Dynamic Media utilizza un modello CDN non valido per creare automaticamente URL da annullare la validità dalla rete CDN (Content Delivery Network). Se nella casella di testo **[!UICONTROL Modello di annullamento validità CDN]** non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse, bensì su URL. Pertanto, è necessario conoscere gli URL completi presenti sul tuo sito web. Dopo aver determinato questi URL, puoi aggiungerli alla casella di testo **[!UICONTROL Invalidate CDN Template (Annulla validità modello CDN)]** descritta nei passaggi precedenti. A questo punto puoi selezionare queste risorse e annullare la validità degli URL, tutto in un unico passaggio.
   >
   >Un&#39;altra opzione è quella di aggiungere URL completi all&#39;elenco **[!UICONTROL Annulla validità CDN]**. Se segui questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare all’opzione **[!UICONTROL File > Annulla validità CDN]** .
