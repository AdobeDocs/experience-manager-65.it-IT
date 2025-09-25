---
title: Gestione delle credenziali HSM
description: Scopri come gestire le credenziali HSM. Puoi gestire HSM dalla pagina Gestione archivio fonti attendibili. Puoi visualizzare, controllare, aggiornare, ripristinare ed eliminare i componenti HSM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1334'
ht-degree: 100%

---

# Gestione delle credenziali HSM {#managing-hsm-credentials}

Dalla pagina Gestione archivio fonti attendibili è possibile gestire le credenziali del modulo di sicurezza hardware (HSM, Hardware Security Module). Un HSM è un dispositivo di terze parti PKCS#11 che puoi utilizzare per generare e memorizzare in modo sicuro le chiavi private. HSM protegge fisicamente l’accesso alle chiavi private e il rispettivo utilizzo.

Il software client è necessario per comunicare con HSM. Il software client HSM deve essere installato e configurato nello stesso computer che ospita AEM Forms.

Le firme digitali di AEM Forms possono utilizzare le credenziali memorizzate in un HSM per applicare le firme digitali lato server. Segui le istruzioni riportate in questa sezione per creare un alias per ogni credenziale HSM che verrà utilizzata da Firme digitali. L’alias contiene tutti i parametri richiesti da HSM.

>[!NOTE]
>
>Dopo aver modificato la configurazione HSM, riavvia il server AEM Forms.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo, digitar una stringa che verrà utilizzata per identificare l’alias. Questo valore viene utilizzato come proprietà per alcune operazioni di firma digitale, ad esempio l’operazione Firma nel campo di firma.
1. Nella casella Libreria PKCS11 digita il percorso completo della libreria client HSM sul server. Ad esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Fai clic su Verifica connettività HSM. Se AEM Forms è in grado di connettersi al dispositivo HSM, viene visualizzato un messaggio che indica che l’HSM è disponibile. Fai clic su Avanti.
1. Utilizza il Nome token, l’ID slot o l’Indice elenco slot per identificare la posizione in cui sono memorizzate le credenziali nell’HSM.

   * **Nome token:** corrisponde al nome della partizione HSM da utilizzare (ad esempio, HSMPART1).
   * **ID slot:** l’ID slot è un identificatore di slot con tipo di dati long.
   * **Indice elenco slot:** se selezioni Indice elenco slot, imposta le informazioni sullo slot su un numero intero ad esso corrispondente. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, verrà fatto riferimento a HSMPART1 utilizzando il valore 0 di SlotListIndex.

1. Nella casella PIN token, digita la password necessaria per accedere alla chiave HSM e fai clic su Avanti.
1. Nella casella Credenziali, seleziona una credenziale. Fai clic su Salva.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo, digitar una stringa che verrà utilizzata per identificare l’alias. Questo valore viene utilizzato come proprietà per alcune operazioni di firma digitale, ad esempio l’operazione Firma nel campo di firma.
1. Nella casella Libreria PKCS11 digita il percorso completo della libreria client HSM sul server. Ad esempio, `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Seleziona la casella di controllo Creazione profilo offline. Fai clic su Avanti.
1. Nell’elenco Periferiche HSM seleziona il produttore del dispositivo HSM in cui è memorizzata la credenziale.
1. Nell’elenco Tipo slot, seleziona ID slot, Indice slot o Nome token e specifica un valore nella casella Informazioni slot. AEM Forms utilizza queste impostazioni per determinare dove vengono memorizzate le credenziali nell’HSM.

   * **Nome token:** corrisponde a un nome di partizione (ad esempio, HSMPART1).
   * **ID slot:** l’ID slot è un numero intero che corrisponde allo slot, a sua volta corrispondente a una partizione. Ad esempio, il client (server Forms) è stato registrato prima con la partizione HSMPART1. Questo mappa lo slot 1 alla partizione HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, l’ID dello slot è 1 e dovresti impostare le informazioni dello slot su 1.

     L’ID dello slot viene impostato su una base client per client. Se hai registrato un secondo computer in una partizione diversa (ad esempio HSMPART2 sullo stesso dispositivo HSM), lo slot 1 verrà associato alla partizione HSMPART2 per tale client.

   * **Slot Index:** se selezioni Slot Index, imposta le informazioni dello slot su un numero intero corrispondente allo slot. Poiché si tratta di un indice basato su 0, se il client viene innanzitutto registrato con la partizione HSMPART1, il mapping dello slot 1 viene eseguito a HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, il valore in Slot Index è 0.

1. Seleziona una di queste opzioni e fornisci il percorso:

   * **Certificato**: (non richiesto se si utilizza SHA1) Fai clic su Sfoglia e individua il percorso della chiave pubblica per le credenziali in uso.
   * **Certificato SHA1:** (non richiesto se si utilizza un certificato fisico) Digita il valore SHA1 (identificazione personale) del file della chiave pubblica (.cer) per le credenziali in uso. Verifica che nel valore SHA1 non siano presenti spazi.

1. Nella casella Password digita la password necessaria per accedere alla chiave HSM per le informazioni sullo slot specificate, quindi fai clic su Salva.

## Visualizzazione delle proprietà alias delle credenziali HSM {#view-hsm-credential-alias-properties}

1. Nella console di amministrazione fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fai clic sul nome dell’alias delle credenziali per visualizzare le proprietà, quindi scegli OK.

## Verifica dello stato di una credenziale HSM {#check-the-status-of-an-hsm-credential}

1. Nella console di amministrazione fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fai clic sulla casella di controllo accanto alle credenziali che desideri verificare, quindi su Controlla stato.

Nella colonna Stato è visualizzato lo stato corrente delle credenziali. In caso di errore, nella colonna Stato viene visualizzata una X rossa. Passa il puntatore del mouse sulla X per visualizzare una descrizione comando contenente il motivo dell’errore.

## Aggiornamento delle proprietà alias delle credenziali HSM {#update-hsm-credential-alias-properties}

1. Nella console di amministrazione fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fai clic sul nome dell’alias delle credenziali.
1. Fai clic su Aggiorna credenziali e aggiorna le impostazioni come richiesto.

## Reimpostazione di tutte le connessioni HSM {#reset-all-hsm-connections}

Reimposta le connessioni aperte su un dispositivo HSM dopo eventuali interruzioni della sessione di rete tra il server Forms e il dispositivo HSM. Ad esempio, possono verificarsi blocchi a causa di un’interruzione della rete o della disconnessione del dispositivo HSM per un aggiornamento software. Dopo un’interruzione, le connessioni esistenti non sono aggiornate e le eventuali richieste di firma relative a tali connessioni non riescono. L’utilizzo dell’opzione Reimposta tutte le connessioni HSM consente di cancellare le connessioni precedenti.

1. Nella console di amministrazione fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fai clic su Reimposta tutte le connessioni HSM.

## Eliminazione di un alias delle credenziali HSM {#delete-an-hsm-credential-alias}

1. Nella console di amministrazione fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Seleziona le caselle di controllo relative alle credenziali HSM che desideri eliminare, fai clic su Elimina, quindi su OK.

## Configurazione del supporto HSM remoto {#configure-remote-hsm-support}

AEM Forms utilizza un meccanismo IPC/RPC basato su servizi web. Questo meccanismo consente ad AEM Forms di utilizzare un modulo HSM installato in un computer remoto. Per utilizzare questa funzionalità, installa il servizio web nel computer remoto in cui è installato il modulo HSM. Per ulteriori informazioni, consulta [Configurazione del supporto HSM per AEM Forms ES con Sun JDK su piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html).

Questo meccanismo non supporta la creazione online di profili HSM o i controlli dello stato. Tuttavia, esistono due modi per creare profili HSM ed eseguire controlli dello stato:

* Crea una credenziale client di AEM Forms passandola con il certificato del firmatario. Segui i passaggi descritti in [Configurazione del supporto HSM per AEM Forms ES con Sun JDK su piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html). La posizione del servizio web viene passata come proprietà della credenziale. È inoltre supportata la creazione di profili HSM offline utilizzando il formato der o esadecimale SHA-1 del certificato. Tuttavia, se hai effettuato l’aggiornamento ad AEM Forms da una versione precedente, apporta modifiche al client perché le credenziali contenevano informazioni sul certificato e sul servizio web.
* La posizione del servizio web è specificata nella console di amministrazione del servizio di firma (consulta [Impostazioni del servizio di firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)). In questo caso, il client conteneva solo l’alias del profilo HSM nell’archivio fonti attendibili. Puoi utilizzare questa opzione senza alcuna modifica al client, anche se hai effettuato l’aggiornamento ad AEM Forms da una versione precedente. Questa opzione non supporta i profili HSM che utilizzano il certificato SHA-1.
