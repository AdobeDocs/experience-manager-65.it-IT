---
title: Prevenzione degli attacchi CSRF
seo-title: Prevenzione degli attacchi CSRF
description: Scoprite come impedire attacchi CSRF (Cross-site request forgery) e proteggere i dati utente da eventuali compromessi.
seo-description: Scoprite come impedire attacchi CSRF (Cross-site request forgery) e proteggere i dati utente da eventuali compromessi.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# Prevenzione degli attacchi CSRF {#preventing-csrf-attacks}

## Funzionamento degli attacchi CSRF {#how-csrf-attacks-work}

Il CSRF (Cross-site request forgery) è una vulnerabilità del sito Web in cui un browser di utenti valido viene utilizzato per inviare una richiesta dannosa, possibilmente tramite un iFrame. Poiché il browser invia i cookie a livello di dominio, se l&#39;utente ha attualmente eseguito il login a un&#39;applicazione, i dati dell&#39;utente potrebbero essere compromessi.

Ad esempio, considerate uno scenario in cui avete eseguito l’accesso alla console di amministrazione in un browser. Riceverete un messaggio e-mail contenente un collegamento. Fai clic sul collegamento per aprire una nuova scheda nel browser. La pagina aperta contiene un iFrame nascosto che esegue una richiesta dannosa al server dei moduli utilizzando il cookie della sessione dei moduli AEM autenticati. Poiché User Management riceve un cookie valido, trasmette la richiesta.

## Termini relativi a CSRF {#csrf-related-terms}

**Referente:** l&#39;indirizzo della pagina di origine da cui proviene una richiesta. Ad esempio, una pagina Web sul sito1.com contiene un collegamento a sito2.com. Facendo clic sul collegamento si invia una richiesta a site2.com. Il referente di questa richiesta è site1.com perché la richiesta viene effettuata da una pagina la cui origine è site1.com.

**URI inseriti nell&#39;elenco Consentiti:** gli URI identificano le risorse sul server dei moduli che vengono richieste, ad esempio, /adminui o /contentspace. Alcune risorse possono consentire l&#39;accesso all&#39;applicazione da siti esterni. Queste risorse vengono considerate URI inseriti nell&#39;elenco Consentiti. Il server dei moduli non esegue mai un controllo referente dagli URI inseriti nell&#39;elenco Consentiti.

**Referente nullo:** Quando si apre una nuova finestra o scheda del browser, si digita un indirizzo e si preme Invio, il referente è nullo. La richiesta è completamente nuova e non proviene da una pagina Web padre; pertanto, non esiste un referente per la richiesta. Il server moduli può ricevere un referente nullo da:

* richieste effettuate su endpoint SOAP o REST da  Acrobat
* qualsiasi client desktop che esegue una richiesta HTTP su un endpoint SOAP o REST AEM moduli
* quando si apre una nuova finestra del browser e viene inserito l&#39;URL per qualsiasi pagina di login AEM modulo per l&#39;applicazione Web

Consentire un referente nullo sugli endpoint SOAP e REST. Consentite inoltre un referente nullo su tutte le pagine di login URI, ad esempio /adminui e /contentspace, e sulle relative risorse mappate. Ad esempio, il servlet mappato per /contentspace è /contentspace/faces/jsp/login.jsp, che deve essere un&#39;eccezione di riferimento null. Questa eccezione è necessaria solo se si abilita il filtro GET per l&#39;applicazione Web. Le applicazioni possono specificare se consentire referenti null. Vedere &quot;Protezione dagli attacchi di contraffazione delle richieste tra siti&quot; in [Protezione e protezione per AEM moduli](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Eccezione referente consentita:** Eccezione referente consentita è un sottoelenco dell&#39;elenco di referenti consentiti, da cui vengono bloccate le richieste. Le eccezioni di riferimento consentite sono particolari per un&#39;applicazione Web. Se un sottoinsieme dei Referenti Consentiti non deve essere autorizzato a richiamare una particolare applicazione Web, è   i referenti tramite Eccezioni Referente Consentite. Le eccezioni di riferimento consentite sono specificate nel file web.xml dell&#39;applicazione. (Vedere &quot;Protezione dagli attacchi di contraffazione delle richieste cross-site&quot; nella pagina Hardening and Security for AEM forms on Help and Tutorials.)

## Come funzionano i referenti {#how-allowed-referers-work}

AEM moduli fornisce un filtro di riferimento, che può aiutare a prevenire attacchi CSRF. Come funziona il filtro dei riferimenti:

1. Il server dei moduli verifica il metodo HTTP utilizzato per la chiamata:

   * Se si tratta di un POST, il server dei moduli esegue il controllo dell&#39;intestazione del referente.
   * Se è GET, il server dei moduli bypassa il controllo del referer, a meno che CSRF_CHECK_GETS non sia impostato su true, nel qual caso esegue il controllo dell&#39;intestazione del referente. CSRF_CHECK_GETS è specificato nel file web.xml dell’applicazione. (Vedere &quot;Protezione dagli attacchi di contraffazione delle richieste cross-site&quot; in [Guida all&#39;indurimento e alla sicurezza](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. Il server dei moduli verifica se l&#39;URI richiesto è inserito nell&#39;elenco Consentiti:

   * Se l’URI viene inserito nell&#39;elenco Consentiti, il server trasmette la richiesta.
   * Se l’URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il referente della richiesta.

1. Se nella richiesta è presente un referente, il server verifica se si tratta di un referente consentito. Se consentita, il server verifica la presenza di un&#39;eccezione di referente:

   * Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   * Se non si tratta di un&#39;eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun referente, il server verifica se è consentito un referente nullo.

   * Se è consentito un referente nullo, la richiesta viene passata.
   * Se non è consentito un referente nullo, il server verifica se l&#39;URI richiesto è un&#39;eccezione per il referente nullo e gestisce la richiesta di conseguenza.

## Configurare i referenti consentiti {#configure-allowed-referers}

Quando si esegue Configuration Manager, l&#39;host e l&#39;indirizzo IP predefiniti o il server moduli vengono aggiunti all&#39;elenco Referente consentito. Potete modificare questo elenco nella console di amministrazione.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Configura URL referente consentiti. L&#39;elenco Referente consentito viene visualizzato nella parte inferiore della pagina.
1. Per aggiungere un referente consentito:

   * Digitare un nome host o un indirizzo IP nella casella Referenti consentiti. Per aggiungere più di un referente consentito alla volta, digita ogni nome host o indirizzo IP su una nuova riga.
   * Nelle caselle Porta HTTP e Porte HTTPS, specificate le porte consentite per HTTP, HTTPS o entrambe. Se lasciate vuote queste caselle, vengono utilizzate le porte predefinite (porta 80 per HTTP e porta 443 per HTTPS). Se immettete `0` (zero) nelle caselle, tutte le porte del server vengono abilitate. Potete inoltre immettere un numero di porta specifico per attivare solo tale porta.
   * Fate clic su Aggiungi.

1. Per rimuovere una voce dall&#39;elenco Referente consentito, selezionarla dall&#39;elenco e fare clic su Elimina.

   Se l’elenco di riferimenti consentiti è vuoto, la funzione CSRF smette di funzionare e il sistema diventa insicuro.

1. Dopo aver modificato l&#39;elenco Referente consentito, riavviare il server moduli AEM.

