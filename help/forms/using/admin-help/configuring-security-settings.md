---
title: Configurare le impostazioni di protezione
description: Scopri come configurare le impostazioni di protezione. Puoi proteggere i documenti PDF limitandone l’accesso. Puoi crittografare, certificare o proteggere il documento tramite password.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator,Document Security
exl-id: be076477-2681-4570-953d-6c44d3c30843
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 88%
---
# Configurare le impostazioni di protezione{#configuring-security-settings}

Puoi limitare l’accesso ai documenti PDF impostando una password e limitando alcune funzionalità, ad esempio la stampa e la modifica. Quando un documento PDF dispone di funzioni limitate, gli strumenti e le voci di menu correlati a tali funzioni vengono disattivati. È inoltre possibile utilizzare altri metodi per creare documenti protetti, ad esempio la crittografia o la certificazione di un documento. Un’impostazione di protezione contiene la password e le opzioni specifiche da utilizzare per determinate conversioni di PDF.

Nella pagina Impostazioni di protezione puoi eseguire le operazioni seguenti:

## Creare o modificare un’impostazione di protezione {#create-or-edit-a-security-setting}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Un’*impostazione di protezione* controlla la protezione e le autorizzazioni per i file convertiti con tale impostazione di protezione.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni di protezione.
1. Fai clic su Nuova o sul nome di un&#39;impostazione di protezione.
1. Nella pagina Nuova/Modifica impostazione di protezione immetti le informazioni richieste per l’impostazione di protezione. (Consulta [Configurazione delle impostazioni tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Fai clic su Salva e nella finestra di dialogo visualizzata digita un nome per l’impostazione, quindi fai clic su OK.

### Impostazioni di protezione {#security-settings}

Queste impostazioni configurano la compatibilità e la crittografia. Per istruzioni sull’accesso alle impostazioni dei font, consulta [Creare o modificare un’impostazione di protezione](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilità:** imposta il tipo di crittografia per l’apertura di un documento protetto da password. L’opzione Acrobat 3.0 e versioni successive utilizza un livello di crittografia basso, mentre le altre opzioni utilizzano un livello di crittografia elevato:

**Acrobat 3.0 e versioni successive:** utilizza un livello di crittografia basso (RC4 a 40 bit).

**Acrobat 5.0 e versioni successive:** utilizza un livello di crittografia elevato (RC4 a 128 bit).

**Acrobat 6.0 e versioni successive:** utilizza un livello di crittografia elevato (RC4 a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca.

**Acrobat 7.0 e versioni successive:** utilizza un livello di crittografia elevato (AES a 128 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo i file allegati.

**Acrobat 9.0 e versioni successive:** utilizza un livello di crittografia elevato (AES a 256 bit). Questa opzione consente di abilitare i metadati per la ricerca e di crittografare solo i file allegati.

Una versione precedente di Acrobat non può aprire un documento PDF con un’impostazione di compatibilità superiore. Se, ad esempio, selezioni l’opzione Acrobat 7.0 e versioni successive, non sarà possibile aprire il documento in Acrobat 6.0 o versioni precedenti.

Assicurati che il livello di compatibilità sia coerente con il livello di compatibilità del PDF per la stessa origine. Se, ad esempio, disponi di una cartella controllata configurata per utilizzare l’impostazione PDF standard, che è compatibile con Acrobat 5.0 o versione successiva, il livello di compatibilità della protezione non deve essere superiore a Acrobat 5.0.

**Limitazione documento:** le limitazioni del documento disponibili dipendono dall’opzione di compatibilità che hai selezionato.

**Nessuna crittografia:** nessuna parte del documento viene crittografata.

**Crittografa tutto il contenuto del documento:** il documento e i metadati del documento vengono crittografati. Quando questa opzione è selezionata, i motori di ricerca non possono accedere ai metadati del documento.

**Crittografa tutto il contenuto del documento tranne i metadati (Acrobat
6 And Later Compatible):** Crittografa il contenuto di un documento, ma consente comunque ai motori di ricerca di accedere ai metadati del documento. Questa opzione è disponibile solo se l’opzione Compatibilità è impostata su Acrobat 6.0 o versioni successive, Acrobat 7.0 o versioni successive oppure Acrobat 9.0 o versioni successive.

**Crittografa Solo File Allegati (Acrobat 7 E Versioni Successive)
Compatibile):** Gli utenti possono aprire il documento senza una password, ma devono immettere una password per aprire i file allegati. Questa opzione è disponibile solo se l’opzione Compatibilità è impostata su Acrobat 7.0 o versioni successive o su Acrobat 9.0 o versioni successive.

Queste impostazioni configurano la protezione della password:

>[!NOTE]
>
>Se dimentichi una password, non potrai recuperarla dal documento. È consigliabile conservare le password in un luogo sicuro nel caso in cui vengano dimenticate. Conserva inoltre una copia di backup del documento non protetta da password.

**Richiedi una password per aprire il documento:** abilita le opzioni della password.

**Password di apertura del documento:** impedisce agli utenti di aprire il documento a meno che non digitino la password da te specificata. Le password distinguono tra maiuscole e minuscole. Acrobat utilizza il metodo RC4 di protezione di RSA Security Inc. per proteggere i documenti PDF tramite password. Se desideri limitare la stampa e la modifica, aggiungi una password di apertura documento per migliorare la protezione.

**Ripeti password di apertura documento:** verifica che la password di apertura del documento sia corretta.

**Richiedi una password per aprire i file allegati:** abilita le opzioni della password. Questa opzione è disponibile solo se l’opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l’opzione di restrizione Documento è impostata su Crittografa solo allegati file.

**Password apertura file allegato:** assicura che sia necessaria una password per aprire un file allegato. Gli utenti possono aprire il documento senza una password. Questa opzione è disponibile solo se l’opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l’opzione di restrizione Documento è impostata su Crittografa solo allegati file.

**Ripeti password file allegato:** verifica che la password sia corretta. Questa opzione è disponibile solo se l’opzione Compatibilità è impostata su Acrobat 7.0 o versione successiva o su Acrobat 9.0 o versione successiva e l’opzione di restrizione Documento è impostata su Crittografa solo allegati file.

Queste opzioni configurano le autorizzazioni:

**Utilizzare Una Password Per Limitare La Stampa E La Modifica Di
Il documento e le relative impostazioni di protezione:** abilita le restrizioni alle autorizzazioni.

**Password autorizzazioni:** impedisce agli utenti di stampare e modificare. Gli utenti non possono modificare queste impostazioni di protezione a meno che non digitino la password specificata. Non è possibile utilizzare la stessa password utilizzata per la password di apertura del documento. Quando imposti una password di autorizzazione, solo gli utenti che digitano tale password possono modificare le impostazioni di protezione. Se il documento PDF dispone di entrambi i tipi di password, verrà aperto da una delle password. Tuttavia, un utente può solo impostare o modificare le funzioni con restrizioni con la password delle autorizzazioni. Se il documento PDF dispone solo della password di autorizzazione o se un utente apre il documento utilizzando la password di apertura del documento, quando l’utente tenta di modificare le impostazioni di sicurezza viene visualizzata la richiesta di password.

**Ripeti password di apertura documento:** verifica che la password di autorizzazione del documento sia corretta.

**Stampa consentita:** specifica la qualità di stampa per il documento PDF:

**Nessuna:** impedisce agli utenti di stampare il documento.

**Bassa risoluzione (150 dpi):** consente agli utenti di stampare il documento con una risoluzione non superiore a 150 dpi. La stampa potrebbe essere più lenta perché ogni pagina viene stampata come immagine bitmap. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta risoluzione:** consente agli utenti di stampare a qualsiasi risoluzione, indirizzando output vettoriale di alta qualità a PostScript e ad altre stampanti che supportano funzionalità di stampa avanzate di alta qualità.

**Modifiche consentite:** definisce le azioni di modifica consentite nel documento di PDF:

**Nessuna:** impedisce agli utenti di modificare il documento, inclusa la compilazione di campi firma e modulo.

**Inserimento, eliminazione e rotazione di pagine:** consente agli utenti di inserire, eliminare e ruotare pagine e di creare segnalibri e pagine in miniatura. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Compilazione Dei Campi Del Modulo E Firma Della Firma Esistente
Campi:** Consente agli utenti di compilare moduli e aggiungere firme digitali. Tuttavia, gli utenti non possono aggiungere commenti o creare campi modulo. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Commento, Compilazione Dei Campi Del Modulo E Firma Esistente
Campi firma:** Consente agli utenti di compilare moduli e aggiungere firme digitali e commenti.

**Layout Di Pagina, Ritocco, Compilazione Dei Campi Del Modulo E Firma
Campi firma esistenti:** consente agli utenti di inserire, ruotare o eliminare pagine e creare segnalibri o miniature, compilare moduli e aggiungere firme digitali. Questa opzione non consente agli utenti di creare campi modulo. Questa opzione è disponibile solo se è selezionato un livello di crittografia basso (Acrobat 3.0).

**Qualsiasi eccezione durante l’estrazione delle pagine:** consente agli utenti di modificare il documento utilizzando qualsiasi metodo nell’elenco Modifiche consentite, ad eccezione della rimozione delle pagine.

**Abilita la copia di testo, immagini e altro contenuto:** consente agli utenti di selezionare e copiare il contenuto del documento PDF. Consente inoltre alle utility che hanno bisogno di accedere ai contenuti di un file PDF, come Acrobat Catalog, di accedere a tali contenuti. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato.

**Abilita L&#39;Accesso Di Testo Ai Dispositivi Reader Per Schermo Per
Ipovedenti:** Consente agli utenti con problemi di vista di leggere il documento utilizzando utilità per la lettura dello schermo. Tuttavia, gli utenti non possono copiare o estrarre il contenuto del documento. Questa opzione è disponibile solo se è stato selezionato un livello di crittografia elevato.

## Eliminare un’impostazione di protezione {#delete-a-security-setting}

Se non è più necessaria, puoi eliminare un’impostazione di protezione. Non è possibile tuttavia eliminare le impostazioni di protezione preconfigurate.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator > Impostazioni di protezione]**.
1. Seleziona la casella di controllo accanto all’impostazione da eliminare. Puoi selezionare più impostazioni.
1. Fai clic su **[!UICONTROL Elimina]** e nella pagina **[!UICONTROL Conferma eliminazione]** fai di nuovo clic su **[!UICONTROL Elimina]**.
