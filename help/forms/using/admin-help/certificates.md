---
title: Gestione dei certificati
seo-title: Gestione dei certificati
description: Scoprite come importare ed esportare un certificato e modificarne le impostazioni di affidabilità.
seo-description: Scoprite come importare ed esportare un certificato e modificarne le impostazioni di affidabilità.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gestione dei certificati {#managing-certificates}

Utilizzando la funzione Trust Store Management, è possibile importare, modificare ed eliminare i certificati affidabili sul server per la convalida delle firme digitali e l&#39;autenticazione tramite certificato. È possibile importare ed esportare qualsiasi numero di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio attendibili. Quando si combinano tipi di store attendibili, tenere in considerazione le seguenti opzioni:

* **** Trust per l&#39;autenticazione certificato con CA: Per la convalida CRL, selezionare Considera attendibile l&#39;identità.
* **** Trust for Certificate Authentication with ICA: Selezionare Solo Trust for Identity. Un&#39;ICA non dovrebbe essere affidabile per l&#39;autenticazione del certificato. Se si considera attendibile l&#39;ICA per l&#39;autenticazione del certificato, l&#39;ICA diventa una CA per la creazione del percorso. Se l&#39;ICA è attendibile sia per Autenticazione certificati che per Identità, il certificato fornitore CA viene ignorato perché l&#39;ICA diventa CA.
* **** Affidabilità per il server OCSP con HTTP: Se il server di risposta OSCP risiede in un percorso HTTP, è necessario selezionare Considera affidabili anche le connessioni SSL. Se il rispondente OSCP richiede la convalida CRL, assicurarsi di selezionare anche Trust for Identity.
* **** Adobe Root: Non selezionate Connessioni SSL o Tipi archivio certificati server OCSP. Adobe Root non è attendibile per connessioni SSL e server OCSP. Adobe non rilascia certificati OCSP e SSL. Adobe Root è implicitamente affidabile con un alias name=&quot;ADOBEROOT&quot;.

Sono supportati solo i certificati X509v3. Questo tipo di certificato può essere fornito in un file binario con codifica DER (file .cer) o in un file di testo contenente una versione codificata Base64 dello stesso certificato con codifica DER (inclusi i certificati X509 in formato PEM (Privacy Enhanced Mail)).

I certificati richiesti per completare la verifica della firma devono trovarsi nello stesso store (HSM o database).

È inoltre possibile importare ed eliminare i certificati utilizzando l&#39;API Trust Manager. Per informazioni dettagliate, consultate &quot;Importazione di certificati tramite l&#39;API Trust Manager&quot; e &quot;Eliminazione di certificati tramite l&#39;API Trust Manager&quot; nella [programmazione con i moduli](https://www.adobe.com/go/learn_aemforms_programming_63)AEM.

## Importare un certificato {#import-a-certificate}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione archivio attendibili > Certificati]**.
1. Fare clic su Importa e, in Tipo archivio attendibili, selezionare una delle seguenti opzioni:

   * **** Considera affidabili le connessioni SSL: Specifica che i moduli AEM possono utilizzare i certificati per connettersi ai sistemi esterni tramite SSL.
   * **** Attendibilità per firma certificata: Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per la certificazione delle firme digitali degli autori.
   * **** Considera attendibile per la firma: Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per le firme digitali non di autori.
   * **** Trust per autenticazione certificato: Specifica che i moduli AEM utilizzano i certificati per l&#39;autenticazione degli utenti mediante l&#39;autenticazione tramite certificato o smart card.
   * **** Trust per il server OCSP: Specifica che i moduli AEM possono utilizzare i certificati per connettersi ai rispondenti OCSP esterni
   * **** Trust for Identity: Specifica che i certificati possono essere utilizzati per considerare attendibili informazioni diverse dai tipi sopra specificati.
   >[!NOTE]
   >
   >L&#39;archivio di trust si fida implicitamente di un certificato di origine Adobe per l&#39;autenticazione, la firma, la certificazione della firma e l&#39;identità dei certificati.

1. Nella casella Alias digitare l&#39;identificatore del certificato.
1. Fate clic su **[!UICONTROL Sfoglia]** per individuare il certificato, quindi fate clic su **[!UICONTROL OK]**.

## Esportare un certificato {#export-a-certificate}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione archivio attendibili > Certificati]**.
1. Fate clic sul nome alias del certificato da esportare. Viene visualizzata la pagina **[!UICONTROL Dettagli]** certificato.
1. Fate clic su **[!UICONTROL Esporta]**, seguite le istruzioni per esportare il certificato, quindi fate clic su **[!UICONTROL OK]**.

## Modifica delle impostazioni di attendibilità e del tipo di archivio certificati {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione archivio attendibili > Certificati]**.
1. Fate clic sul nome alias del certificato da modificare.
1. Fate clic su **[!UICONTROL Aggiorna certificato]**.
1. Per modificare il nome alias del certificato, digitare un nuovo nome nella casella Alias.
1. Per aggiornare il tipo di archivio attendibili per il certificato, selezionare il tipo di archivio attendibili appropriato.
1. Per aggiornare le restrizioni dei criteri, nella casella Criteri certificati digitare le informazioni sui criteri, quindi fare clic su **[!UICONTROL OK]**.

## Eliminare un certificato {#delete-a-certificate}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione archivio attendibili > Certificati]**.
1. Selezionare le caselle di controllo per i certificati da eliminare, fare clic su **[!UICONTROL Elimina]** e quindi su **[!UICONTROL OK]**.

