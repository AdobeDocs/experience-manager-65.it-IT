---
title: Prevenzione degli attacchi CSRF
seo-title: Preventing CSRF attacks
description: Scopri come evitare attacchi CSRF (Cross-site request forgery) e proteggere i dati utente da compromessi.
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

## Funzionamento degli attacchi del CSRF {#how-csrf-attacks-work}

La vulnerabilità cross-site request forgery (CSRF) è una vulnerabilità del sito web in cui il browser di un utente valido viene utilizzato per inviare una richiesta dannosa, possibilmente tramite un iFrame. Poiché il browser invia i cookie a livello di dominio, se l’utente ha effettuato l’accesso a un’applicazione, i dati dell’utente potrebbero essere compromessi.

Ad esempio, considera uno scenario in cui hai effettuato l’accesso alla console di amministrazione in un browser. Ricevi un messaggio e-mail contenente un collegamento. Fai clic sul collegamento , per aprire una nuova scheda nel browser. La pagina aperta contiene un iFrame nascosto che effettua una richiesta dannosa al server dei moduli utilizzando il cookie della sessione dei moduli AEM autenticati. Poiché User Management riceve un cookie valido, trasmette la richiesta.

## Termini relativi al CSRF {#csrf-related-terms}

**Referente:** Indirizzo della pagina di origine da cui proviene una richiesta. Ad esempio, una pagina web su site1.com contiene un collegamento a site2.com. Facendo clic sul collegamento viene pubblicata una richiesta a site2.com. Il referente di questa richiesta è site1.com perché la richiesta viene effettuata da una pagina la cui origine è site1.com.

**URI inseriti nell&#39;elenco Consentiti:** Gli URI identificano le risorse sul server dei moduli richieste, ad esempio /adminui o /contentspace. Alcune risorse possono consentire a una richiesta di accedere all’applicazione da siti esterni. Queste risorse sono considerate URI inseriti nell&#39;elenco Consentiti. Il server dei moduli non esegue mai un controllo referente dagli URI inseriti nell&#39;elenco Consentiti.

**Referente Null:** Quando apri una nuova finestra o scheda del browser, digita un indirizzo e premi Invio, il referente è nullo. La richiesta è completamente nuova e non proviene da una pagina web padre; pertanto, non esiste un referente per la richiesta. Il server dei moduli può ricevere un referente null da:

* richieste effettuate su endpoint SOAP o REST da Acrobat
* qualsiasi client desktop che effettua una richiesta HTTP su un endpoint SOAP o REST di AEM forms
* quando viene aperta una nuova finestra del browser e viene inserito l’URL per qualsiasi pagina di accesso dell’applicazione Web AEM forms

Consenti un referer null sugli endpoint SOAP e REST. Consentire anche un referer nullo su tutte le pagine di accesso URI come /adminui e /contentspace e le relative risorse mappate. Ad esempio, il servlet mappato per /contentspace è /contentspace/faces/jsp/login.jsp, che dovrebbe essere un&#39;eccezione referer null. Questa eccezione è necessaria solo se si abilita il filtro GET per l&#39;applicazione Web. Le applicazioni possono specificare se consentire riferimenti nulli. Consulta &quot;Proteggere da attacchi di falsificazione di richieste intersito&quot; in [Hardening e sicurezza per i moduli AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Eccezione referente consentita:** Eccezione referente consentita è un sottoelenco dell’elenco dei referenti consentiti, da cui le richieste sono bloccate. Le eccezioni di riferimento consentite sono particolari per un&#39;applicazione web. Se un sottoinsieme dei referenti consentiti non deve essere autorizzato a richiamare una particolare applicazione web, puoi inserire nell&#39;elenco Bloccati i referenti tramite Eccezioni referente consentite. Le eccezioni di riferimento consentite sono specificate nel file web.xml per la tua applicazione. (Vedere &quot;Protezione dagli attacchi di vulnerabilità cross-site Request Forgery&quot; in Hardening and Security for AEM forms nella pagina Aiuto e Tutorials.)

## Funzionamento dei referenti consentiti {#how-allowed-referers-work}

I moduli AEM forniscono un filtro di riferimento che può aiutare a prevenire attacchi CSRF. Come funziona il filtro dei referenti:

1. Il server dei moduli controlla il metodo HTTP utilizzato per la chiamata:

   * Se si tratta di POST, il server dei moduli esegue il controllo dell’intestazione del referente.
   * Se è GET, il server dei moduli ignora il controllo referer, a meno che CSRF_CHECK_GETS non sia impostato su true, nel qual caso esegue il controllo di intestazione referer. CSRF_CHECK_GETS è specificato nel file web.xml per l&#39;applicazione. (Vedi &quot;Protezione dagli attacchi di vulnerabilità cross-site Request Forgery&quot; in [Guida all’indurimento e alla sicurezza](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Il server dei moduli controlla se l’URI richiesto è inserito nell&#39;elenco Consentiti:

   * Se l’URI viene inserito nell&#39;elenco Consentiti, il server trasmette la richiesta.
   * Se l’URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il referente della richiesta.

1. Se nella richiesta è presente un referente, il server controlla se si tratta di un referente consentito. Se consentito, il server verifica la presenza di un&#39;eccezione referer:

   * Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   * Se non si tratta di un’eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun referente, il server controlla se è consentito un referente null.

   * Se è consentito un referente null, la richiesta viene trasmessa.
   * Se non è consentito un referente null, il server controlla se l’URI richiesto è un’eccezione per il referente null e gestisce la richiesta di conseguenza.

## Configurare i referenti consentiti {#configure-allowed-referers}

Quando si esegue Configuration Manager, l&#39;host e l&#39;indirizzo IP predefiniti o il server dei moduli vengono aggiunti all&#39;elenco Riferimenti consentiti. Puoi modificare questo elenco nella console di amministrazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura gli URL di riferimento consentiti. L’elenco Riferimenti consentiti viene visualizzato nella parte inferiore della pagina.
1. Per aggiungere un referente consentito:

   * Digita un nome host o un indirizzo IP nella casella Riferimenti consentiti . Per aggiungere più di un referente consentito alla volta, digita ogni nome host o indirizzo IP su una nuova riga.
   * Nelle caselle Porta HTTP e Porte HTTPS specificare le porte consentite per HTTP, HTTPS o entrambe. Se queste caselle vengono lasciate vuote, vengono utilizzate le porte predefinite (porta 80 per HTTP e porta 443 per HTTPS). Se immetti `0` (zero) nelle caselle, tutte le porte di quel server sono abilitate. È inoltre possibile immettere un numero di porta specifico per abilitare solo tale porta.
   * Fate clic su Aggiungi.

1. Per rimuovere la voce dall’elenco Riferimenti consentiti, selezionarla dall’elenco e fare clic su Elimina.

   Se l’elenco dei referenti consentiti è vuoto, la funzione CSRF smette di funzionare e il sistema diventa insicuro.

1. Dopo aver modificato l’elenco Riferimenti consentiti, riavviare il server dei moduli AEM.
