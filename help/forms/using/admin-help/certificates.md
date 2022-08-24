---
title: Gestione dei certificati
seo-title: Managing certificates
description: Scopri come importare ed esportare un certificato e modificarne le impostazioni di attendibilità.
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Gestione dei certificati {#managing-certificates}

Utilizzando la gestione dell&#39;archivio certificati è possibile importare, modificare ed eliminare i certificati ritenuti attendibili nel server per la convalida delle firme digitali e l&#39;autenticazione dei certificati. È possibile importare ed esportare qualsiasi numero di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio attendibilità. Quando si combinano tipi di archivio attendibili, tenere in considerazione le seguenti opzioni:

* **Attendibilità per l&#39;autenticazione del certificato con CA:** Per la convalida CRL, selezionare Considera attendibile l&#39;identità.
* **Fiducia per l’autenticazione del certificato con ICA:** Seleziona Solo attendibilità per identità. Un&#39;ICA non deve essere attendibile per l&#39;autenticazione del certificato. Se si considera attendibile l’ICA per l’autenticazione del certificato, l’ICA diventa una CA per la creazione del percorso. Se l’ICA è attendibile sia per l’autenticazione del certificato che per l’identità, il certificato del fornitore della CA viene ignorato perché l’ICA diventa la CA.
* **Affidabilità per il server OCSP con HTTP:** Se il server di risposta OSCP risiede in un percorso HTTP, è necessario selezionare Considera attendibili anche le connessioni SSL. Se il rispondente OSCP richiede la convalida CRL, assicurarsi anche di selezionare Considera attendibile l’identità.
* **Directory principale Adobe:** Non selezionare connessioni SSL o tipi dell&#39;archivio di attendibilità del server OCSP. La directory principale di Adobe non è attendibile per le connessioni SSL e il server OCSP. Adobe non rilascia certificati OCSP e SSL. Adobe Root è implicitamente attendibile con un alias name=&quot;ADOBEROOT&quot;.

Sono supportati solo i certificati X509v3. Questo tipo di certificato può essere fornito in un file binario con codifica DER (file .cer) o in un file di testo contenente una versione codificata Base64 dello stesso certificato con codifica DER (inclusi i certificati X509 in formato PEM (Privacy Enhanced Mail)).

I certificati necessari per completare una verifica della firma devono trovarsi nello stesso archivio (HSM o database).

È inoltre possibile importare ed eliminare i certificati utilizzando l&#39;API di Trust Manager. Per informazioni dettagliate, vedere &quot;Importazione di certificati tramite l&#39;API di Trust Manager&quot; e &quot;Eliminazione di certificati tramite l&#39;API di Trust Manager&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importare un certificato {#import-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fare clic su Importa e, in Tipo archivio attendibili, selezionare una delle seguenti opzioni:

   * **Considera attendibili le connessioni SSL:** Specifica che AEM moduli possono utilizzare i certificati per connettersi a sistemi esterni tramite SSL.
   * **Attendibilità per firma certificata:** Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per la certificazione delle firme digitali dell&#39;autore.
   * **Attendibilità per la firma:** Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per le firme digitali non di authoring.
   * **Trust per l’autenticazione del certificato:** Specifica AEM moduli utilizza certificati per l’autenticazione degli utenti tramite autenticazione tramite certificato o smart card.
   * **Trust per il server OCSP:** Specifica che i moduli AEM possono utilizzare i certificati per connettersi ai risponditori OCSP esterni
   * **Considera attendibile l&#39;identità:** Specifica che i certificati possono essere utilizzati per considerare attendibili informazioni diverse dai tipi specificati in precedenza.

   >[!NOTE]
   >
   >L’archivio attendibilità si fida implicitamente di un certificato radice Adobe per l’autenticazione, la firma, la certificazione della firma e l’identità del certificato.

1. Nella casella Alias, digitare l&#39;identificatore del certificato.
1. Fai clic su **[!UICONTROL Sfoglia]** per individuare il certificato, quindi fare clic su **[!UICONTROL OK]**.

## Esportare un certificato {#export-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fare clic sul nome alias del certificato da esportare. La **[!UICONTROL Dettagli certificato]** viene visualizzata la pagina .
1. Fai clic su **[!UICONTROL Esporta]**, seguire le istruzioni per esportare il certificato, quindi fare clic su **[!UICONTROL OK]**.

## Modificare le impostazioni di attendibilità e il tipo di archivio attendibilità di un certificato {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fai clic sul nome alias del certificato da modificare.
1. Fai clic su **[!UICONTROL Aggiorna certificato]**.
1. Per modificare il nome alias del certificato, digitare un nuovo nome nella casella Alias.
1. Per aggiornare il tipo di archivio attendibilità per il certificato, selezionare il tipo di archivio attendibilità appropriato.
1. Per aggiornare le restrizioni dei criteri, digitare le informazioni relative ai criteri nella casella Criteri certificato, quindi fare clic su **[!UICONTROL OK]**.

## Eliminare un certificato {#delete-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Selezionare le caselle di controllo per i certificati da eliminare, fare clic su **[!UICONTROL Elimina]**, quindi fai clic su **[!UICONTROL OK]**.
