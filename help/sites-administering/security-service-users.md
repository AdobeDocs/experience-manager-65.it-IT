---
title: Utenti del servizio in Adobe Experience Manager
description: Scopri gli utenti del servizio in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---


# Utenti del servizio in Adobe Experience Manager (AEM) {#service-users-in-aem}

## Panoramica {#overview}

Il modo principale per ottenere una sessione amministrativa o un risolutore risorse in AEM è stato l&#39;utilizzo dei metodi `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` forniti da Sling.

Tuttavia, nessuno di questi metodi è stato progettato in base al principio [di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege). In questo modo è troppo semplice per uno sviluppatore non pianificare in anticipo una struttura appropriata e i corrispondenti livelli di controllo di accesso (ACL, Access Control Levels) per il contenuto. Se una vulnerabilità è presente in un servizio di questo tipo, spesso si verificano escalation di privilegi per l&#39;utente `admin`, anche se il codice stesso non avrebbe bisogno di privilegi amministrativi per funzionare.

## Come eliminare gradualmente le sessioni di amministrazione {#how-to-phase-out-admin-sessions}

### Priorità 0: la funzione è attiva/necessaria/obsoleta? {#priority-is-the-feature-active-needed-derelict}

In alcuni casi, la sessione di amministrazione non viene utilizzata oppure la funzione viene completamente disabilitata. In tal caso, assicurati di rimuovere completamente la funzionalità o di adattarla con [codice NOP](https://en.wikipedia.org/wiki/NOP).

### Priorità 1: Utilizzare La Sessione Di Richiesta {#priority-use-the-request-session}

Quando possibile, effettua il refactoring della funzione in modo che la sessione di richiesta autenticata specificata possa essere utilizzata per la lettura o la scrittura di contenuti. Se ciò non è fattibile, spesso è possibile realizzarlo applicando le priorità seguenti.

### Priorità 2: Ristrutturazione del contenuto {#priority-restructure-content}

Molti problemi possono essere risolti ristrutturando il contenuto. Durante la ristrutturazione, considera queste semplici regole:

* **Modifica controllo dell&#39;accesso**

   * Assicurati che gli utenti o i gruppi che necessitano effettivamente di accesso abbiano effettivamente accesso;

* **Perfeziona struttura contenuto**

   * Spostalo in altre posizioni, ad esempio, in cui il controllo di accesso corrisponde alle sessioni di richiesta disponibili;
   * Modificare la granularità del contenuto;

* **Effettua il refactoring del codice per renderlo un servizio appropriato**

   * Sposta la logica di business dal codice JSP al servizio. Questo consente una modellazione del contenuto diversa.

Inoltre, assicurati che tutte le nuove funzioni sviluppate siano conformi ai seguenti principi:

* **I requisiti di sicurezza devono guidare la struttura del contenuto**

   * La gestione del controllo degli accessi dovrebbe essere naturale
   * Il controllo degli accessi deve essere applicato dall&#39;archivio, non dall&#39;applicazione

* **Usa tipi di nodo**

   * Limita il set di proprietà che è possibile impostare

* **Rispetta impostazioni privacy**

   * Se sono presenti profili privati, un esempio potrebbe essere quello di non esporre l’immagine del profilo, l’e-mail o il nome completo trovati sul nodo `/profile` privato.

## Controllo accesso rigoroso {#strict-access-control}

Sia che si applichi il controllo degli accessi durante la ristrutturazione dei contenuti o quando lo si fa per un nuovo utente del servizio, è necessario applicare gli ACL più severi possibili. Usare tutte le possibilità di controllo degli accessi:

* Ad esempio, invece di applicare `jcr:read` su `/apps`, applicarlo solo a `/apps/*/components/*/analytics`

* Usa [restrizioni](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Applica ACL per i tipi di nodo
* Limita le autorizzazioni

   * ad esempio, se devi solo scrivere le proprietà, non dare l&#39;autorizzazione `jcr:write`; usa invece `jcr:modifyProperties`

## Utenti e mappature dei servizi {#service-users-and-mappings}

Se quanto sopra non va a buon fine, Sling 7 offre un servizio di mappatura degli utenti del servizio, che consente di configurare una mappatura bundle-to-user e due metodi API corrispondenti:

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

I metodi restituiscono un risolutore sessione/risorsa con i privilegi solo di un utente configurato. Questi metodi presentano le seguenti caratteristiche:

* Consentono di mappare i servizi agli utenti
* Consentono di definire gli utenti dei servizi secondari
* Punto di configurazione centrale: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; nome-servizio]

* `service-id` è mappato a un resolver di risorse e/o all&#39;ID utente dell&#39;archivio JCR per l&#39;autenticazione
* `service-name` è il nome simbolico del bundle che fornisce il servizio

## Altro Recommendations {#other-recommendations}

### Sostituzione della sessione di amministrazione con un utente del servizio {#replacing-the-admin-session-with-a-service-user}

Un utente del servizio è un utente JCR senza password impostata e con un set minimo di privilegi necessari per eseguire un’attività specifica. Se non viene impostata alcuna password, non è possibile effettuare l&#39;accesso con un utente del servizio.

Un modo per rendere obsoleta una sessione amministrativa consiste nel sostituirla con sessioni utente di servizio. Se necessario, può anche essere sostituito da più utenti del servizio secondario.

Per sostituire la sessione di amministrazione con un utente del servizio, è necessario effettuare le seguenti operazioni:

1. Identifica le autorizzazioni necessarie per il servizio, tenendo presente il principio delle autorizzazioni minime.
1. Controlla se è già disponibile un utente con esattamente la configurazione delle autorizzazioni necessaria. Crea un utente del servizio di sistema se nessun utente esistente soddisfa le tue esigenze. RTC è necessario per creare un utente di servizio. A volte, ha senso creare più utenti di servizi secondari (ad esempio, uno per la scrittura e uno per la lettura) per suddividere ulteriormente l’accesso.
1. Configurare e testare le ACE per l&#39;utente.
1. Aggiungi un mapping `service-user` per il servizio e per `user/sub-users`

1. Rendi disponibile la funzionalità sling per l&#39;utente del servizio nel tuo bundle: aggiorna alla versione più recente di `org.apache.sling.api`.

1. Sostituisci `admin-session` nel codice con le API `loginService` o `getServiceResourceResolver`.

## Creazione di un utente del servizio {#creating-a-new-service-user}

Dopo aver verificato che nessun utente nell’elenco degli utenti del servizio AEM è applicabile al tuo caso d’uso e che i corrispondenti problemi RTC sono stati approvati, aggiungi il nuovo utente al contenuto predefinito.

L&#39;approccio consigliato consiste nel creare un utente del servizio per utilizzare Esplora repository in *https://&lt;server>:&lt;porta>/crx/explorer/index.jsp*

L&#39;obiettivo è ottenere una proprietà `jcr:uuid` valida, obbligatoria per la creazione dell&#39;utente tramite un&#39;installazione del pacchetto di contenuti.

Per creare utenti del servizio, segui questi passaggi:

1. Passaggio a Esplora repository in *https://&lt;server>:&lt;porta>/crx/explorer/index.jsp*
1. Accesso come amministratore premendo il collegamento **Accedi** nell&#39;angolo superiore sinistro della schermata.
1. Quindi, crea e assegna un nome all’utente del sistema. Per creare l&#39;utente come utente di sistema, impostare il percorso intermedio come `system` e aggiungere sottocartelle facoltative in base alle proprie esigenze:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Verifica che il nodo utente del sistema sia visualizzato come segue:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Nessun tipo mixin associato agli utenti del servizio. Ciò significa che non esistono criteri di controllo di accesso per gli utenti del sistema.

Quando aggiungi il file .content.xml corrispondente al contenuto del bundle, assicurati di aver impostato `rep:authorizableId` e che il tipo primario sia `rep:SystemUser`. Dovrebbe essere simile al seguente:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Aggiunta di una modifica alla configurazione ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Per aggiungere una mappatura dal servizio agli utenti di sistema corrispondenti, creare una configurazione di fabbrica per il servizio [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html). Per mantenere modulare questa configurazione, è possibile fornirla utilizzando il meccanismo di modifica [Sling](https://issues.apache.org/jira/browse/SLING-3578). Per installare queste configurazioni con il bundle, si consiglia di utilizzare [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Crea una sottocartella SLING-INF/content sotto la cartella src/main/resources del bundle
1. In questa cartella, crea un file denominato org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;nome univoco per la configurazione di fabbrica>.xml con il contenuto della configurazione di fabbrica (comprese tutte le mappature utente dei servizi secondari). Esempio:

1. Crea una cartella `SLING-INF/content` sotto la cartella `src/main/resources` del bundle;
1. In questa cartella creare un file `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con il contenuto della configurazione di fabbrica, incluse tutte le mappature utente del servizio secondario.

   A scopo illustrativo, prendere il file denominato `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Fai riferimento al contenuto iniziale di Sling nella configurazione di `maven-bundle-plugin` in `pom.xml` del bundle. Esempio:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Installa il bundle e assicurati che la configurazione di fabbrica sia installata. Per farlo, segui questi passaggi:

   * Accesso alla console Web all&#39;indirizzo *https://serverhost:serveraddress/system/console/configMgr*
   * Cerca **Modifica del servizio User Mapper di Apache Sling Service**
   * Fai clic sul collegamento per verificare se è presente la configurazione corretta.

## Gestione delle sessioni condivise nei servizi {#dealing-with-shared-sessions-in-services}

Le chiamate a `loginAdministrative()` vengono spesso visualizzate insieme alle sessioni condivise. Queste sessioni vengono acquisite al momento dell’attivazione del servizio e vengono disconnesse solo dopo che il servizio è stato arrestato. Anche se si tratta di una pratica comune, ciò comporta due problemi:

* **Sicurezza:** tali sessioni di amministrazione vengono utilizzate per memorizzare nella cache e restituire risorse o altri oggetti associati alla sessione condivisa. Più avanti nello stack di chiamate questi oggetti potevano essere adattati a sessioni o risolutori di risorse con privilegi elevati. Spesso non è chiaro per il chiamante che si tratta di una sessione di amministrazione con cui stanno operando.
* **Prestazioni:** In Oak, le sessioni condivise possono causare problemi di prestazioni e non è consigliabile utilizzarle.

La soluzione più ovvia per il rischio di sicurezza consiste semplicemente nel sostituire la chiamata `loginAdministrative()` con una chiamata `loginService()` a un utente con privilegi limitati. Tuttavia, questo non ha alcun impatto sul potenziale deterioramento delle prestazioni. Una possibilità per mitigare questo consiste nel racchiudere tutte le informazioni richieste in un oggetto che non ha alcuna associazione con la sessione. Quindi, crea (o elimina) la sessione su richiesta.

L’approccio consigliato consiste nel refactoring dell’API del servizio per dare al chiamante il controllo sulla creazione/distruzione della sessione.

## Sessioni amministrative in JSP {#administrative-sessions-in-jsps}

JSP non può usare `loginService()`, perché non esiste un servizio associato. Tuttavia, le sessioni amministrative nelle JSP sono di solito un segno di violazione del paradigma MVC.

Questo problema può essere risolto in due modi:

1. Ristrutturare il contenuto in modo da poterlo manipolare con la sessione utente;
1. Estrazione della logica in un servizio che fornisce un’API che può quindi essere utilizzata da JSP.

Il primo metodo è quello preferito.

## Elaborazione di eventi, preprocessori di replica e processi {#processing-events-replication-preprocessors-and-jobs}

Durante l’elaborazione di eventi o processi e talvolta di flussi di lavoro, la sessione corrispondente che ha attivato l’evento viene persa. Questo porta i gestori di eventi e gli elaboratori di processi a utilizzare spesso sessioni amministrative per svolgere il proprio lavoro. Esistono diversi approcci possibili per risolvere questo problema, ciascuno con i suoi vantaggi e svantaggi:

1. Passa `user-id` nel payload dell&#39;evento e utilizza la rappresentazione.

   **Vantaggi:** di facile utilizzo.

   **Svantaggi:** Utilizza ancora `loginAdministrative()`. Autentica nuovamente una richiesta già autenticata.

1. Crea o riutilizza un utente del servizio che ha accesso ai dati.

   **Vantaggi:** coerente con la progettazione corrente. Richiede modifiche minime.

   **Svantaggi:** richiede la flessibilità degli utenti potenti del servizio, che può facilmente comportare l&#39;escalation dei privilegi. Evita il modello di protezione.

1. Passa una serializzazione di `Subject` nel payload dell&#39;evento e crea un `ResourceResolver` in base a tale oggetto. Un esempio potrebbe essere l&#39;utilizzo di JAAS `doAsPrivileged` in `ResourceResolverFactory`.

   **Vantaggi:** ripulisci l&#39;implementazione dal punto di vista della sicurezza. Evita la riautenticazione e funziona con i privilegi originali. Il codice pertinente per la sicurezza è trasparente per il consumatore dell’evento.

   **Svantaggi:** è necessario eseguire il refactoring. Anche il fatto che il codice pertinente in materia di sicurezza sia trasparente per il consumatore dell’evento potrebbe causare problemi.

Il terzo approccio è la tecnica di elaborazione preferita.

## Processi flusso di lavoro {#workflow-processes}

All’interno delle implementazioni dei processi di flusso di lavoro, viene persa la sessione utente corrispondente che ha attivato il flusso di lavoro. Questo porta a processi di flusso di lavoro che spesso utilizzano sessioni amministrative per eseguire il proprio lavoro.

Per risolvere questi problemi, si consiglia di utilizzare gli stessi approcci indicati in [Elaborazione di eventi, preprocessori di replica e processi](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Processori Sling POST e pagine eliminate {#sling-post-processors-and-deleted-pages}

Esistono un paio di sessioni amministrative utilizzate nelle implementazioni del processore sling POST. In genere, le sessioni amministrative vengono utilizzate per accedere ai nodi in attesa di eliminazione all’interno del POST in fase di elaborazione. Di conseguenza, non sono più disponibili tramite la sessione di richiesta. È possibile accedere a un nodo in attesa di eliminazione per divulgare metadati che altrimenti non dovrebbero essere accessibili.
