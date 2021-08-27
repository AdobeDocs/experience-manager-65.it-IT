---
title: Frammenti di contenuto - Browser di configurazione
description: Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.
feature: Content Fragments
role: User
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 18%

---

# Frammenti di contenuto - Browser di configurazione{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare Frammenti di contenuto è necessario utilizzare il **Browser configurazioni** per abilitare:

* **Modelli per frammenti di contenuto**  - obbligatori
* **Query persistenti GraphQL**  - facoltativo

>[!CAUTION]
>
>Se non abiliti **Modelli di frammento di contenuto**:
>
>* l’opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.
>* non potrai [selezionare la configurazione Sites per creare il relativo punto finale](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilita l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser di configurazione
* Applica la configurazione alla cartella Assets

### Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model) **è necessario** prima abilitarle tramite il **Browser di configurazione**:

>[!NOTE]
>
>Per ulteriori dettagli, consulta anche [Browser di configurazione:](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Le sottoconfigurazioni (una configurazione nidificata all’interno di una configurazione) non sono supportate per l’uso con Frammenti di contenuto.

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo in cui:

   1. Specifica un **titolo**.
   1. Per attivarne l&#39;uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cfm-conf-01.png)


1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **global** è abilitata per la funzionalità di frammento di contenuto, si applica a qualsiasi cartella Assets.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
