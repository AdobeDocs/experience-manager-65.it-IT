---
title: Configurare il connettore di traduzione
description: Scopri come connettersi AEM a un servizio di traduzione.
index: true
hide: false
hidefromtoc: false
source-git-commit: 7cf68868e0963930bde9fcda647822a03914b61d
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Configurare il connettore di traduzione {#configure-connector}

Scopri come connettersi AEM a un servizio di traduzione.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di traduzione senza testa AEM, [Guida introduttiva alla traduzione senza testa AEM](learn-about.md) hai imparato a organizzare i contenuti headless e come funzionano gli strumenti di traduzione AEM e dovresti ora:

* Comprendere l’importanza della struttura dei contenuti per la traduzione.
* Comprendere come AEM memorizza i contenuti headless.
* Conoscere AEM strumenti di traduzione.

Questo articolo si basa su queste nozioni di base per permetterti di compiere il primo passaggio di configurazione e impostare un servizio di traduzione, che utilizzerai successivamente nel percorso per tradurre i contenuti.

## Obiettivo {#objective}

Questo documento spiega come impostare un connettore AEM per il servizio di traduzione selezionato. Dopo la lettura è necessario:

* Comprendi gli importanti parametri del framework di integrazione della traduzione in AEM.
* È possibile impostare la propria connessione al servizio di traduzione.

## Quadro di riferimento per l&#39;integrazione della traduzione {#tif}

AEM Translation Integration Framework (TIF) si integra con servizi di traduzione di terze parti per orchestrare la traduzione dei contenuti AEM. Si tratta di tre passaggi fondamentali.

1. Connettiti al provider di servizi di traduzione.
1. Creare una configurazione di Translation Integration Framework.
1. Associa la configurazione al contenuto.

Le sezioni seguenti descrivono questi passaggi in modo più dettagliato.

## Connessione a un provider di servizi di traduzione {#connect-translation-provider}

Il primo passo è quello di scegliere quale servizio di traduzione si desidera utilizzare. Ci sono molte scelte per i servizi di traduzione umana e automatica disponibili per AEM. La maggior parte dei provider offre un pacchetto di traduzione da installare. Consulta la sezione [Risorse aggiuntive](#additional-resources) per una selezione di opzioni disponibili.

>[!NOTE]
>
>Lo specialista della traduzione è generalmente responsabile della scelta del servizio di traduzione da utilizzare, ma in genere l&#39;amministratore è responsabile dell&#39;installazione del pacchetto del connettore di traduzione richiesto.

Ai fini del presente percorso, utilizziamo Microsoft Translator che AEM fornito con una licenza di prova preconfigurata. Consulta la sezione [Risorse aggiuntive](#additional-resources) per ulteriori informazioni su questo provider.

Se scegli un altro provider, l’amministratore deve installare il pacchetto del connettore in base alle istruzioni fornite dal servizio di traduzione.

>[!NOTE]
>
>L’utilizzo di Microsoft Translator in AEM non richiede un’ulteriore configurazione e funziona così come è senza ulteriore configurazione del connettore.
>
>Se scegli di utilizzare il connettore Microsoft Translator a scopo di test, non è necessario eseguire i passaggi descritti nelle due sezioni successive: [Creazione di una configurazione dell’integrazione di traduzione](#create-config) e [Associa la configurazione al contenuto.](#associate) Si consiglia tuttavia di leggerli in modo da conoscere i passaggi necessari per configurare il connettore preferito.
>
>La licenza di prova del connettore Microsoft Translator non è destinata alla produzione e, se si decide di concedere la licenza, l’amministratore di sistema deve seguire i passaggi descritti in [Risorse aggiuntive](#additional-resources) alla fine del presente documento per configurare tale licenza.

## Creazione di una configurazione dell’integrazione di traduzione {#create-config}

Dopo aver installato il pacchetto del connettore per il servizio di traduzione preferito, è necessario creare una configurazione di Translation Integration Framework per tale servizio. La configurazione include le seguenti informazioni:

* Quale provider di servizi di traduzione utilizzare
* Se la traduzione umana o automatica deve essere eseguita
* Se tradurre altri contenuti associati al frammento di contenuto, ad esempio i tag

Per creare una nuova configurazione di traduzione:

1. Nel menu di navigazione globale, tocca o fai clic su **Strumenti** -> **Cloud Services** -> **Cloud Services di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione nella struttura del contenuto. Spesso si basa su un particolare progetto o può essere globale.
   * Ad esempio, in questo caso, una configurazione può essere resa globale da applicare a tutti i contenuti o solo al progetto WKND.

   ![Percorso di configurazione della traduzione](assets/translation-configuration-location.png)

1. Fornisci le seguenti informazioni nei campi, quindi tocca o fai clic su **Crea**.
   1. Seleziona **Tipo di configurazione** nel menu a discesa . Seleziona **Integrazione della traduzione** dall&#39;elenco.
   1. Inserisci un **Titolo** per la configurazione. La **Titolo** identifica la configurazione nel **Cloud Services** negli elenchi a discesa delle proprietà della pagina e .
   1. Facoltativamente, digita un **Nome** da utilizzare per il nodo del repository che memorizza la configurazione.

   ![Creare una configurazione di traduzione](assets/create-translation-configuration.png)

1. Tocca o fai clic su **Crea** e **Modifica configurazione** viene visualizzata la finestra in cui è possibile configurare le proprietà di configurazione.

1. I frammenti di contenuto sono memorizzati come risorse in AEM. Tocca o fai clic sul pulsante **Risorse** scheda .

![Proprietà di configurazione della traduzione](assets/translation-configuration.png)

1. Fornisci le seguenti informazioni.

   1. **Metodo di traduzione** - Seleziona **Traduzione automatica** o **Traduzione umana** a seconda del provider di traduzione. Ai fini di questo percorso si assume la traduzione automatica.
   1. **Fornitori di traduzioni** - Selezionare dall&#39;elenco il connettore installato per il servizio di traduzione.
   1. **Categoria contenuto** - Selezionare la categoria più appropriata per eseguire meglio il targeting della traduzione (solo per la traduzione automatica).
   1. **Tradurre le risorse dei frammenti di contenuto** : seleziona questa opzione per tradurre le risorse associate ai frammenti di contenuto.
   1. **Tradurre le risorse** - Controlla questo per tradurre le risorse.
   1. **Traduci metadati** - Controlla questo per tradurre i metadati delle risorse.
   1. **Traduci tag** - Seleziona questa opzione per tradurre i tag associati alla risorsa.
   1. **Esegui automaticamente traduzione** - Controlla questa proprietà se vuoi che le traduzioni vengano inviate automaticamente al tuo servizio di traduzione.

1. Tocca o fai clic su **Salva e chiudi**.

Il connettore è stato configurato nel servizio di traduzione.

## Associare la configurazione al contenuto {#associate}

AEM è uno strumento flessibile e potente e supporta più servizi di traduzione simultanea tramite più connettori e configurazioni multiple. L&#39;impostazione di tale configurazione va oltre l&#39;ambito di questo percorso. Tuttavia, questa flessibilità implica la necessità di specificare quali connettori e configurazione devono essere utilizzati per tradurre il contenuto associando questa configurazione al contenuto.

A questo scopo, accedi alla directory principale della lingua del contenuto. Per il nostro esempio:

```text
/content/dam/<your-project>/en
```

1. Vai alla navigazione globale e vai a **Navigazione** -> **Risorse** -> **File**.
1. Nella console delle risorse, seleziona la directory principale lingua da configurare e tocca o fai clic su . **Proprietà**.
1. Tocca o fai clic sul pulsante **Cloud Services** scheda .
1. Sotto **Configurazioni Cloud Service** in **Aggiungi configurazione** a discesa, seleziona il connettore. Dovrebbe apparire nel menu a discesa quando hai installato il pacchetto come [descritto in precedenza.](#connect-translation-provider)
1. Sotto **Configurazioni Cloud Service** in **Aggiungi configurazione** seleziona anche la configurazione.
1. Tocca o fai clic su **Salva e chiudi**.

![Seleziona le configurazioni del servizio cloud](assets/select-cloud-service-configurations.png)

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di traduzione headless dovresti:

* Comprendi gli importanti parametri del framework di integrazione della traduzione in AEM.
* È possibile impostare la propria connessione al servizio di traduzione.

Sviluppa questa conoscenza e continua il tuo percorso di traduzione senza testa AEM prossimo revisione del documento [Configura le regole di traduzione,](translation-rules.md) dove imparerai a definire quale contenuto tradurre.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di traduzione headless rivedendo il documento [Configurare le regole di traduzione](translation-rules.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [Configurazione del framework di integrazione della traduzione](/help/sites-administering/tc-tic.md) - Rivedi un elenco di connettori di traduzione selezionati e scopri come configurare il framework di integrazione della traduzione per l’integrazione con i servizi di traduzione di terze parti.
* [Connessione a Microsoft Translator](/help/sites-administering/tc-msconf.md) - AEM fornisce un account di traduzione Microsoft di prova a scopo di test.
