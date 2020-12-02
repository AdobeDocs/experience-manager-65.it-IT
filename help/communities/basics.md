---
title: Nozioni di base sui componenti per community
seo-title: Nozioni di base sui componenti per community
description: Aggiunta di funzioni di Communities ai siti AEM in modalità di modifica e configurazione dei componenti
seo-description: Aggiunta di funzioni di Communities ai siti AEM in modalità di modifica e configurazione dei componenti
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# Nozioni di base sui componenti community {#communities-components-basics}

## Panoramica {#overview}

La sezione relativa all’authoring della documentazione descrive l’aggiunta delle funzioni di Communities ai siti AEM in modalità di modifica dell’autore, nonché la descrizione delle configurazioni dei componenti.

I componenti possono essere esplorati utilizzando un&#39;istanza AEM e la guida [Community Components Guide](components-guide.md) interattiva.

## Accesso ai componenti di Communities {#accessing-communities-components}

Durante la creazione di contenuti di pagina, se il modello sottostante consente di apportare modifiche alla progettazione della pagina, è possibile abilitare componenti che non sono già disponibili nel browser Componenti come parte della struttura del sito.

I componenti Community disponibili sono elencati [qui](author-communities.md#available-communities-components).

>[!NOTE]
>
>Per informazioni generali sull&#39;authoring, consultare la [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).
>
>Se non hai familiarità con AEM, consulta la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md).

### Accesso alla modalità Progettazione {#entering-design-mode}

Se un componente **Communities** non viene trovato nel browser Componenti (barra laterale), sarà necessario inserire `Design Mode` per aggiungere altri componenti Community. [Potrebbe essere necessario aggiungere anche librerie](#required-clientlibs)  lato client (clientlibs) obbligatorie.

Per informazioni dettagliate, vedere [Configurazione dei componenti in modalità Progettazione](../../help/sites-authoring/default-components-designmode.md).

Di seguito sono riportate le immagini che mostrano come selezionare alcuni componenti Community e visualizzarli nel browser Componenti:

![progettazione di componenti](assets/component-design.png)

I componenti selezionati sono ora disponibili nel browser Componenti:

![component-design1](assets/component-design1.png)

## Clientlibs richiesti {#required-clientlibs}

[Le librerie](../../help/sites-developing/clientlibs.md)  lato client (clientlibs) sono necessarie per il corretto funzionamento (JavaScript) e lo stile (CSS) di un componente.

Quando si aggiunge un componente Community a una pagina, se il risultato è un errore o un aspetto imprevisto, la prima cosa da provare è aggiungere i clientlibs richiesti per il componente Community. Per informazioni dettagliate, vedere [Clientlibs for Communities Components](clientlibs.md).

### Esempio: Recensioni posizionate inizialmente senza librerie client... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... E con le librerie client {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Assegnazione tag {#tagging}

Molte funzioni di Communities possono essere configurate per consentire ai membri di assegnare tag ai contenuti immessi (pubblicati) nell&#39;ambiente di pubblicazione.

Se l&#39;assegnazione di tag è consentita, la configurazione del sito community può essere impostata in modo da limitare gli spazi dei nomi presentati ai membri nell&#39;ambiente di pubblicazione. Vedere la [console Siti community](sites-console.md#tagging).

Funzioni che consentono l’aggiunta di tag: [blog](blog-feature.md), [calendario](calendar.md), [libreria di file](file-library.md), [forum](forum.md)

Funzioni che utilizzano i tag: [catalog](catalog.md), [search](search.md), [social tag cloud](tagcloud.md)

Per informazioni sull’authoring:

* [Utilizzo dei tag](../../help/sites-authoring/tags.md)

Per informazioni amministrative:

* Creazione di spazi dei nomi dei tag (tassonomia): [Amministrazione dei tag](../../help/sites-administering/tags.md)
* Configurazione sito community: vedere [TAG](sites-console.md#tagging)
* [Assegnazione di tag ai contenuti generati dall&#39;utente](../../help/sites-authoring/tags.md)
* [Assegnazione tag alle risorse di abilitazione](tag-resources.md)

Per informazioni sullo sviluppatore:

* [AEM Tagging Framework](../../help/sites-developing/framework.md)
* [Assegnazione di tag Essentials](tag.md)

