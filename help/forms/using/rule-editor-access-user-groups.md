---
title: Concedere l’accesso all’editor di regole a specifici gruppi di utenti
seo-title: Grant rule editor access to select user groups
description: Concedi l'accesso limitato all'editor di regole per selezionare i gruppi di utenti.
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 6%

---

# Concedere l’accesso all’editor di regole a specifici gruppi di utenti{#grant-rule-editor-access-to-select-user-groups}

## Panoramica {#overview}

Puoi avere diversi tipi di utenti con competenze diverse che funzionano con Adaptive Forms. Anche se gli utenti esperti possono avere le conoscenze necessarie per lavorare con script e regole complesse, potrebbero esserci utenti di livello base che devono utilizzare solo il layout e le proprietà di base dei moduli adattivi.

AEM Forms ti consente di limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione di Forms adattivo, puoi specificare il [gruppi di utenti](/help/sites-administering/security.md) che può visualizzare e accedere all’editor di regole.

## Specificare i gruppi di utenti che possono accedere all&#39;editor di regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedi ad AEM Forms come amministratore.
1. Nell’istanza di authoring, fai clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer.png) > Operazioni > Console web. La console Web viene visualizzata in una nuova finestra.

   ![1-2](assets/1-2.png)

1. Nella finestra Console Web, individuare e fare clic su **[!UICONTROL Configurazione del canale web per moduli adattivi e comunicazioni interattive]**. **[!UICONTROL Configurazione del canale web per moduli adattivi e comunicazioni interattive]** viene visualizzata la finestra di dialogo . Non modificare alcun valore e fai clic su **Salva**.

   Crea un file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config in CRX-repository.

1. Accedi a CRXDE come amministratore. Apri il file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config per la modifica.
1. Utilizzare la seguente proprietà per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **Salva tutto**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l&#39;accesso per più gruppi, specifica un elenco di valori separati da virgole:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Ora, quando un utente che non fa parte di un gruppo di utenti specificato (in questo caso RuleEditorsUserGroup) tocca un campo, l’icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile nella barra degli strumenti dei componenti:

   ![componentstoolbarwith](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all’editor di regole

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti dei componenti visibile per un utente senza accesso all’editor di regole

   Per istruzioni su come aggiungere utenti ai gruppi, consulta [Amministrazione degli utenti e sicurezza](/help/sites-administering/security.md).
