---
title: Frammenti di contenuto - Browser configurazioni
description: Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per utilizzare le potenti funzioni di distribuzione headless di Adobe Experience Manager.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 45%

---

# Frammenti di contenuto - Browser configurazioni{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per utilizzare le potenti funzioni di distribuzione headless di Adobe Experience Manager (AEM).

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, utilizzare **Browser di configurazione** per abilitare quanto segue:

* **Modelli per frammenti di contenuto**: obbligatorio
* **Query GraphQL persistenti**: facoltativo

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* l&#39;opzione **Crea** non sarà disponibile per la creazione di modelli.
>* impossibile [selezionare la configurazione Sites per creare l&#39;endpoint correlato](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

Per abilitare la funzionalità dei frammenti di contenuto, è necessario effettuare le seguenti operazioni:

* Abilitare l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser configurazioni
* Applicare la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model), è necessario **attivarle** tramite il **browser configurazioni**:

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Browser configurazioni:](/help/sites-administering/configurations.md#using-configuration-browser).

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

Quando la configurazione **global** è abilitata per la funzionalità frammento di contenuto, viene applicata a qualsiasi cartella di Assets.

Per utilizzare altre configurazioni (ovvero escludendo quelle globali) con una cartella Assets simile, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Servizi cloud** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
