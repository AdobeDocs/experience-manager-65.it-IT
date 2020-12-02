---
title: Introduzione alla pubblicazione di moduli su un portale
seo-title: Introduzione alla pubblicazione di moduli su un portale
description: ' AEM Forms fornisce componenti che è possibile utilizzare per creare il portale dei moduli. In questi articoli vengono presentati i componenti del portale dei moduli disponibili.'
seo-description: ' AEM Forms fornisce componenti che è possibile utilizzare per creare il portale dei moduli. In questi articoli vengono presentati i componenti del portale dei moduli disponibili.'
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# Introduzione alla pubblicazione di moduli su un portale{#introduction-to-publishing-forms-on-a-portal}

##  dei componenti del portale AEM Forms {#aem-forms-portal-components-overview}

In uno scenario di implementazione tipico del portale incentrato sui moduli, lo sviluppo dei moduli e lo sviluppo del portale sono due attività discongiunte. Mentre i progettisti di moduli progettano e memorizzano i moduli in un archivio, gli sviluppatori Web creano un&#39;applicazione Web per elencare i moduli e gestire l&#39;invio dei moduli. Forms viene copiato sul livello Web in quanto non è disponibile alcuna comunicazione tra l&#39;archivio dei moduli e l&#39;applicazione Web.

Tali scenari spesso causano problemi di gestione e ritardi nella produzione. Ad esempio, se è disponibile una versione più recente di un modulo nella directory archivio, è necessario sostituire il modulo sul livello Web, modificare l&#39;applicazione Web e ridistribuire il modulo sul sito pubblico. La riimplementazione dell&#39;applicazione Web potrebbe causare un certo tempo di inattività del server. In genere, il tempo di inattività del server è un&#39;attività pianificata e pertanto le modifiche non possono essere inviate istantaneamente al sito pubblico.

 AEM Forms fornisce componenti del portale che riducono i costi generali di gestione e i ritardi di produzione. I componenti consentono agli sviluppatori Web di creare e personalizzare un portale moduli sui siti Web creati con Adobe Experience Manager (AEM).

![ portale AEM Forms](assets/aem-forms-portal.png)

I componenti del portale moduli consentono di aggiungere le seguenti funzionalità:

* Elenca i moduli in layout personalizzati. Sono disponibili layout di visualizzazione a elenco, a schede e a pannelli. Potete creare layout personalizzati.
* Consente di visualizzare i metadati personalizzati e le azioni personalizzate durante l&#39;elencazione.
* Elenca i moduli pubblicati dallinterfaccia utente di AEM Forms nell’istanza di pubblicazione in cui vengono utilizzati i componenti di Forms Portal.
* Consentire agli utenti finali di eseguire il rendering dei moduli in formato HTML e PDF.
* Utilizzare un profilo HTML personalizzato per eseguire il rendering dei moduli.
* Abilitare la ricerca di moduli in base a vari criteri, ad esempio proprietà del modulo, metadati e tag.
* Inviare i dati del modulo a un servlet.
* Utilizzate CSS personalizzato per personalizzare l&#39;aspetto del portale.
* Creare collegamenti ai moduli.
* Elenca le bozze e gli invii relativi al modulo adattivo creato dall&#39;utente finale.

## Componenti  portale AEM Forms {#available-aem-forms-portal-components} disponibili

 AEM Forms fornisce i seguenti componenti del portale, raggruppati in **Document Services** e **Document Services Predicates** gruppi di componenti:

### Ricerca ed elenco {#search-amp-lister}

Il componente Ricerca e filtro consente di elencare i moduli dall&#39;archivio moduli nella pagina del portale e fornisce opzioni di configurazione per elencare i moduli in base a criteri specifici. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di effettuare ricerche nell&#39;elenco dei moduli.

### Bozze e invii {#drafts-amp-submissions}

Mentre il componente Ricerca e filtro visualizza i moduli resi pubblici dall&#39;autore di Forms, il componente Bozze e invii mostra i moduli salvati come bozza per la compilazione e l&#39;invio di moduli in un secondo momento. Questo componente offre un’esperienza personalizzata a qualsiasi utente che ha effettuato l’accesso.

### Collegamento {#link}

Il componente Collegamento consente di creare un collegamento a un modulo ovunque sulla pagina. Considerate uno scenario in cui offrite un programma di formazione e desiderate che gli utenti inviino un modulo per registrarsi alla formazione. Sul sito Web sono stati pubblicati i dettagli del programma. Sotto i dettagli, è necessario fornire un collegamento al modulo di registrazione. Il componente Collegamento può facilitare la creazione di tale collegamento.

## Flusso di lavoro Forms Portal {#forms-portal-workflow}

Il portale Forms consente di elencare i moduli dall&#39;archivio moduli nella pagina del portale. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di effettuare ricerche nell&#39;elenco dei moduli. È inoltre possibile utilizzare il componente Bozze e invii per visualizzare i moduli salvati come bozza per la compilazione e l&#39;invio di moduli in un secondo momento. Prima di rendere disponibili tali funzionalità in una pagina Siti, è necessario eseguire una serie di operazioni. Effettuate i passaggi della sequenza elencata per rendere disponibili su una pagina del sito i componenti e le rispettive funzionalità:

1. **Abilitare i componenti** di Forms Portal: I componenti del portale moduli non sono disponibili per l&#39;uso. [Abilitare i componenti da AEM ](/help/forms/using/enabling-forms-portal-components.md) barra laterale per una pagina AEM Sites .
1. **Elenca i moduli in una pagina (pagina del portale per la creazione di moduli):** È possibile elencare i moduli sia  pagine di AEM Sites che pagine di siti non AEM. L’elenco contiene moduli disponibili nell’istanza di pubblicazione. Un utente può aprire i moduli e iniziare a compilarli. Ogni volta che un utente apre un modulo, viene creata una nuova istanza del modulo:

   1. **Elenca i moduli in una pagina** AEM Sites : Aggiungere il componente  **[Ricerca e](../../forms/using/creating-form-portal-page.md)** Listercomponenti alla pagina e configurare il pannello  **[Elenco](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** per elencare i moduli su una pagina. Aggiungete e configurate il componente **Riquadro di ricerca** anche al componente **Ricerca e filtro** per aggiungere funzionalità di ricerca alla pagina. La pagina con il componente Portale moduli è nota come pagina del portale [moduli](../../forms/using/creating-form-portal-page.md).

   1. **Elenca i moduli in una pagina AEM Sites non :** utilizzare le  [API di ricerca del portale ](/help/forms/using/listing-forms-webpage-using-apis.md) dei moduli per eseguire query, recuperare ed elencare moduli su pagine AEM Sites non .

1. **Elenca i moduli bozza e inviati in una pagina** del portale moduli: Aggiungere e configurare il componente Bozze e invii nella pagina del portale dei moduli. Il componente elenca tutti i moduli che si trovano nello stato bozza e quelli già inviati.

   Per abilitare la visualizzazione di un modulo adattivo inviato nella scheda di invio, impostare l&#39;azione **Invia** su **[Forms Portal Submit Action](configuring-submit-actions.md).** In alternativa, abilitate l&#39;opzione Invia di Forms Portal. Ogni volta che un utente invia il modulo, il modulo viene aggiunto alla scheda di invio.

1. **Configurare la memorizzazione per i dati della bozza e dei moduli inviati:** per impostazione predefinita, i dati delle bozze e degli invii vengono memorizzati nell&#39;archivio AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati AEM repository. [Configurare il componente del portale dei moduli per salvare i dati in una posizione](../../forms/using/draft-submission-component.md#customizing-the-storage) protetta.
1. **(Facoltativo) Personalizzazione dei componenti del portale dei moduli:** [Personalizzazione dei ](../../forms/using/customizing-templates-forms-portal-components.md) modelli di pagina del portale dei moduli per fornire un aspetto distintivo ai componenti.
1. **(Facoltativo) Aggiungere metadati personalizzati ai moduli:** [aggiungere metadati personalizzati ai ](../../forms/using/customizing-templates-forms-portal-components.md) moduli per migliorare l&#39;elenco e l&#39;esperienza di ricerca.
1. **Pubblicare la pagina del portale dei moduli:** La pagina del portale dei moduli è ora pronta. Pubblicate la pagina.

## Articoli correlati {#related-articles}

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale moduli](../../forms/using/creating-form-portal-page.md)
* [Elencare i moduli in una pagina Web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Bozze e invii](../../forms/using/draft-submission-component.md)
* [Personalizzazione dell&#39;archiviazione delle bozze e dei moduli inviati](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Esempio per l’integrazione del componente bozze e invii con il database](integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale moduli](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md)

