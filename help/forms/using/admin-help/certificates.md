---
title: Gestione dei certificati
description: Scopri come importare ed esportare un certificato e modificarne le impostazioni di attendibilità.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Gestione dei certificati {#managing-certificates}

Tramite la gestione dell&#39;archivio fonti attendibili è possibile importare, modificare ed eliminare certificati attendibili nel server per la convalida delle firme digitali e l&#39;autenticazione dei certificati. È possibile importare ed esportare un numero qualsiasi di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio fonti attendibili. Quando si combinano tipi di archivio fonti attendibili, prendere in considerazione le opzioni seguenti:

* **Attendibilità per autenticazione certificato con CA:** Per la convalida CRL, selezionare anche Attendibilità per identità.
* **Attendibilità per l’autenticazione dei certificati con ICA:** Selezionare Solo attendibilità per identità. Non è consigliabile considerare attendibile un&#39;istanza di autenticazione per l&#39;autenticazione dei certificati. Se si considera attendibile l&#39;ICA per l&#39;autenticazione dei certificati, l&#39;ICA diventa una CA per la creazione di percorsi. Se l&#39;ICA è attendibile sia per l&#39;autenticazione dei certificati che per l&#39;identità, il certificato del fornitore CA viene ignorato perché l&#39;ICA diventa la CA.
* **Attendibilità per il server OCSP con HTTP:** Se il server del partecipante OSCP risiede in una posizione HTTP, è necessario selezionare anche Considera attendibili le connessioni SSL. Se il rispondente OSCP richiede la convalida CRL, assicurarsi di selezionare anche Attendibilità per identità.
* **Directory principale Adobe:** Non selezionare Connessioni SSL o Tipi di archivio fonti attendibili del server OCSP. La radice Adobe non è attendibile per le connessioni SSL e il server OCSP. L’Adobe non rilascia certificati OCSP e SSL. Adobe Root è implicitamente attendibile con un alias name=&quot;ADOBEROOT&quot;.

Sono supportati solo i certificati X509v3. Questo tipo di certificato può essere fornito in un file binario con codifica DER (file con estensione cer) o in un file di testo contenente una versione con codifica Base64 dello stesso certificato con codifica DER (inclusi i certificati X509 in formato PEM (Privacy Enhanced Mail)).

I certificati necessari per completare una verifica della firma devono trovarsi nello stesso archivio (HSM o database).

È inoltre possibile importare ed eliminare certificati utilizzando l&#39;API di Gestione fonti attendibili. Per informazioni dettagliate, vedere &quot;Importazione di certificati tramite l&#39;API di Gestione trust&quot; e &quot;Eliminazione di certificati tramite l&#39;API di Gestione trust&quot; in [Programmazione con i moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importare un certificato {#import-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fare clic su Importa e in Tipo di archivio fonti attendibili selezionare una delle opzioni seguenti:

   * **Considera attendibili le connessioni SSL:** Specifica che i moduli AEM possono utilizzare i certificati per connettersi a sistemi esterni tramite SSL.
   * **Attendibilità per la firma del certificato:** Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per la certificazione delle firme digitali dell&#39;autore.
   * **Attendibilità per la firma:** Specifica che i certificati sono attendibili nelle operazioni di firma dei documenti per le firme digitali non di creazione.
   * **Attendibilità per autenticazione certificato:** Specifica che i moduli AEM utilizzano certificati per l&#39;autenticazione degli utenti tramite l&#39;autenticazione basata su certificati o smart card.
   * **Trust per il server OCSP:** Specifica che i moduli AEM possono utilizzare i certificati per la connessione a risponditori OCSP esterni
   * **Attendibilità per identità:** Specifica che i certificati possono essere utilizzati per considerare attendibili informazioni diverse dai tipi specificati in precedenza.

   >[!NOTE]
   >
   >L&#39;archivio fonti attendibili considera in modo implicito attendibile un certificato radice Adobe per l&#39;autenticazione, la firma, la firma di certificazione e l&#39;identità del certificato.

1. Nella casella Alias digitare l&#39;identificatore del certificato.
1. Clic **[!UICONTROL Sfoglia]** per individuare il certificato e quindi fare clic su **[!UICONTROL OK]**.

## Esportare un certificato {#export-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fare clic sul nome alias del certificato da esportare. Il **[!UICONTROL Dettagli certificato]** viene visualizzata.
1. Clic **[!UICONTROL Esporta]**, seguire le istruzioni per esportare il certificato e quindi fare clic su **[!UICONTROL OK]**.

## Modificare le impostazioni di attendibilità e il tipo di archivio fonti attendibili di un certificato {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fai clic sul nome alias del certificato da modificare.
1. Clic **[!UICONTROL Aggiorna certificato]**.
1. Per modificare il nome alias del certificato, digitare un nuovo nome nella casella Alias.
1. Per aggiornare il tipo di archivio fonti attendibili per il certificato, selezionare il tipo di archivio fonti attendibili appropriato.
1. Per aggiornare le restrizioni dei criteri, nella casella Criteri certificato digitare le informazioni sui criteri e quindi fare clic su **[!UICONTROL OK]**.

## Eliminare un certificato {#delete-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Selezionare le caselle di controllo relative ai certificati da eliminare, quindi fare clic su **[!UICONTROL Elimina]** e quindi fare clic su **[!UICONTROL OK]**.
