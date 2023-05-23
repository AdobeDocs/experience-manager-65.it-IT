---
title: Prevenzione degli attacchi CSRF
seo-title: Preventing CSRF attacks
description: Scopri come evitare attacchi CSRF (Cross-Site Request Forgery) e proteggere i dati utente da possibili compromessi.
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Prevenzione degli attacchi CSRF {#preventing-csrf-attacks}

## Funzionamento degli attacchi CSRF {#how-csrf-attacks-work}

La vulnerabilità cross-site request forgery (CSRF) è una vulnerabilità del sito web in cui un browser dell’utente valido viene utilizzato per inviare una richiesta dannosa, possibilmente tramite un iFrame. Poiché il browser invia cookie su base di dominio, se l’utente ha attualmente effettuato l’accesso a un’applicazione, i suoi dati potrebbero essere compromessi.

Ad esempio, considera uno scenario in cui hai effettuato l’accesso alla console di amministrazione in un browser. Ricevi un messaggio e-mail contenente un collegamento. Fai clic sul collegamento, che apre una nuova scheda nel browser. La pagina aperta contiene un iFrame nascosto che invia una richiesta dannosa al server Forms utilizzando il cookie della sessione autenticata dei moduli AEM. Poiché la gestione utenti riceve un cookie valido, trasmette la richiesta.

## Termini relativi a CSRF {#csrf-related-terms}

**Referer:** Indirizzo della pagina sorgente da cui proviene una richiesta. Ad esempio, una pagina Web su site1.com contiene un collegamento a site2.com. Facendo clic sul collegamento viene inviata una richiesta a site2.com. Il referente di questa richiesta è site1.com perché la richiesta viene effettuata da una pagina la cui origine è site1.com.

**URI inseriti nell&#39;elenco Consentiti:** Gli URI identificano le risorse nel server Forms richieste, ad esempio /adminui o /contentspace. Alcune risorse possono consentire una richiesta di accesso all’applicazione da siti esterni. Queste risorse sono considerate URI inseriti nell&#39;elenco Consentiti. Il server forms non esegue mai un controllo referente dagli URI inseriti nell&#39;elenco Consentiti.

**Referente nullo:** Quando apri una nuova finestra o scheda del browser, quindi digiti un indirizzo e premi Invio, il referente è nullo. La richiesta è completamente nuova e non proviene da una pagina web principale; pertanto, non vi è alcun referente per la richiesta. Il server Forms può ricevere un riferimento null da:

* richieste effettuate sugli endpoint SOAP o REST da Acrobat
* qualsiasi client desktop che effettua una richiesta HTTP su un AEM forma un endpoint SOAP o REST
* quando viene aperta una nuova finestra del browser e viene inserito l’URL per qualsiasi pagina di accesso all’applicazione web AEM forms

Consenti un referente null negli endpoint SOAP e REST. Consenti anche un referente null in tutte le pagine di accesso URI, ad esempio /adminui e /contentspace, e nelle relative risorse mappate corrispondenti. Ad esempio, il servlet mappato per /contentspace è /contentspace/faces/jsp/login.jsp, che deve essere un&#39;eccezione di riferimento null. Questa eccezione è necessaria solo se si abilita il filtro GET per l&#39;applicazione Web. Le applicazioni possono specificare se consentire l&#39;utilizzo di referenti null. Consulta &quot;Protezione da attacchi di tipo Cross-Site Request Forgery&quot; in [Indurimento e sicurezza dei moduli AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Eccezione referente consentita:** Eccezione riferimenti consentiti è un sottoelenco dell’elenco dei riferimenti consentiti, dai quali le richieste sono bloccate. Le eccezioni Riferimenti consentiti sono specifiche per un’applicazione web. Se a un sottoinsieme dei Riferimenti consentiti non deve essere consentito richiamare una particolare applicazione web, puoi inserire nell&#39;elenco Bloccati i referenti tramite Eccezioni di Riferimenti consentiti. Le eccezioni di riferimento consentite sono specificate nel file web.xml dell’applicazione. (Consulta &quot;Protezione da attacchi di tipo Cross-Site Request Forgery&quot; in Protezione e protezione per i moduli AEM nella pagina Guida e Tutorials.)

## Funzionamento dei referenti consentiti {#how-allowed-referers-work}

I moduli AEM forniscono un filtro dei referenti che può aiutare a prevenire gli attacchi CSRF. Ecco come funziona il filtro dei riferimenti:

1. Il server forms controlla il metodo HTTP utilizzato per la chiamata:

   * Se si tratta di POST, il server Forms esegue il controllo dell&#39;intestazione del referente.
   * Se è GET, il server Forms ignora il controllo del referente, a meno che CSRF_CHECK_GETS non sia impostato su true, nel qual caso esegue il controllo dell&#39;intestazione del referente. CSRF_CHECK_GETS è specificato nel file web.xml dell&#39;applicazione. (Consulta &quot;Protezione da attacchi di tipo Cross-Site Request Forgery&quot; in [Guida all’irrigidimento e alla sicurezza](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Il server Forms controlla se l’URI richiesto è inserito nell&#39;elenco Consentiti:

   * Se l’URI viene inserito nell&#39;elenco Consentiti, il server trasmette la richiesta.
   * Se l&#39;URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il referente della richiesta.

1. Se nella richiesta è presente un referente, il server controlla se si tratta di un referente consentito. Se consentito, il server verifica la presenza di un&#39;eccezione referente:

   * Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   * Se non si tratta di un’eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun referente, il server controlla se è consentito un referente null.

   * Se è consentito un referente null, la richiesta viene passata.
   * Se un referente null non è consentito, il server controlla se l&#39;URI richiesto è un&#39;eccezione per il referente null e gestisce la richiesta di conseguenza.

## Configurare i referenti consentiti {#configure-allowed-referers}

Quando si esegue Configuration Manager, l&#39;host e l&#39;indirizzo IP predefiniti o il server Forms vengono aggiunti all&#39;elenco dei riferimenti consentiti. Puoi modificare questo elenco nella console di amministrazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura URL di riferimento consentiti. L&#39;elenco Riferimenti consentiti viene visualizzato nella parte inferiore della pagina.
1. Per aggiungere un referente consentito:

   * Digita un nome host o un indirizzo IP nella casella Riferimenti consentiti. Per aggiungere più di un referente consentito alla volta, digitare ogni nome host o indirizzo IP in una nuova riga.
   * Nelle caselle Porta HTTP e Porte HTTPS specificare le porte consentite per HTTP, HTTPS o entrambe. Se queste caselle vengono lasciate vuote, vengono utilizzate le porte predefinite (porta 80 per HTTP e porta 443 per HTTPS). Se si immette `0` (zero) nelle caselle, tutte le porte del server sono abilitate. È inoltre possibile immettere un numero di porta specifico per abilitare solo tale porta.
   * Fai clic su Aggiungi.

1. Per rimuovere una voce dall&#39;elenco Riferimenti consentiti, selezionare la voce dall&#39;elenco e fare clic su Elimina.

   Se l&#39;elenco dei riferimenti consentiti è vuoto, la funzione CSRF smette di funzionare e il sistema non è più sicuro.

1. Dopo aver modificato l’elenco dei riferimenti consentiti, riavvia il server AEM forms.
