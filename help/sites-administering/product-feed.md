---
title: Feed prodotto
seo-title: Feed prodotto
description: Ulteriori informazioni sul feed AEM prodotto.
seo-description: Ulteriori informazioni sul feed AEM prodotto.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---


# Feed prodotto {#product-feed}

AEM si integra con [Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) e consente di:

* utilizzate l&#39;API eCommerce, indipendentemente dalla struttura del repository sottostante e dalla piattaforma di eCommerce.
* sfruttate la funzione del connettore indice di Search&amp;Promote per fornire un feed di prodotto in formato XML.
* utilizzare la funzione di controllo remoto del Search&amp;Promote per eseguire richieste on-demand o programmate del feed del prodotto
* generazione di feed per account di Search&amp;Promote diversi, configurati come configurazioni di servizi cloud.

È necessario disporre di un account valido e [configurare la connessione a Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). È inoltre necessario verificare di utilizzare il [data center](/help/sites-administering/search-and-promote.md#configuring-the-data-center) corretto e assicurarsi che l&#39;URI **Remote server **sia configurato.

## Impostare il Feed prodotto {#set-up-the-product-feed}

È innanzitutto necessario immettere un elemento principale del sito Web e un attributo di identificatore. Per effettuare ciò:

1. Andate alla configurazione del Search&amp;Promote.
1. Fate clic su **[!UICONTROL Modifica]**. 
1. Fare clic sulla scheda **[!UICONTROL Configurazione feed connettore indice]**.
1. Immettere l&#39;attributo **[!UICONTROL radice del sito Web]** e l&#39;attributo **[!UICONTROL Identificatore]**.

   >[!NOTE]
   >
   >La **[!UICONTROL radice del sito Web]** è la radice del sito Web eCommerce, ad esempio `/content/geometrixx-outdoors/en`.
   >
   >L&#39;attributo **[!UICONTROL Identifier]** è una proprietà JCR che identifica in modo univoco il prodotto: `identifier`.

1. Fai clic su **[!UICONTROL OK]**.

Quindi è necessario modificare due configurazioni nella console Web prima di poter generare feed di prodotto.

### Configurazione dell’implementazione di Day CQ Search&amp;Promote Products Crawler per l’Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Andate a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Fare clic su **[!UICONTROL Day CQ Search&amp;Promote prodotti implementazione crawler per Geometrixx]**.
1. Specificate il numero di account Search&amp;Promote a cui è collegato il crawler. Verrà utilizzato per cercare la configurazione dei servizi cloud utilizzata da questo crawler.
1. Fai clic su **[!UICONTROL Salva]**.

### Configurazione di Day CQ Search&amp;Promote Feed Generator per il Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Andate a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Fare clic su **[!UICONTROL Day CQ Search&amp;Promote feed generatore per Geometrixx]**.
1. Specificate il numero di account Search&amp;Promote a cui è collegato questo generatore. Sarà utilizzato per cercare la configurazione dei servizi cloud utilizzata da questo generatore.
1. Fai clic su **[!UICONTROL Salva]**.

## Pianificare il feed di prodotto {#schedule-the-product-feed}

Per abilitare la generazione di feed pianificata, devi configurare un pianificatore per tale generazione.
Un pianificatore è configurato come configurazione figlia della configurazione specifica dei servizi cloud di Search&amp;Promote.

1. Andate alla configurazione del Search&amp;Promote.
1. Fare clic su **[!UICONTROL +]** accanto a **[!UICONTROL Configurazione dell&#39;utilità di pianificazione]**.
1. Immettere un **[!UICONTROL Titolo]** riconoscibile per gli autori di pagine e un **[!UICONTROL Nome]** univoco.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Immettere la **[!UICONTROL Password del telecomando]**. È la password configurata nel tuo account Search&amp;Pronote.

   >[!NOTE]
   >
   >Questa non è la password del tuo account di Search&amp;Promote. È possibile trovare e modificare questa password effettuando l&#39;accesso al proprio account di Search&amp;Promote e andando a **[!UICONTROL Index]** e poi a **[!UICONTROL Controllo remoto]**.

1. Selezionare la casella **[!UICONTROL Abilita pianificazione]**.
1. Selezionare una **[!UICONTROL Pianificazione]**. È la pianificazione effettiva della generazione dei feed.
1. Abilitare o meno l&#39;indicizzazione su richiesta **[!UICONTROL on-demand]**. Questa funzione viene utilizzata per chiamare manualmente l&#39;indice di Search&amp;Promote. Se **[!UICONTROL Richiedi feed prodotti completi]** è selezionato, il Search&amp;Promote richiederà un feed prodotti completo. In caso contrario, viene richiesto un feed di prodotti incrementali.

   >[!NOTE]
   >
   >La funzione di indicizzazione on-demand utilizza la funzione di controllo remoto del Search&amp;Promote. Quando viene chiamata un&#39;indicizzazione remota, l&#39;indicizzazione non viene avviata immediatamente, ma una richiesta di indicizzazione viene inviata alle Search&amp;Promote utilizzando la funzione di controllo remoto.

1. Fai clic su **[!UICONTROL OK]**.

Ora che avete configurato tutto, potete vedere una pagina XML contenente tutti i prodotti nella directory principale del sito Web configurata: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
