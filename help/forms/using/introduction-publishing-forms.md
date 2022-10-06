---
title: Introduzione alla pubblicazione di moduli su un portale
seo-title: Introduction to publishing forms on a portal
description: AEM Forms fornisce i componenti che è possibile utilizzare per creare il portale dei moduli. Questi articoli ti introducono ai componenti del portale dei moduli disponibili.
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# Introduzione alla pubblicazione di moduli su un portale{#introduction-to-publishing-forms-on-a-portal}

## Panoramica dei componenti del portale AEM Forms {#aem-forms-portal-components-overview}

In uno scenario di distribuzione tipico del portale incentrato sui moduli, lo sviluppo dei moduli e lo sviluppo del portale sono due attività discongiunte. Mentre i progettisti di moduli progettano e memorizzano i moduli in un archivio, gli sviluppatori web creano un’applicazione Web per elencare i moduli e gestire l’invio dei moduli. Forms viene copiato sul livello web in quanto non vi è comunicazione tra l’archivio dei moduli e l’applicazione web.

Tali scenari si traducono spesso in problemi di gestione e ritardi nella produzione. Ad esempio, se nella directory archivio è disponibile una versione più recente del modulo, è necessario sostituire il modulo sul livello Web, modificare l’applicazione Web e ridistribuire il modulo sul sito pubblico. La ridistribuzione dell&#39;applicazione Web potrebbe causare tempi di inattività del server. In genere, i tempi di inattività del server sono un’attività pianificata e pertanto le modifiche non possono essere inviate istantaneamente al sito pubblico.

AEM Forms fornisce componenti del portale che riducono i costi generali di gestione e i ritardi di produzione. I componenti consentono agli sviluppatori web di creare e personalizzare un portale moduli sui siti web creati con Adobe Experience Manager (AEM).

![Portale AEM Forms](assets/aem-forms-portal.png)

I componenti del portale dei moduli consentono di aggiungere le funzionalità seguenti:

* Elencare moduli in layout personalizzati. Sono disponibili i layout predefiniti per le viste a elenco, a schede e per le viste a pannello. Puoi creare layout personalizzati.
* Consente di visualizzare metadati personalizzati e azioni personalizzate durante l’elenco.
* Elenca i moduli pubblicati dall’interfaccia utente di AEM Forms nell’istanza di pubblicazione in cui vengono utilizzati i componenti di Forms Portal.
* Consentire agli utenti finali di eseguire il rendering dei moduli in HTML e in formato PDF.
* Utilizzare il profilo HTML personalizzato per eseguire il rendering dei moduli.
* Abilita la ricerca di moduli in base a vari criteri, ad esempio proprietà del modulo, metadati e tag.
* Invia i dati del modulo a un servlet.
* Utilizza CSS personalizzati per personalizzare l’aspetto del portale.
* Creare collegamenti ai moduli.
* Elenca le bozze e gli invii relativi al modulo adattivo creato dall’utente finale.

## Componenti del portale AEM Forms disponibili {#available-aem-forms-portal-components}

AEM Forms fornisce i seguenti componenti portale pronti all’uso, raggruppati in **Servizi basati su documenti** e **Predicati di Document Services** gruppi di componenti:

### Ricerca ed elenco {#search-amp-lister}

Il componente Ricerca e filtro consente di elencare i moduli dall’archivio moduli nella pagina del portale e fornisce opzioni di configurazione per elencare i moduli in base a criteri specifici. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di eseguire ricerche nell’elenco dei moduli.

### Bozze e invii {#drafts-amp-submissions}

Mentre il componente Ricerca e filtro visualizza i moduli resi pubblici dall’autore di Forms, il componente Bozze e invii visualizza i moduli salvati come bozze per essere completati in seguito e inviati. Questo componente offre un’esperienza personalizzata a qualsiasi utente connesso.

### Collegamento {#link}

Il componente Collegamento consente di creare un collegamento a un modulo in qualsiasi punto della pagina. Considera uno scenario in cui stai offrendo un programma di formazione e vuoi che gli utenti inviino un modulo per registrarti al corso. Sul tuo sito web hai pubblicato i dettagli del programma. Sotto i dettagli, si desidera fornire un link al modulo di registrazione. Il componente Collegamento può essere utile per creare il collegamento.

## Flusso di lavoro di Forms Portal {#forms-portal-workflow}

Il portale Forms consente di elencare i moduli dall’archivio moduli nella pagina del portale. Consente inoltre di specificare i criteri di ricerca per consentire agli utenti del portale di eseguire ricerche nell’elenco dei moduli. È inoltre possibile utilizzare il componente Bozze e invii per visualizzare i moduli salvati come bozze per completare in seguito i moduli e inviarli. È necessario eseguire un certo set di operazioni prima che queste funzionalità siano disponibili in una pagina Sites. Esegui i passaggi della sequenza elencata per rendere disponibili i componenti e le rispettive funzionalità in una pagina dei siti:

1. **Abilitare i componenti di Forms Portal**: I componenti del portale dei moduli non sono disponibili per l’uso. [Abilitare i componenti dalla barra laterale AEM](/help/forms/using/enabling-forms-portal-components.md) per una pagina AEM Sites.
1. **Elencare moduli in una pagina (pagina del portale dei moduli):** È possibile elencare i moduli sia su pagine di AEM Sites che su pagine di siti non AEM. L’elenco contiene i moduli disponibili nell’istanza di pubblicazione. Un utente può aprire i moduli e iniziare a compilarli. Ogni volta che un utente apre un modulo, viene creata una nuova istanza del modulo:

   1. **Elencare moduli in una pagina AEM Sites**: Aggiungi il **[Ricerca e filtro](../../forms/using/creating-form-portal-page.md)** alla pagina e configura il **[Riquadro elenco](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** per elencare i moduli su una pagina. Aggiungi e configura le **Riquadro di ricerca** nella **Ricerca e filtro** per aggiungere alla pagina anche funzionalità di ricerca. La pagina con il componente portale moduli è nota come [pagina del portale moduli](../../forms/using/creating-form-portal-page.md).

   1. **Elencare moduli in una pagina non AEM Sites:** Utilizza la [API di ricerca nel portale dei moduli](/help/forms/using/listing-forms-webpage-using-apis.md) per eseguire query, recuperare ed elencare i moduli su pagine non AEM Sites.

1. **Elenco dei moduli bozza e inviati in una pagina del portale moduli**: Aggiungi e configura il componente Bozze e invii nella pagina del portale dei moduli. Il componente elenca tutti i moduli in stato di bozza e i moduli già inviati.

   Per abilitare la visualizzazione di un modulo adattivo inviato nella scheda Invia, impostare **Invia azione** a **[Azione di invio Forms Portal](configuring-submit-actions.md).** In alternativa, abilita l’opzione Invia di Forms Portal. Ogni volta che un utente invia il modulo, questo viene aggiunto alla scheda Invii.

1. **Configura l’archiviazione per la bozza e i dati dei moduli inviati:** Per impostazione predefinita, i dati di bozza e di invio vengono memorizzati nell’archivio AEM. In un ambiente di produzione, si consiglia di non archiviare le bozze o i dati del modulo inviati in AEM archivio. [Configurare il componente del portale moduli per il salvataggio dei dati in una posizione protetta](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Facoltativo) Personalizzazione dei componenti del portale dei moduli:** [Personalizzare i modelli di pagina del portale moduli](../../forms/using/customizing-templates-forms-portal-components.md) fornire un aspetto distintivo ai componenti.
1. **(Facoltativo) Aggiungi metadati personalizzati ai moduli:** [Aggiungere metadati personalizzati ai moduli](../../forms/using/customizing-templates-forms-portal-components.md) per migliorare l’esperienza di inserimento e ricerca nell’elenco.
1. **Pubblicare la pagina del portale dei moduli:** La pagina del portale dei moduli è ora pronta. Pubblica la pagina.

## Articoli correlati {#related-articles}

* [Abilitare i componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* [Pagina del portale dei moduli](../../forms/using/creating-form-portal-page.md)
* [Elencare moduli in una pagina web utilizzando le API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usa componente Bozze e invii](../../forms/using/draft-submission-component.md)
* [Personalizzare l’archiviazione delle bozze e dei moduli inviati](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Esempio per l&#39;integrazione del componente bozze e invii con il database](integrate-draft-submission-database.md)
* [Personalizzazione dei modelli per i componenti del portale dei moduli](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introduzione alla pubblicazione di moduli su un portale](../../forms/using/introduction-publishing-forms.md)
