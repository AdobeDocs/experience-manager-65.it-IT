---
title: Frammenti di contenuto - Browser configurazioni
description: Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per utilizzare le potenti funzioni di distribuzione headless di Adobe Experience Manager.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 41%

---

# Frammenti di contenuto - Browser configurazioni{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per utilizzare le potenti funzioni di distribuzione headless di Adobe Experience Manager (AEM).

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, utilizza **Browser configurazioni** per attivare quanto segue:

* **Modelli per frammenti di contenuto**: obbligatorio
* **Query GraphQL persistenti**: facoltativo

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* il **Crea** non sarà disponibile per la creazione di modelli.
>* non puoi [seleziona la configurazione Sites per creare il relativo endpoint](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

Per abilitare la funzionalità dei frammenti di contenuto, è necessario effettuare le seguenti operazioni:

* Abilitare l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser configurazioni
* Applicare la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-in-configuration-browser}

A [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model), tu **deve** prima attivarli tramite **Browser configurazioni**:

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Browser configurazioni:](/help/sites-administering/configurations.md#using-configuration-browser).

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

Per utilizzare altre configurazioni (ovvero escludendo globali) con una cartella Risorse simile, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Servizi cloud** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
