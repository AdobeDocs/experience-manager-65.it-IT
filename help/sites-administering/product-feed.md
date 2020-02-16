---
title: Feed prodotto
seo-title: Feed prodotto
description: Ulteriori informazioni sul feed di prodotto AEM.
seo-description: Ulteriori informazioni sul feed di prodotto AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Product Feed {#product-feed}

AEM si integra con [Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) e consente di:

* utilizzate l&#39;API eCommerce, indipendentemente dalla struttura del repository sottostante e dalla piattaforma di eCommerce.
* sfruttate la funzione Connettore indice di Search&amp;Promote per fornire un feed di prodotto in formato XML.
* utilizzare la funzione di controllo remoto di Search&amp;Promote per eseguire richieste on-demand o programmate del feed di prodotto
* generazione di feed per diversi account Search&amp;Promote, configurati come configurazioni di servizi cloud.

È necessario disporre di un account valido e per [configurare la connessione a Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). È inoltre necessario verificare di utilizzare il centro [](/help/sites-administering/search-and-promote.md#configuring-the-data-center) dati corretto e assicurarsi che l&#39;URI **Server remoto **sia configurato.

## Configurare il feed di prodotto {#set-up-the-product-feed}

È innanzitutto necessario immettere un elemento principale del sito Web e un attributo di identificatore. Per effettuare ciò:

1. Andate alla configurazione Search&amp;Promote.
1. Fate clic su **[!UICONTROL Modifica]**. 
1. Fare clic sulla scheda Configurazione **[!UICONTROL feed connettore]** indice.
1. Immettere l&#39;attributo **[!UICONTROL principale]** e **[!UICONTROL Identificatore del sito Web]**.

   >[!NOTE]
   >
   >La radice **[!UICONTROL del sito]** Web è la radice del sito Web eCommerce, ad esempio `/content/geometrixx-outdoors/en`.
   >
   >L&#39;attributo **** Identifier è una proprietà JCR che identifica in modo univoco il prodotto: `identifier`.

1. Fai clic su **[!UICONTROL OK]**. 

Quindi è necessario modificare due configurazioni nella console Web prima di poter generare feed di prodotto.

### Configurazione dell’implementazione di CQ Search&amp;Promote Products Crawler Day CQ per Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Andate a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Fate clic su Implementazione crawler dei prodotti CQ Search&amp;Promote **[!UICONTROL Day per Geometrixx]**.
1. Specificate il numero di account Search&amp;Promote a cui è collegato questo crawler. Verrà utilizzato per cercare la configurazione dei servizi cloud utilizzata da questo crawler.
1. Fai clic su **[!UICONTROL Salva]**.

### Configurazione di Day CQ Search&amp;Promote Products Feed Generator per Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Andate a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Fate clic su Generatore di feed di prodotti CQ Search&amp;Promote **[!UICONTROL Day per Geometrixx]**.
1. Specificate il numero di account Search&amp;Promote a cui è collegato questo generatore. Sarà utilizzato per cercare la configurazione dei servizi cloud utilizzata da questo generatore.
1. Fai clic su **[!UICONTROL Salva]**.

## Pianificazione del feed di prodotto {#schedule-the-product-feed}

Per abilitare la generazione di feed pianificata, devi configurare un pianificatore.
Un pianificatore è configurato come configurazione figlia della configurazione specifica dei servizi cloud Search&amp;Promote.

1. Andate alla configurazione Search&amp;Promote.
1. Fate clic **[!UICONTROL +]** accanto alla configurazione **** Pianificatore.
1. Inserite un **[!UICONTROL Titolo]** riconoscibile per gli autori della pagina e un **[!UICONTROL Nome]** univoco.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Immettere la password **[!UICONTROL del controllo]** remoto. È la password configurata nel tuo account Search&amp;Pronote.

   >[!NOTE]
   >
   >Questa non è la password del tuo account Search&amp;Promote. Puoi trovare e modificare questa password accedendo al tuo account Search&amp;Promote e andando a **[!UICONTROL Index]** e poi a **[!UICONTROL Remote Control]**.

1. Selezionare **[!UICONTROL Abilita pianificazione]** .
1. Selezionare una **[!UICONTROL pianificazione]**. È la pianificazione effettiva della generazione dei feed.
1. Abilitare o meno l&#39;indicizzazione **** on-demand. Questa funzione viene utilizzata per chiamare manualmente l’indice Search&amp;Promote. Se **[!UICONTROL Richiedi feed]** prodotti completi è selezionato, Search&amp;Promote richiederà un feed prodotti completo. In caso contrario, viene richiesto un feed di prodotti incrementali.

   >[!NOTE]
   >
   >La funzione di indicizzazione su richiesta utilizza la funzione di controllo remoto di Search&amp;Promote. Quando viene chiamato un indicizzazione remota, l&#39;indicizzazione non verrà avviata immediatamente, ma una richiesta di indicizzazione verrà inviata a Search&amp;Promote tramite la funzione di controllo remoto.

1. Fai clic su **[!UICONTROL OK]**. 

Ora che avete configurato tutto, potete vedere una pagina XML contenente tutti i prodotti nella directory principale del sito Web configurata: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
