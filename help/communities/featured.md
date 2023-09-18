---
title: Funzione Contenuto in primo piano
description: La funzione Contenuto in primo piano consente ai visitatori del sito che hanno effettuato l’accesso di evidenziare il contenuto
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# Funzione Contenuto in primo piano {#featured-content-feature}

## Introduzione {#introduction}

La funzione di contenuto in primo piano fornisce un’area per i visitatori del sito connessi (membri della community) nell’ambiente di pubblicazione per evidenziare i contenuti per:

* [Blog](blog-feature.md)
* [Calendari](calendar.md)
* [Forum](forum.md)
* [Idee](ideation-feature.md)
* [D/R](working-with-qna.md)

Una volta contrassegnato come in primo piano, il contenuto viene elencato all’interno di questo componente, che può essere inserito in pagine di destinazione o aree specifiche che catturano facilmente l’attenzione dei membri della community.

La possibilità di includere contenuto può essere consentita o negata per ogni componente.

Questa sezione della documentazione descrive:

* Aggiunta di contenuto in primo piano a un sito community.
* Impostazioni di configurazione per `Featured Content` componente.

## Aggiunta di contenuto in primo piano a una pagina {#adding-featured-content-to-a-page}

Per aggiungere una `Featured Content` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Featured Content`

Trascinalo in una pagina in cui dovrebbe apparire il contenuto in primo piano.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](essentials-featured.md#essentials-for-client-side) sono inclusi, è così che `Featured Content` viene visualizzato il componente:

![feature dcontent](assets/featuredcontent.png)

## Configurazione del contenuto in primo piano {#configuring-featured-content}

Seleziona la inserita `Featured Content` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Scheda Impostazioni {#settings-tab}

Sotto **[!UICONTROL Impostazioni]** , identifica il contenuto da visualizzare:

* **[!UICONTROL Nome visualizzato]**

  Titolo dell’elenco dei contenuti in primo piano. Ad esempio: `Featured Questions` o `Featured Ideas`. Il valore predefinito è `Featured Content` se lasciato vuoto.

* **[!UICONTROL Posizione del contenuto in primo piano]**

  *(Obbligatorio)* Passa alla pagina contenente il contenuto che potrebbe essere visualizzato (i componenti di quella pagina devono essere configurati per Consenti contenuto in primo piano). Esempio: `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite di visualizzazione]**

  Il numero massimo di contenuti in primo piano da visualizzare. Il valore predefinito è 5.

## Esperienza visitatore del sito {#site-visitor-experience}

La possibilità di contrassegnare il contenuto come contenuto in primo piano richiede privilegi di moderatore.

Quando un moderatore visualizza il contenuto pubblicato, ha accesso ai flag di moderazione nel contesto, che includono il nuovo `Feature` flag.

![site-visitor-experience](assets/site-visitor-experience.png)

Dopo essere stato contrassegnato come caratteristica, il contrassegno di moderazione diventa `Unfeature`.

La pagina contenente `Featured Content` componente, ora include questo post.

![site-visitor-experience1](assets/site-visitor-experience1.png)

Il `Read More` collegamenti al post effettivo.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Contenuto in primo piano](essentials-featured.md) pagina per sviluppatori.

Per segnalare il contenuto come in primo piano, consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).
