---
title: Questo articolo include le istruzioni per disinstallare il pacchetto del componente aggiuntivo Forms tramite Gestione pacchetti CRX.
description: Scopri i passaggi per disinstallare il pacchetto del componente aggiuntivo Forms utilizzando Gestione pacchetti CRX.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Disinstallare il pacchetto del componente aggiuntivo AEM Forms dall’istanza AEM

Questo articolo illustra i passaggi necessari per disinstallare correttamente il pacchetto dei componenti aggiuntivi per AEM Forms da un’istanza SDK di AEM Forms. Segui questi passaggi per garantire la rimozione del pacchetto del componente aggiuntivo Forms, evitando potenziali problemi con l’ambiente AEM.

## Prerequisito

Assicurati di eseguire il backup per evitare perdite di dati.

## Per disinstallare il pacchetto del componente aggiuntivo AEM Forms

Per disinstallare il pacchetto del componente aggiuntivo AEM Forms, effettua le seguenti operazioni:

1. **Disinstallare il pacchetto del componente aggiuntivo AEM Forms:**
   1. Passare a `http://[host]:[port]/crx/de/index.jsp`.
   1. Individuare e disinstallare `AEM Forms add-on package`.

   ![Disinstalla pacchetto](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Elimina la cartella nativa da CRXDE:**
   1. Passare a `http://[host]:[port]/crx/de/index.jsp`.
   1. Vai a `/libs/fd/native/install` ed elimina la cartella `native` in CRXDE.

      ![Elimina nodo nativo da CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Salva le modifiche.

1. **Arrestare l&#39;SDK di AEM Forms:**
   1. Arresta l’istanza dell’SDK AEM Forms utilizzando il comando &quot;Ctrl + C&quot;.

1. **Verifica la presenza di elementi di base e installa le cartelle nella cartella crx-quickstart**
   1. Passa alla cartella `..author\crx-quickstart` nell&#39;istanza SDK di AEM Forms.
   1. Cercare le cartelle con nome `bedrock` e `install`.
Se vengono trovati, assicurati che vengano eliminati dalla cartella `crx-quickstart` nell&#39;istanza SDK di AEM Forms.

   >[!NOTE]
   >
   > La cartella `bedrock` viene creata nuovamente automaticamente al riavvio dell&#39;istanza dell&#39;SDK AEM Forms.

1. **Riavviare l&#39;istanza AEM:**
   1. Una volta completati tutti i passaggi precedenti, [riavvia l&#39;istanza SDK di AEM Forms](/help/forms/using/restart-aem-sdk.md).




