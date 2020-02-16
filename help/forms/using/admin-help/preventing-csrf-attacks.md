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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prevenzione degli attacchi CSRF {#preventing-csrf-attacks}

## Funzionamento degli attacchi CSRF {#how-csrf-attacks-work}

Il CSRF (Cross-site request forgery) è una vulnerabilità del sito Web in cui un browser di utenti valido viene utilizzato per inviare una richiesta dannosa, possibilmente tramite un iFrame. Poiché il browser invia i cookie a livello di dominio, se l&#39;utente ha attualmente eseguito il login a un&#39;applicazione, i dati dell&#39;utente potrebbero essere compromessi.

Ad esempio, considerate uno scenario in cui avete eseguito l’accesso alla console di amministrazione in un browser. Riceverete un messaggio e-mail contenente un collegamento. Fai clic sul collegamento per aprire una nuova scheda nel browser. La pagina aperta contiene un iFrame nascosto che invia una richiesta dannosa al server dei moduli tramite il cookie proveniente dalla sessione autenticata dei moduli AEM. Poiché User Management riceve un cookie valido, trasmette la richiesta.

## Termini relativi al CSRF {#csrf-related-terms}

**** Referente: L&#39;indirizzo della pagina di origine da cui proviene la richiesta. Ad esempio, una pagina Web sul sito1.com contiene un collegamento a sito2.com. Facendo clic sul collegamento si invia una richiesta a site2.com. Il referente di questa richiesta è site1.com perché la richiesta viene effettuata da una pagina la cui origine è site1.com.

**** URI inseriti nella whitelist: Gli URI identificano le risorse sul server dei moduli che vengono richieste, ad esempio, /adminui o /contentspace. Alcune risorse possono consentire l&#39;accesso all&#39;applicazione da siti esterni. Queste risorse vengono considerate URI inseriti nella whitelist. Il server moduli non esegue mai un controllo referente dagli URI inseriti nella whitelist.

**** Referente nullo: Quando aprite una nuova finestra o scheda del browser, digitate un indirizzo e premete Invio, il referente è nullo. La richiesta è completamente nuova e non proviene da una pagina Web padre; pertanto, non esiste un referente per la richiesta. Il server moduli può ricevere un referente nullo da:

* richieste effettuate sugli endpoint SOAP o REST di Acrobat
* qualsiasi client desktop che esegue una richiesta HTTP su un endpoint SOAP o REST di moduli AEM
* quando si apre una nuova finestra del browser e viene inserito l’URL di qualsiasi pagina di accesso dell’applicazione Web AEM

Consentire un referente nullo sugli endpoint SOAP e REST. Consentite inoltre un referente nullo su tutte le pagine di login URI, ad esempio /adminui e /contentspace, e sulle relative risorse mappate. Ad esempio, il servlet mappato per /contentspace è /contentspace/faces/jsp/login.jsp, che deve essere un&#39;eccezione di riferimento null. Questa eccezione è necessaria solo se abilitate il filtro GET per l&#39;applicazione Web. Le applicazioni possono specificare se consentire referenti null. Consulta &quot;Protezione dagli attacchi di contraffazione delle richieste cross-site&quot; in [Sicurezza e protezione per i moduli](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)AEM.

**** Eccezione Referente Consentita: Eccezione referente consentita è un sottoelenco dell&#39;elenco di referenti consentiti, dal quale le richieste vengono bloccate. Le eccezioni di riferimento consentite sono particolari per un&#39;applicazione Web. Se a un sottoinsieme dei Referenti consentiti non è consentito richiamare una particolare applicazione Web, è possibile inserire in blacklist i referenti tramite Eccezioni referente consentite. Le eccezioni di riferimento consentite sono specificate nel file web.xml dell&#39;applicazione. (consultate &quot;Proteggere dagli attacchi di contraffazione delle richieste cross-site&quot; nei moduli Hardening e Security for AEM nella pagina Guida ed esercitazioni).

## Funzionamento dei referenti consentiti {#how-allowed-referers-work}

I moduli AEM forniscono un filtro di riferimento che può aiutare a prevenire attacchi CSRF. Come funziona il filtro dei riferimenti:

1. Il server dei moduli verifica il metodo HTTP utilizzato per la chiamata:

   * Se è POST, il server dei moduli esegue il controllo dell&#39;intestazione del referente.
   * Se si tratta di GET, il server dei moduli bypassa il controllo del referer, a meno che CSRF_CHECK_GETS non sia impostato su true, nel qual caso esegue il controllo dell&#39;intestazione del referer. CSRF_CHECK_GETS è specificato nel file web.xml dell’applicazione. (vedere &quot;Proteggere dagli attacchi di contraffazione delle richieste cross-site&quot; nella guida all&#39; [applicazione e alla](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)sicurezza).

1. Il server dei moduli verifica se l&#39;URI richiesto è inserito nella lista bianca:

   * Se l’URI è inserito nella white list, il server trasmette la richiesta.
   * Se l’URI richiesto non è inserito nella white list, il server recupera il referente della richiesta.

1. Se nella richiesta è presente un referente, il server verifica se si tratta di un referente consentito. Se consentita, il server verifica la presenza di un&#39;eccezione di referente:

   * Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   * Se non è un&#39;eccezione, la richiesta viene passata.

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

1. Dopo aver modificato l&#39;elenco Referente autorizzato, riavvia il server moduli AEM.

