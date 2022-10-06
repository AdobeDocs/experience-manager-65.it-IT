---
title: Configurazione dei componenti in modalità Progettazione
seo-title: Configuring Components in Design Mode
description: Quando si installa un’istanza di AEM out-of-the-box, nella barra laterale è immediatamente disponibile una serie di componenti. Oltre a questi, sono disponibili anche vari altri componenti. Puoi usare la modalità Progettazione per attivarli o disattivarli.
seo-description: When AEM instance is installed out-of-the-box, a selection of components are immediately available in the sidekick. In addition to these, various other components are also available. You can use Design mode to Enable/disable such components.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 92%

---

# Configurazione dei componenti in modalità Progettazione{#configuring-components-in-design-mode}

Quando si installa un’istanza di AEM out-of-the-box, nella barra laterale è immediatamente disponibile una serie di componenti.

Oltre a questi, sono disponibili anche vari altri componenti. Puoi usare la modalità Progettazione [per attivarli o disattivarli](#enabledisablecomponentsusingdesignmode). Quando sono attivati e ti trovi su una pagina, puoi usare la modalità Progettazione per [configurare alcuni aspetti dei componenti](#configuringcomponentsusingdesignmode) modificandone i parametri degli attributi.

>[!NOTE]
>
>Quando modifichi tali componenti, presta molta attenzione. Le impostazioni sono spesso una parte integrante della progettazione dell’intero sito Web e dovrebbero essere modificate solo da un utente con la necessaria esperienza e con le relative autorizzazioni, ad esempio un amministratore o sviluppatore. Per ulteriori informazioni, consulta [Sviluppo di componenti](/help/sites-developing/components.md).

Ciò comporta l’aggiunta o la rimozione dei componenti consentiti nel sistema di paragrafi per la pagina. Anche il sistema di paragrafi (`parsys`) stesso è un componente, che contiene gli altri componenti paragrafo. Il sistema di paragrafi consente agli autori di aggiungere a una pagina componenti di tipi diversi e contiene tutti gli altri componenti paragrafo. Ciascun tipo di paragrafo è rappresentato da un componente.

Ad esempio, il contenuto di una pagina prodotto può contenere quanto segue:

* Un’immagine del prodotto (sotto forma di immagine o paragrafo testo e immagine)
* La descrizione del prodotto (come paragrafo testo)
* Una tabella con dati tecnici (come un paragrafo tabella)
* Un modulo che può essere compilato dagli utenti (come paragrafo inizio modulo, elemento modulo e fine modulo)

>[!NOTE]
>
>Per ulteriori informazioni su [](/help/sites-developing/components.md#paragraphsystem), consulta [Sviluppo di componenti](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) e `parsys`Linee guida per l’utilizzo di modelli e componenti.

## Attivare o disattivare componenti {#enable-disable-components}

In modalità Progettazione, la barra laterale viene ridotta a icona ed è possibile configurare i componenti disponibili per l’authoring:

1. Per passare alla modalità Progettazione, apri una pagina da modificare e utilizza l’icona Barra laterale:

   ![](do-not-localize/chlimage_1.png)

1. Fai clic su **Modifica** sul sistema Paragrafo (**Progettazione di par**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Viene aperta una finestra di dialogo in cui sono elencati i gruppi di componenti visualizzati nella barra laterale e i singoli componenti inclusi in questi ultimi.

   In base alle esigenze, seleziona i componenti che desideri aggiungere o rimuovere nella barra laterale.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. Nella modalità Progettazione la barra laterale viene ridotta a icona. Facendo clic sulla freccia è possibile ingrandire la barra laterale e tornare alla modalità di modifica:

   ![](do-not-localize/sidekick-collapsed.png)

## Configurare l’aspetto di un componente {#configuring-the-design-of-a-component}

In modalità Progettazione è inoltre possibile configurare gli attributi di singoli componenti. Ogni componente ha i propri parametri. L’esempio di seguito mostra il componente **Immagine**:

1. Per passare alla modalità Progettazione, apri una pagina da modificare e utilizza l’icona Barra laterale:

   ![](do-not-localize/chlimage_1-1.png)

1. È possibile configurare l’aspetto dei componenti.

   Ad esempio, se fai clic su **Modifica** sul componente Immagine (**Progettazione di immagini**) puoi configurare i parametri specifici del componente:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Fate clic su **OK** per salvare le modifiche.

1. Nella modalità Progettazione la barra laterale viene ridotta a icona. Facendo clic sulla freccia è possibile ingrandire la barra laterale e tornare alla modalità di modifica:

   ![](do-not-localize/sidekick-collapsed-1.png)
