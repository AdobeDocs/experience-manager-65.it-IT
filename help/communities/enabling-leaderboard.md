---
title: Funzionalità della classifica
seo-title: Leaderboard Feature
description: Aggiunta di un componente della classifica a una pagina
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# Funzionalità della classifica {#leaderboard-feature}

## Introduzione {#introduction}

La `Leaderboard` Il componente consente di ottenere un&#39;idea di come i membri interagiscono all&#39;interno della comunità, in base ai punti guadagnati (punteggio di base) o alla loro esperienza (punteggio avanzato).

Prima di includere il componente della classifica in una pagina, è necessario configurare [Punteggio e badge delle community](/help/communities/implementing-scoring.md).

Questa sezione della documentazione descrive:

* Aggiunta di `Leaderboard` a un [sito della community](/help/communities/overview.md#community-sites).
* Impostazioni di configurazione per `Leaderboard` componente.

### Aggiunta di una classifica a una pagina {#adding-a-leaderboard-to-a-page}

Per aggiungere una `Leaderboard` in una pagina in modalità di authoring, individua il componente

* `Communities / Leaderboard`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando viene posizionato per la prima volta su una pagina di un sito della community, viene visualizzato questo componente:

![classifica](assets/leaderboard.png)

### Configurazione della classifica {#configuring-leaderboard}

Seleziona il `Leaderboard` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

![configurare la classifica](assets/configure-leaderboard.png)

#### Scheda Impostazioni {#settings-tab}

Sotto la **[!UICONTROL Impostazioni]** , specifica quali informazioni relative al membro vengono visualizzate :

* **Nome visualizzato**

   Un nome descrittivo da visualizzare per la bacheca, che rifletta le regole selezionate per la visualizzazione di badge e punteggi.
Il valore predefinito è `Leaderboard`, se non è stato inserito nulla.

* **Badge**

   Se questa opzione è selezionata, nella classifica è inclusa una colonna per le icone del badge.
Il valore predefinito è deselezionato.

* **Nome badge**

   Se questa opzione è selezionata, nella classifica è inclusa una colonna relativa al nome del badge.
Il valore predefinito è deselezionato.

* **Usa avatar**

   Se questa opzione è selezionata, l&#39;immagine avatar del membro viene inclusa nella classifica, accanto al collegamento del nome al profilo membro.
Il valore predefinito è deselezionato.

#### Scheda Regole {#rules-tab}

Sotto la **Regole** scheda , il sito community e le relative regole di valutazione e contrassegno

* **Percorso regola**

   (Obbligatorio) Posizione in cui è configurata la regola Punteggio/Badging .

* **Regola punteggio**

   (Obbligatorio) Regola specifica che genera i punteggi da visualizzare.

* **Regola assegnazione badge**

   (Obbligatorio) Regola specifica che genera il badge da visualizzare.

* **Limite di visualizzazione**

   Numero di membri da visualizzare per pagina. Il valore predefinito è 10.

### Esempio: Leader dei partecipanti {#example-participants-leaderboard}

Questo rapporto della classifica deriva dall’applicazione di regole di punteggio di base.

Configurazione del componente della classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Participation Board`
   * `checked`:

      * Badge
      * Nome badge
      * Usa avatar

* Scheda Regole :

   * Percorso regola = `/content/sites/<site name>/jcr:content`
   * Regola punteggio = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regola assegnazione badge = `/libs/settings/community/badging/rules//reference-badging`
   * Limite di visualizzazione = `10`

![consiglio dei partecipanti](assets/participants-leaderboard.png)

### Esempio: Leaderboard di esperti {#example-experts-leaderboard}

Questo rapporto della classifica deriva dall’applicazione di regole di punteggio avanzate.

Configurazione del componente della classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Expertise Board`
   * `checked`:

      * Badge
      * Usa avatar

* Scheda Regole :

   * Percorso regola = `/content/sites/<site name>/jcr:content`
   * Regola punteggio = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regola assegnazione badge = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite di visualizzazione = `10`

![classifica degli esperti](assets/experts-leaderboard.png)

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sulla classifica](/help/communities/leaderboard.md) per sviluppatori.

Le istruzioni per la creazione delle regole sono fornite nella sezione [Punteggio e badge delle community](/help/communities/implementing-scoring.md) per amministratori.
