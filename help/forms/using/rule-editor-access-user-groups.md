---
title: Concedere l'accesso all'editor di regole a gruppi di utenti selezionati
seo-title: Concedere l'accesso all'editor di regole a gruppi di utenti selezionati
description: Concedere accesso limitato all'editor delle regole per selezionare gruppi di utenti.
seo-description: Concedere accesso limitato all'editor delle regole per selezionare gruppi di utenti.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---


# Concedere l&#39;accesso all&#39;editor di regole a gruppi di utenti selezionati{#grant-rule-editor-access-to-select-user-groups}

## Panoramica {#overview}

Potete avere diversi tipi di utenti con competenze diverse che funzionano con Forms adattivo. Anche se gli utenti esperti possono avere la conoscenza necessaria per lavorare con script e regole complesse, potrebbero essere presenti utenti di livello base che devono utilizzare solo il layout e le proprietà di base dei moduli adattivi.

 AEM Forms consente di limitare l&#39;accesso all&#39;editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione Forms adattivo, potete specificare i [gruppi di utenti](/help/sites-administering/security.md) che possono visualizzare e accedere all&#39;editor delle regole.

## Specificare i gruppi di utenti che possono accedere all&#39;editor delle regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedete a  AEM Forms come amministratore.
1. Nell&#39;istanza di authoring, fare clic su ![adobeexperience emanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer.png) > Operazioni > Console Web. La console Web si apre in una nuova finestra.

   ![1-2](assets/1-2.png)

1. Nella finestra Console Web, individuare e fare clic su **Servizio configurazione modulo adattivo**. **Viene visualizzata** la finestra di dialogo Servizio configurazione modulo adattivo. Non modificare alcun valore e fare clic su **Salva**.

   Crea un file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config in CRX-repository.

1. Accedete a CRXDE come amministratore. Aprite il file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config per la modifica.
1. Utilizzare la proprietà seguente per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **Salva tutto**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l&#39;accesso a più gruppi, specificate un elenco di valori separati da virgola:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Ora, quando un utente che non fa parte di un gruppo di utenti specificato (in questo caso RuleEditorsUserGroup) tocca un campo, l&#39;icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile per l&#39;utente nella barra degli strumenti dei componenti:

   ![componentstoolbarwith](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all&#39;editor di regole

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti dei componenti visibile a un utente senza accesso all&#39;editor di regole

   Per istruzioni sull&#39;aggiunta di utenti ai gruppi, consultate [Amministrazione utente e sicurezza](/help/sites-administering/security.md).

