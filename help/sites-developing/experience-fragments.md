---
title: Frammenti esperienza
seo-title: Frammenti esperienza
description: Scopri come personalizzare i frammenti esperienza.
seo-description: Scopri come personalizzare i frammenti esperienza.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b

---


# Frammenti esperienza{#experience-fragments}

## Nozioni di base {#the-basics}

Un [Frammento esperienza](/help/sites-authoring/experience-fragments.md) è un gruppo di uno o più componenti, che include contenuto e layout, a cui è possibile fare riferimento tra le pagine.

Un elemento principale e/o variante del frammento esperienza utilizza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Poiché non esiste, `/libs/cq/experience-fragments/components/xfpage/xfpage.html` viene ripristinato

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## La rappresentazione HTML semplice {#the-plain-html-rendition}

Utilizzando il `.plain.` selettore nell’URL, potete accedere alla rappresentazione HTML semplice.

Questo è disponibile dal browser, ma il suo scopo principale è consentire ad altre applicazioni (ad esempio, app Web di terze parti, implementazioni mobili personalizzate) di accedere direttamente al contenuto del frammento esperienza, utilizzando solo l&#39;URL.

La rappresentazione HTML semplice aggiunge protocollo, host e percorso contestuale a percorsi che sono:

* del tipo: `src`, `href`oppure `action`

* o terminare con: `-src`, oppure `-href`

Esempio:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>I collegamenti fanno sempre riferimento all’istanza di pubblicazione. Sono destinati a essere utilizzati da terzi, pertanto il collegamento verrà sempre chiamato dall’istanza pubblica, non dall’autore.

![xf-14](assets/xf-14.png)

Il selettore di rappresentazione semplice utilizza un trasformatore invece di script aggiuntivi; il trasformatore [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) . Questa è configurata in

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variazioni social {#social-variations}

Le varianti social possono essere pubblicate sui social media (testo e immagine). In AEM queste varianti social possono contenere componenti; ad esempio, componenti di testo, componenti immagine.

L&#39;immagine e il testo per il post social possono essere tratti da qualsiasi tipo di risorsa immagine o testo a qualsiasi livello di profondità (nel blocco predefinito o nel contenitore di layout).

Le variazioni sociali consentono anche di creare blocchi e di tenerne conto quando si effettuano azioni sociali (nell’ambiente di pubblicazione).

Per pubblicare il testo e l&#39;immagine corretti sul social media, alcune convenzioni devono essere rispettate se state sviluppando componenti personalizzati.

A tal fine, è necessario utilizzare le seguenti proprietà:

* Per l&#39;estrazione dell&#39;immagine

   * `fileReference`
   * `fileName`

* Per l&#39;estrazione del testo

   * `text`

I componenti che non utilizzano questa convenzione non saranno presi in considerazione.

## Modelli per frammenti esperienza {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Per i frammenti esperienza sono supportati solo*** i modelli [](/help/sites-developing/page-templates-editable.md) modificabili.

Nello sviluppo di un nuovo modello per i frammenti esperienza, puoi seguire le procedure standard per un modello [](/help/sites-developing/page-templates-editable.md)modificabile.

Per creare un modello di frammento esperienza rilevato dalla procedura guidata **Crea frammento** esperienza, è necessario seguire uno dei seguenti set di regole:

1. Entrambe:

   1. Il tipo di risorsa del modello (il nodo iniziale) deve ereditare da:
      `cq/experience-fragments/components/xfpage`

   1. Il nome del modello deve iniziare con:
      `experience-fragments`
Questo consente agli utenti di creare frammenti esperienza in /content/experience-fragments, poiché la `cq:allowedTemplates` proprietà di questa cartella include tutti i modelli con nomi che iniziano con `experience-fragment`. I clienti possono aggiornare questa proprietà per includere i propri schemi di denominazione o le posizioni dei modelli.

1. [I modelli](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) consentiti possono essere configurati nella console Frammenti esperienza.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componenti per frammenti esperienza {#components-for-experience-fragments}

[Lo sviluppo di componenti](/help/sites-developing/components.md) utilizzabili con/in frammenti esperienza segue le procedure standard.

L&#39;unica configurazione aggiuntiva consiste nell&#39;assicurare che i componenti siano [consentiti nel modello, come avviene con l&#39;applicazione Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

In AEM è possibile creare frammenti esperienza. Caratteristiche di un Frammento esperienza:

* è costituito da un gruppo di componenti con un layout,
* può esistere indipendentemente da una pagina AEM.

Uno dei casi d’uso per tali gruppi è l’incorporazione di contenuto nei punti di contatto di terze parti, come Adobe Target.

### Riscrittura collegamento predefinito {#default-link-rewriting}

Utilizzando la funzione [Esporta in Target](/help/sites-administering/experience-fragments-target.md) , potete:

* creare un frammento esperienza,
* aggiungere componenti,
* quindi esportatelo come offerta Adobe Target, in formato HTML o in formato JSON.

Questa funzione può essere [attivata in un’istanza di authoring di AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Richiede una configurazione Adobe Target valida e configurazioni per Link Externalizer.

Link Externalizer viene utilizzato per determinare gli URL corretti necessari alla creazione della versione HTML dell&#39;offerta Target, che viene successivamente inviata ad Adobe Target. Ciò è necessario in quanto Adobe Target richiede che tutti i collegamenti all&#39;interno dell&#39;offerta HTML di Target siano accessibili al pubblico; ciò significa che tutte le risorse a cui fanno riferimento i collegamenti e il frammento esperienza devono essere pubblicate prima di poter essere utilizzate.

Per impostazione predefinita, quando create un&#39;offerta HTML Target, una richiesta viene inviata a un selettore Sling personalizzato in AEM. Questo selettore è chiamato `.nocloudconfigs.html`. Come suggerisce il nome, crea un rendering HTML semplice di un frammento esperienza, ma non include configurazioni cloud (che sarebbero informazioni superflue).

Dopo aver generato la pagina HTML, la pipeline Sling Rewriter apporta modifiche all&#39;output:

1. Gli `html`elementi, `head`e `body` sono sostituiti da `div` elementi. Gli `meta`, `noscript` e `title` gli elementi vengono rimossi (sono elementi secondari dell&#39; `head` elemento originale e non vengono considerati quando questo viene sostituito dall&#39; `div` elemento).

   Questo viene fatto per garantire che l&#39;offerta HTML Target possa essere inclusa nelle attività Target.

1. AEM modifica tutti i collegamenti interni presenti nell’HTML, in modo che puntino a una risorsa pubblicata.

   Per determinare i collegamenti da modificare, AEM segue questo pattern per gli attributi degli elementi HTML:

   1. `src` attribute
   1. `href` attribute
   1. `*-src` attributi (come data-src, custom-src, ecc.)
   1. `*-href` attributi (come `data-href`, `custom-href`, `img-href`, ecc.)
   >[!NOTE]
   >
   >Nella maggior parte dei casi, i collegamenti interni nell’HTML sono collegamenti relativi, ma potrebbero verificarsi casi in cui i componenti personalizzati forniscono URL completi nell’HTML. Per impostazione predefinita, AEM ignora questi URL completamente acquisiti e non apporta alcuna modifica.

   I collegamenti di questi attributi vengono eseguiti tramite AEM Link Externalizer `publishLink()` per ricreare l’URL come se si trovasse in un’istanza pubblicata e, come tale, disponibile al pubblico.

Quando si utilizza un&#39;implementazione out-of-the-box, il processo descritto sopra dovrebbe essere sufficiente per generare l&#39;offerta Target dal frammento esperienza e quindi esportarla in Adobe Target. Esistono tuttavia alcuni casi d&#39;uso che non vengono presi in considerazione in questo processo; tra cui:

* Mappatura Sling disponibile solo nell’istanza di pubblicazione
* Reindirizzamento del dispatcher

Per questi casi d’uso, AEM fornisce l’interfaccia per il provider di rewriter dei collegamenti.

### Interfaccia provider rewriter link {#link-rewriter-provider-interface}

>[!NOTE]
>
>Questa interfaccia è stata introdotta in [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Per i casi più complessi, non coperti dall’ [impostazione predefinita](#default-link-rewriting), AEM offre l’interfaccia Link Rewriter Provider. Questa è un&#39; `ConsumerType` interfaccia che puoi implementare nei tuoi bundle, come servizio. Ignora le modifiche eseguite da AEM sui collegamenti interni di un&#39;offerta HTML rappresentata da un frammento esperienza. Questa interfaccia consente di personalizzare il processo di riscrittura dei collegamenti HTML interni in base alle esigenze aziendali.

Esempi di casi d’uso per l’implementazione di questa interfaccia come servizio:

* Le mappature Sling sono abilitate nelle istanze pubblicate, ma non nell’istanza di creazione
* Un dispatcher o una tecnologia simile viene utilizzata per reindirizzare internamente gli URL
* Sono `sling:alias mechanisms` disponibili risorse

>[!NOTE]
>
>Questa interfaccia elabora solo i collegamenti HTML interni dall&#39;offerta Target generata.

L&#39;interfaccia del provider di rewriter del collegamento ( `ExperienceFragmentLinkRewriterProvider`) è la seguente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Come utilizzare l&#39;interfaccia del provider di rewriter del collegamento {#how-to-use-the-link-rewriter-provider-interface}

Per utilizzare l&#39;interfaccia occorre innanzitutto creare un bundle contenente un nuovo componente di servizio che implementa l&#39;interfaccia Link Rewriter Provider.

Questo servizio verrà utilizzato per collegarsi alla riscrittura di Experience Fragment Export to Target al fine di poter accedere ai vari collegamenti.

Esempio, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Per il funzionamento del servizio, sono ora necessari tre metodi di implementazione all&#39;interno del servizio:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### mustRewrite {#shouldrewrite}

È necessario indicare al sistema se è necessario riscrivere i collegamenti quando viene effettuata una chiamata per l&#39;esportazione in Target in una determinata variante di frammento esperienza. A tal fine, implementate il metodo:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Esempio:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Questo metodo riceve, come parametro, la Variazione frammento esperienza che il sistema Esporta in Target sta riscritgendo.

Nell&#39;esempio precedente, desideriamo riscrivere:

* collegamenti presenti in `src`

* `href` solo attributi

* per un frammento esperienza specifico:
   `/content/experience-fragment/master`

Eventuali altri frammenti esperienza passati attraverso il sistema Esporta in Target vengono ignorati e non sono interessati dalle modifiche implementate in questo servizio.

#### rewriteLink {#rewritelink}

Per la variante del frammento esperienza interessata dal processo di riscrittura, il servizio dovrà quindi gestire la riscrittura del collegamento. Ogni volta che viene rilevato un collegamento nell’HTML interno, viene richiamato il metodo seguente:

`rewriteLink(String link, String tag, String attribute)`

Come input, il metodo riceve i parametri:

* `link`
La `String` rappresentazione del collegamento attualmente in fase di elaborazione. Si tratta in genere di un URL relativo che indica la risorsa nell’istanza di creazione.

* `tag`
Nome dell&#39;elemento HTML attualmente in fase di elaborazione.

* `attribute`
Il nome esatto dell&#39;attributo.

Se, ad esempio, il sistema Esporta in Target sta elaborando questo elemento, potete definire `CSSInclude` come:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La chiamata al `rewriteLink()` metodo viene effettuata utilizzando i seguenti parametri:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Quando crei il servizio puoi prendere decisioni in base all&#39;input specificato e quindi riscrivere il collegamento di conseguenza.

Ad esempio, vorremmo rimuovere la `/etc.clientlibs` parte dell’URL e aggiungere il dominio esterno appropriato. Per semplificare le cose, considereremo di avere accesso a un Resource Resolver per il vostro servizio, come in `rewriteLinkExample2`:

>[!NOTE]
>
>Per ulteriori informazioni su come ottenere un risolutore delle risorse tramite un utente di servizi, consultate Utenti [di servizi in AEM](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Se il metodo precedente restituisce `null`, il sistema Esporta in Target lascerà il collegamento così com’è, un collegamento relativo a una risorsa.

#### Priorità - getPriority {#priorities-getpriority}

Non è raro che siano necessari diversi servizi per gestire diversi tipi di frammenti esperienza, o che sia disponibile un servizio generico che gestisce l&#39;esternalizzazione e la mappatura di tutti i frammenti esperienza. In questi casi, potrebbero sorgere conflitti su quale servizio utilizzare, pertanto AEM offre la possibilità di definire **le priorità** per i diversi servizi. Le priorità sono specificate utilizzando il metodo:

* `getPriority()`

Questo metodo consente l’uso di diversi servizi se il `shouldRewrite()` metodo restituisce true per lo stesso frammento esperienza. Il servizio che restituisce il numero più alto dal relativo `getPriority()`metodo è il servizio che gestisce la variante del frammento esperienza.

Ad esempio, puoi disporre di un elemento `GenericLinkRewriterProvider` che gestisce la mappatura di base per tutti i frammenti esperienza e quando il `shouldRewrite()` metodo restituisce `true` per tutte le varianti di frammento esperienza. Per diversi frammenti esperienza specifici, può essere utile una gestione speciale, pertanto in questo caso è possibile specificare un valore `SpecificLinkRewriterProvider` `shouldRewrite()` per il quale il metodo restituisce true solo per alcune Variazioni frammento esperienza. Per essere certi che `SpecificLinkRewriterProvider` venga scelto di gestire tali Variazioni di frammento esperienza, nel suo `getPriority()` metodo deve essere restituito un numero maggiore di `GenericLinkRewriterProvider.`
