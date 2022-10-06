---
title: Funzionalità di contenuto
seo-title: Featured Content Feature
description: La funzione Contenuto in primo piano consente ai visitatori del sito che hanno effettuato l’accesso di evidenziare i contenuti
seo-description: The Featured Content feature lets signed-in site visitors highlight content
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 5%

---

# Funzionalità di contenuto {#featured-content-feature}

## Introduzione {#introduction}

La funzione di contenuto in primo piano fornisce un’area per i visitatori del sito che hanno effettuato l’accesso (membri della community) nell’ambiente di pubblicazione per evidenziare i contenuti relativi a:

* [Blog](blog-feature.md)
* [Calendari](calendar.md)
* [Forum](forum.md)
* [Idee](ideation-feature.md)
* [D/R](working-with-qna.md)

Una volta che il contenuto viene contrassegnato come in primo piano, viene elencato all’interno di questo componente, che può essere posizionato in pagine di destinazione o aree specifiche che catturano facilmente l’attenzione dei membri della community.

La possibilità di includere contenuti può essere consentita o disabilitata per ciascun componente.

Questa sezione della documentazione descrive:

* Aggiunta di contenuti in primo piano a un sito della community.
* Impostazioni di configurazione per `Featured Content` componente.

## Aggiunta di contenuto in primo piano a una pagina {#adding-featured-content-to-a-page}

Per aggiungere una `Featured Content` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Featured Content`

e trascinarlo nella posizione desiderata su una pagina in cui dovrebbe essere visualizzato il contenuto in primo piano.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](essentials-featured.md#essentials-for-client-side) sono inclusi, è così che `Featured Content` apparirà il componente:

![featuredcontent](assets/featuredcontent.png)

## Configurazione del contenuto in primo piano {#configuring-featured-content}

Seleziona il `Featured Content` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Scheda Impostazioni {#settings-tab}

Sotto la **[!UICONTROL Impostazioni]** , identifica il contenuto da feature:

* **[!UICONTROL Nome visualizzato]**

   Titolo dell’elenco dei contenuti in primo piano. Esempio `Featured Questions` o `Featured Ideas`. Il valore predefinito è `Featured Content` se lasciato vuoto.

* **[!UICONTROL Posizione del contenuto in primo piano]**

   *(Obbligatorio)* Passa alla pagina contenente il contenuto che può essere una funzione (i componenti di quella pagina devono essere configurati per consentire il contenuto in primo piano). Esempio: `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite di visualizzazione]**

   Il numero massimo di contenuti in primo piano da visualizzare. Il valore predefinito è 5.

## Esperienza dei visitatori del sito {#site-visitor-experience}

La possibilità di contrassegnare il contenuto come contenuto in primo piano richiede privilegi di moderatore.

Quando un moderatore visualizza il contenuto pubblicato, ha accesso ai flag di moderazione nel contesto, che includono il nuovo `Feature` bandiera.

![site-visitor-experience](assets/site-visitor-experience.png)

Una volta contrassegnato come feature, il flag di moderazione diventa `Unfeature`.

La pagina contenente `Featured Content` ora includerà questo post.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` è un collegamento al post effettivo.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Contenuto in primo piano](essentials-featured.md) per sviluppatori.

Per contrassegnare il contenuto come in primo piano, consulta [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).
