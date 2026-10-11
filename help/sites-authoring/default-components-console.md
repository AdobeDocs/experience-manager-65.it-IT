---
title: Console Componenti
description: La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza e visualizzare le informazioni chiave di ciascun componente.
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%
---
# Console Componenti{#components-console}

La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza e visualizzare le informazioni chiave di ciascun componente.

È accessibile da **Strumenti >** **Generale >** **Componenti**. Nella console sono disponibili le viste a schede e a elenco. Poiché non esiste una struttura ad albero per i componenti, la vista a colonne non è disponibile.

![schermata_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La console Componenti mostra tutti i componenti del sistema. Il [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser) mostra i componenti disponibili per gli autori e nasconde eventuali gruppi di componenti che iniziano con un punto ( `.`).

## Ricerca {#searching}

L’icona **Solo contenuto** (in alto a sinistra) permette di aprire il pannello **Ricerca** per cercare e/o filtrare i componenti:

![schermata_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Dettagli dei componenti {#component-details}

Per visualizzare i dettagli di un componente specifico, fai clic sulla risorsa richiesta. Tre schede forniscono:

* **Proprietà**

  ![schermata_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  Nella scheda Proprietà puoi:

  * Visualizzare le proprietà generali del componente.
  * Visualizza come è stata definita l&#39;icona o l&#39;abbreviazione [](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) per il componente.

    * Facendo clic sull’origine dell’icona si aprirà quel componente.

  * Visualizzare il **Tipo risorsa** e il **Super Tipo risorsa** (se definito) per il componente.

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

  Se lo sviluppatore ha fornito [documentazione per il componente](/help/sites-developing/developing-components.md#documenting-your-component), questa verrà visualizzata nella scheda **Documentazione**. Se la documentazione non è disponibile, la scheda **Documentazione** non verrà visualizzata.

  ![Documentazione](assets/chlimage_1-171.png)
