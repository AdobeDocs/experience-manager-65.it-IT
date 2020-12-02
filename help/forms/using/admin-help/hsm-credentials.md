---
title: Gestione delle credenziali HSM
seo-title: Gestione delle credenziali HSM
description: Scoprite come gestire le credenziali HSM.
seo-description: Scoprite come gestire le credenziali HSM.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 0%

---


# Gestione delle credenziali HSM {#managing-hsm-credentials}

Dalla pagina Gestione archivio attendibili, potete gestire le credenziali HSM (Hardware Security Module). Un HSM è un dispositivo PKCS#11 di terze parti che potete utilizzare per generare e memorizzare in modo sicuro le chiavi private. L&#39;HSM protegge fisicamente l&#39;accesso e l&#39;uso delle chiavi private.

Il software client è necessario per comunicare con l&#39;HSM. Il software client HSM deve essere installato e configurato sullo stesso computer dei moduli AEM.

AEM moduli Digital Signatures può utilizzare le credenziali archiviate in un HSM per applicare firme digitali lato server. Seguire le istruzioni riportate in questa sezione per creare un alias per ciascuna credenziale HSM che verrà utilizzata dalle firme digitali. L&#39;alias contiene tutti i parametri richiesti dall&#39;HSM.

>[!NOTE]
>
>Dopo aver modificato la configurazione HSM, riavviare il server moduli AEM.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM, quindi fate clic su Aggiungi.
1. Nella casella Nome profilo, digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni Digital Signatures, ad esempio l&#39;operazione Sign Signature Field.
1. Nella casella Libreria PKCS11, digitate il percorso completo della libreria client HSM sul server. Esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Fate clic su Test della connettività HSM. Se AEM moduli è in grado di connettersi al dispositivo HSM, viene visualizzato un messaggio in cui si informa che l&#39;HSM è disponibile. Fai clic su Avanti.
1. Utilizzate Nome token, ID slot o Indice elenco slot per identificare la posizione in cui sono memorizzate le credenziali nell&#39;HSM.

   * **Nome token:** corrisponde al nome della partizione HSM da utilizzare (ad esempio, HSMPART1).
   * **ID slot:** L&#39;ID slot è un identificatore slot di tipo di dati long.
   * **Indice elenco slot:** se si seleziona Indice elenco slot, impostare le informazioni slot su un numero intero che corrisponde allo slot. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, HSMPART1 verrà fatto riferimento al valore SlotListIndex 0.

1. Nella casella Pin token, digitate la password necessaria per accedere alla chiave HSM e fate clic su Avanti.
1. Nella casella Credenziali, selezionare una credenziale. Fate clic su Salva.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM, quindi fate clic su Aggiungi.
1. Nella casella Nome profilo, digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni Digital Signatures, ad esempio l&#39;operazione Sign Signature Field.
1. Nella casella Libreria PKCS11, digitate il percorso completo della libreria client HSM sul server. Esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Selezionate la casella di controllo Creazione profilo offline. Fai clic su Avanti.
1. Nell&#39;elenco dei dispositivi HSM, selezionare il produttore del dispositivo HSM in cui è memorizzata la credenziale.
1. Nell&#39;elenco Tipo di slot, selezionare l&#39;ID slot, l&#39;indice slot o il nome token e specificare un valore nella casella Informazioni slot. AEM moduli utilizza queste impostazioni per determinare dove sono memorizzate le credenziali nell&#39;HSM.

   * **Nome token:** corrisponde al nome di una partizione (ad esempio, HSMPART1).
   * **ID slot:** L&#39;ID slot è un numero intero che corrisponde allo slot, che a sua volta corrisponde a una partizione. Ad esempio, il client (server moduli) registrato prima con la partizione HSMPART1. Questo mappa lo slot 1 alla partizione HSMPART1, per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;ID slot è 1 e si imposta Slot Info su 1.

      L&#39;ID slot è impostato client per client. Se si registra un secondo computer in una partizione diversa (ad esempio, HSMPART2 sullo stesso dispositivo HSM), lo slot 1 sarà associato alla partizione HSMPART2 per quel client.

   * **Indice di slot:** se si seleziona Indice di slot, impostare le informazioni di slot su un numero intero che corrisponde allo slot. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, lo slot 1 viene mappato sull&#39;HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;indice di slot è 0.

1. Selezionare una delle seguenti opzioni e specificare il percorso:

   * **Certificato**: (Non richiesto se si utilizza SHA1) Fare clic su Sfoglia e individuare il percorso della chiave pubblica per la credenziale in uso.
   * **Certificato SHA1:** (non richiesto se si utilizza un certificato fisico) Digitare il valore SHA1 (identificazione personale) del file di chiave pubblica (.cer) per la credenziale in uso. Verificare che non siano presenti spazi utilizzati nel valore SHA1.

1. Nella casella Password digitare la password necessaria per accedere alla chiave HSM per le informazioni sullo slot, quindi fare clic su Salva.

## Visualizza proprietà alias credenziali HSM {#view-hsm-credential-alias-properties}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM.
1. Fare clic sul nome alias dell&#39;alias della credenziale per visualizzare le proprietà, quindi fare clic su OK.

## Verificare lo stato di una credenziale HSM {#check-the-status-of-an-hsm-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM.
1. Fare clic sulla casella di controllo accanto alla credenziale che si desidera controllare e fare clic su Controlla stato.

La colonna Stato riflette lo stato corrente della credenziale. In caso di errore, nella colonna Stato viene visualizzata una X rossa. Passate il puntatore del mouse sulla X per visualizzare una descrizione contenente il motivo dell’errore.

## Aggiorna proprietà alias credenziali HSM {#update-hsm-credential-alias-properties}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM.
1. Fare clic sul nome alias dell&#39;alias della credenziale.
1. Fate clic su Aggiorna credenziali e aggiornate le impostazioni come richiesto.

## Reimposta tutte le connessioni HSM {#reset-all-hsm-connections}

Ripristinare le connessioni aperte a un dispositivo HSM dopo un&#39;interruzione della sessione di rete tra il server dei moduli e il dispositivo HSM. Ad esempio, le interruzioni possono verificarsi a causa di un&#39;interruzione di rete o del fatto che il dispositivo HSM viene portato offline per un aggiornamento software. Dopo un&#39;interruzione, le connessioni esistenti sono scadenti e qualsiasi richiesta di firma relativa a tali connessioni non riesce. L&#39;opzione Reimposta tutte le connessioni HSM cancella le vecchie connessioni.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM.
1. Fate clic su Reimposta tutte le connessioni HSM.

## Eliminare un alias di credenziali HSM {#delete-an-hsm-credential-alias}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali HSM.
1. Selezionate le caselle di controllo relative alle credenziali HSM da eliminare, fate clic su Elimina, quindi su OK.

## Configurare il supporto HSM remoto {#configure-remote-hsm-support}

AEM moduli utilizza un meccanismo IPC/RPC basato su Servizi Web. Questo meccanismo consente AEM moduli di utilizzare un HSM installato su un computer remoto. Per utilizzare questa funzionalità, installare il servizio Web sul computer remoto in cui è installato l&#39;HSM. Per ulteriori informazioni, vedere [Configurazione del supporto HSM per AEM moduli ES utilizzando Sun JDK sulla piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html).

Questo meccanismo non supporta la creazione online di profili HSM o controlli dello stato. Esistono tuttavia due modi per creare profili HSM ed eseguire controlli di stato:

* Creare una credenziale client AEM modulo trasmettendola nel Certificato del firmatario. Seguire i passaggi descritti in [Configurazione del supporto HSM per AEM moduli ES utilizzando Sun JDK sulla piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html). La posizione del servizio Web viene passata come proprietà Credential. Sono supportati anche i profili HSM offline creati utilizzando certificati der o certificati SHA-1 hex. Tuttavia, se si è effettuato l&#39;aggiornamento ai moduli AEM da una versione precedente dei moduli AEM, apportare modifiche al client perché le credenziali includevano informazioni sul certificato e sul servizio Web.
* Il percorso del servizio Web è specificato nella console di amministrazione per il servizio Signature. (Vedere [Impostazioni del servizio firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) In questo caso, l&#39;alias del profilo HSM era presente solo nel trust store. È possibile utilizzare questa opzione senza apportare alcuna modifica al client, anche se si è effettuato l&#39;aggiornamento ai moduli AEM da una versione precedente dei moduli AEM. Questa opzione non supporta i profili HSM che utilizzano il certificato SHA-1.

