---
title: Configurazione delle impostazioni di protezione
description: Scopri come configurare le impostazioni di sicurezza. È possibile proteggere i documenti di PDF limitando l’accesso. È possibile crittografare, certificare o proteggere il documento tramite password.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator,Document Security
exl-id: be076477-2681-4570-953d-6c44d3c30843
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Configurazione delle impostazioni di protezione{#configuring-security-settings}

È possibile limitare l&#39;accesso ai documenti PDF impostando password e limitando alcune funzionalità, ad esempio la stampa e la modifica. Quando un documento PDF dispone di funzioni limitate, gli strumenti e le voci di menu correlati a tali funzioni vengono disattivati. È inoltre possibile utilizzare altri metodi per creare documenti protetti, ad esempio la crittografia o la certificazione di un documento. Un&#39;impostazione di protezione contiene la password e le opzioni specifiche da utilizzare per determinate conversioni di PDF.

Nella pagina Impostazioni protezione è possibile eseguire le operazioni seguenti:

## Creare o modificare un&#39;impostazione di protezione {#create-or-edit-a-security-setting}

Un&#39;impostazione di protezione ** controlla la protezione e le autorizzazioni per i file convertiti con tale impostazione di protezione.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni di sicurezza.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione di protezione.
1. Nella pagina Nuova/Modifica impostazione di protezione immettere le informazioni richieste per l&#39;impostazione di protezione. (Vedi [Configurazione delle impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Fare clic su Salva e nella finestra di dialogo visualizzata digitare un nome per l&#39;impostazione e quindi fare clic su OK.

### Impostazioni di protezione {#security-settings}

Queste impostazioni configurano la compatibilità e la crittografia. Per istruzioni sull&#39;accesso alle impostazioni dei caratteri, vedere [Creare o modificare un&#39;impostazione di protezione](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilità:** Imposta il tipo di crittografia per l&#39;apertura di un documento protetto da password. L’opzione Acrobat 3.0 e versioni successive utilizza un livello di crittografia basso, mentre le altre opzioni utilizzano un livello di crittografia elevato:

**Acrobat 3.0 E versioni successive:** utilizza una crittografia bassa (RC4 a 40 bit).

**Acrobat 5.0 E versioni successive:** utilizza la crittografia elevata (RC4 a 128 bit).

**Acrobat 6.0 E versioni successive:** utilizza la crittografia elevata (RC4 a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca.

**Acrobat 7.0 E versioni successive:** utilizza la crittografia elevata (AES a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo gli allegati.

**Acrobat 9.0 E versioni successive:** utilizza la crittografia elevata (AES a 256 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo gli allegati.

Una versione precedente di Acrobat non può aprire un documento PDF con un&#39;impostazione di compatibilità superiore. Se ad esempio si seleziona l&#39;opzione Acrobat 7.0 e versioni successive, non sarà possibile aprire il documento in Acrobat 6.0 o versioni precedenti.

Assicurati che il livello di compatibilità sia coerente con il livello di compatibilità PDF per la stessa origine. Ad esempio, se hai una cartella controllata configurata per utilizzare l’impostazione Standard PDF, compatibile con Acrobat 5.0 o versione successiva, il livello di compatibilità della sicurezza non deve essere superiore a Acrobat 5.0.

**Limitazione documento:** Le restrizioni dei documenti disponibili dipendono dall&#39;opzione di compatibilità selezionata.

**Nessuna crittografia:** non crittografa alcuna parte del documento.

**Crittografa tutto il contenuto del documento:** Crittografa il documento e i metadati del documento. Quando questa opzione è selezionata, i motori di ricerca non possono accedere ai metadati del documento.

**Crittografa tutto il contenuto del documento tranne i metadati (Acrobat
6 And Later Compatible):** Crittografa il contenuto di un documento, ma consente comunque ai motori di ricerca di accedere ai metadati del documento. Questa opzione è disponibile solo se l&#39;opzione Compatibilità è impostata su Acrobat 6.0 o versione successiva, Acrobat 7.0 o versione successiva oppure Acrobat 9.0 o versione successiva.

**Crittografa Solo File Allegati (Acrobat 7 E Versioni Successive
Compatibile):** Gli utenti possono aprire il documento senza una password, ma devono immettere una password per aprire i file allegati. Questa opzione è disponibile solo se l&#39;opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva.

Queste impostazioni configurano la protezione della password:

>[!NOTE]
>
>Se si dimentica una password, non sarà possibile recuperarla dal documento. Si consiglia di memorizzare le password in un&#39;altra posizione sicura nel caso in cui vengano dimenticate. Mantenere inoltre una copia di backup del documento non protetta da password.

**Richiedi Password Per Aprire Il Documento:** Abilita Le Opzioni Password.

**Password apertura documento:** Impedisce agli utenti di aprire il documento a meno che non digitino la password specificata. Le password distinguono tra maiuscole e minuscole. Acrobat utilizza il metodo RC4 di protezione di RSA Security Inc. per proteggere i documenti PDF tramite password. Se si desidera limitare la stampa e la modifica, è consigliabile aggiungere una password di apertura documento per migliorare la protezione.

**Password apertura documento Retype:** Verifica che la password di apertura del documento sia corretta.

**Richiedi una password per aprire i file allegati:** Abilita le opzioni della password. Questa opzione è disponibile solo se l&#39;opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l&#39;opzione di restrizione Documento è impostata su Crittografa solo allegati file.

**Password apertura file allegato:** assicura che sia necessaria una password per aprire un file allegato. Gli utenti possono aprire il documento senza una password. Questa opzione è disponibile solo se l&#39;opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l&#39;opzione di restrizione Documento è impostata su Crittografa solo allegati file.

**File allegato Retype:** verifica che la password sia corretta. Questa opzione è disponibile solo se l&#39;opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l&#39;opzione di restrizione Documento è impostata su Crittografa solo allegati file.

Queste opzioni configurano le autorizzazioni:

**Utilizzare Una Password Per Limitare La Stampa E La Modifica Di
Il documento e le relative impostazioni di protezione:** abilita le restrizioni alle autorizzazioni.

**Password autorizzazioni:** impedisce agli utenti di stampare e modificare. Gli utenti non possono modificare queste impostazioni di protezione a meno che non digitino la password specificata. Non è possibile utilizzare la stessa password utilizzata per la password di apertura documento. Quando si imposta una password di autorizzazione, solo gli utenti che digitano tale password possono modificare le impostazioni di protezione. Se il documento PDF dispone di entrambi i tipi di password, verrà aperto con una password. Tuttavia, un utente può solo impostare o modificare le funzioni con restrizioni con la password delle autorizzazioni. Se il documento PDF dispone solo della password di autorizzazione o se un utente apre il documento utilizzando la password di apertura del documento, la richiesta della password viene visualizzata quando l&#39;utente tenta di modificare le impostazioni di protezione.

**Password autorizzazioni Retype:** Verifica che la password delle autorizzazioni sia corretta.

**Stampa consentita:** Specifica la qualità di stampa del documento PDF:

**Nessuno:** impedisce agli utenti di stampare il documento.

**Bassa risoluzione (150 dpi):** consente agli utenti di stampare il documento con una risoluzione non superiore a 150 dpi. La stampa potrebbe essere più lenta perché ogni pagina viene stampata come immagine bitmap. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta risoluzione:** consente agli utenti di stampare a qualsiasi risoluzione, indirizzando output vettoriale di alta qualità a PostScript e ad altre stampanti che supportano funzionalità di stampa avanzate di alta qualità.

**Modifiche consentite:** definisce le azioni di modifica consentite nel documento di PDF:

**Nessuno:** Impedisce agli utenti di modificare il documento, inclusa la compilazione di campi firma e modulo.

**Inserimento, eliminazione e rotazione di pagine:** consente agli utenti di inserire, eliminare e ruotare pagine e di creare segnalibri e pagine di miniature. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Compilazione Dei Campi Del Modulo E Firma Della Firma Esistente
Campi:** consente agli utenti di compilare moduli e aggiungere firme digitali. Tuttavia, gli utenti non possono aggiungere commenti o creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Commento, Compilazione Dei Campi Del Modulo E Firma Esistente
Campi firma:** consente agli utenti di compilare moduli e aggiungere firme digitali e commenti.

**Layout Di Pagina, Ritocco, Compilazione Dei Campi Del Modulo E Firma
Campi firma esistenti:** consente agli utenti di inserire, ruotare o eliminare pagine e creare segnalibri o miniature, compilare moduli e aggiungere firme digitali. Questa opzione non consente agli utenti di creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di crittografia basso (Acrobat 3.0).

**Qualsiasi eccezione durante l&#39;estrazione delle pagine:** Consente agli utenti di modificare il documento utilizzando qualsiasi metodo nell&#39;Elenco Consentiti Modifiche, ad eccezione della rimozione delle pagine.

**Abilita la copia di testo, immagini e altro contenuto:** consente agli utenti di selezionare e copiare il contenuto del documento PDF. Consente inoltre alle utility che hanno bisogno di accedere ai contenuti di un file PDF, come Acrobat Catalog, di accedere a tali contenuti. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato.

**Abilita L&#39;Accesso Al Testo Dei Dispositivi Di Reader Dello Schermo Per
Ipovedenti:** Consente agli utenti con problemi di vista di leggere il documento utilizzando utilità per la lettura dello schermo. Tuttavia, gli utenti non possono copiare o estrarre il contenuto del documento. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato.

## Eliminare un&#39;impostazione di protezione {#delete-a-security-setting}

Se non è più necessaria, è possibile eliminare un&#39;impostazione di protezione. Non è tuttavia possibile eliminare le impostazioni di protezione preconfigurate.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > PDF Generator > Impostazioni protezione]**.
1. Selezionare la casella di controllo accanto all&#39;impostazione da eliminare. È possibile selezionare più impostazioni.
1. Fai clic su **[!UICONTROL Elimina]** e nella pagina **[!UICONTROL Conferma eliminazione]** fai di nuovo clic su **[!UICONTROL Elimina]**.
