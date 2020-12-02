---
title: Componenti di configurazione dei frammenti di contenuto per il rendering
seo-title: Componenti di configurazione dei frammenti di contenuto per il rendering
description: Componenti di configurazione dei frammenti di contenuto per il rendering
seo-description: Componenti di configurazione dei frammenti di contenuto per il rendering
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---


# Componenti di configurazione dei frammenti di contenuto per il rendering{#content-fragments-configuring-components-for-rendering}

Esistono diversi [servizi avanzati](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) correlati al rendering dei frammenti di contenuto. Per utilizzare questi servizi, i tipi di risorse di tali componenti devono essere resi noti al framework dei frammenti di contenuto.

Questa operazione viene eseguita configurando il [servizio OSGi - configurazione componente frammento di contenuto](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Se non è necessario disporre dei [servizi avanzati](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) descritti di seguito, puoi ignorare questa configurazione.

>[!CAUTION]
>
>Quando si estendono o si utilizzano i componenti forniti, non è consigliabile modificare la configurazione.

>[!CAUTION]
>
>È possibile scrivere un componente da zero che utilizza solo l&#39;API dei frammenti di contenuto, senza servizi avanzati. Tuttavia, in tal caso, sarà necessario sviluppare il componente in modo che gestisca l’elaborazione appropriata.
>
>Si consiglia pertanto di utilizzare i componenti core.

## Definizione di servizi avanzati che richiedono la configurazione {#definition-of-advanced-services-that-need-configuration}

I servizi che richiedono la registrazione di un componente sono:

* Determinazione corretta delle dipendenze durante la pubblicazione (ad esempio, verificare che frammenti e modelli possano essere pubblicati automaticamente con una pagina se sono stati modificati dall’ultima pubblicazione).
* Supporto per i frammenti di contenuto nella ricerca full-text.
* Gestione/gestione di *contenuti intermedi.*
* Gestione/gestione di *risorse multimediali diverse.*
* Dispatcher flush per i frammenti di riferimento (se una pagina contenente un frammento viene pubblicata nuovamente).
* Utilizzo del rendering basato su paragrafo.

Se avete bisogno di una o più di queste funzioni, è più semplice utilizzare la funzionalità out-of-the-box, anziché svilupparla da zero.

## Servizio OSGi - Configurazione componente frammento di contenuto {#osgi-service-content-fragment-component-configuration}

La configurazione deve essere associata al servizio OSGi **Configurazione componente frammento di contenuto**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Esempio:

![cfm-01](assets/cfm-01.png)

La configurazione OSGi è:

<table>
 <tbody>
  <tr>
   <td>Etichetta</td>
   <td>Configurazione OSGi<br /> </td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><strong>Tipo risorsa</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>Il tipo di risorsa da registrare; ad esempio <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Proprietà Reference</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nome della proprietà contenente il riferimento al frammento; ad esempio <code>fragmentPath</code> oppure <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà Element(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Il nome della proprietà che contiene i nomi degli elementi di cui eseguire il rendering; ad esempio<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà variante</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Il nome della proprietà che contiene il nome della variante da rappresentare; ad esempio<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Per alcune funzionalità (ad es. per eseguire il rendering solo di un intervallo di paragrafi), dovrete aderire ad alcune convenzioni:

<table>
 <tbody>
  <tr>
   <td>Nome proprietà</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una proprietà stringa che definisce l'intervallo di paragrafi da restituire se in <em>modalità di rendering elemento singolo</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> oppure <code>1-3</code> o <code>1-3;6;7-8</code> oppure <code>*-3;5-*</code></li>
     <li>valutato solo se <code>paragraphScope</code> è impostato su <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una proprietà stringa che definisce la modalità di output dei paragrafi in <em>modalità di rendering a elemento singolo</em>.</p> <p>Valori:</p>
    <ul>
     <li><code>all</code> : per eseguire il rendering di tutti i paragrafi</li>
     <li><code>range</code> : per eseguire il rendering dell'intervallo di paragrafi fornito da <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una proprietà booleana che definisce se le intestazioni (ad esempio, <code>h1</code>, <code>h2</code>, <code>h3</code>) sono conteggiate come paragrafi (<code>true</code>) o meno (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Questo può cambiare in 6,5 tappe successive.

## Esempio {#example}

Ad esempio, vedete quanto segue (in un&#39;istanza AEM out-of-the-box):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

