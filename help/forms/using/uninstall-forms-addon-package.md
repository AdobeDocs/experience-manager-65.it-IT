---
title: Questo articolo include l’istruzione di disinstallare il pacchetto del componente aggiuntivo Forms utilizzando Gestione pacchetti CRX.
description: Scopri come disinstallare il pacchetto del componente aggiuntivo Forms utilizzando Gestione pacchetti CRX.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 975f1f580404ea1f2940aec5981f5668dced4b95
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---


# Disinstallare il pacchetto del componente aggiuntivo AEM Forms dall’istanza AEM

Questo articolo illustra i passaggi necessari per disinstallare correttamente il pacchetto dei componenti aggiuntivi per AEM Forms da un’istanza SDK di AEM Forms. Segui questi passaggi per garantire la rimozione del pacchetto del componente aggiuntivo Forms, evitando potenziali problemi con l’ambiente AEM.

## Prerequisiti

Assicurati di eseguire il backup di moduli e dati per evitare perdite di dati.

## Per disinstallare il pacchetto del componente aggiuntivo AEM Forms

Per disinstallare il pacchetto del componente aggiuntivo AEM Forms, effettua le seguenti operazioni:

1. **Disinstalla il pacchetto del componente aggiuntivo AEM Forms:**
   1. Accedi a `http://[host]:[port]/crx/de/index.jsp`.
   1. Individuare e disinstallare `AEM Forms add-on package`.

   ![Disinstalla pacchetto](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Elimina la cartella nativa da CRXDE:**
   1. Accedi a `http://[host]:[port]/crx/de/index.jsp`.
   1. Vai a `/libs/fd/native/install` ed eliminare `native` in CRXDE.

      ![Elimina nodo nativo da CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Salva le modifiche.

1. **Arresta l’SDK di AEM Forms:**
   1. Arresta l’istanza dell’SDK AEM Forms utilizzando il comando &quot;Ctrl + C&quot;.

1. **Verifica la presenza di elementi di base e installa le cartelle nella cartella crx-quickstart**
   1. Accedi a `..author\crx-quickstart` nell’istanza SDK di AEM Forms.
   1. Cerca cartelle denominate `bedrock` e `install`.
Se vengono trovati, assicurati che vengano eliminati dal `crx-quickstart` nell’istanza SDK di AEM Forms.

   >[!NOTE]
   >
   > Il `bedrock` La cartella viene creata nuovamente automaticamente al riavvio dell’istanza SDK di AEM Forms.

1. **Riavvia l’istanza dell’AEM:**
   1. Una volta completati tutti i passaggi precedenti, [riavviare l&#39;istanza dell&#39;SDK AEM Forms](/help/forms/using/restart-aem-sdk.md).




