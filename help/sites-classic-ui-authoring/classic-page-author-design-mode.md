---
title: Configurazione dei componenti in modalità Progettazione
description: Quando l’istanza AEM è installata come preconfigurata, nella barra laterale è immediatamente disponibile una selezione di componenti. Oltre a questi, sono disponibili vari altri componenti. È possibile utilizzare la modalità Progettazione per abilitare/disabilitare tali componenti.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Configurazione dei componenti in modalità Progettazione{#configuring-components-in-design-mode}

Quando l’istanza AEM è installata come preconfigurata, nella barra laterale è immediatamente disponibile una selezione di componenti.

Oltre a questi, sono disponibili vari altri componenti. È possibile utilizzare la modalità Progettazione per [Attiva/disattiva tali componenti](#enabledisablecomponentsusingdesignmode). Se questa opzione è abilitata e si trova sulla pagina, è possibile utilizzare la modalità Progettazione per [configurare gli aspetti della progettazione del componente](#configuringcomponentsusingdesignmode) modificando i parametri degli attributi.

>[!NOTE]
>
>Presta attenzione quando modifichi questi componenti. Le impostazioni di progettazione sono spesso parte integrante della progettazione dell’intero sito web, pertanto devono essere modificate solo da utenti con i privilegi (e l’esperienza) appropriati, spesso amministratori o sviluppatori. Consulta [Sviluppo di componenti](/help/sites-developing/components.md) per ulteriori informazioni.

Ciò comporta effettivamente l’aggiunta o la rimozione dei componenti consentiti nel sistema paragrafo per la pagina. Il sistema paragrafo ( `parsys`) è un componente composto che contiene tutti gli altri componenti paragrafo. Il sistema paragrafo consente agli autori di aggiungere a una pagina componenti di tipi diversi, in quanto contiene tutti gli altri componenti paragrafo. Ogni tipo di paragrafo è rappresentato come componente.

Ad esempio, il contenuto di una pagina di prodotto può contenere un sistema paragrafo con i seguenti elementi:

* Immagine del prodotto (sotto forma di immagine o paragrafo textimage)
* Descrizione del prodotto (come paragrafo di testo)
* Tabella con dati tecnici (come paragrafo di tabella)
* Compilazione di un modulo da parte degli utenti (come inizio del modulo, elemento del modulo e paragrafo finale del modulo)

>[!NOTE]
>
>Consulta [Sviluppo di componenti](/help/sites-developing/components.md#paragraphsystem) e [Linee guida per l’utilizzo di modelli e componenti](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) per ulteriori informazioni su `parsys`.

## Abilita/Disabilita componenti {#enable-disable-components}

In modalità Progettazione, la barra laterale viene ridotta a icona e puoi configurare i componenti accessibili per l’authoring:

1. Per accedere alla modalità Progettazione, apri una pagina per la modifica e utilizza l’icona della barra laterale:

   ![](do-not-localize/chlimage_1.png)

1. Clic **Modifica** sul sistema Paragrafo (**Disegno della parte**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Viene aperta una finestra di dialogo in cui sono elencati i gruppi di componenti visualizzati nella barra laterale e i singoli componenti in essi contenuti.

   Seleziona questa opzione per aggiungere o rimuovere i componenti da rendere disponibili nella barra laterale.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. La barra laterale consente di ridurre al minimo le dimensioni in modalità Progettazione. Facendo clic sulla freccia potete ingrandire la barra laterale e tornare alla modalità di modifica:

   ![](do-not-localize/sidekick-collapsed.png)

## Configurazione della progettazione di un componente {#configuring-the-design-of-a-component}

In modalità Progettazione è inoltre possibile configurare gli attributi per i singoli componenti. Ogni componente ha i propri parametri, l’esempio seguente mostra **Immagine** componente:

1. Per accedere alla modalità Progettazione, apri una pagina per la modifica e utilizza l’icona della barra laterale:

   ![](do-not-localize/chlimage_1-1.png)

1. Puoi configurare la progettazione dei componenti.

   Ad esempio, se fai clic su **Modifica** sul componente Immagine (**Progettazione dell&#39;immagine**) puoi configurare i parametri specifici del componente:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Clic **OK** per salvare le modifiche.

1. La barra laterale consente di ridurre al minimo le dimensioni in modalità Progettazione. Facendo clic sulla freccia potete ingrandire la barra laterale e tornare alla modalità di modifica:

   ![](do-not-localize/sidekick-collapsed-1.png)
