---
title: Funzionalità della classifica
seo-title: Funzionalità della classifica
description: Aggiunta di un componente della classifica a una pagina
seo-description: Aggiunta di un componente della classifica a una pagina
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funzionalità della classifica{#leaderboard-feature}

## Introduzione {#introduction}

Il `Leaderboard` componente fornisce la capacità di ottenere un&#39;idea di come i membri interagiscono all&#39;interno della comunità, in base ai punti guadagnati (punteggio di base) o alla loro esperienza (punteggio avanzato).

Prima di includere il componente della classifica in una pagina, è necessario configurare [Communities Scoring and Badges](/help/communities/implementing-scoring.md).

Questa sezione della documentazione descrive

* aggiunta del `Leaderboard` componente a un sito [community](/help/communities/overview.md#community-sites)
* impostazioni di configurazione per il `Leaderboard` componente

### Adding a Leaderboard to a Page {#adding-a-leaderboard-to-a-page}

Per aggiungere un `Leaderboard` componente a una pagina in modalità di creazione, individuare il componente

* `Communities / Leaderboard`

e trascinarlo nella posizione desiderata su una pagina.

Per le informazioni necessarie, visita [Community Components Basics](/help/communities/basics.md).

La prima volta che il componente viene inserito in una pagina di un sito community, viene visualizzato così:

![chlimage_1-19](assets/chlimage_1-19.png)

### Configurazione della classifica {#configuring-leaderboard}

Selezionate il `Leaderboard` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-20](assets/chlimage_1-20.png) ![chlimage_1-21](assets/chlimage_1-21.png)

#### scheda Impostazioni {#settings-tab}

Nella scheda **Settings **(Impostazioni), specificare quali informazioni relative al membro vengono visualizzate:

* **Nome visualizzato**

   Un nome descrittivo da visualizzare per la bacheca, che riflette le regole selezionate per la visualizzazione di simboli e punteggi.
Il valore predefinito è `Leaderboard`, se non è stato immesso nulla.

* **Badge**

   Se questa opzione è selezionata, nella classifica è inclusa una colonna per le icone dei simboli.
Il valore predefinito è deselezionato.

* **Nome badge**

   Se questa opzione è selezionata, nella classifica viene inclusa una colonna per il nome del contrassegno.
Il valore predefinito è deselezionato.

* **Usa avatar**

   Se questa opzione è attivata, l&#39;immagine avatar del membro viene inclusa nella classifica, accanto al collegamento del suo nome al profilo del membro.
Il valore predefinito è deselezionato.

#### Scheda Regole {#rules-tab}

Nella scheda **Regole** , il sito della community e le relative regole di valutazione e contrassegno

* **Percorso regola**

   (obbligatorio) Posizione in cui è configurata la regola Punteggio/Badging.

* **Regola punteggio**

   (obbligatorio) Regola specifica che genera i punteggi da visualizzare.

* **Regola assegnazione badge**

   (obbligatorio) Regola specifica che genera il contrassegno da visualizzare.

* **Limite di visualizzazione**

   Numero di membri da visualizzare per pagina.

   Il valore predefinito è 10.

### Esempio: Guida dei partecipanti {#example-participants-leaderboard}

Questo rapporto della classifica deriva dall&#39;applicazione di regole di punteggio di base.

Configurazione del componente della classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Participation Board`
   * `checked`:

      * Badge
      * Nome badge
      * Usa avatar

* Scheda Regole:

   * Percorso regola = `/content/sites/communities/jcr:content`
   * Regola punteggio = `/etc/community/scoring/rules/forums-scoring`
   * Regola assegnazione badge = `/etc/community/badging/rules/reference-badging`
   * Limite di visualizzazione = `10`

![chlimage_1-22](assets/chlimage_1-22.png)

### Esempio: Leaderboard di esperti {#example-experts-leaderboard}

Questo rapporto della classifica deriva dall&#39;applicazione di regole di punteggio avanzate.

Configurazione del componente della classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Expertise Board`
   * `checked`:

      * Badge
      * Usa avatar

* Scheda Regole:

   * Percorso regola = `/content/sites/communities/jcr:content`
   * Regola punteggio = `/etc/community/scoring/rules/adv-forums-scoring`
   * Regola assegnazione badge = `/etc/community/badging/rules/adv-forums-badging`
   * Limite di visualizzazione = `10`

![chlimage_1-23](assets/chlimage_1-23.png)

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Leaderboard Essentials](/help/communities/leaderboard.md) per gli sviluppatori.

Le istruzioni per la creazione di regole sono fornite nella pagina [Communities Scoring and Badges](/help/communities/implementing-scoring.md) (Punteggio e Badgecommunity) per gli amministratori.
