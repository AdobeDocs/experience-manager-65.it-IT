---
title: Gestire i certificati
description: Scopri come importare ed esportare un certificato e come modificarne le impostazioni di affidabilità.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '646'
ht-degree: 100%

---

# Gestire i certificati {#managing-certificates}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Tramite la gestione dell’archivio fonti attendibili puoi importare, modificare o eliminare dal server i certificati che consideri attendibili per la convalida delle firme digitali e l’autenticazione. Puoi importare ed esportare un numero illimitato di certificati. Dopo l’importazione di un certificato, puoi modificare le impostazioni di affidabilità e il tipo di archivio fonti attendibili. Quando combini diversi tipi di archivio fonti attendibili, tieni presenti le seguenti opzioni:

* **Affidabilità per autenticazione certificato con CA:** per la convalida CRL, seleziona anche Affidabilità per identità.
* **Affidabilità per autenticazione certificato con ICA:** seleziona solo Affidabilità per identità. Non è consigliabile considerare attendibile un’Autorità di autenticazione intermedia (ICA) per l’autenticazione dei certificati. Se consideri attendibile l’ICA per l’autenticazione dei certificati, l’ICA diventa un’Autorità di certificazione (CA) per la creazione di percorsi. Se l’ICA è attendibile sia per l’autenticazione che per l’identità del certificato, il certificato del fornitore CA viene ignorato perché l’ICA diventa la CA.
* **Affidabilità del server OCSP con HTTPs:** se il server rispondente OCSP si trova in una posizione HTTPs, devi selezionare anche Affidabilità per connessioni SSL. Se il server rispondente OCSP richiede la convalida CRL, verifica di selezionare anche Affidabilità per identità.
* **Certificato radice Adobe:** non selezionare Connessioni SSL o Tipi di archivi fonti affidabili del server OCSP. Il certificato radice Adobe non è affidabile per le connessioni SSL e i server OCSP. Adobe non rilascia certificati OCSP e SSL. Il certificato radice Adobe è implicitamente affidabile con un alias name=“ADOBEROOT”.

Sono supportati solo i certificati X509v3. Questo tipo di certificato può essere fornito in un file binario con codifica DER (file con estensione cer) o in un file di testo contenente una versione con codifica Base64 dello stesso certificato con codifica DER (inclusi i certificati X509 in formato PEM, Privacy Enhanced Mail).

I certificati necessari per completare una verifica della firma devono trovarsi nello stesso archivio (HSM o database).

Puoi anche importare ed eliminare certificati utilizzando l’API Gestore affidabilità. Per informazioni dettagliate, consulta “Importare certificati tramite l’API Gestore affidabilità” ed “Eliminare certificati tramite l’API Gestore affidabilità” in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63_it).

## Importare un certificato {#import-a-certificate}

1. Nella Console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fai clic su Importa, quindi in Tipo di archivio fonti attendibili seleziona una delle opzioni seguenti:

   * **Affidabilità per connessioni SSL:** specifica che i moduli AEM possono utilizzare certificati per connettersi a sistemi esterni tramite SSL.
   * **Affidabilità per la firma di certificazione:** specifica che i certificati sono affidabili per la certificazione delle firme digitali degli autori nelle operazioni di firma dei documenti.
   * **Affidabilità della firma:** specifica che i certificati sono affidabili nelle operazioni di firma dei documenti per le firme digitali di base.
   * **Affidabilità dell’autenticazione del certificato:** specifica che i moduli AEM utilizzano i certificati per l’autenticazione degli utenti basata su certificati o smart card.
   * **Affidabilità del server OCSP:** specifica che i moduli AEM possono utilizzare i certificati per connettersi ai partecipanti OCSP esterni
   * **Affidabilità per identità:** specifica che i certificati possono essere utilizzati per considerare affidabili informazioni di tipo diverso da quelli specificati in precedenza.

   >[!NOTE]
   >
   >L’archivio fonti affidabili considera implicitamente affidabile un certificato radice Adobe per l’autenticazione, la firma, la firma di certificazione e l’identità dei certificati.

1. Nella casella Alias digita l’identificatore del certificato.
1. Fai clic su **[!UICONTROL Sfoglia]** per individuare il certificato e quindi su **[!UICONTROL OK]**.

## Esportare un certificato {#export-a-certificate}

1. Nella Console di amministrazione fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fai clic sul nome dell’alias del certificato da esportare. Viene visualizzata la pagina **[!UICONTROL Dettagli del certificato]**.
1. Fai clic su **[!UICONTROL Esporta]**, segui le istruzioni per esportare il certificato, quindi fai clic su **[!UICONTROL OK]**.

## Modificare le impostazioni di affidabilità e il tipo di archivio fonti affidabili di un certificato {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. Nella Console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio fonti attendibili > Certificati]**.
1. Fai clic sul nome dell’alias del certificato da modificare.
1. Fai clic su **[!UICONTROL Aggiorna certificato]**.
1. Per modificare il nome dell’alias del certificato, digita un nuovo nome nella casella Alias.
1. Per aggiornare il tipo di archivio fonti attendibili per il certificato, seleziona il tipo di archivio appropriato.
1. Per aggiornare le limitazioni dei criteri, digita le informazioni dei criteri nella casella Criteri certificato, quindi fai clic su **[!UICONTROL OK]**.

## Eliminare un certificato {#delete-a-certificate}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione archivio certificati attendibili > Certificati]**.
1. Seleziona le caselle di controllo per i certificati da eliminare, fai clic su **[!UICONTROL Elimina]** e quindi su **[!UICONTROL OK]**.
