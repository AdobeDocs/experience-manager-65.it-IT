---
title: Introduzione alla pubblicazione di moduli su un portale
description: Adobe Experience Manager Forms fornisce componenti che puoi utilizzare per creare il tuo Forms Portal. Questo articolo illustra i componenti disponibili di Forms Portal.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 1%

---

# Introduzione alla pubblicazione di moduli su un portale{#introduction-to-publishing-forms-on-a-portal}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=it) |
| AEM 6.5 | Questo articolo |


## Panoramica dei componenti di AEM Forms portal {#aem-forms-portal-components-overview}

In un tipico scenario di distribuzione di un portale incentrato sui moduli, lo sviluppo di moduli e lo sviluppo di portali sono due attività separate. Mentre i progettisti di moduli progettano e memorizzano i moduli in un repository, gli sviluppatori Web creano un&#39;applicazione Web per elencare i moduli e gestirne l&#39;invio. Forms viene copiato sul livello web in quanto non vi è alcuna comunicazione tra l’archivio dei moduli e l’applicazione web.

Tali scenari spesso causano problemi di gestione e ritardi nella produzione. Ad esempio, se nell&#39;archivio è disponibile una versione più recente di un modulo, è necessario sostituire il modulo sul livello Web, modificare l&#39;applicazione Web e ridistribuire il modulo sul sito pubblico. La ridistribuzione dell’applicazione web potrebbe causare tempi di inattività del server. In genere, il tempo di inattività del server è un’attività pianificata e pertanto le modifiche non possono essere inviate istantaneamente al sito pubblico.

AEM Forms fornisce componenti portale che riducono i costi generali di gestione e i ritardi di produzione. I componenti consentono agli sviluppatori Web di creare e personalizzare un portale Forms nei siti Web creati con Adobe Experience Manager (AEM).

![Portale AEM Forms](assets/aem-forms-portal.png)

I componenti portale moduli consentono di aggiungere le funzionalità seguenti:

* Elencare i moduli in layout personalizzati. I layout predefiniti includono la vista a elenco, a schede e a pannello. È possibile creare layout personalizzati.
* Consente di visualizzare metadati personalizzati e azioni personalizzate durante la visualizzazione dell’elenco.
* Elenca i moduli pubblicati dall’interfaccia utente di AEM Forms nell’istanza di pubblicazione in cui vengono utilizzati i componenti di Forms Portal.
* Consenti agli utenti finali di eseguire il rendering dei moduli in formato HTML e PDF.
* Utilizza un profilo HTML personalizzato per eseguire il rendering dei moduli.
* Consente di cercare i moduli in base a diversi criteri, ad esempio proprietà, metadati e tag.
* Invia i dati del modulo a un servlet.
* Utilizza CSS personalizzato per personalizzare l’aspetto del portale.
* Creare collegamenti ai moduli.
* Elenca le bozze e gli invii relativi al modulo adattivo creato dall’utente finale.

## Componenti disponibili di AEM Forms Portal {#available-aem-forms-portal-components}

AEM Forms fornisce i seguenti componenti portale pronti all’uso, raggruppati in **Document Services** e **Predicati Document Services** gruppi di componenti:

### Ricerca ed elenco {#search-amp-lister}

Il componente Ricerca ed elenco consente di elencare i moduli dall’archivio dei moduli alla pagina del portale e fornisce opzioni di configurazione per elencare i moduli in base a criteri specifici. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di eseguire ricerche nell&#39;elenco dei moduli.

### Bozze e invii {#drafts-amp-submissions}

Mentre il componente Ricerca ed elenco visualizza i moduli resi pubblici da Forms Author, il componente Bozze e invii visualizza i moduli salvati come bozza per il completamento successivo e i moduli inviati. Questo componente fornisce un’esperienza personalizzata a qualsiasi utente connesso.

### Collegamento {#link}

Il componente Collegamento consente di creare un collegamento a un modulo in un punto qualsiasi della pagina. Considera uno scenario in cui stai offrendo un programma di formazione e desideri che gli utenti inviino un modulo per registrarsi al corso di formazione. Sul tuo sito web, hai pubblicato i dettagli del programma. Sotto i dettagli, inserire un collegamento al modulo di registrazione. Il componente Collegamento può essere utile per creare il collegamento.

## Flusso di lavoro di Forms Portal {#forms-portal-workflow}

Forms Portal consente di elencare i moduli dal repository dei moduli nella pagina del portale. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di eseguire ricerche nell&#39;elenco dei moduli. È inoltre possibile utilizzare il componente Bozze e invii per visualizzare i moduli salvati come bozza da compilare in un secondo momento e quelli inviati. Prima di rendere disponibili queste funzionalità in una pagina Sites, è necessario eseguire un determinato insieme di operazioni. Per rendere disponibili i componenti e le rispettive funzionalità in una pagina del sito, effettua le operazioni riportate nella sequenza riportata di seguito:

1. **Abilitare i componenti di Forms Portal**: i componenti del portale Forms non sono pronti all’uso. [Abilita i componenti dalla barra laterale AEM](/help/forms/using/enabling-forms-portal-components.md) per una pagina AEM Sites.
1. **Elencare i moduli in una pagina (pagina Crea portale Forms):** Puoi elencare i moduli sia sulle pagine di AEM Sites che su quelle di siti non AEM. L’elenco contiene i moduli disponibili nell’istanza Publish. Un utente può aprire i moduli e iniziare a compilarli. Ogni volta che un utente apre un modulo, viene creata una nuova istanza del modulo:

   1. **Elencare moduli su una pagina AEM Sites**: aggiungi **[Ricerca ed elenco](../../forms/using/creating-form-portal-page.md)** alla pagina e configura il **[Riquadro elenco](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** per elencare i moduli in una pagina. Aggiungere e configurare **Riquadro di ricerca** componente per **Ricerca ed elenco** per aggiungere la funzionalità di ricerca alla pagina. La pagina con il componente Forms Portal è nota come [Pagina portale Forms](../../forms/using/creating-form-portal-page.md).

   1. **Elencare i moduli su una pagina non AEM Sites:** Utilizza il [API di ricerca di Forms Portal](/help/forms/using/listing-forms-webpage-using-apis.md) per eseguire query, recuperare ed elencare moduli su pagine non AEM Sites.

1. **Elencare le bozze e i moduli inviati in una pagina di Forms Portal**: aggiungi e configura il componente Bozze e invii alla pagina del portale Forms. Il componente elenca tutti i moduli in stato di bozza e quelli già inviati.

   Per consentire la visualizzazione di un modulo adattivo inviato nella scheda Invii, imposta **Azione di invio** a **[Azione di invio Forms Portal](configuring-submit-actions.md).** In alternativa, abilitare l&#39;opzione di invio di Forms Portal. Ogni volta che un utente invia il modulo, questo viene aggiunto alla scheda Invii.

1. **Configura l’archiviazione per i dati delle bozze e dei moduli inviati:** Per impostazione predefinita, i dati relativi alle bozze e alle richieste vengono memorizzati nell’archivio dell’AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell’archivio AEM. [Configurare il componente Forms Portal per il salvataggio dei dati in una posizione sicura](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Facoltativo) Personalizzazione dei componenti di Forms Portal:** [Personalizzare i modelli di pagina di Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md) conferire ai componenti un aspetto distintivo.
1. **(Facoltativo) Aggiungi metadati personalizzati ai moduli:** [Aggiungere metadati personalizzati ai moduli](../../forms/using/customizing-templates-forms-portal-components.md) per migliorare l’esperienza di inserimento e ricerca.
1. **Pubblica la pagina del portale Forms:** La pagina del portale Forms è ora pronta. Publish la pagina.

## Articoli correlati {#related-articles}

* [Abilitare i componenti di Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina Crea portale Forms](../../forms/using/creating-form-portal-page.md)
* [Elencare moduli su una pagina web utilizzando API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utilizzare il componente Bozze e invii](../../forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Esempio per integrare il componente Bozze e invii con il database](integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti di Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md)
