---
title: Utenti del servizio in AEM
seo-title: Utenti del servizio in AEM
description: Scopri i Service Users in AEM.
seo-description: Scopri i Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---


# Utenti del servizio in AEM{#service-users-in-aem}

## Panoramica {#overview}

Il modo principale per ottenere una sessione amministrativa o un risolutore di risorse in AEM era utilizzare i metodi `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` forniti da Sling.

Tuttavia, nessuno di questi metodi è stato progettato in base al principio [del privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e rende troppo semplice per uno sviluppatore non pianificare una struttura adeguata e i corrispondenti livelli di controllo degli accessi per il contenuto fin dall&#39;inizio. Se una vulnerabilità è presente in un servizio di questo tipo, porta spesso ad escalation di privilegi per l&#39;utente `admin`, anche se il codice stesso non avrebbe bisogno di privilegi amministrativi per funzionare.

## Modalità di eliminazione delle sessioni di amministrazione {#how-to-phase-out-admin-sessions}

### Priorità 0: La funzione è attiva/necessaria/non disponibile? {#priority-is-the-feature-active-needed-derelict}

In alcuni casi la sessione di amministrazione non viene utilizzata, oppure la funzione viene disattivata completamente. Se questo è il caso dell&#39;implementazione, accertatevi di rimuovere completamente la funzionalità o di adattarla con [Codice NOP](https://en.wikipedia.org/wiki/NOP).

### Priorità 1: Utilizzare la sessione di richiesta {#priority-use-the-request-session}

Se possibile, potete reimpostare la funzione in modo che la specifica sessione di richiesta autenticata possa essere utilizzata per leggere o scrivere contenuti. Se ciò non è fattibile, spesso può essere raggiunto applicando le priorità seguenti.

### Priorità 2: Contenuto ristrutturazione {#priority-restructure-content}

Molti problemi possono essere risolti ristrutturando il contenuto. Durante la ristrutturazione, tenete presenti queste semplici regole:

* **Modifica controllo accesso**

   * Assicuratevi che gli utenti o i gruppi che hanno veramente bisogno di accesso abbiano effettivamente accesso;

* **Ottimizzare la struttura del contenuto**

   * Spostatela in altre posizioni, ad esempio dove il controllo di accesso corrisponde alle sessioni di richiesta disponibili;
   * Modificare la granularità del contenuto;

* **Ridefinizione del codice in modo da renderlo un servizio adeguato**

   * Sposta la logica aziendale dal codice JSP al servizio. Questo consente di creare diversi modelli di contenuto.

Inoltre, accertatevi che le nuove funzioni sviluppate siano conformi ai seguenti principi:

* **I requisiti di sicurezza dovrebbero guidare la struttura del contenuto**

   * Gestione del controllo dell&#39;accesso
   * Il controllo di accesso deve essere imposto dal repository, non dall&#39;applicazione

* **Utilizzare i tipi di nodo**

   * Limita il set di proprietà che è possibile impostare

* **Rispetta le impostazioni di privacy**

   * Nel caso dei profili privati, un esempio potrebbe consistere nel non esporre l&#39;immagine del profilo, l&#39;e-mail o il nome completo trovato sul nodo privato `/profile`.

## Controllo degli accessi rigidi {#strict-access-control}

Sia che si applichi il controllo di accesso durante la ristrutturazione del contenuto, sia che lo si faccia per un nuovo utente di servizi, è necessario applicare gli ACL più restrittivi possibili. Utilizzare tutte le possibili strutture di controllo di accesso:

* Ad esempio, invece di applicare `jcr:read` su `/apps`, applicarlo solo a `/apps/*/components/*/analytics`

* Usa [limitazioni](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Applicazione di ACL per i tipi di nodo
* Limite autorizzazioni

   * ad esempio, quando è solo necessario scrivere le proprietà, non concedere l&#39;autorizzazione `jcr:write`; utilizzare `jcr:modifyProperties`

## Utenti e mappature dei servizi {#service-users-and-mappings}

In caso di errore, Sling 7 offre un servizio di mappatura utenti servizi che consente di configurare una mappatura bundle-utente e due metodi API corrispondenti: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` e ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` che restituiscono una sessione/risolutore di risorse con i privilegi di un solo utente configurato. Tali metodi hanno le seguenti caratteristiche:

* Consentono agli utenti di mappare i servizi
* Consentono di definire gli utenti dei servizi secondari
* Il punto di configurazione centrale è: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` viene mappato a un risolutore risorse e/o a un ID utente dell&#39;archivio JCR per l&#39;autenticazione
* `service-name` è il nome simbolico del bundle che fornisce il servizio

## Altro Recommendations {#other-recommendations}

### Sostituzione della sessione di amministrazione con un utente del servizio {#replacing-the-admin-session-with-a-service-user}

Un utente di servizio è un utente JCR senza password e con un set minimo di privilegi necessari per eseguire un&#39;attività specifica. Se non viene impostata alcuna password, non sarà possibile accedere con un utente del servizio.

Un modo per rendere obsoleta una sessione amministrativa consiste nel sostituirla con sessioni utente di servizio. Se necessario, potrebbe essere sostituito da più utenti di servizi secondari.

Per sostituire la sessione di amministrazione con un utente di servizio, è necessario eseguire i seguenti passaggi:

1. Identificate le autorizzazioni necessarie per il vostro servizio, tenendo presente il principio di meno autorizzazione.
1. Verificate che sia già disponibile un utente con esattamente la configurazione dell&#39;autorizzazione necessaria. Crea un nuovo utente del servizio di sistema se nessun utente esistente soddisfa le tue esigenze. RTC è necessario per creare un nuovo utente di servizio. A volte, ha senso creare più utenti di servizi secondari (ad esempio, uno per la scrittura e uno per la lettura) per compartimentare ulteriormente l&#39;accesso.
1. Configurazione e test di ACE per l’utente.
1. Aggiungi una mappatura `service-user` per il servizio e per `user/sub-users`

1. Rendi disponibile la funzionalità di sling dell&#39;utente del servizio nel pacchetto: aggiornamento alla versione più recente di `org.apache.sling.api`.

1. Sostituisci `admin-session` nel codice con le API `loginService` o `getServiceResourceResolver`.

## Creazione di un nuovo utente di servizio {#creating-a-new-service-user}

Dopo aver verificato che nessun utente nell’elenco degli utenti AEM servizio sia applicabile al caso d’uso e che i problemi RTC corrispondenti siano stati approvati, potete continuare ad aggiungere il nuovo utente al contenuto predefinito.

L&#39;approccio consigliato consiste nel creare un utente di servizio che utilizzi l&#39;utilità di esplorazione repository all&#39;indirizzo *https://&lt;server>:&lt;porta>/crx/explorer/index.jsp*

L&#39;obiettivo è ottenere una proprietà `jcr:uuid` valida, obbligatoria per creare l&#39;utente tramite un&#39;installazione di pacchetti di contenuti.

Puoi creare utenti di servizi:

1. Per accedere alla directory principale archivio, visitare il sito Web all&#39;indirizzo *https://&lt;server>:&lt;porta>/crx/explorer/index.jsp*
1. Accedere come amministratore premendo il collegamento **Accesso** nell&#39;angolo superiore sinistro dello schermo.
1. Quindi, create e denominate l&#39;utente del sistema. Per creare l&#39;utente come un sistema, impostate il percorso intermedio come `system` e aggiungete sottocartelle facoltative in base alle vostre esigenze:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verificare che il nodo utente del sistema sia nel modo seguente:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Non esistono tipi di mixin associati agli utenti del servizio. Ciò significa che non saranno presenti criteri di controllo degli accessi per gli utenti del sistema.

Quando aggiungete il file .content.xml corrispondente al contenuto del bundle, accertatevi di aver impostato `rep:authorizableId` e che il tipo principale sia `rep:SystemUser`. Dovrebbe essere così:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Aggiunta di una modifica alla configurazione ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Per aggiungere una mappatura dal servizio agli utenti di sistema corrispondenti, è necessario creare una configurazione di fabbrica per il servizio ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`. Per mantenere questo modulare tali configurazioni possono essere fornite utilizzando il [Meccanismo di modifica Sling](https://issues.apache.org/jira/browse/SLING-3578). Il modo consigliato per installare tali configurazioni con il pacchetto è utilizzare [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Creare una sottocartella SLING-INF/content sotto la cartella src/main/resources del bundle
1. In questa cartella create un file denominato org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;un nome univoco per la configurazione di fabbrica>.xml con il contenuto della configurazione di fabbrica (inclusi tutti i mapping utente dei servizi secondari). Esempio:

1. Create una cartella `SLING-INF/content` sotto la cartella `src/main/resources` del pacchetto;
1. In questa cartella create un file `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con il contenuto della configurazione di fabbrica, incluse tutte le mappature utente dei servizi secondari.

   A scopo illustrativo, eseguite un file denominato `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Fate riferimento al contenuto iniziale Sling nella configurazione del `maven-bundle-plugin` nel `pom.xml` del pacchetto. Esempio:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Installate il bundle e accertatevi che la configurazione di fabbrica sia stata installata. È possibile eseguire questa operazione tramite:

   * Passate alla console Web all&#39;indirizzo *https://serverhost:serveraddress/system/console/configMgr*
   * Cerca **Apache Sling Service User Mapper Service Modifica**
   * Fai clic sul collegamento per verificare se è già attiva la configurazione corretta.

## Gestione delle sessioni condivise nei servizi {#dealing-with-shared-sessions-in-services}

Le chiamate a `loginAdministrative()` vengono spesso visualizzate insieme alle sessioni condivise. Queste sessioni vengono acquisite al momento dell&#39;attivazione del servizio e vengono disconnesse solo dopo l&#39;arresto del servizio. Sebbene questa sia una pratica comune, comporta due problemi:

* **Protezione:** Tali sessioni di amministrazione vengono utilizzate per memorizzare nella cache e restituire risorse o altri oggetti associati alla sessione condivisa. Più tardi nello stack di chiamate questi oggetti potrebbero essere adattati alle sessioni o ai risolutori di risorse con privilegi elevati, e spesso non è chiaro al chiamante che si tratta di una sessione di amministrazione con cui stanno operando.
* **Prestazioni:** nelle sessioni condivise di Oak possono verificarsi problemi di prestazioni ed è attualmente sconsigliato utilizzarli.

La soluzione più ovvia per il rischio di sicurezza è semplicemente sostituire la `loginAdministrative()` chiamata con una `loginService()` a un utente con privilegi limitati. Tuttavia, ciò non avrà alcun impatto su eventuali degrado delle prestazioni. Una possibilità di attenuare tale situazione consiste nel racchiudere tutte le informazioni richieste in un oggetto che non ha alcuna associazione con la sessione. Quindi create (o eliminate) la sessione su richiesta.

L&#39;approccio consigliato consiste nel reimpostare l&#39;API del servizio in modo da fornire al chiamante il controllo sulla creazione/distruzione della sessione.

## Sessioni amministrative in JSP {#administrative-sessions-in-jsps}

I JSP non possono utilizzare `loginService()` perché non è associato alcun servizio. Tuttavia, le sessioni amministrative in JSP solitamente sono un segno di una violazione del paradigma MVC.

Questo problema può essere risolto in due modi:

1. Ristrutturazione del contenuto in modo da consentirne la manipolazione con la sessione utente;
1. Estrazione della logica in un servizio che fornisce un&#39;API che può quindi essere utilizzata dalla JSP.

Il primo metodo è quello preferito.

## Eventi di elaborazione, preprocessori di replica e processi {#processing-events-replication-preprocessors-and-jobs}

Quando si elaborano eventi o processi e, in alcuni casi, flussi di lavoro, la sessione corrispondente che ha attivato l’evento in genere viene persa. Ciò comporta che i gestori di eventi e i processori di processo spesso utilizzano sessioni amministrative per svolgere il proprio lavoro. Esistono diversi approcci concepibili per risolvere questo problema, ciascuno con i suoi vantaggi e svantaggi:

1. Passa la `user-id` nel payload dell&#39;evento e utilizza la rappresentazione.

   **Vantaggi:** Facile da usare.

   **Svantaggi:utilizzi** fissi  `loginAdministrative()`. autentica di nuovo una richiesta già autenticata.

1. Creare o riutilizzare un utente del servizio che ha accesso ai dati.

   **Vantaggi:** Coerenza con la progettazione corrente. Ha bisogno di modifiche minime.

   **Svantaggi:** necessita di utenti di servizi molto potenti per essere flessibili, il che può facilmente portare a escalation di privilegi. Circola il modello di sicurezza.

1. Passate una serializzazione della `Subject` nel payload dell&#39;evento e create una `ResourceResolver` in base a tale oggetto. Un esempio potrebbe essere l&#39;utilizzo del JAAS `doAsPrivileged` in `ResourceResolverFactory`.

   **Vantaggi:implementazione** pulita da un punto di vista di sicurezza. Evita la riautenticazione e funziona con i privilegi originali. Il codice relativo alla sicurezza è trasparente per il consumatore dell&#39;evento.

   **Svantaggi:** Necessità di refactoring. Anche il fatto che il codice di sicurezza pertinente trasparente per il consumatore dell&#39;evento possa causare problemi.

Il terzo approccio è attualmente la tecnica di elaborazione preferita.

## Processi del flusso di lavoro {#workflow-processes}

Nelle implementazioni del processo del flusso di lavoro, la sessione utente corrispondente che ha attivato il flusso di lavoro in genere va persa. Ciò porta ai processi di workflow che spesso utilizzano sessioni amministrative per eseguire il proprio lavoro.

Per risolvere questi problemi, si consiglia di utilizzare gli stessi approcci indicati in [Eventi di elaborazione, Preprocessori di replica e Processi](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Processori POST Sling e pagine eliminate {#sling-post-processors-and-deleted-pages}

Ci sono un paio di sessioni amministrative utilizzate nelle implementazioni del processore POST Sling. Solitamente, le sessioni amministrative vengono utilizzate per accedere ai nodi in attesa di eliminazione all&#39;interno del POST in elaborazione. Di conseguenza, non sono più disponibili tramite la sessione di richiesta. È possibile accedere a un nodo in attesa di eliminazione per indicare una metada che altrimenti non dovrebbe essere accessibile.
