---
title: Nozioni di base su SRP e UGC
description: Panoramica del provider di risorse di archiviazione e dei contenuti generati dall'utente
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Nozioni di base su SRP e UGC {#srp-and-ugc-essentials}

## Introduzione {#introduction}

Se non conosci il provider di risorse di archiviazione (SRP) e la sua relazione con i contenuti generati dagli utenti (UGC), visita [Community Content Storage](working-with-srp.md) e [Storage Resource Provider Overview](srp.md).

Questa sezione della documentazione fornisce alcune informazioni essenziali su SRP e UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

L’API SocialResourceProvider (API SRP) è un’estensione di varie API Sling Resource Provider. Include il supporto per la paginazione e l&#39;incremento atomico (utile per la conteggio e il punteggio).

Le query sono necessarie per i componenti SCF in quanto è necessario ordinare per data, utilità, numero di voti e così via. Tutte le opzioni SRP dispongono di meccanismi di query flessibili che non si basano sul bucket.

La posizione di archiviazione SRP incorpora il percorso del componente. Utilizza sempre l’API SRP per accedere a UGC, in quanto il percorso principale dipende dall’opzione SRP selezionata, ad esempio ASRP, MSRP o JSRP.

L’API SRP non è una classe astratta, è un’interfaccia. Un’implementazione personalizzata non deve essere intrapresa leggermente, in quanto i vantaggi di miglioramenti futuri alle implementazioni interne verrebbero meno con l’aggiornamento a una nuova versione.

I mezzi per utilizzare l’API SRP sono le utility fornite, come quelle presenti nel pacchetto SocialResourceUtilities.

Durante l’aggiornamento da AEM 6.0 o versioni precedenti, sarà necessario eseguire la migrazione di UGC per tutti gli SRP per i quali è disponibile uno strumento Open Source. Consulta [Aggiornamento ad AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Storicamente, le utility per l’accesso a UGC si trovavano nel pacchetto SocialUtils, che non esiste più.
>
>Per le utilità sostitutive, vedi [Refactoring di SocialUtils](socialutils.md).

## Metodo di utilità per accedere a UGC {#utility-method-to-access-ugc}

Per accedere a UGC, utilizza un metodo del pacchetto SocialResourceUtilities che restituisce un percorso adatto per l’accesso a UGC da SRP e sostituisce il metodo obsoleto trovato nel pacchetto SocialUtils.

Di seguito è riportato un esempio minimo di utilizzo del metodo resourceToUGCStoragePath() in un servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

Per altre sostituzioni di SocialUtils, vedi [Refactoring di SocialUtils](socialutils.md).

Per le linee guida sulla codifica, visita [Accesso a UGC con SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Il percorso restituito da resourceToUGCStoragePath() è *not* adatto per il [controllo ACL](srp.md#for-access-control-acls).

## Metodo di utilità per accedere alle ACL {#utility-method-to-access-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community in database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell’archivio locale a cui possono essere applicati gli ACL.

Utilizzando l&#39;API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione ombra prima di tutte le operazioni CRUD.

Per verificare gli ACL, utilizza un metodo che restituisca un percorso adatto per la verifica delle autorizzazioni applicate all’UGC della risorsa.

Di seguito è riportato un semplice esempio di utilizzo del metodo resourceToACLPath() in un servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>Il percorso restituito da resourceToACLPath() è *not* idoneo per l&#39;accesso a [UGC](#utility-method-to-access-acls) stesso.

## Posizioni di archiviazione relative a UGC {#ugc-related-storage-locations}

Le seguenti descrizioni della posizione di archiviazione possono essere utili per lo sviluppo con JSRP o eventualmente MSRP. Attualmente non è disponibile alcuna interfaccia utente per accedere a contenuti generati dagli utenti archiviati in ASRP, in quanto sono disponibili strumenti JSRP ([CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (MongoDB).

**Percorso componente**

Quando un membro immette contenuti generati dagli utenti (UGC) nell’ambiente di pubblicazione, interagisce con un componente come parte di un sito AEM.

Un esempio di tale componente è il componente [comments](http://localhost:4502/content/community-components/en/comments.html) presente nel sito [Guida ai componenti della community](components-guide.md). Il percorso del nodo del commento nell’archivio locale è:

* Percorso componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Posizione nodo shadow**

La creazione di UGC crea anche un [nodo shadow](srp.md#about-shadow-nodes-in-jcr) a cui vengono applicati gli ACL necessari. Il percorso del nodo shadow corrispondente nell’archivio locale è il risultato dell’anteprima del percorso principale del nodo shadow al percorso del componente:

* Percorso directory principale = `/content/usergenerated`
* Commento nodo shadow = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Posizione UGC**

UGC viene creato in nessuna di queste posizioni e dovrebbe essere accessibile solo utilizzando un [metodo di utilità](#utility-method-to-access-ugc) che richiama l&#39;API SRP.

* Percorso directory principale = `/content/usergenerated/asi/srp-choice`
* Nodo UGC per JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Tieni presente*, per JSRP il nodo UGC *only* sarà presente nell&#39;istanza AEM (di authoring o pubblicazione) in cui è stato immesso. Se viene immesso in un&#39;istanza pubblicata, la moderazione non sarà possibile dalla console di moderazione nell&#39;istanza di authoring.

## Informazioni correlate {#related-information}

* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti ai metodi di utilità SRP correnti.
