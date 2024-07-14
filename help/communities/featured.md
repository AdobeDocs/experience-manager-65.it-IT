---
title: Funzione Contenuto in primo piano
description: La funzione Contenuto in primo piano consente ai visitatori del sito che hanno effettuato l’accesso di evidenziare il contenuto
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

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
* Impostazioni di configurazione per il componente `Featured Content`.

## Aggiunta di contenuto in primo piano a una pagina {#adding-featured-content-to-a-page}

Per aggiungere un componente `Featured Content` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Featured Content`

Trascinalo in una pagina in cui dovrebbe apparire il contenuto in primo piano.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](essentials-featured.md#essentials-for-client-side), il componente `Featured Content` viene visualizzato in questo modo:

![contenuto funzionalità](assets/featuredcontent.png)

## Configurazione del contenuto in primo piano {#configuring-featured-content}

Selezionare il componente `Featured Content` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura-nuovo](assets/configure-new.png)

![contenutofunzionalità1](assets/featuredcontent1.png)

### Scheda Impostazioni {#settings-tab}

Nella scheda **[!UICONTROL Impostazioni]**, identifica il contenuto da visualizzare:

* **[!UICONTROL Nome visualizzato]**

  Titolo dell’elenco dei contenuti in primo piano. Ad esempio, `Featured Questions` o `Featured Ideas`. Il valore predefinito è `Featured Content` se lasciato vuoto.

* **[!UICONTROL Posizione del contenuto in primo piano]**

  *(Obbligatorio)* Passa alla pagina contenente il contenuto che potrebbe essere visualizzato (i componenti della pagina devono essere configurati per Consentire contenuto in primo piano). Esempio: `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite di visualizzazione]**

  Il numero massimo di contenuti in primo piano da visualizzare. Il valore predefinito è 5.

## Esperienza visitatore del sito {#site-visitor-experience}

La possibilità di contrassegnare il contenuto come contenuto in primo piano richiede privilegi di moderatore.

Quando un moderatore visualizza il contenuto pubblicato, ha accesso ai flag di moderazione nel contesto, che includono il nuovo flag `Feature`.

![esperienza-visitatore-sito](assets/site-visitor-experience.png)

Dopo essere stato contrassegnato come funzionalità, il flag di moderazione diventa `Unfeature`.

La pagina contenente il componente `Featured Content`, ora include questo post.

![esperienza-visitatore-sito1](assets/site-visitor-experience1.png)

`Read More` si collega al post effettivo.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Contenuto in primo piano](essentials-featured.md) per gli sviluppatori.

Per contrassegnare il contenuto come in primo piano, vedere [Moderazione del contenuto generato dall&#39;utente](moderate-ugc.md).
