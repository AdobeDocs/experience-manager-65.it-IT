---
title: Integrazione con  Search&Promote Adobe
seo-title: Integrazione con  Search&Promote Adobe
description: Scoprite come integrare  Search&Promote Adobe.
seo-description: Scoprite come integrare  Search&Promote Adobe.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# Integrazione con  Search&amp;Promote Adobe{#integrating-with-adobe-search-promote}

Per richiamare il servizio di Search&amp;Promote  dal sito Web, effettuate le seguenti operazioni:

1. Specificate l&#39;URL del cloud.
1. Configurare la connessione al servizio Search&amp;Promote.
1. Aggiungere componenti Search&amp;Promote alla barra laterale.
1. Utilizzate i componenti per creare il contenuto. (Vedere [Aggiunta di funzionalità di Search&amp;Promote a una pagina Web](/help/sites-authoring/search-and-promote.md).)
1. Aggiungete i banner alle pagine. Le immagini dei banner sono sensibili ai dati degli Search&amp;Promote.
1. Generare una mappa del sito per il servizio di Search&amp;Promote da utilizzare.

>[!NOTE]
>
>Se utilizzate Search&amp;Promote con una configurazione proxy personalizzata, dovete configurare sia le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x, sia le API 4.x:
>
>* 3.x è configurato con [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Modifica dell&#39;URL del servizio di Search&amp;Promote {#changing-the-search-promote-service-url}

L&#39;URL predefinito configurato per il servizio di Search&amp;Promote è `https://searchandpromote.omniture.com/px/`. Per usare un servizio diverso, usate la console OSGi per specificare un URL diverso.

1. Aprite la console OSGi e fate clic sulla scheda Configurazione. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Fate clic sull’elemento Configurazione Search&amp;Promote di CQ Day.
1. Immettete l’URL nella casella URI del server remoto e fate clic su Salva.

## Configurazione della connessione all&#39;Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configurate una o più connessioni alle Search&amp;Promote in modo che le pagine Web possano interagire con il servizio. Per connettersi, è necessario l&#39;identificazione del membro e il numero di account dell&#39;account di Search&amp;Promote.

1. Dall&#39;icona **Strumenti** > **Distribuzione**, selezionare **Cloud Services**.

   Viene visualizzato il Pannello Cloud Services. Se su un computer locale, l&#39;URL del dashboard sarà simile al seguente:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Nella pagina Cloud Services, fate clic sul collegamento Search&amp;Promote Adobe  o sull’icona del Search&amp;Promote.

1. Se si tratta della prima volta che si sta configurando  Search&amp;Promote, fare clic su **Configura ora** per aprire il pannello Crea configurazione.

   Per ulteriori informazioni sull&#39;Search&amp;Promote, fare clic su **Ulteriori informazioni** invece.

   ![](assets/chlimage_1-59.png)

1. Immettete un **Titolo** riconoscibile per gli autori di pagine e immettete un **Nome** univoco, quindi fate clic su **Crea**.

   Viene aperta la finestra **Edit Component**.

   Inoltre, la configurazione appena creata viene visualizzata sotto **Configurazioni disponibili** nel **pannello Cloud Services**  Adobe Search&amp;Promote voce di elenco.

   ![](assets/chlimage_1-60.png)

1. Aggiungere quanto segue ai campi della finestra di dialogo **Modifica componente**.

   * **ID membro**
   * **Numero account**

   >[!NOTE]
   >
   >Per ottenere queste informazioni **per prima cosa,** è necessario accedere a
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >utilizzando le credenziali Seach&amp;Promote valide (e-mail/password).
   >Quindi, devi guardare il tuo url nella barra degli indirizzi del tuo brouser che dovrebbe assomigliare a qualcosa di simile a questo:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Dove:**
   >
   >    * **** XXXXXXXX corrisponde al tuo** ID membro**
   >    * **** spYYYYYYYY corrisponde al numero  **account**


1. Fare clic su **Connetti a Search&amp;Promote**.

   Quando viene visualizzato il messaggio di riuscita della connessione, fare clic su **OK**.

   Dopo la connessione, il testo del pulsante diventa** Connetti di nuovo a Search&amp;Promote**.

1. Fai clic su **OK**. Viene visualizzata la pagina Impostazioni Search&amp;Promote per la configurazione appena creata.

## Configurazione del centro dati {#configuring-the-data-center}

Se l&#39;account di Search&amp;Promote è in Asia o in Europa, è necessario modificare il centro dati predefinito in modo che punti a quello destro (il centro dati predefinito è per gli account nordamericani).

Per configurare il data center:

1. Andate alla console Web all&#39;indirizzo `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. A seconda della posizione del server, imposta l’URI su una delle seguenti opzioni:

   * America del Nord: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Fai clic su **Salva**.

## Aggiunta di componenti Search&amp;Promote alla barra laterale {#adding-search-promote-components-to-sidekick}

In modalità Progettazione, modificate un componente **par** per consentire ai componenti Search&amp;Promote nella barra laterale. Per ulteriori informazioni, consultare la documentazione relativa ai [componenti](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode).

Per informazioni sull&#39;utilizzo dei componenti, vedere [Aggiunta di funzionalità di Search&amp;Promote a una pagina Web](/help/sites-authoring/search-and-promote.md).

## Specifica del servizio di Search&amp;Promote utilizzato dalle pagine {#specifying-the-search-promote-service-that-your-pages-use}

Configurate le pagine Web in modo che utilizzino un servizio Search&amp;Promote specifico. I componenti di Search&amp;Promote utilizzano automaticamente il servizio della pagina host.

Quando si configurano le proprietà degli Search&amp;Promote per una pagina, tutte le pagine figlie ereditano le impostazioni. Se necessario, potete configurare le pagine figlie in modo da ignorare le impostazioni ereditate.

>[!NOTE]
>
>La connessione del servizio deve essere già configurata. (Vedere [Configurare la connessione a Search&amp;Promote](#connection).)

1. Aprire la finestra di dialogo **Proprietà pagina**. Ad esempio, nella pagina** Siti Web**, fare clic con il pulsante destro del mouse sulla pagina e scegliere **Proprietà**.
1. Fare clic sulla scheda **Cloud Services**.
1. Per disabilitare l&#39;ereditarietà delle configurazioni dei servizi cloud da una pagina padre, fai clic sull&#39;icona lucchetto accanto al percorso di ereditarietà.

   ![](assets/sandpinheritpadlock.png)

1. Fare clic su **Aggiungi servizio**, selezionare **Search&amp;Promote**, quindi fare clic su **OK**.
1. Selezionate la configurazione della connessione per l&#39;account di Search&amp;Promote, quindi fate clic su **OK**.

## Feed prodotto {#product-feed}

L&#39;integrazione del Search&amp;Promote consente di:

* utilizzate l&#39;API eCommerce, indipendentemente dalla struttura del repository sottostante e dalla piattaforma di eCommerce.
* sfruttate la funzione del connettore indice di Search&amp;Promote per fornire un feed di prodotto in formato XML.
* utilizzare la funzione di controllo remoto del Search&amp;Promote per eseguire richieste on-demand o programmate del feed del prodotto
* generazione di feed per account di Search&amp;Promote diversi, configurati come configurazioni di servizi cloud.

Per ulteriori informazioni, consultare [Feed prodotto](/help/sites-administering/product-feed.md).
