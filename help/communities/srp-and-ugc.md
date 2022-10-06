---
title: Essenze SRP e UGC
seo-title: SRP and UGC Essentials
description: Panoramica del provider di risorse di archiviazione e dei contenuti generati dall’utente
seo-description: Storage resource provider and user-generated content overview
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Essenze SRP e UGC {#srp-and-ugc-essentials}

## Introduzione {#introduction}

Se non conosci il provider delle risorse di archiviazione (SRP) e la sua relazione con il contenuto generato dall’utente (UGC), visita [Archiviazione dei contenuti della community](working-with-srp.md) e [Panoramica del provider di risorse di storage](srp.md).

Questa sezione della documentazione fornisce alcune informazioni essenziali su SRP e UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

L&#39;API SocialResourceProvider (API SRP) è un&#39;estensione di varie API dei provider di risorse Sling. Include il supporto per l’impaginazione e l’incremento atomico (utile per il conteggio e il punteggio).

Le interrogazioni sono necessarie per i componenti SCF in quanto è necessario ordinare per data, disponibilità, numero di voti e così via. Tutte le opzioni SRP dispongono di meccanismi di query flessibili che non si basano sul bucket.

La posizione di archiviazione SRP incorpora il percorso del componente. L’API SRP deve sempre essere utilizzata per accedere all’UGC, in quanto il percorso principale dipende dall’opzione SRP selezionata, ad esempio ASRP, MSRP o JSRP.

L’API SRP non è una classe astratta, è un’interfaccia. Un’implementazione personalizzata non dovrebbe essere eseguita alla leggera, in quanto i vantaggi dei miglioramenti futuri alle implementazioni interne verrebbero persi quando si esegue l’aggiornamento a una nuova versione.

I mezzi per utilizzare l’API SRP sono attraverso le utility fornite, come quelle presenti nel pacchetto SocialResourceUtilities .

Quando esegui l’aggiornamento da AEM 6.0 o versioni precedenti, sarà necessario migrare UGC per tutti gli SRP, per i quali è disponibile uno strumento Open Source. Vedi [Aggiornamento ad AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Storicamente, le utility per l&#39;accesso a UGC sono state trovate nel pacchetto SocialUtils, che non esiste più.
>
>Per le utilità di sostituzione, vedi [Refactoring di SocialUtils](socialutils.md).

## Metodo di utilità per accedere all&#39;UGC {#utility-method-to-access-ugc}

Per accedere a UGC, utilizza un metodo del pacchetto SocialResourceUtilities che restituisce un percorso adatto per l&#39;accesso a UGC dall&#39;SRP e sostituisce il metodo obsoleto trovato nel pacchetto SocialUtils.

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
>Il percorso resourceToUGCStoragePath() restituisce is *not* adatto [Controllo ACL](srp.md#for-access-control-acls).

## Metodo di utilità per accedere agli ACL {#utility-method-to-access-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community nei database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell&#39;archivio locale a cui possono essere applicate le ACL.

Utilizzando l’API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione shadow prima di tutte le operazioni CRUD.

Per controllare le ACL, utilizza un metodo che restituisce un percorso adatto per controllare le autorizzazioni applicate all&#39;UGC della risorsa.

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
>Il percorso restituito da resourceToACLPath() è *not* adatto [accesso all&#39;UGC](#utility-method-to-access-acls) stesso.

## Posizioni di storage correlate all&#39;UGC {#ugc-related-storage-locations}

Le seguenti descrizioni del percorso di archiviazione possono essere di aiuto durante lo sviluppo con JSRP o forse MSRP. Non esiste attualmente alcuna interfaccia utente per accedere all’UGC memorizzato in ASRP, in quanto esiste per JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (strumenti MongoDB).

**Posizione del componente**

Quando un membro accede a contenuti generati dagli utenti nell’ambiente di pubblicazione, interagisce con un componente come parte di un sito AEM.

Un esempio di tale componente è la variabile [componente commenti](http://localhost:4502/content/community-components/en/comments.html) che esiste nel [Guida ai componenti della community](components-guide.md) sito. Il percorso del nodo di commento nell&#39;archivio locale è:

* Percorso componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Posizione nodo ombreggiato**

La creazione di UGC crea anche un [nodo ombra](srp.md#about-shadow-nodes-in-jcr) a cui vengono applicati gli ACL necessari. Il percorso del nodo shadow corrispondente nell&#39;archivio locale è il risultato della precedenza del percorso principale del nodo shadow al percorso del componente:

* Percorso directory principale = `/content/usergenerated`
* Nodo ombra commento = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC**

L’UGC viene creato in nessuna di queste posizioni e deve essere accessibile solo utilizzando un [metodo di utilità](#utility-method-to-access-ugc) che richiama l’API SRP.

* Percorso directory principale = `/content/usergenerated/asi/srp-choice`
* Nodo UGC per JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Attenzione*, per JSRP, il nodo UGC *only* essere presente nell’istanza AEM (autore o pubblicazione) in cui è stata inserita. Se inserito in un’istanza di pubblicazione, la moderazione non sarà possibile dalla console di moderazione sull’autore.

## Informazioni correlate {#related-information}

* [Panoramica del provider di risorse di storage](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.
