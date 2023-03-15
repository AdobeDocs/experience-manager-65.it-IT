---
title: Gestione delle credenziali HSM
seo-title: Managing HSM credentials
description: Scopri come gestire le credenziali HSM.
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# Gestione delle credenziali HSM {#managing-hsm-credentials}

Dalla pagina Gestione dell&#39;archivio fonti attendibili è possibile gestire le credenziali del modulo di sicurezza hardware (HSM). Un HSM è un dispositivo PKCS#11 di terze parti che può essere utilizzato per generare e memorizzare in modo sicuro le chiavi private. L&#39;HSM protegge fisicamente l&#39;accesso e l&#39;uso delle chiavi private.

Il software client è necessario per comunicare con l&#39;HSM. Il software client HSM deve essere installato e configurato sullo stesso computer dei moduli AEM.

AEM moduli Le firme digitali possono utilizzare le credenziali memorizzate in un HSM per applicare le firme digitali lato server. Segui le istruzioni riportate in questa sezione per creare un alias per ogni credenziale HSM che verranno utilizzate con Digital Signatures. L&#39;alias contiene tutti i parametri richiesti dall&#39;HSM.

>[!NOTE]
>
>Dopo aver modificato la configurazione HSM, riavviare il server dei moduli AEM.

## Crea un alias per una credenziale HSM quando il dispositivo HSM è online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni relative alle firme digitali, ad esempio l’operazione Firma campo firma.
1. Nella casella Libreria PKCS11 digitare il percorso completo della libreria client HSM sul server. Esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Fai clic su Test della connettività HSM. Se AEM moduli è in grado di connettersi al dispositivo HSM, viene visualizzato un messaggio in cui si informa che l’HSM è disponibile. Fai clic su Avanti.
1. Utilizza il Nome token, l’ID slot o l’indice dell’elenco di slot per identificare la posizione in cui le credenziali sono memorizzate nell’HSM.

   * **Nome token:** Corrisponde al nome della partizione HSM da utilizzare (ad esempio, HSMPART1).
   * **ID slot:** L&#39;ID slot è un identificatore slot di tipo dati long.
   * **Indice elenco slot:** Se si seleziona Indice elenco slot, impostare le informazioni slot su un numero intero corrispondente allo slot. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, HSMPART1 verrà indicato utilizzando il valore SlotListIndex 0.

1. Nella casella Token Pin digitare la password necessaria per accedere alla chiave HSM e fare clic su Avanti.
1. Nella casella Credenziali selezionare una credenziale. Fai clic su Salva.

## Crea un alias per una credenziale HSM quando il dispositivo HSM è offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni relative alle firme digitali, ad esempio l’operazione Firma campo firma.
1. Nella casella Libreria PKCS11 digitare il percorso completo della libreria client HSM sul server. Esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Selezionare la casella di controllo Creazione profilo offline. Fai clic su Avanti.
1. Nell’elenco dei dispositivi HSM, selezionare il produttore del dispositivo HSM in cui è memorizzata la credenziale.
1. Nell’elenco Tipo di slot, selezionare ID slot, Indice slot o Nome token e specificare un valore nella casella Informazioni slot. Nei moduli AEM vengono utilizzate queste impostazioni per determinare dove sono memorizzate le credenziali nell’HSM.

   * **Nome token:** Corrisponde al nome di una partizione (ad esempio, HSMPART1).
   * **ID slot:** L&#39;ID slot è un numero intero che corrisponde allo slot, che a sua volta corrisponde a una partizione. Ad esempio, il client (server forms) registrato prima con la partizione HSMPART1. Questo mappa lo slot 1 alla partizione HSMPART1, per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;ID slot è 1 e si imposta Slot Info su 1.

      L&#39;ID dello slot è impostato client per client. Se si registra una seconda macchina in una partizione diversa (ad esempio, HSMPART2 sullo stesso dispositivo HSM), lo slot 1 verrebbe associato alla partizione HSMPART2 per quel client.

   * **Indice della slot:** Se si seleziona Indice slot, impostare le informazioni slot su un numero intero corrispondente allo slot. Questo è un indice basato su 0, il che significa che se il client è registrato prima con la partizione HSMPART1, lo slot 1 è mappato all&#39;HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;indice di slot è 0.

1. Selezionare una delle seguenti opzioni e specificare il percorso:

   * **Certificato**: (Non obbligatorio se si utilizza SHA1) Fare clic su Sfoglia e individuare il percorso della chiave pubblica per la credenziale in uso.
   * **Certificato SHA1:** (Non obbligatorio se si utilizza un certificato fisico) Digitare il valore SHA1 (identificazione personale) del file della chiave pubblica (.cer) per la credenziale in uso. Assicurati che non ci siano spazi utilizzati nel valore SHA1.

1. Nella casella Password digitare la password necessaria per accedere alla chiave HSM per le informazioni sullo slot specificate, quindi fare clic su Salva.

## Visualizza proprietà alias credenziali HSM {#view-hsm-credential-alias-properties}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM.
1. Fare clic sul nome dell&#39;alias della credenziale per visualizzare le proprietà, quindi fare clic su OK.

## Controllare lo stato di una credenziale HSM {#check-the-status-of-an-hsm-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM.
1. Fare clic sulla casella di controllo accanto alla credenziale che si desidera controllare e fare clic su Verifica stato.

La colonna Stato riflette lo stato corrente della credenziale. In caso di errore, nella colonna Stato viene visualizzata una X rossa. Passa il mouse sulla X per visualizzare una descrizione comandi contenente il motivo dell’errore.

## Aggiorna le proprietà alias delle credenziali HSM {#update-hsm-credential-alias-properties}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM.
1. Fare clic sul nome dell&#39;alias della credenziale.
1. Fare clic su Aggiorna credenziali e aggiornare le impostazioni in base alle esigenze.

## Reimposta tutte le connessioni HSM {#reset-all-hsm-connections}

Ripristinare le connessioni aperte a un dispositivo HSM dopo eventuali interruzioni della sessione di rete tra il server dei moduli e il dispositivo HSM. Ad esempio, possono verificarsi interruzioni a causa di un&#39;interruzione di rete o di un dispositivo HSM che viene portato offline per un aggiornamento software. Dopo un’interruzione, le connessioni esistenti non sono più aggiornate e le richieste di firma relative a tali connessioni falliscono. L&#39;opzione Reset All HSM Connections cancella le vecchie connessioni.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM.
1. Fare clic su Reimposta tutte le connessioni HSM.

## Eliminare un alias di credenziali HSM {#delete-an-hsm-credential-alias}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Credenziali HSM.
1. Selezionare le caselle di controllo relative alle credenziali HSM che si desidera eliminare, fare clic su Elimina e quindi su OK.

## Configurare il supporto HSM remoto {#configure-remote-hsm-support}

I moduli AEM utilizzano un meccanismo IPC/RPC basato su servizi Web. Questo meccanismo consente ai moduli AEM di utilizzare un HSM installato su un computer remoto. Per utilizzare questa funzionalità, installare il servizio Web sul computer remoto in cui è installato l&#39;HSM. Vedi [Configurazione del supporto HSM per AEM forms ES utilizzando Sun JDK sulla piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html)per ulteriori informazioni.

Questo meccanismo non supporta la creazione online di profili HSM o controlli di stato. Tuttavia, esistono due modi per creare profili HSM ed eseguire controlli di stato:

* Crea una credenziale client di AEM forms trasmettendola il certificato del firmatario. Segui i passaggi descritti in [Configurazione del supporto HSM per AEM forms ES utilizzando Sun JDK sulla piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html). Il percorso del servizio Web viene passato come proprietà Credential. Sono supportati anche i profili HSM offline creati utilizzando il certificato der o il certificato SHA-1 hex. Tuttavia, se si è eseguito l’aggiornamento a AEM moduli da una versione precedente di AEM forms, apportare modifiche al client perché le credenziali riportavano informazioni sul certificato e sul servizio Web.
* Il percorso del servizio Web è specificato nella console di amministrazione per il servizio Signature. (Vedi [Impostazioni del servizio Firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) In questo caso, il client ha effettuato solo l’alias del profilo HSM nell’archivio attendibilità. È possibile utilizzare questa opzione senza apportare modifiche al client, anche se si è eseguito l’aggiornamento a AEM moduli da una versione precedente di AEM moduli. Questa opzione non supporta i profili HSM che utilizzano il certificato SHA-1.
