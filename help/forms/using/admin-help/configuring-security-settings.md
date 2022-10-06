---
title: Configurazione delle impostazioni di protezione
seo-title: Configuring security settings
description: Scopri come configurare le impostazioni di protezione.
seo-description: Learn how to configure security settings.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: PDF Generator
exl-id: be076477-2681-4570-953d-6c44d3c30843
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Configurazione delle impostazioni di protezione{#configuring-security-settings}

È possibile limitare l’accesso ai documenti PDF impostando le password e limitando alcune funzioni, ad esempio la stampa e la modifica. Quando un documento PDF dispone di funzioni limitate, gli strumenti e le voci di menu correlati a tali funzioni sono disattivati. È inoltre possibile utilizzare altri metodi per creare documenti protetti, ad esempio per cifrare o certificare un documento. Un&#39;impostazione di sicurezza contiene la password e le opzioni specifiche da utilizzare per alcune conversioni di PDF.

Nella pagina Impostazioni protezione è possibile effettuare le seguenti operazioni:

## Creare o modificare un’impostazione di protezione {#create-or-edit-a-security-setting}

A *impostazione di sicurezza* controlla la protezione e le autorizzazioni per i file convertiti con tale impostazione di protezione.

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > Impostazioni di protezione.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione di protezione.
1. Nella pagina Nuova/Modifica impostazione di protezione , completa le informazioni richieste per l’impostazione di protezione. (Vedi [Configurazione delle impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Fare clic su Salva e, nella finestra di dialogo visualizzata, digitare un nome per l&#39;impostazione, quindi fare clic su OK.

### Impostazioni di protezione {#security-settings}

Queste impostazioni configurano la compatibilità e la crittografia. Per istruzioni su come accedere alle impostazioni dei font, consulta [Creare o modificare un’impostazione di protezione](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilità:** Imposta il tipo di crittografia per l&#39;apertura di un documento protetto da password. L’opzione Acrobat 3.0 e versioni successive utilizza un livello di crittografia basso, ma le altre opzioni utilizzano un livello di crittografia elevato:

**Acrobat 3.0 E Versioni Successive:** Utilizza crittografia bassa (RC4 a 40 bit).

**Acrobat 5.0 E Versioni Successive:** Utilizza la crittografia elevata (RC4 a 128 bit).

**Acrobat 6.0 E Versioni Successive:** Utilizza la crittografia elevata (RC4 a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca.

**Acrobat 7.0 E Versioni Successive:** Utilizza la crittografia elevata (AES a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo gli allegati di file.

**Acrobat 9.0 E Versioni Successive:** Utilizza la crittografia elevata (AES a 256 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo gli allegati di file.

Una versione precedente di Acrobat non può aprire un documento PDF con un’impostazione di compatibilità più elevata. Ad esempio, se selezioni l’opzione Acrobat 7.0 E versioni successive, non puoi aprire il documento in Acrobat 6.0 o versioni precedenti.

Assicurati che il livello di compatibilità sia coerente con il livello di compatibilità PDF per la stessa origine. Ad esempio, se disponi di una cartella di controllo configurata per utilizzare l’impostazione Standard PDF, compatibile con Acrobat 5.0 o versione successiva, il livello di compatibilità di sicurezza non deve essere superiore a Acrobat 5.0.

**Restrizione documento:** Le limitazioni dei documenti disponibili dipendono dall’opzione Compatibilità selezionata.

**Nessuna crittografia:** Non crittografa alcuna parte del documento.

**Cifra tutto il contenuto del documento:** Cifra il documento e i metadati del documento. Quando questa opzione è selezionata, i motori di ricerca non possono accedere ai metadati del documento.

**Cifra Tutto Il Contenuto Del Documento Ad Eccezione Dei Metadati (Acrobat 6 E Versioni Successive Compatibili):** Cifra il contenuto di un documento, ma consente comunque ai motori di ricerca di accedere ai metadati del documento. Questa opzione è disponibile solo quando l’opzione Compatibilità è impostata su Acrobat 6.0 o versioni successive, Acrobat 7.0 o versioni successive o Acrobat 9.0 o versioni successive.

**Cifra Solo Allegati Di File (Compatibili Con Acrobat 7 E Versioni Successive):** Gli utenti possono aprire il documento senza una password ma devono immettere una password per aprire gli allegati dei file. Questa opzione è disponibile solo quando l’opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva oppure su Acrobat 9.0 o versione successiva.

Queste impostazioni configurano la protezione tramite password:

>[!NOTE]
>
>Se si dimentica una password, non può essere recuperata dal documento. Si consiglia di memorizzare le password in un&#39;altra posizione sicura nel caso in cui le si dimentichi. Inoltre, conservare una copia di backup del documento non protetta da password.

**Richiedi Una Password Per Aprire Il Documento:** Abilita le opzioni della password.

**Password di apertura documento:** Impedisce agli utenti di aprire il documento a meno che non digitino la password specificata. Le password distinguono tra maiuscole e minuscole. Acrobat utilizza il metodo di sicurezza RC4 di RSA Security Inc. per proteggere i documenti PDF tramite password. Se si limitano la stampa e la modifica, è consigliabile aggiungere una password di apertura del documento per migliorare la sicurezza.

**Ridigitare la password di apertura documento:** Assicurarsi che la password di apertura del documento sia corretta.

**Richiedi Una Password Per Aprire Gli Allegati Di File:** Abilita le opzioni della password. Questa opzione è disponibile solo quando l’opzione Compatibilità è impostata su Acrobat 7.0 o versioni successive o su Acrobat 9.0 o versioni successive e l’opzione Restrizione documento è impostata su Cifra solo allegati di file.

**Password di apertura file allegato:** Assicurati che sia necessaria una password per aprire un file allegato. Gli utenti possono aprire il documento senza una password. Questa opzione è disponibile solo quando l’opzione Compatibilità è impostata su Acrobat 7.0 o versioni successive o su Acrobat 9.0 o versioni successive e l’opzione Restrizione documento è impostata su Cifra solo allegati di file.

**Ridigita allegato file:** Verifica che la password sia corretta. Questa opzione è disponibile solo quando l’opzione Compatibilità è impostata su Acrobat 7.0 o versioni successive o su Acrobat 9.0 o versioni successive e l’opzione Restrizione documento è impostata su Cifra solo allegati di file.

Queste opzioni configurano le autorizzazioni:

**Utilizzare Una Password Per Limitare La Stampa E La Modifica Del Documento E Delle Relative Impostazioni Di Sicurezza:** Abilita restrizioni alle autorizzazioni.

**Password autorizzazioni:** Limita la stampa e la modifica degli utenti. Gli utenti non possono modificare queste impostazioni di protezione a meno che non digitino la password specificata. Non è possibile utilizzare la stessa password utilizzata per la password di apertura documento. Quando si imposta una password di autorizzazione, solo le persone che digitano la password possono modificare le impostazioni di protezione. Se il documento PDF dispone di entrambi i tipi di password, verrà aperto da una delle due password. Tuttavia, un utente può solo impostare o modificare le funzioni limitate con la password delle autorizzazioni. Se il documento PDF dispone solo della password di autorizzazione o se un utente apre il documento utilizzando la password di apertura del documento, quando l’utente tenta di modificare le impostazioni di protezione viene visualizzato il prompt della password.

**Digitare nuovamente la password delle autorizzazioni:** Verifica che la password delle autorizzazioni sia corretta.

**Stampa consentita:** Specifica la qualità di stampa del documento PDF:

**Nessuno:** Impedisce agli utenti la stampa del documento.

**Bassa risoluzione (150 dpi):** Consente agli utenti di stampare il documento con una risoluzione non superiore a 150 dpi. La stampa può essere più lenta perché ogni pagina viene stampata come immagine bitmap. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta risoluzione:** Consente agli utenti di stampare a qualsiasi risoluzione, indirizzando l&#39;uscita vettoriale di alta qualità a PostScript e ad altre stampanti che supportano funzioni di stampa avanzate di alta qualità.

**Modifiche consentite:** Definisce quali azioni di modifica sono consentite nel documento PDF:

**Nessuno:** Impedisce agli utenti la modifica del documento, inclusa la compilazione di campi firma e modulo.

**Inserimento, Eliminazione E Rotazione Delle Pagine:** Consente agli utenti di inserire, eliminare e ruotare le pagine, nonché di creare segnalibri e miniature. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Compilazione Di Campi Modulo E Firma Di Campi Firma Esistenti:** Consente agli utenti di compilare i moduli e aggiungere firme digitali. Tuttavia, gli utenti non possono aggiungere commenti o creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Creazione Di Commenti, Compilazione Di Campi Modulo E Firma Di Campi Firma Esistenti:** Consente agli utenti di compilare moduli e aggiungere firme digitali e commenti.

**Layout Di Pagina, Ritocco, Compilazione Di Campi Modulo E Firma Di Campi Firma Esistenti:** Consente agli utenti di inserire, ruotare o eliminare pagine e creare segnalibri o immagini in miniatura, compilare moduli e aggiungere firme digitali. Questa opzione non consente agli utenti di creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di crittografia basso (Acrobat 3.0).

**Ad Eccezione Dell’Estrazione Delle Pagine:** Consente agli utenti di modificare il documento utilizzando qualsiasi metodo nell&#39;Elenco Consentiti Modifiche, ad eccezione delle pagine di rimozione.

**Abilita Copia Di Testo, Immagini E Altri Contenuti:** Consente agli utenti di selezionare e copiare il contenuto del documento di PDF. Consente inoltre alle utilità che necessitano di accesso al contenuto di un file PDF, come Acrobat Catalog, di accedervi. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato.

**Abilitare L’Accesso Al Testo Dei Dispositivi Di Reader Per I Disabili Visivi:** Consente agli utenti con problemi di vista di leggere il documento utilizzando assistenti vocali. Tuttavia, gli utenti non possono copiare o estrarre il contenuto del documento. Questa opzione è disponibile solo se è selezionato un livello di crittografia elevato.

## Eliminare un’impostazione di protezione {#delete-a-security-setting}

Se non è più necessario, è possibile eliminare un’impostazione di protezione. Tuttavia, le impostazioni di protezione preconfigurate non possono essere eliminate.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator > Impostazioni di sicurezza]**.
1. Seleziona la casella di controllo accanto all’impostazione da eliminare. È possibile selezionare più impostazioni.
1. Fai clic su **[!UICONTROL Elimina]** e **[!UICONTROL Conferma eliminazione]** pagina, fai clic su **[!UICONTROL Elimina]** di nuovo.
