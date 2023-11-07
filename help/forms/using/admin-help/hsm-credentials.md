---
title: Gestione delle credenziali HSM
description: Scopri come gestire le credenziali HSM. Puoi gestire HSM dalla pagina Gestione archivio fonti attendibili. Puoi visualizzare, controllare, aggiornare, reimpostare ed eliminare i componenti HSM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# Gestione delle credenziali HSM {#managing-hsm-credentials}

Dalla pagina Gestione dell&#39;archivio fonti attendibili è possibile gestire le credenziali del modulo di protezione hardware. Un HSM è un dispositivo di terze parti PKCS#11 che puoi utilizzare per generare e memorizzare in modo sicuro le chiavi private. HSM protegge fisicamente l&#39;accesso e l&#39;uso delle chiavi private.

Il software client è necessario per comunicare con HSM. Il software client HSM deve essere installato e configurato sullo stesso computer dei moduli AEM.

Le firme digitali dei moduli AEM possono utilizzare le credenziali memorizzate su un HSM per applicare le firme digitali lato server. Segui le istruzioni riportate in questa sezione per creare un alias per ogni credenziale HSM utilizzata da Digital Signatures. L’alias contiene tutti i parametri richiesti da HSM.

>[!NOTE]
>
>Dopo aver modificato la configurazione HSM, riavvia il server AEM Forms.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni di Firma digitale, ad esempio l&#39;operazione Firma campo.
1. Nella casella Libreria PKCS11 digitare il percorso completo della libreria client HSM sul server. Esempio: `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Fare clic su Verifica connettività HSM. Se i moduli AEM sono in grado di connettersi al dispositivo HSM, viene visualizzato un messaggio che informa che il dispositivo HSM è disponibile. Fai clic su Avanti.
1. Utilizzare il Nome token, l&#39;ID slot o l&#39;Indice elenco slot per identificare la posizione in cui sono memorizzate le credenziali nell&#39;HSM.

   * **Nome token:** Corrisponde al nome della partizione HSM da utilizzare, ad esempio HSMPART1.
   * **ID slot:** L&#39;ID slot è un identificatore di slot di tipo long.
   * **Indice elenco slot:** Se selezionate Indice elenco slot (Slot List Index), impostate le informazioni sullo slot su un numero intero corrispondente allo slot. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, verrà fatto riferimento a HSMPART1 utilizzando il valore 0 di SlotListIndex.

1. Nella casella Token Pin, digita la password necessaria per accedere alla chiave HSM e fai clic su Avanti.
1. Nella casella Credenziali selezionare una credenziale. Fai clic su Salva.

## Creare un alias per una credenziale HSM quando il dispositivo HSM è offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM, quindi fai clic su Aggiungi.
1. Nella casella Nome profilo digitare una stringa utilizzata per identificare l&#39;alias. Questo valore viene utilizzato come proprietà per alcune operazioni di Firma digitale, ad esempio l&#39;operazione Firma campo.
1. Nella casella Libreria PKCS11 digitare il percorso completo della libreria client HSM sul server. Esempio: `c:\Program Files\LunaSA\cryptoki.dll`. In un ambiente cluster, questo percorso deve essere identico per tutti i server del cluster.
1. Selezionare la casella di controllo Creazione profilo offline. Fai clic su Avanti.
1. Nell&#39;elenco Periferiche HSM selezionare il produttore della periferica HSM in cui sono memorizzate le credenziali.
1. Nell&#39;elenco Tipo slot (Slot Type), selezionate ID slot (Slot Id), Indice slot (Slot Index) o Nome token (Token Name) e specificate un valore nella casella Informazioni slot (Slot Info). I moduli AEM utilizzano queste impostazioni per determinare dove vengono memorizzate le credenziali nell&#39;HSM.

   * **Nome token:** Corrisponde al nome di una partizione (ad esempio, HSMPART1).
   * **ID slot:** L&#39;ID slot è un numero intero che corrisponde allo slot, che a sua volta corrisponde a una partizione. Ad esempio, il client (server Forms) è stato registrato prima con la partizione HSMPART1. Questo mappa lo slot 1 alla partizione HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;ID dello slot è 1 e le informazioni sullo slot vengono impostate su 1.

     L&#39;ID dello slot viene impostato client per client. Se si registra un secondo computer in una partizione diversa (ad esempio, HSMPART2 sullo stesso dispositivo HSM), lo slot 1 verrà associato alla partizione HSMPART2 per tale client.

   * **Indice slot:** Se selezionate Indice slot (Slot Index), impostate le informazioni sullo slot su un numero intero corrispondente allo slot. Si tratta di un indice basato su 0, il che significa che se il client viene registrato prima con la partizione HSMPART1, lo slot 1 viene mappato a HSMPART1 per questo client. Poiché HSMPART1 è la prima partizione registrata, l&#39;indice di slot è 0.

1. Seleziona una di queste opzioni e fornisci il percorso:

   * **Certificato**: (non obbligatorio se si utilizza SHA1) Fare clic su Sfoglia e individuare il percorso della chiave pubblica per le credenziali in uso.
   * **Certificato SHA1:** (Non richiesto se si utilizza un certificato fisico) Digitare il valore SHA1 (identificazione personale) del file della chiave pubblica (.cer) per le credenziali in uso. Verificare che nel valore SHA1 non siano presenti spazi.

1. Nella casella Password digitare la password necessaria per accedere alla chiave HSM per le informazioni sullo slot specificate e quindi fare clic su Salva.

## Visualizza proprietà alias credenziali HSM {#view-hsm-credential-alias-properties}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fare clic sul nome dell&#39;alias delle credenziali per visualizzare le proprietà, quindi scegliere OK.

## Verificare lo stato di una credenziale HSM {#check-the-status-of-an-hsm-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fare clic sulla casella di controllo accanto alle credenziali che si desidera verificare e quindi su Verifica stato.

La colonna Stato riflette lo stato corrente delle credenziali. In caso di errore, nella colonna Stato viene visualizzata una X rossa. Passa il puntatore del mouse sulla X per visualizzare una descrizione comando contenente il motivo dell’errore.

## Aggiorna proprietà alias credenziali HSM {#update-hsm-credential-alias-properties}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fare clic sul nome dell&#39;alias delle credenziali.
1. Fai clic su Aggiorna credenziali e aggiorna le impostazioni come richiesto.

## Reimposta tutte le connessioni HSM {#reset-all-hsm-connections}

Ripristina le connessioni aperte a un dispositivo HSM dopo eventuali interruzioni della sessione di rete tra il server Forms e il dispositivo HSM. Ad esempio, possono verificarsi interruzioni a causa di un’interruzione della rete o della disconnessione del dispositivo HSM per un aggiornamento software. Dopo un’interruzione, le connessioni esistenti non sono aggiornate e le eventuali richieste di firma relative a tali connessioni non riescono. L&#39;utilizzo dell&#39;opzione Reimposta tutte le connessioni HSM consente di cancellare le connessioni precedenti.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Fare clic su Reimposta tutte le connessioni HSM.

## Eliminare un alias delle credenziali HSM {#delete-an-hsm-credential-alias}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali HSM.
1. Selezionare le caselle di controllo relative alle credenziali HSM che si desidera eliminare, fare clic su Elimina e quindi su OK.

## Configurare il supporto HSM remoto {#configure-remote-hsm-support}

I moduli AEM utilizzano un meccanismo IPC/RPC basato su servizi Web. Questo meccanismo consente ai moduli AEM di utilizzare un HSM installato in un computer remoto. Per utilizzare questa funzionalità, installare il servizio Web nel computer remoto in cui è installato HSM. Consulta [Configurazione del supporto HSM per AEM Forms ES con Sun JDK su piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html)per ulteriori informazioni.

Questo meccanismo non supporta la creazione online di profili HSM o i controlli dello stato. Tuttavia, esistono due modi per creare profili HSM ed eseguire controlli dello stato:

* Creare un AEM per creare le credenziali del client trasmettendole il certificato del firmatario. Segui i passaggi descritti in [Configurazione del supporto HSM per AEM Forms ES con Sun JDK su piattaforma Windows a 64 bit](https://kb2.adobe.com/cps/808/cpsid_80835.html). Il percorso del servizio Web viene passato come proprietà Credential. È inoltre supportata la creazione di profili HSM offline utilizzando il gestore di certificati o l’esadecimale SHA-1 del certificato. Tuttavia, se hai effettuato l’aggiornamento ai moduli AEM da una versione precedente di moduli AEM, apporta modifiche al client perché le credenziali contenevano informazioni sul certificato e sul servizio Web.
* Il percorso del servizio Web è specificato nella console di amministrazione del servizio di firma. (vedere [Impostazioni del servizio di firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) In questo caso, il client conteneva solo l’alias del profilo HSM nell’archivio fonti attendibili. Puoi utilizzare questa opzione senza apportare alcuna modifica al client, anche se hai effettuato l’aggiornamento ai moduli AEM da una versione precedente dei moduli AEM. Questa opzione non supporta i profili HSM che utilizzano il certificato SHA-1.
