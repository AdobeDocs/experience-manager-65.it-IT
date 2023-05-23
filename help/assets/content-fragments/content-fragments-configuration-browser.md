---
title: Frammenti di contenuto - Browser configurazioni
description: Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per sfruttare le potenti funzionalità di distribuzione headless dell’AEM.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 78%

---

# Frammenti di contenuto - Browser configurazioni{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per sfruttare le potenti funzionalità di distribuzione headless dell’AEM.

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, è necessario utilizzare la funzione **Browser di configurazione** per abilitare:

* **Modelli per frammenti di contenuto**: obbligatorio
* **Query GraphQL persistenti**: facoltativo

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* l’opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.
>* non potrai [selezionare la configurazione Sites per creare il relativo endpoint](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).


Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilitare l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser configurazioni
* Applicare la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model) **devi** per prima cosa attivarle tramite il **browser configurazioni**:

>[!NOTE]
>
>Per maggiori dettagli vedi anche [Browser configurazioni:](/help/sites-administering/configurations.md#using-configuration-browser).

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo, in cui:

   1. Specificare un **Titolo**.
   1. Per attivarne l’uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query GraphQL persistenti**

      ![Definire la configurazione](assets/cfm-conf-01.png)


1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella Risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **globale** è abilitato per la funzionalità frammento di contenuto, quindi si applica a qualsiasi cartella Risorse.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Servizi cloud** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
