---
title: Come si generano e funzionano gli hash nei PDF forms dinamici?
description: Generazione e utilizzo degli hash nei PDF forms dinamici
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Generazione e utilizzo degli hash nei PDF forms dinamici {#generate-work-with-hashes-dynamic-pdf-forms}


## Conoscenze preliminari {#prerequisite-knowledge}

È necessaria una certa esperienza con AEM Forms su JEE Designer, così come la possibilità di accedere e chiamare funzioni in oggetti script.

## Livello utente {#user-level}

Inizio

Quando si desidera nascondere una password nel modulo PDF senza inserirla in testo non crittografato nel codice sorgente o in qualsiasi altro punto del documento PDF, è fondamentale sapere come generare e utilizzare gli hash MD4, MD5, SHA-1 e SHA-256.

L’idea è quella di oscurare la password generando un hash univoco e archiviarlo nel documento di PDF. Questo hash univoco può essere generato da diverse funzioni hash. In questo articolo ti mostrerò come generarli all’interno del modulo PDF e come utilizzarli.

Una funzione hash accetta come input una stringa lunga (o messaggio) di qualsiasi lunghezza e produce come output una stringa di lunghezza fissa, a volte denominata message digest o impronta digitale.

AEM Forms su JEE Designer consente di implementare le diverse funzioni hash negli oggetti script come JavaScript ed eseguirle all’interno di un documento Dynamic PDF. I PDF di esempio inclusi nei file di esempio per questo articolo utilizzano implementazioni open source delle seguenti funzioni hash:

* MD4 e MD5 - progettati da Ronald Rivest

* SHA-1 e SHA-256 - definiti dal NIST

Il principale vantaggio dell’utilizzo degli hash è che non è necessario confrontare direttamente le password confrontando stringhe di testo non crittografate, ma è possibile confrontare i due hash delle due password. Poiché è molto improbabile che due stringhe diverse abbiano lo stesso hash, se entrambi gli hash sono identici, puoi supporre che anche le stringhe confrontate (in questo caso, le password) siano identiche.

>[!NOTE]
>
>Esistono alcuni noti problemi di sicurezza (cosiddetti conflitti hash) con MD4 o MD5. A causa di queste collisioni di hash e di altri hack SHA-1 (inclusi i tavoli arcobaleno), ho deciso di concentrarmi sulla funzione di hash SHA-256 nel secondo campione.  Per ulteriori informazioni, vedere [Collisione](https://en.wikipedia.org/wiki/Hash_collision) e [Tavola arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table) pagine da Wikipedia.

## Analisi degli oggetti script {#examining-script-objects}

Quando apri uno dei due esempi forniti in AEM Forms su JEE Designer, troverai i quattro oggetti script nella palette Gerarchia (vedi la Figura seguente).

![Variabili](assets/variables.jpg)

Per visualizzare l&#39;implementazione JavaScript delle funzioni hash all&#39;interno di questi oggetti script, selezionare l&#39;oggetto script ed esplorare il codice nell&#39;editor di script.  Puoi vedere come sono state implementate le seguenti funzioni hash:

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

Come puoi vedere da questo elenco, sono disponibili diverse funzioni per i diversi tipi di output dell’hash. Puoi scegliere tra `hex_` per le cifre esadecimali, `b64_` per output con codifica Base64, o `str_` per la codifica di stringhe semplice.

A seconda della funzione di hash scelta, la lunghezza dell’hash varia:

* MD4: 128 bit
* MD5: 128 bit
* SHA-1: 160 bit
* SHA-256: 256 bit

## Prova dei PDF forms di esempio {#try-sample-pdf-forms}

I file di esempio per questo articolo includono due PDF forms. Il primo esempio consente di digitare una stringa e quindi generare i valori hash MD4, MD5, SHA-1 e SHA-256 per la stringa.  Il secondo esempio è un modulo semplice che consente di sbloccare i campi di testo se viene immessa una password corretta.

### Esempio 1: generazione di hash {#generating-dashes}

Per provare il primo esempio, procedere come segue:

1. Dopo aver scaricato e decompresso i file di esempio, apri hashing_forms_sample1.pdf con AEM Forms su JEE Designer. In alternativa, puoi utilizzare Adobe Reader o Adobe Acrobat Professional per aprire e visualizzare l’esempio, ma non sarà possibile visualizzare il codice sorgente.
1. Nel campo di testo etichettato [!UICONTROL testo non crittografato] digita una password o qualsiasi altro messaggio a cui desideri applicare l’hash.
1. Fare clic su uno dei quattro pulsanti per generare l&#39;hash MD4, MD5, SHA-1 o SHA-256. A seconda del pulsante premuto, viene chiamata una delle quattro funzioni hash che produce l&#39;output esadecimale e viene applicato l&#39;hash alla stringa o al messaggio.

Il risultato dell’operazione hash viene visualizzato nel campo etichettato [!UICONTROL hash]. La lunghezza dell’hash varia a seconda della funzione di hash scelta.

Tutti gli esempi utilizzano cifre esadecimali come tipo di output. È possibile utilizzare l&#39;editor di script per modificare gli esempi e modificare il tipo di output in Base64 o in String semplice.

### Esempio 2: password corrispondenti {#matching-passwords}

Il secondo esempio mostra come gli hash vengono confrontati in background, senza dover rivelare la vera password. La password immessa è sottoposta ad hashing. Anche la password reale, memorizzata in un campo invisibile, viene sottoposta ad hashing. La password è protetta non perché è invisibile, ma perché è stata sottoposta a hashing. Poiché è impossibile ricostruire la password dal valore con hash, è possibile esporla in modo sicuro sotto forma di hash. Il confronto viene fatto solo tra gli hash, non tra le password in testo non crittografato. Se entrambi gli hash sono uguali, è possibile supporre che le password siano identiche.

Per provare il secondo esempio, procedere come segue:

1. Apri `hashing_forms_sample2.pdf` con AEM Forms su JEE Designer. In alternativa, puoi utilizzare Adobe Reader o Adobe Acrobat Professional per aprire e visualizzare l’esempio, ma non sarà possibile visualizzare il codice sorgente.
1. Scegli uno dei due campi di password etichettati [!UICONTROL MAN password] o [!UICONTROL Password WOMAN] e digita le password:
   1. La password per l&#39;uomo è `bob`
   1. La password per la donna è `alice`
1. Quando si sposta lo stato attivo dai campi della password o si preme il tasto Invio, l&#39;hash della password immessa viene generato automaticamente e viene confrontato con l&#39;hash memorizzato della password corretta in background. Le password con hash corrette vengono memorizzate nei campi di testo invisibili etichettati `passwd_man_hashed` e `passwd_woman_hashed`. Se si digita la password corretta per l&#39;uomo, i campi di testo etichettati `Man 1` e `Man 2` sono rese accessibili per consentirvi di digitare testo. Lo stesso comportamento si applica ai campi della donna.
1. In alternativa, è possibile fare clic sul pulsante con l&#39;etichetta &quot;elimina password&quot;, che disabilita i campi di testo e ne modifica il bordo.

Il codice per confrontare i due valori con hash e abilitare i campi di testo è semplice:

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Dove andare da qui {#next-steps}

Dove ti servirebbe qualcosa del genere? Considera un modulo di PDF con campi che devono essere compilati solo da persone autorizzate. Proteggendo questi campi con una password, che non può essere visualizzata in testo non crittografato in nessuna parte del documento, come in Sample_2.pdf, è possibile garantire che tali campi siano accessibili solo agli utenti che conoscono la password.

Ti incoraggio a continuare a esplorare i due file PDF di esempio.  È possibile generare nuovi valori hash con Sample_1.pdf e utilizzare i valori generati per modificare la password o la funzione hash utilizzata in Sample_2.pdf.  Le risorse elencate nella sezione Attribution forniscono anche informazioni aggiuntive sull’hashing e sulle implementazioni JavaScript specifiche utilizzate in questo articolo.

## Attribution {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Collisione hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Tavolo arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table)
* [Home page del progetto JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [Home page del progetto jsSHA2](https://anmar.eu.org/projects/jssha2/)
