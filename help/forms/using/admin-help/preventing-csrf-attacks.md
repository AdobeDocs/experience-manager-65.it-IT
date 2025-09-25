---
title: Prevenzione degli attacchi CSFR
description: Scopri come evitare attacchi CSRF (vulnerabilità cross-site request forgery) e proteggere i dati utente da possibili compromissioni.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '955'
ht-degree: 100%

---

# Prevenzione degli attacchi CSFR {#preventing-csrf-attacks}

## Funzionamento degli attacchi CSRF {#how-csrf-attacks-work}

La vulnerabilità cross-site request forgery (CSRF) è una vulnerabilità del sito web in cui il browser di un utente valido viene utilizzato per inviare una richiesta dannosa, possibilmente tramite un iFrame. Poiché il browser invia cookie in base al dominio, se l’utente ha effettuato l’accesso a un’applicazione, i relativi dati potrebbero essere compromessi.

Ad esempio, prendi in considerazione uno scenario in cui hai effettuato l’accesso alla console di amministrazione in un browser. Ricevi un messaggio e-mail che contiene un collegamento. Quando fai clic sul collegamento, si apre una nuova scheda nel browser. La pagina aperta contiene un iFrame nascosto che invia una richiesta dannosa al server Forms utilizzando il cookie della sessione autenticata di AEM Forms. Poiché la gestione utenti riceve un cookie valido, trasmette la richiesta.

## Termini relativi a CSRF {#csrf-related-terms}

**Referer:** l’indirizzo della pagina di origine da cui proviene una richiesta. Ad esempio, una pagina Web su site1.com contiene un collegamento a site2.com. Facendo clic sul collegamento viene inviata una richiesta a site2.com. Il referrer di questa richiesta è site1.com perché la richiesta viene effettuata da una pagina la cui origine è site1.com.

**URI inseriti nell’elenco consentiti:** gli URI identificano le risorse nel server Forms richieste, ad esempio /adminui o /contentspace. Alcune risorse possono consentire una richiesta di accesso all’applicazione da siti esterni. Queste risorse sono considerate URI inseriti nell’elenco consentiti. Forms Server non esegue mai un controllo relativo al referrer dagli URI inseriti nell’elenco Consentiti.

**Referrer nullo:** quando apri una nuova finestra o scheda del browser, digiti un indirizzo e premi Invio, il referrer è nullo. La richiesta è completamente nuova e non proviene da una pagina web principale; pertanto, non esiste un referrer per la richiesta. Il server Forms può ricevere un referrer null da:

* richieste effettuate su endpoint SOAP o REST da Acrobat
* qualsiasi client desktop che effettua una richiesta HTTP su un endpoint SOAP o REST di AEM Forms
* quando viene aperta una nuova finestra del browser e viene inserito l’URL per qualsiasi pagina di accesso all’applicazione web AEM forms

Consentire un referrer null sugli endpoint SOAP e REST. Consenti anche un referrer nullo in tutte le pagine di accesso URI, ad esempio /adminui e /contentspace, e nelle relative risorse mappate corrispondenti. Ad esempio, il servlet mappato per /contentspace è /contentspace/faces/jsp/login.jsp, che deve essere un’eccezione referrer nullo. Questa eccezione è necessaria solo se abiliti il filtro GET per l’applicazione Web. Le applicazioni possono specificare se consentire l’utilizzo di referrer nulli. Consulta “Protezione da attacchi di vulnerabilità cross-Site request forgery” in [Protezione avanzata e sicurezza di AEM forms](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Eccezione referrer consentita:** l’eccezione referrer consentita è un sottoelenco dell’elenco dei referrer consentiti da cui le richieste sono bloccate. Le eccezioni referrer consentiti sono specifiche per un’applicazione web. Se a un sottoinsieme dei referrer consentiti non deve essere permesso di richiamare una particolare applicazione web, puoi inserire i referrer nell’elenco bloccati tramite le eccezioni referrer consentiti. Le eccezioni referrer consentiti sono specificate nel file web.xml dell’applicazione. Consulta “Protezione da attacchi di vulnerabilità cross-Site request forgery” in Rafforzamento e protezione per i moduli AEM nella pagina Guida e tutorial.

## Funzionamento dei referrer consentiti {#how-allowed-referers-work}

AEM Forms fornisce il filtro del referrer che può aiutare a prevenire gli attacchi CSRF. Ecco come funziona il filtro del referrer:

1. Forms Server controlla il metodo HTTP utilizzato per la chiamata:

   * se è POST, Forms Server esegue il controllo dell’intestazione del referrer.
   * Se si tratta di GET, Forms Server ignora il controllo del referrer, a meno che CSRF_CHECK_GETS non sia impostato su true, nel qual caso esegue il controllo dell’intestazione del referente. CSRF_CHECK_GETS è specificato nel file web.xml dell’applicazione. Consulta “Protezione da attacchi di vulnerabilità cross-Site request forgery” nella [Guida per il rafforzamento e la protezione](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

1. Forms Server verifica se l’URI richiesto è inserito nell’elenco consentiti:

   * Se l’URI viene inserito nell’elenco consentiti, il server trasmette la richiesta.
   * Se l’URI richiesto non viene inserito nell’elenco consentiti, il server recupera il referrer della richiesta.

1. Se nella richiesta è presente un referrer, il server controlla se si tratta di un referrer consentito. Se consentito, il server controlla la presenza di un’eccezione del referrer:

   * Se si tratta di un’eccezione, la richiesta viene bloccata.
   * Se non si tratta di un’eccezione, la richiesta viene trasmessa.

1. Se nella richiesta non è presente alcun referrer, il server controlla se è consentito un referrer null.

   * Se è consentito un referrer null, la richiesta viene trasmessa.
   * Se non è consentito un referrer null, il server controlla se l’URI richiesto è un’eccezione per il referrer null e gestisce la richiesta di conseguenza.

## Configurare i referrer consentiti {#configure-allowed-referers}

Quando esegui Configuration Manager, l’host e l’indirizzo IP predefiniti o il server Forms vengono aggiunti all’elenco Referrer consentiti. Puoi modificare questo elenco nella console di amministrazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Configura URL referrer consentiti. L’elenco Referrer consentiti viene visualizzato nella parte inferiore della pagina.
1. Per aggiungere un referrer consentito:

   * Digita un nome host o un indirizzo IP nella casella Referrer consentiti. Per aggiungere più di un referrer consentito alla volta, digita ogni nome host o indirizzo IP in una nuova riga.
   * Nelle caselle Porta HTTP e Porte HTTPS specifica le porte consentite per HTTP, HTTPS o entrambe. Se lasci vuote queste caselle, vengono utilizzate le porte predefinite (porta 80 per HTTP e porta 443 per HTTPS). Se immetti `0` (zero) nelle caselle, tutte le porte del server sono abilitate. Puoi inoltre immettere un numero di porta specifico per abilitare solo tale porta.
   * Fai clic su Aggiungi.

1. Per rimuovere una voce dall’elenco Referrer consentiti, seleziona la voce dall’elenco e fai clic su Elimina.

   Se l’elenco dei referrer consentiti è vuoto, la funzione CSRF smette di funzionare e il sistema non è più sicuro.

1. Dopo aver modificato l’elenco Referrer consentiti, riavvia il server AEM Forms.
