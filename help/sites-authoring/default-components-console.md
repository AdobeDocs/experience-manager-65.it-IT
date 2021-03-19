---
title: Console Componenti
seo-title: Console Componenti
description: Console Componenti
seo-description: 'null'
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 97%

---


# Console Componenti{#components-console}

La console Componenti consente di consultare tutti i componenti definiti nell’istanza e di visualizzare le informazioni chiave di ciascun componente.

È possibile accedervi da **Strumenti ->** **Generale ->** **Componenti**. Nella console sono disponibili le viste a schede e a elenco. Poiché non esiste una struttura ad albero per i componenti, la vista a colonne non è disponibile.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La console dei componenti mostra tutti i componenti del sistema. Il [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser) mostra i componenti disponibili per gli autori e nasconde eventuali gruppi di componenti che iniziano con un punto ( `.`).

## Ricerca {#searching}

L’icona **Solo contenuto** (in alto a sinistra) permette di aprire il pannello **Ricerca** per cercare e/o filtrare i componenti:

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Dettagli dei componenti {#component-details}

Per visualizzare i dettagli relativi a un componente specifico, tocca/fai clic sulla risorsa desiderata. Sono disponibili tre schede:

* **Proprietà**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   Nella scheda Proprietà puoi:

   * Visualizzare le proprietà generali del componente.
   * Visualizzare come è stata definita [l’icona o l’abbreviazione](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) per il componente.

      * Facendo clic sull’origine dell’icona passerai al relativo componente.
   * Visualizzare il **tipo di risorsa** e il **Super Type della risorsa** (se definito) per il componente.

      * Facendo clic su Super Type della risorsa passerai al relativo componente.
   >[!NOTE]
   >
   >Poiché `/apps` non è modificabile in fase di esecuzione, la console Componenti è disponibile in sola lettura.

* **Criteri**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **Utilizzo live**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >A causa della natura delle informazioni raccolte, può essere necessario qualche momento per combinarle e visualizzarle.

* **Documentazione**

   Se lo sviluppatore ha fornito la [documentazione per il componente](/help/sites-developing/developing-components.md#documenting-your-component), questa viene visualizzata nella scheda **Documentazione**. Se la documentazione non è disponibile, la scheda **Documentazione** non verrà visualizzata.

   ![chlimage_1-171](assets/chlimage_1-171.png)

