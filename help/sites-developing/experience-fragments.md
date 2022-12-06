---
title: Frammenti di esperienza
seo-title: Experience Fragments
description: Scopri come personalizzare i frammenti esperienza.
seo-description: Learn about customizing Experience Fragments.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: 6e54073a0c1d67218283b096db3f2e5597f10376
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 3%

---

# Frammenti di esperienza{#experience-fragments}

## Nozioni di base {#the-basics}

Un [Frammento esperienza](/help/sites-authoring/experience-fragments.md) è un gruppo di uno o più componenti, che include contenuto e layout, a cui è possibile fare riferimento tra le pagine.

Un elemento principale e/o variante del frammento esperienza utilizza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Poiché non esiste `/libs/cq/experience-fragments/components/xfpage/xfpage.html` ritorna a

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Rendering HTML semplice {#the-plain-html-rendition}

Utilizzo della `.plain.` nell’URL, puoi accedere al rendering semplice di HTML.

Questo è disponibile dal browser, ma il suo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti, implementazioni mobili personalizzate) di accedere direttamente al contenuto del frammento esperienza, utilizzando solo l’URL.

Il rendering HTML semplice aggiunge il protocollo, l&#39;host e il percorso contestuale a percorsi che sono:

* del tipo: `src`, `href`oppure `action`

* o termina con: `-src`oppure `-href`

Esempio:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>I collegamenti fanno sempre riferimento all’istanza di pubblicazione. Sono destinati a essere utilizzati da terze parti, pertanto il collegamento verrà sempre chiamato dall’istanza di pubblicazione, non dall’autore.

![xf-14](assets/xf-14.png)

Il selettore di rendering normale utilizza un trasformatore invece degli script aggiuntivi; la [Rewriter Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) viene utilizzato come trasformatore. Questa configurazione è disponibile in

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configurazione della generazione del rendering di HTML {#configuring-html-rendition-generation}

Il rendering di HTML viene generato utilizzando le pipeline di rewriter Sling. La pipeline è definita in `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML Transformer supporta le seguenti opzioni:

* `allowedCssClasses`
   * Espressione RegEx che corrisponde alle classi CSS che devono essere lasciate nel rendering finale.
   * Questa funzione è utile se il cliente desidera eliminare alcune classi CSS specifiche
* `allowedTags`
   * Elenco di tag HTML da consentire nel rendering finale.
   * Per impostazione predefinita sono consentiti i seguenti tag (non è necessaria alcuna configurazione): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link e script

Si consiglia di configurare il rewriter utilizzando una sovrapposizione. Vedi [Sovrapposizioni in AEM as a Cloud Service](/help/sites-developing/overlays.md)

## Variazioni social {#social-variations}

Le varianti social possono essere pubblicate sui social media (testo e immagine). In AEM queste varianti sociali possono contenere componenti; ad esempio, componenti di testo, componenti immagine.

L&#39;immagine e il testo per il post social possono essere estratti da qualsiasi tipo di risorsa immagine o di risorsa di testo a qualsiasi livello di profondità (nel blocco predefinito o nel contenitore di layout).

Le variazioni sociali permettono anche di creare elementi e di tenerli in considerazione quando si effettuano azioni sociali (sull&#39;ambiente di pubblicazione).

Per pubblicare il testo e l&#39;immagine corretti sul social media network, è necessario rispettare alcune convenzioni se si stanno sviluppando componenti personalizzati.

A questo scopo, è necessario utilizzare le seguenti proprietà:

* Per estrarre l’immagine

   * `fileReference`
   * `fileName`

* Estrazione del testo

   * `text`

I componenti che non utilizzano questa convenzione non saranno presi in considerazione.

## Modelli per frammenti esperienza {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo*** [modelli modificabili](/help/sites-developing/page-templates-editable.md) sono supportate per i frammenti esperienza.

Quando si sviluppa un nuovo modello per Frammenti esperienza è possibile seguire le pratiche standard per un [modello modificabile](/help/sites-developing/page-templates-editable.md).

Per creare un modello di frammento di esperienza rilevato dalla **Crea frammento esperienza** è necessario seguire uno dei seguenti set di regole:

1. Entrambe:

   1. Il tipo di risorsa del modello (il nodo iniziale) deve ereditare da:
      `cq/experience-fragments/components/xfpage`

   1. Il nome del modello deve iniziare con:
      `experience-fragments`
Questo consente agli utenti di creare frammenti di esperienza in /content/experience-fragments come 
`cq:allowedTemplates` La proprietà di questa cartella include tutti i modelli con nomi che iniziano con `experience-fragment`. I clienti possono aggiornare questa proprietà per includere i propri schemi di denominazione o posizioni di modelli.

1. [Modelli consentiti](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) può essere configurato nella console Frammenti esperienza .

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componenti per i frammenti esperienza {#components-for-experience-fragments}

[Sviluppo di componenti](/help/sites-developing/components.md) per l’utilizzo con/in Frammenti esperienza segui le pratiche standard.

L’unica configurazione aggiuntiva è quella di garantire che i componenti siano [consentito nel modello, questo viene ottenuto con i criteri dei contenuti](/help/sites-developing/page-templates-editable.md#content-policies).

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

In AEM puoi creare frammenti esperienza. Caratteristiche di un Frammento esperienza:

* è costituito da un gruppo di componenti e da un layout,
* può esistere indipendentemente da una pagina AEM.

Uno dei casi d’uso per tali gruppi è l’incorporazione di contenuto in punti di contatto di terze parti, ad esempio Adobe Target.

### Riscrittura del collegamento predefinito {#default-link-rewriting}

Utilizzo della [Esportazione in Target](/help/sites-administering/experience-fragments-target.md) puoi:

* creare un frammento esperienza,
* aggiungervi componenti,
* quindi esportalo come offerta Adobe Target, in formato HTML o in formato JSON.

Questa funzione può essere [abilitato su un&#39;istanza di authoring di AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Richiede una configurazione Adobe Target valida e configurazioni per il Link Externalizer.

L’Externalizer di collegamenti viene utilizzato per determinare gli URL corretti necessari per la creazione della versione HTML dell’offerta Target, che viene successivamente inviata ad Adobe Target. Ciò è necessario in quanto Adobe Target richiede che tutti i collegamenti all’interno dell’offerta di Target HTML siano accessibili al pubblico; ciò significa che tutte le risorse a cui fanno riferimento i collegamenti e il frammento esperienza stesso devono essere pubblicate prima di poter essere utilizzate.

Per impostazione predefinita, quando crei un’offerta HTML di Target, viene inviata una richiesta a un selettore Sling personalizzato in AEM. Questo selettore è denominato `.nocloudconfigs.html`. Come suggerisce il nome, crea un rendering HTML semplice di un frammento esperienza, ma non include configurazioni cloud (che sarebbero informazioni superflue).

Dopo aver generato la pagina HTML, la pipeline Sling Rewriter apporta modifiche all’output:

1. La `html`, `head`e `body` gli elementi vengono sostituiti con `div` elementi. La `meta`, `noscript` e `title` gli elementi vengono rimossi (sono elementi secondari dell&#39;originale `head` e non sono considerati quando viene sostituito dal `div` elemento).

   Questo viene fatto per garantire che l’offerta HTML Target possa essere inclusa nelle attività di Target.

1. AEM modifica tutti i collegamenti interni presenti in HTML, in modo che puntino a una risorsa pubblicata.

   Per determinare i collegamenti da modificare, AEM segue questo pattern per gli attributi degli elementi di HTML:

   1. `src` attributes
   1. `href` attributes
   1. `*-src` attributi (come data-src, custom-src, ecc.)
   1. `*-href` attributi (come `data-href`, `custom-href`, `img-href`, ecc.)

   >[!NOTE]
   >
   >Nella maggior parte dei casi, i collegamenti interni in HTML sono collegamenti relativi, ma in alcuni casi i componenti personalizzati forniscono URL completi in HTML. Per impostazione predefinita, AEM ignora questi URL completi e non apporta modifiche.

   I collegamenti in questi attributi vengono eseguiti tramite l’esternalizzatore di collegamenti AEM `publishLink()` per ricreare l’URL come se si trovasse su un’istanza pubblicata e, come tale, accessibile al pubblico.

Quando utilizzi un’implementazione standard, il processo descritto sopra dovrebbe essere sufficiente per generare l’offerta Target dal frammento esperienza e quindi esportarla in Adobe Target. Tuttavia, ci sono alcuni casi d&#39;uso che non vengono presi in considerazione in questo processo; tra cui:

* Sling Mapping disponibile solo nell’istanza di pubblicazione
* Reindirizzamenti di Dispatcher

Per questi casi d&#39;uso AEM fornisce l&#39;interfaccia Link Rewriter Provider.

### Interfaccia provider rewriter link {#link-rewriter-provider-interface}

>[!NOTE]
>
>Questa interfaccia è stata introdotta in [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/previous/6.5.1.md).

Per i casi più complicati, non coperti dal [default](#default-link-rewriting), AEM offre l’interfaccia Link Rewriter Provider. Questa è una `ConsumerType` interfaccia che puoi implementare nei tuoi bundle, come servizio. Ignora le modifiche AEM sui collegamenti interni di un’offerta HTML, come viene eseguito il rendering da un frammento esperienza. Questa interfaccia ti consente di personalizzare il processo di riscrittura dei collegamenti HTML interni in base alle tue esigenze aziendali.

Esempi di casi d’uso per l’implementazione di questa interfaccia come servizio includono:

* Le mappature Sling sono abilitate nelle istanze di pubblicazione, ma non nell’istanza di authoring
* Un dispatcher o una tecnologia simile viene utilizzata per reindirizzare internamente gli URL
* Ci sono `sling:alias mechanisms` in funzione delle risorse

>[!NOTE]
>
>Questa interfaccia elabora solo i collegamenti interni di HTML dall’offerta Target generata.

Interfaccia del provider di rewriter di collegamento ( `ExperienceFragmentLinkRewriterProvider`) è la seguente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Come utilizzare l&#39;interfaccia Link Rewriter Provider {#how-to-use-the-link-rewriter-provider-interface}

Per utilizzare l&#39;interfaccia è innanzitutto necessario creare un bundle contenente un nuovo componente di servizio che implementa l&#39;interfaccia Link Rewriter Provider.

Questo servizio verrà utilizzato per eseguire il plug in Experience Fragment Export to Target rewrite (Esportazione frammento esperienza in riscrittura) al fine di poter accedere ai vari collegamenti.

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

Affinché il servizio funzioni, sono ora necessari tre metodi all’interno del servizio:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Devi indicare al sistema se è necessario riscrivere i collegamenti quando viene effettuata una chiamata per l’esportazione in Target su una determinata variante del frammento esperienza. A tale scopo, implementa il metodo :

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Esempio:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Questo metodo riceve, come parametro, la Variazione del frammento esperienza che il sistema di esportazione in Target sta attualmente riscrivendo.

Nell’esempio precedente, desideriamo riscrivere:

* collegamenti presenti in `src`

* `href` solo attributi

* per un frammento esperienza specifico:
   `/content/experience-fragment/master`

Qualsiasi altro frammento esperienza passato attraverso il sistema Export to Target viene ignorato e non viene influenzato dalle modifiche implementate in questo servizio.

#### rewriteLink {#rewritelink}

Per la variante del frammento esperienza interessata dal processo di riscrittura, il servizio gestirà la riscrittura del collegamento. Ogni volta che viene rilevato un collegamento in HTML interno, viene richiamato il seguente metodo:

`rewriteLink(String link, String tag, String attribute)`

Come input, il metodo riceve i parametri:

* `link`Le azioni    
`String` rappresentazione del collegamento in corso di elaborazione. In genere si tratta di un URL relativo che punta alla risorsa sull’istanza di authoring.

* `tag`
Nome dell’elemento HTML in fase di elaborazione.

* `attribute`
Il nome esatto dell&#39;attributo.

Se, ad esempio, il sistema di esportazione in Target sta attualmente elaborando questo elemento, puoi definire `CSSInclude` come:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La chiamata al `rewriteLink()` viene eseguito utilizzando i seguenti parametri:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Quando crei il servizio puoi prendere decisioni in base al dato input e quindi riscrivere il collegamento di conseguenza.

Per il nostro esempio, desideriamo rimuovere il `/etc.clientlibs` parte dell’URL e aggiungi il dominio esterno appropriato. Per semplificare le cose, considereremo di avere accesso a un Resource Resolver per il tuo servizio, come in `rewriteLinkExample2`:

>[!NOTE]
>
>Per ulteriori informazioni su come ottenere un risolutore di risorse attraverso un utente di servizio, vedi [Utenti del servizio in AEM](/help/sites-administering/security-service-users.md).

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
>Se il metodo precedente restituisce `null`, quindi il sistema di esportazione in Target lascerà il collegamento così com’è, un collegamento relativo a una risorsa.

#### Priorità - getPriority {#priorities-getpriority}

Non è raro che siano necessari diversi servizi per gestire diversi tipi di frammenti esperienza o che sia anche necessario disporre di un servizio generico che gestisce l’esternalizzazione e la mappatura di tutti i frammenti esperienza. In questi casi, possono sorgere conflitti su quale servizio usare, quindi AEM offre la possibilità di definire **Priorità** per servizi diversi. Le priorità sono specificate utilizzando il metodo :

* `getPriority()`

Questo metodo consente l&#39;uso di diversi servizi quando `shouldRewrite()` restituisce true per lo stesso frammento esperienza. Il servizio che restituisce il numero più alto dal relativo `getPriority()`è il servizio che gestisce la variante del frammento esperienza.

Ad esempio, puoi avere un `GenericLinkRewriterProvider` che gestisce la mappatura di base per tutti i frammenti esperienza e quando `shouldRewrite()` restituisce il metodo `true` per tutte le varianti dei frammenti esperienza. Per diversi frammenti esperienza specifici, potresti voler usare una gestione speciale, quindi in questo caso puoi fornire un `SpecificLinkRewriterProvider` per i quali `shouldRewrite()` restituisce true solo per alcune varianti di frammento esperienza. Assicurati che `SpecificLinkRewriterProvider` viene scelto per gestire le varianti dei frammenti esperienza, deve restituire `getPriority()` un numero superiore a `GenericLinkRewriterProvider.`
