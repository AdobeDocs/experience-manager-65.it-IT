---
title: Integrazione con Adobe Search&Promote
seo-title: Integrazione con Adobe Search&Promote
description: Scopri come integrare con Adobe Search&Promote.
seo-description: Scopri come integrare con Adobe Search&Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# Integrazione con Adobe Search&amp;Promote{#integrating-with-adobe-search-promote}

Per chiamare il servizio Adobe Search&amp;Promote dal sito web, esegui le seguenti attività:

1. Specifica l’URL del cloud.
1. Configura la connessione al servizio Search&amp;Promote.
1. Aggiungete componenti Search&amp;Promote alla barra laterale.
1. Utilizza i componenti per creare i contenuti. (Vedere [Aggiunta di funzionalità di Search&amp;Promote a una pagina Web](/help/sites-authoring/search-and-promote.md).)
1. Aggiungi dei banner alle tue pagine. Le immagini dei banner sono sensibili ai dati di Search&amp;Promote.
1. Genera una mappa del sito per il servizio Search&amp;Promote da utilizzare.

>[!NOTE]
>
>Se utilizzi Search&amp;Promote con una configurazione proxy personalizzata, devi configurare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x e altre le API 4.x:
>
>* 3.x è configurato con [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Modifica dell&#39;URL del servizio Search&amp;Promote {#changing-the-search-promote-service-url}

L’URL predefinito configurato per il servizio Search&amp;Promote è `https://searchandpromote.omniture.com/px/`. Per utilizzare un servizio diverso, utilizza la console OSGi per specificare un URL diverso.

1. Apri la console OSGi e fai clic sulla scheda Configurazione . ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Fai clic sull&#39;elemento Day CQ Search&amp;Promote Configuration.
1. Immettere l&#39;URL nella casella URI server remoto e fare clic su Salva.

## Configurazione della connessione a Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configura una o più connessioni a Search&amp;Promote in modo che le pagine web possano interagire con il servizio. Per connettersi, è necessario l&#39;identificazione dei membri e il numero di account dell&#39;account di Search&amp;Promote.

1. Dall&#39;icona **Strumenti** > **Implementazione**, selezionare **Cloud Services**.

   Viene visualizzato il Dashboard dei Cloud Services. Se su un computer locale, l’url del dashboard sarà simile al seguente:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Nella pagina Cloud Services, fai clic sul collegamento del Search&amp;Promote di Adobe o sull’icona del Search&amp;Promote.

1. Se questa è la prima volta che si configura Adobe Search&amp;Promote, fare clic su **Configura ora** per aprire il pannello Crea configurazione.

   Per ulteriori informazioni su Search&amp;Promote, fai clic su **Ulteriori informazioni** anziché.

   ![](assets/chlimage_1-59.png)

1. Immetti un **Titolo** riconoscibile dagli autori di pagine e immetti un **Nome** univoco, quindi fai clic su **Crea**.

   Viene visualizzata la finestra **Modifica componente**.

   Inoltre, la configurazione appena creata viene visualizzata sotto **Configurazioni disponibili** sulla voce dell&#39;elenco di Search&amp;Promote **dashboard Cloud Services** Adobe.

   ![](assets/chlimage_1-60.png)

1. Aggiungi quanto segue ai campi della finestra di dialogo **Modifica componente** .

   * **ID membro**
   * **Numero di conto**

   >[!NOTE]
   >
   >Per ottenere queste informazioni **autonomamente,** è necessario prima accedere a
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >utilizzando le credenziali valide di Seach&amp;Promote (e-mail/password).
   >Poi, devi guardare il tuo url nella barra degli indirizzi del tuo brouser che dovrebbe assomigliare a qualcosa di simile a questo:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Dove:**
   >
   >    * **** XXXXXXXX corrisponde al tuo* ID membro**
   >    * **** spYYYYYYYYcorrisponde al numero del tuo  **account**


1. Fare clic su **Connetti a Search&amp;Promote**.

   Quando viene visualizzato il messaggio di connessione riuscita, fare clic su **OK**.

   (Dopo la connessione, il testo del pulsante cambia in** Connetti di nuovo a Search&amp;Promote**.)

1. Fai clic su **OK**. Viene visualizzata la pagina Impostazioni Search&amp;Promote per la configurazione appena creata.

## Configurazione del centro dati {#configuring-the-data-center}

Se l’account di Search&amp;Promote si trova in Asia o in Europa, è necessario modificare il centro dati predefinito in modo che punti a quello destro (il centro dati predefinito è per gli account nordamericani).

Per configurare il data center:

1. Passa alla console Web all’indirizzo `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. A seconda della posizione del server, modificare l’URI in uno dei seguenti modi:

   * America del Nord: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Fai clic su **Salva**.

## Aggiunta di componenti Search&amp;Promote alla barra laterale {#adding-search-promote-components-to-sidekick}

In modalità Progettazione, modifica un componente **par** per consentire l’utilizzo dei componenti Search&amp;Promote nella barra laterale. (Per ulteriori informazioni, consulta la documentazione [Componenti](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) .)

Per informazioni sull&#39;utilizzo dei componenti, vedere [Aggiunta di funzionalità di Search&amp;Promote a una pagina Web](/help/sites-authoring/search-and-promote.md).)

## Specifica del servizio Search&amp;Promote utilizzato dalle pagine {#specifying-the-search-promote-service-that-your-pages-use}

Configura le pagine web in modo che utilizzino un servizio Search&amp;Promote specifico. I componenti di Search&amp;Promote utilizzano automaticamente il servizio della relativa pagina host.

Quando si configurano le proprietà Search&amp;Promote per una pagina, tutte le pagine figlie ereditano le impostazioni. Se necessario, è possibile configurare le pagine figlie in modo da ignorare le impostazioni ereditate.

>[!NOTE]
>
>La connessione al servizio deve essere già configurata. (Consultare [Configurare la connessione a Search&amp;Promote](#connection).)

1. Apri la finestra di dialogo **Proprietà pagina** . Ad esempio, nella pagina** Siti web**, fai clic con il pulsante destro del mouse sulla pagina e fai clic su **Proprietà**.
1. Fare clic sulla scheda **Cloud Services**.
1. Per disabilitare l’ereditarietà delle configurazioni di servizi cloud da una pagina padre, fai clic sull’icona a forma di lucchetto accanto al percorso di ereditarietà.

   ![](assets/sandpinheritpadlock.png)

1. Fai clic su **Aggiungi servizio**, seleziona **Search&amp;Promote Adobe** e fai clic su **OK**.
1. Seleziona la configurazione della connessione per il tuo account Search&amp;Promote, quindi fai clic su **OK**.

## Feed di prodotto {#product-feed}

L’integrazione Search&amp;Promote consente di:

* utilizza l’API eCommerce, indipendentemente dalla struttura dell’archivio sottostante e dalla piattaforma commerce.
* sfrutta la funzione Connettore indice di Search&amp;Promote per fornire un feed di prodotto in formato XML.
* sfrutta la funzione di controllo remoto di Search&amp;Promote per eseguire richieste on-demand o pianificate del feed di prodotto
* generazione di feed per diversi account di Search&amp;Promote, configurati come configurazioni di cloud services.

Per ulteriori informazioni, consulta [Feed prodotto](/help/sites-administering/product-feed.md).
