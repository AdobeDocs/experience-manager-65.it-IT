---
title: Funzioni di base SRP e UGC
seo-title: Funzioni di base SRP e UGC
description: Panoramica del provider delle risorse di storage e del contenuto generato dall’utente
seo-description: Panoramica del provider delle risorse di storage e del contenuto generato dall’utente
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Funzioni di base SRP e UGC {#srp-and-ugc-essentials}

## Introduzione {#introduction}

Se non avete familiarità con il provider delle risorse di storage (SRP) e la sua relazione con il contenuto generato dall&#39;utente (UGC), visitate la pagina [Community Content Storage](working-with-srp.md) and [Storage Resource Provider Overview](srp.md).

Questa sezione della documentazione fornisce alcune informazioni essenziali sull&#39;SRP e sull&#39;UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

L&#39;API SocialResourceProvider (API SRP) è un&#39;estensione di diverse API Sling Resource Provider. Include il supporto dell&#39;impaginazione e dell&#39;incremento atomico (utile per il conteggio e il punteggio).

Le query sono necessarie per i componenti SCF in quanto è necessario ordinare per data, disponibilità, numero di voti e così via. Tutte le opzioni SRP dispongono di meccanismi di query flessibili che non si affidano al bucketing.

La posizione di storage SRP incorpora il percorso del componente. L&#39;API SRP deve sempre essere utilizzata per accedere a UGC, in quanto il percorso principale dipende dall&#39;opzione SRP selezionata, come ASRP, MSRP o JSRP.

L&#39;API SRP non è una classe astratta, è un&#39;interfaccia. L&#39;implementazione personalizzata non dovrebbe essere eseguita in modo leggero, in quanto i vantaggi dei futuri miglioramenti alle implementazioni interne non sarebbero stati apportati al momento dell&#39;aggiornamento a una nuova versione.

I mezzi per utilizzare l&#39;API SRP sono attraverso le utility fornite, come quelle presenti nel pacchetto SocialResourceUtilities.

Durante l&#39;aggiornamento da AEM 6.0 o versioni precedenti, sarà necessario migrare UGC per tutti gli SRP, per i quali è disponibile uno strumento Open Source. Vedere [Aggiornamento a  AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Storicamente, le utility per l&#39;accesso a UGC sono state trovate nel pacchetto SocialUtils, che non esiste più.
>
>Per le utility di sostituzione, vedere [Refactoring SocialUtils](socialutils.md).

## Metodo di utilità per accedere a UGC {#utility-method-to-access-ugc}

Per accedere a UGC, utilizzate un metodo del pacchetto SocialResourceUtilities che restituisce un percorso adatto per l&#39;accesso a UGC da SRP e sostituisce il metodo obsoleto trovato nel pacchetto SocialUtils.

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

Per altre sostituzioni di SocialUtils, vedere [Refactoring SocialUtils](socialutils.md).

Per le linee guida sulla codifica, visitare [Accesso a UGC con SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>Il percorso resourceToUGCStoragePath() restituisce *not* adatto per il controllo ACL [](srp.md#for-access-control-acls).

## Metodo di utilità per accedere agli ACL {#utility-method-to-access-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community in database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell&#39;archivio locale in cui è possibile applicare gli ACL.

Utilizzando l&#39;API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione dell&#39;ombra prima di tutte le operazioni CRUD.

Per controllare gli ACL, utilizzare un metodo che restituisca un percorso adatto per verificare le autorizzazioni applicate all&#39;UGC della risorsa.

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
>Il percorso restituito da resourceToACLPath() è *not* adatto per [l&#39;accesso all&#39;UGC](#utility-method-to-access-acls) stesso.

## UGC: posizioni di storage correlate {#ugc-related-storage-locations}

Le seguenti descrizioni della posizione di storage possono essere di aiuto durante lo sviluppo con JSRP o forse MSRP. Attualmente non esiste alcuna interfaccia utente per accedere a UGC memorizzati in ASRP, in quanto esistono per JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) e MSRP (strumenti MongoDB).

**Posizione del componente**

Quando un membro accede a UGC nell’ambiente di pubblicazione, interagisce con un componente come parte di un sito AEM.

Un esempio di tale componente è il componente [commenti](http://localhost:4502/content/community-components/en/comments.html) presente nel sito [Community Components Guide](components-guide.md). Il percorso del nodo del commento nell&#39;archivio locale è:

* Percorso componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Posizione nodo ombreggiato**

La creazione di UGC crea anche un [nodo ombra](srp.md#about-shadow-nodes-in-jcr) a cui vengono applicati gli ACL necessari. Il percorso del nodo shadow corrispondente nell&#39;archivio locale è il risultato della precedenza del percorso principale del nodo shadow al percorso del componente:

* Percorso directory principale = `/content/usergenerated`
* Nodo ombra commento = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC, posizione**

L&#39;UGC viene creato in nessuna di queste posizioni e dovrebbe essere accessibile solo utilizzando un [metodo di utilità](#utility-method-to-access-ugc) che richiama l&#39;API SRP.

* Percorso directory principale = `/content/usergenerated/asi/srp-choice`
* Nodo UGC per JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Tenete presente* che per JSRP il nodo UGC è presente  ** solo nell’istanza AEM (autore o pubblicazione) in cui è stato immesso. Se immessa in un’istanza di pubblicazione, la moderazione non sarà possibile dalla console di moderazione sull’autore.

## Informazioni correlate {#related-information}

* [Panoramica](srp.md)  del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [Refactoring](socialutils.md)  SocialUtils - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.
