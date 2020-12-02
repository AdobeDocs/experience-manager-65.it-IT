---
title: Configurazione delle impostazioni di protezione
seo-title: Configurazione delle impostazioni di protezione
description: Scoprite come configurare le impostazioni di protezione.
seo-description: Scoprite come configurare le impostazioni di protezione.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 0%

---


# Configurazione delle impostazioni di protezione{#configuring-security-settings}

È possibile limitare l&#39;accesso ai documenti PDF impostando le password e limitando determinate funzioni, ad esempio la stampa e la modifica. Quando un documento PDF presenta funzioni limitate, gli strumenti e le voci di menu correlate a tali funzioni non sono disponibili. È inoltre possibile utilizzare altri metodi per creare documenti protetti, ad esempio per cifrare o certificare un documento. Un&#39;impostazione di protezione contiene la password e le opzioni specifiche da utilizzare per determinate conversioni PDF.

Nella pagina Impostazioni di protezione, potete effettuare le seguenti operazioni:

## Creare o modificare un&#39;impostazione di protezione {#create-or-edit-a-security-setting}

Le *impostazioni di protezione* controllano la protezione e le autorizzazioni per i file convertiti con tale impostazione di protezione.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Impostazioni di protezione.
1. Fate clic su Nuovo o fate clic sul nome di un’impostazione di protezione.
1. Nella pagina Nuova/Modifica impostazione di protezione, completate le informazioni necessarie per l’impostazione di protezione. (Vedere [Configurazione delle impostazioni dei tipi di file](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Fare clic su Salva e, nella finestra di dialogo visualizzata, digitare un nome per l&#39;impostazione, quindi fare clic su OK.

### Impostazioni di protezione {#security-settings}

Queste impostazioni configurano la compatibilità e la crittografia. Per istruzioni su come accedere alle impostazioni dei font, vedere [Creare o modificare un&#39;impostazione di protezione](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilità:** imposta il tipo di cifratura per l&#39;apertura di un documento protetto da password. L&#39;opzione  Acrobat 3.0 e versioni successive utilizza un livello di cifratura basso, mentre le altre opzioni utilizzano un livello di cifratura elevato:

**Acrobat 3.0 E Versioni Successive:** Utilizza crittografia bassa (RC4 a 40 bit).

**Acrobat 5.0 E Versioni Successive:** Utilizza la crittografia elevata (RC4 a 128 bit).

**Acrobat 6.0 E Versioni Successive:** Utilizza la crittografia elevata (RC4 a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca.

**Acrobat 7.0 E Versioni Successive:** utilizza la crittografia elevata (AES a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca e di cifrare solo gli allegati.

**Acrobat 9.0 E Versioni Successive:** utilizza la crittografia elevata (AES a 256 bit). Questa opzione consente di abilitare i metadati per la ricerca e di cifrare solo gli allegati.

Una versione precedente di  Acrobat non è in grado di aprire un documento PDF con un&#39;impostazione di compatibilità più elevata. Ad esempio, se selezionate l&#39;opzione  Acrobat 7.0 e versioni successive, non potete aprire il documento in  Acrobat 6.0 o versioni precedenti.

Assicurarsi che il livello di compatibilità sia coerente con il livello di compatibilità PDF per la stessa origine. Ad esempio, se disponete di una cartella esaminata configurata per l’utilizzo dell’impostazione PDF standard, compatibile con  Acrobat 5.0 o versione successiva, il livello di compatibilità di protezione non deve essere superiore a  Acrobat 5.0.

**Limitazione documento:** le limitazioni del documento disponibili dipendono dall&#39;opzione Compatibilità selezionata.

**Nessuna cifratura:** non esegue la cifratura di alcuna parte del documento.

**Cifra tutto il contenuto del documento:** Cifra il documento e i metadati del documento. Quando questa opzione è selezionata, i motori di ricerca non possono accedere ai metadati del documento.

**Cifra tutto il contenuto del documento tranne i metadati ( compatibile con Acrobat 6 e versioni successive):** Cifra il contenuto di un documento ma consente comunque ai motori di ricerca di accedere ai metadati del documento. Questa opzione è disponibile solo quando l&#39;opzione Compatibilità è impostata su  Acrobat 6.0 o versioni successive,  Acrobat 7.0 o versioni successive o  Acrobat 9.0 o versioni successive.

**Cifra solo gli allegati del file ( compatibile con Acrobat 7 e versioni successive):** gli utenti possono aprire il documento senza una password ma devono immettere una password per aprire gli allegati del file. Questa opzione è disponibile solo quando l&#39;opzione Compatibilità è impostata su  Acrobat 7.0 o versioni successive o su  Acrobat 9.0 o versioni successive.

Queste impostazioni configurano la protezione della password:

>[!NOTE]
>
>Se si dimentica una password, non può essere recuperata dal documento. Si consiglia di memorizzare le password in un&#39;altra posizione sicura nel caso in cui le si dimentichi. Inoltre, conservare una copia di backup del documento non protetta da password.

**Richiedi una password per aprire il documento:** abilita le opzioni della password.

**Password di apertura documento:** impedisce agli utenti di aprire il documento a meno che non immettano la password specificata. Per le password viene fatta distinzione tra maiuscole e minuscole.  Acrobat utilizza il metodo di protezione RC4 di RSA Security Inc. per proteggere i documenti PDF tramite password. Se si limitano la stampa e la modifica, è consigliabile aggiungere una password di apertura documento per migliorare la sicurezza.

**Ridigita password di apertura documento:** assicura che la password di apertura del documento sia corretta.

**Richiedi una password per aprire gli allegati del file:** abilita le opzioni della password. Questa opzione è disponibile solo quando l&#39;opzione Compatibilità è impostata su  Acrobat 7.0 o versioni successive o su  Acrobat 9.0 o versioni successive e l&#39;opzione Limitazione documento è impostata su Cifra solo allegati di file.

**Password di apertura allegato file:** assicura che sia necessaria una password per aprire un allegato del file. Gli utenti possono aprire il documento senza una password. Questa opzione è disponibile solo quando l&#39;opzione Compatibilità è impostata su  Acrobat 7.0 o versioni successive o su  Acrobat 9.0 o versioni successive e l&#39;opzione Limitazione documento è impostata su Cifra solo allegati di file.

**Ridigita allegato file:** verifica che la password sia corretta. Questa opzione è disponibile solo quando l&#39;opzione Compatibilità è impostata su  Acrobat 7.0 o versioni successive o su  Acrobat 9.0 o versioni successive e l&#39;opzione Limitazione documento è impostata su Cifra solo allegati di file.

Queste opzioni configurano le autorizzazioni:

**Usate Una Password Per Limitare La Stampa E La Modifica Del Documento E Le Relative Impostazioni Di Protezione:** Consente Di Limitare Le Autorizzazioni.

**Password autorizzazioni:** limita la stampa e la modifica degli utenti. Gli utenti non possono modificare queste impostazioni di protezione a meno che non immettano la password specificata. Non è possibile utilizzare la stessa password utilizzata per Password di apertura documento. Quando impostate una password di autorizzazione, solo gli utenti che digitano tale password possono modificare le impostazioni di protezione. Se il documento PDF dispone di entrambi i tipi di password, verrà aperta una delle due password. Tuttavia, un utente può impostare o modificare solo le funzioni limitate con la password delle autorizzazioni. Se il documento PDF dispone solo della password per l&#39;autorizzazione o se un utente apre il documento utilizzando la password di apertura del documento, quando l&#39;utente tenta di modificare le impostazioni di protezione viene visualizzato un prompt con la password.

**Ridigita password autorizzazioni:** verifica che la password delle autorizzazioni sia corretta.

**Stampa consentita:** specifica la qualità di stampa del documento PDF:

**Nessuno:** impedisce agli utenti di stampare il documento.

**Bassa risoluzione (150 dpi):** consente agli utenti di stampare il documento con una risoluzione non superiore a 150 dpi. La stampa potrebbe risultare più lenta, in quanto ogni pagina viene stampata come immagine bitmap. Questa opzione è disponibile solo se è selezionato un livello di cifratura elevato ( Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta risoluzione:** consente agli utenti di stampare a qualsiasi risoluzione, indirizzando l&#39;output vettoriale di alta qualità a PostScript e altre stampanti che supportano funzioni di stampa avanzate di alta qualità.

**Modifiche consentite:** Definisce le azioni di modifica consentite nel documento PDF:

**Nessuno:** impedisce agli utenti di modificare il documento, inclusa la compilazione dei campi firma e del modulo.

**Inserimento, eliminazione e rotazione delle pagine:** consente agli utenti di inserire, eliminare e ruotare le pagine, nonché creare segnalibri e pagine di miniature. Questa opzione è disponibile solo se è selezionato un livello di cifratura elevato ( Acrobat 5.0, 6.0, 7.0 o 9.0).

**Compilazione Di Campi Modulo E Firma Di Campi Firma Esistenti:** Consente Agli Utenti Di Compilare Moduli E Aggiungere Firme Digitali. Tuttavia, gli utenti non possono aggiungere commenti o creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di cifratura elevato ( Acrobat 5.0, 6.0, 7.0 o 9.0).

**Creazione Di Commenti, Compilazione Di Campi Modulo E Firma Di Campi Firma Esistenti:** Consente Agli Utenti Di Compilare Moduli E Aggiungere Firme E Commenti Digitali.

**Layout pagina, Ritocco, Compilazione di campi modulo e firma di campi firma esistenti:** Consente agli utenti di inserire, ruotare o eliminare pagine e creare segnalibri o immagini in miniatura, compilare moduli e aggiungere firme digitali. Questa opzione non consente agli utenti di creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di cifratura basso ( Acrobat 3.0).

**Qualsiasi tranne l’estrazione di pagine:** consente agli utenti di modificare il documento utilizzando qualsiasi metodo presente nel Elenco Consentiti Modifiche , ad eccezione delle pagine rimosse.

**Abilita copia di testo, immagini e altro contenuto:** consente agli utenti di selezionare e copiare il contenuto del documento PDF. Consente inoltre alle utility che devono accedere ai contenuti di un file PDF, come  Acrobat Catalog, di accedervi. Questa opzione è disponibile solo se è selezionato un livello di cifratura elevato.

**Attiva l&#39;accesso al testo dei dispositivi di Reader per gli ipovedenti:** consente agli utenti con problemi di vista di leggere il documento utilizzando gli assistenti vocali. Tuttavia, gli utenti non possono copiare o estrarre il contenuto del documento. Questa opzione è disponibile solo se è selezionato un livello di cifratura elevato.

## Eliminare un&#39;impostazione di protezione {#delete-a-security-setting}

È possibile eliminare un&#39;impostazione di protezione se non è più necessaria. Tuttavia, le impostazioni di protezione preconfigurate non possono essere eliminate.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > PDF Generator > Security Settings]**.
1. Selezionate la casella accanto all’impostazione da eliminare. Potete selezionare più impostazioni.
1. Fare clic su **[!UICONTROL Elimina]** e, nella pagina **[!UICONTROL Elimina conferma]**, fare di nuovo clic su **[!UICONTROL Elimina]**.

