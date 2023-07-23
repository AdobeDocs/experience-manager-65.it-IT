---
title: Concedere l’accesso all’editor di regole a specifici gruppi di utenti
seo-title: Grant rule editor access to select user groups
description: Concedi accesso limitato all’editor di regole per selezionare i gruppi di utenti.
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 7%

---

# Concedere l’accesso all’editor di regole a specifici gruppi di utenti{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

Potresti avere diversi tipi di utenti con diverse competenze che lavorano con Adaptive Forms. Anche se gli utenti esperti possono avere le giuste conoscenze per lavorare con script e regole complesse, ci possono essere utenti di livello base che devono lavorare solo con il layout e le proprietà di base dei moduli adattivi.

AEM Forms ti consente di limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione di Adaptive Forms puoi specificare [gruppi di utenti](/help/sites-administering/security.md) che possono visualizzare e accedere all’editor di regole.

## Specificare i gruppi di utenti che possono accedere all’editor di regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedi ad AEM Forms come amministratore.
1. Nell’istanza di authoring, fai clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer.png) > Operazioni > Console web. La console Web si apre in una nuova finestra.

   ![1-2](assets/1-2.png)

1. Nella finestra della console Web, individua e fai clic su **[!UICONTROL Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva]**. **[!UICONTROL Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva]** viene visualizzata. Non modificare alcun valore e fai clic su **Salva**.

   Crea un file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config in CRX-repository.

1. Accedi a CRXDE come amministratore. Apri il file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config per la modifica.
1. Utilizzare la proprietà seguente per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **Salva tutto**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l’accesso per più gruppi, specifica un elenco di valori separati da virgole:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Ora, quando un utente che non fa parte di un gruppo di utenti specificato (in questo caso RuleEditorsUserGroup) tocca un campo, l’icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile nella barra degli strumenti dei componenti:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all’editor di regole

   ![componentstoolbarwithout outre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti Componenti visibile a un utente senza accesso all’editor di regole

   Per istruzioni sull’aggiunta di utenti ai gruppi, consulta [Amministrazione utenti e sicurezza](/help/sites-administering/security.md).
