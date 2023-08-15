---
title: Console Componenti
seo-title: Components Console
description: Console Componenti
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 55%

---

# Console Componenti{#components-console}

La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza e visualizzare le informazioni chiave di ciascun componente.

È possibile accedervi da **Strumenti ->** **Generale ->** **Componenti**. Nella console sono disponibili le viste a schede e a elenco. Poiché non esiste una struttura ad albero per i componenti, la vista a colonne non è disponibile.

![schermata_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La console Componenti mostra tutti i componenti del sistema. Il [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser) mostra i componenti disponibili per gli autori e nasconde eventuali gruppi di componenti che iniziano con un punto ( `.`).

## Ricerca {#searching}

L’icona **Solo contenuto** (in alto a sinistra) permette di aprire il pannello **Ricerca** per cercare e/o filtrare i componenti:

![schermata_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Dettagli dei componenti {#component-details}

Per visualizzare i dettagli di un componente specifico, tocca o fai clic sulla risorsa richiesta. Tre schede forniscono:

* **Proprietà**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  Nella scheda Proprietà puoi:

   * Visualizzare le proprietà generali del componente.
   * Visualizza come [è stata definita un&#39;icona o un&#39;abbreviazione](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) per il componente.

      * Facendo clic sull’origine dell’icona si aprirà quel componente.

   * Visualizza **Tipo di risorsa** e **Super Type risorsa** (se definito) per il componente.

      * Facendo clic sul Super Type della risorsa si aprirà quel componente.

  >[!NOTE]
  >
  >Poiché `/apps` non è modificabile in fase di esecuzione, la console Componenti è disponibile in sola lettura.

* **Criteri**

  ![Criteri](assets/chlimage_1-169.png)

* **Utilizzo live**

  ![Utilizzo live](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >A causa della natura delle informazioni raccolte, può essere necessario qualche momento per combinarle e visualizzarle.

* **Documentazione**

  Se lo sviluppatore ha fornito [documentazione del componente](/help/sites-developing/developing-components.md#documenting-your-component), apparirà sulla **Documentazione** scheda. Se la documentazione non è disponibile, la scheda **Documentazione** non verrà visualizzata.

  ![Documentazione](assets/chlimage_1-171.png)
