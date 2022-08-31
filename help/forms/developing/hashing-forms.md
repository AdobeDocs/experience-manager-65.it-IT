---
title: Come si generano e si utilizzano gli hash nei PDF forms dinamici?
description: Generazione e utilizzo degli hash nei PDF forms dinamici
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Generazione e utilizzo degli hash nei PDF forms dinamici {#generate-work-with-hashes-dynamic-pdf-forms}


## Conoscenze preliminari {#prerequisite-knowledge}

È necessaria un’esperienza con AEM Forms su JEE Designer, così come la possibilità di accedere e chiamare funzioni negli oggetti script.

## Livello utente {#user-level}

Inizio

Quando si desidera nascondere una password nel modulo PDF e non si desidera visualizzarla in testo libero all’interno del codice sorgente o in qualsiasi altro punto del documento PDF, è fondamentale sapere come generare e utilizzare hash MD4, MD5, SHA-1 e SHA-256.

L’idea è quella di offuscare la password generando un hash univoco e archiviarlo nel documento PDF. Questo hash univoco può essere generato da diverse funzioni hash e in questo articolo ti mostrerò come generarle all’interno del modulo PDF e come utilizzarle.

Una funzione hash prende una stringa lunga (o messaggio) di qualsiasi lunghezza come input e produce come output una stringa a lunghezza fissa, a volte definita digest del messaggio o impronta digitale.

AEM Forms su JEE Designer consente di implementare le diverse funzioni hash negli oggetti script come JavaScript e di eseguirle all’interno di un documento dinamico PDF. I PDF di esempio inclusi nei file di esempio per questo articolo utilizzano implementazioni open source delle seguenti funzioni hash:

* MD4 e MD5 - progettati da Ronald Rivest

* SHA-1 e SHA-256 - come definiti dal NIST

Il vantaggio maggiore dell&#39;utilizzo degli hash è che non è necessario confrontare direttamente le password confrontando stringhe di testo chiare; è invece possibile confrontare i due hash delle due password. Poiché è molto improbabile che due stringhe diverse abbiano lo stesso hash, se entrambi gli hash sono identici, è possibile presumere che anche le stringhe confrontate (in questo caso, le password) siano identiche.

>[!NOTE]
>
>Esistono alcuni noti problemi di sicurezza (cosiddetti conflitti hash) con MD4 o MD5. A causa delle collisioni di hash e di altri hacks SHA-1 (compresi i tavoli arcobaleno), ho deciso di concentrarmi sulla funzione hash SHA-256 nel secondo campione.  Per ulteriori informazioni, consulta la sezione [Collisione](https://en.wikipedia.org/wiki/Hash_collision) e [Tavola arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table) pagine da Wikipedia.

## Analisi degli oggetti script {#examining-script-objects}

Quando si apre uno dei due esempi forniti in AEM Forms su JEE Designer, i quattro oggetti script sono disponibili nella palette Gerarchia (vedere la figura seguente).

![Variabili](assets/variables.jpg)

Per visualizzare l&#39;implementazione JavaScript delle funzioni hash all&#39;interno di questi oggetti script, selezionare l&#39;oggetto script ed esplorare il codice nell&#39;Editor di script.  Puoi vedere come è stata implementata ciascuna delle seguenti funzioni hash:

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

Come puoi vedere da questo elenco, sono disponibili diverse funzioni per i diversi tipi di output dell’hash. Puoi scegliere tra `hex_` per cifre esadecimali, `b64_` per l&#39;output codificato Base64, oppure `str_` per una codifica stringa semplice.

A seconda della funzione hash scelta, la lunghezza dell’hash varia:

* MD4: 128 bit
* MD5: 128 bit
* SHA-1: 160 bit
* SHA-256: 256 bit

## Prova dei PDF forms di esempio {#try-sample-pdf-forms}

I file di esempio per questo articolo includono due PDF forms. Il primo esempio consente di digitare una stringa e quindi generare valori hash MD4, MD5, SHA-1 e SHA-256 per la stringa.  Il secondo esempio è un modulo semplice che sblocca i campi di testo se viene immessa una password corretta.

### Campione 1: generazione di hash {#generating-dashes}

Per provare il primo esempio, effettua le seguenti operazioni:

1. Dopo aver scaricato e decompresso i file di esempio, apri hashing_forms_sample1.pdf con AEM Forms su JEE Designer. In alternativa, puoi utilizzare Adobe Reader o Adobe Acrobat Professional per aprire e visualizzare l’esempio, ma non potrai vedere il codice sorgente.
1. Nel campo di testo contrassegnato [!UICONTROL cancellare il testo] digita una password o qualsiasi altro messaggio con cui desideri essere dotato di hash.
1. Fare clic su uno dei quattro pulsanti per generare l&#39;hash MD4, MD5, SHA-1 o SHA-256. A seconda del pulsante premuto, viene chiamata una delle quattro funzioni hash che producono l’output esadecimale e viene eseguito l’hashing della stringa o del messaggio.

Il risultato dell’operazione hash viene visualizzato nel campo contrassegnato [!UICONTROL hash]. La lunghezza dell’hash varia a seconda della funzione hash scelta.

Tutti i campioni utilizzano cifre esadecimali come tipo di output. È possibile utilizzare l&#39;Editor di script per modificare i campioni e modificare il tipo di output in Base64 o Stringa semplice.

### Campione 2: password corrispondenti {#matching-passwords}

Il secondo esempio mostra come gli hash vengono confrontati in background, senza dover svelare la password reale. La password immessa è con hash. Anche la password reale, memorizzata in un campo invisibile, viene sottoposta a hash. La password è protetta non perché è invisibile, ma perché è stata impostata con hash. Poiché è impossibile ricostruire la password dal valore con hash, è sicuro esporre la password in forma con hash. Il confronto viene effettuato solo tra gli hash, non tra le password in un testo chiaro. Se entrambi gli hash sono uguali, è possibile presumere che le password siano identiche.

Per provare il secondo esempio, effettua le seguenti operazioni:

1. Apri `hashing_forms_sample2.pdf` con AEM Forms su JEE Designer. In alternativa, puoi utilizzare Adobe Reader o Adobe Acrobat Professional per aprire e visualizzare l’esempio, ma non potrai vedere il codice sorgente.
1. Scegliere uno dei due campi password etichettati [!UICONTROL Password MAN] o [!UICONTROL Password DONNA] e digitare le password:
   1. La password per l&#39;uomo è `bob`
   1. La password per la donna è `alice`
1. Quando si sposta lo stato attivo dai campi password o si preme il tasto Invio, l’hash della password immessa viene generato automaticamente e viene confrontato con l’hash memorizzato della password corretta in background. Le password corrette e con hash vengono memorizzate nei campi di testo invisibili etichettati `passwd_man_hashed` e `passwd_woman_hashed`. Se si digita la password corretta per l&#39;uomo, i campi di testo etichettati `Man 1` e `Man 2` sono rese accessibili, in modo da poter digitare il testo al loro interno. Lo stesso comportamento si applica ai campi della donna.
1. Facoltativamente, è possibile fare clic sul pulsante &quot;elimina password&quot;, che disabiliterà i campi di testo e cambierà il loro bordo.

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

Dove vi servirebbe qualcosa del genere? Si consideri un modulo PDF con campi che devono essere compilati solo da persone autorizzate. Proteggendo questi campi con una password, che non può essere visualizzata in un testo trasparente in qualsiasi punto del documento come in Sample_2.pdf, è possibile garantire che tali campi siano accessibili solo agli utenti che conoscono la password.

Vi incoraggio a continuare a esplorare i due file PDF di esempio.  È possibile generare nuovi valori hash con Sample_1.pdf e utilizzare i valori generati per modificare la password o la funzione hash utilizzata in Sample_2.pdf.  Le risorse elencate nella sezione Attribuzioni forniscono anche informazioni aggiuntive sull’hashing e sulle implementazioni JavaScript specifiche utilizzate in questo articolo.

## Attribuzioni {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NISTA](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Collisione hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Tavolino arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table)
* [Home page del progetto JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [home page del progetto jsSHA2](https://anmar.eu.org/projects/jssha2/)
