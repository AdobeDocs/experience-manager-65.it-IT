---
title: Invalidare la cache di rete per la distribuzione dei contenuti tramite Dynamic Media Classic
description: L’annullamento della validità della rete CDN (Content Delivery Network) consente di aggiornare rapidamente le risorse distribuite da Dynamic Media Classic, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: e17747bc-9b7b-44e6-a443-f54229a02620
    internal-label: Integrations
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: fc27aefe-8efd-48a6-89bf-c46e0e334a63
    internal-label: CDN cache
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%
---
# Invalidare la cache di rete per la distribuzione dei contenuti tramite Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Le risorse Dynamic Media vengono memorizzate nella cache dalla rete CDN (Content Delivery Network) per velocizzarne la distribuzione. Tuttavia, quando apporti aggiornamenti a una risorsa, vuoi che tali modifiche diventino effettive immediatamente. L’annullamento della validità del contenuto CDN memorizzato nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, invece di attendere la scadenza della cache.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo a Dynamic Media in Adobe Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versioni precedenti.<br>Se utilizzi Dynamic Media in Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o versione successiva, segui i passaggi descritti in [Invalidare la cache CDN tramite Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Per annullare la validità della cache CDN tramite Dynamic Media Classic:**

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=it#system-requirements-dmc-app), quindi accedi al tuo account.

   Le credenziali e l&#39;accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti Adobe.

1. Nell&#39;angolo superiore destro della pagina passare a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**.
1. Nella pagina Impostazioni generali applicazione, sotto l&#39;intestazione del gruppo Server, individuare la casella di testo **[!UICONTROL Modello di annullamento validità CDN]**.

1. Specifica il modello utilizzato per annullare la validità della cache CDN (Content Delivery Network).

   Si supponga, ad esempio, di immettere un URL immagine (inclusi predefiniti immagine o modificatori) che fa riferimento a `<ID>`, anziché un ID immagine specifico come nell&#39;esempio seguente:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<server>/is/image` dove `<server>` è il nome del server di pubblicazione definito nelle impostazioni generali e &lt;ID> è la risorsa selezionata per l&#39;annullamento della validità.

1. Nell&#39;angolo inferiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
1. Nell&#39;interfaccia utente di Dynamic Media Classic, seleziona una o più risorse, quindi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**. Viene visualizzato un elenco di uno o più URL generati dal modello creato e dalle risorse selezionate. Utilizza l’URL del server elencato in &quot;Published Server Name&quot; (Nome server pubblicato) nelle impostazioni generali dell’applicazione.

   Ad esempio, con il modello di annullamento della validità CDN impostato nel passaggio precedente, supponi di aver selezionato una singola immagine della risorsa immagine denominata `Backpack_B`. Quando si passa a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, nell&#39;interfaccia utente di annullamento validità CDN viene generato il seguente URL:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Nella casella di riepilogo URL selezionare **[!UICONTROL Continua]** per cancellare la cache per ogni URL specifico. Puoi modificare un URL oppure aggiungerlo digitandolo o incollandolo nella casella di riepilogo URL; non è necessario impostare in precedenza il modello di annullamento validità CDN.

   Dopo aver selezionato **[!UICONTROL Continua]**, viene visualizzato un indicatore che fornisce una stima del tempo necessario per cancellare la cache.

   Se hai selezionato più risorse e poi sei passato a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, a ciascuna risorsa viene fatto riferimento nell&#39;**[!UICONTROL URL modello]** salvato. Puoi quindi definire un **[!UICONTROL Modello di annullamento validità CDN]** facendo riferimento a ciascun predefinito dell&#39;URL immagine a cui viene fatto riferimento nel tuo sito Web (ad esempio dettagli del prodotto e risultati di ricerca). Quindi, quando selezioni una o più immagini della cache di cui annullare la validità, gli URL compilano automaticamente l’interfaccia.

   >[!NOTE]
   >
   >Quando selezioni le risorse e poi vai a **[!UICONTROL File]** > **[!UICONTROL Annulla validità CDN]**, Dynamic Media utilizza un modello CDN non valido per creare automaticamente gli URL da annullare la validità dalla rete CDN (Content Delivery Network). Se nella casella di testo **[!UICONTROL Modello di annullamento validità CDN]** non è presente alcun elemento, viene visualizzato un elenco URL vuoto. La memorizzazione nella cache della rete CDN non è basata su risorse, bensì su URL. Pertanto, è necessario conoscere gli URL completi presenti sul tuo sito web. Dopo aver determinato questi URL, puoi aggiungerli alla casella di testo **[!UICONTROL Invalidate CDN Template (Annulla validità modello CDN)]** descritta nei passaggi precedenti. A questo punto puoi selezionare queste risorse e annullare la validità degli URL, tutto in un unico passaggio.
   >
   >Un&#39;altra opzione consiste nell&#39;aggiungere URL completi all&#39;elenco **[!UICONTROL Annulla validità CDN]**. Se si segue questo approccio, non è necessario selezionare le risorse in Dynamic Media Classic prima di passare all&#39;opzione **[!UICONTROL File > Annulla validità CDN]**.
