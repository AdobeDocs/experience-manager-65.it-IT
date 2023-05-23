---
title: Componenti di configurazione dei frammenti di contenuto per il rendering
seo-title: Content Fragments Configuring Components for Rendering
description: Componenti di configurazione dei frammenti di contenuto per il rendering
seo-description: Content Fragments Configuring Components for Rendering
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 7%

---

# Componenti di configurazione dei frammenti di contenuto per il rendering{#content-fragments-configuring-components-for-rendering}

Ce ne sono diversi [servizi avanzati](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) relative al rendering dei frammenti di contenuto. Per utilizzare questi servizi, i tipi di risorse di tali componenti devono farsi conoscere nel framework dei frammenti di contenuto.

Questa operazione viene eseguita configurando [Servizio OSGi - Configurazione del componente Frammento di contenuto](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Se non è necessario [servizi avanzati](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) come descritto di seguito, puoi ignorare questa configurazione.

>[!CAUTION]
>
>Quando estendi o utilizzi i componenti predefiniti, si sconsiglia di modificare la configurazione.

>[!CAUTION]
>
>Puoi scrivere da zero un componente che utilizza solo l’API Frammenti di contenuto, senza servizi avanzati. Tuttavia, in questo caso, dovrai sviluppare il componente in modo che gestisca l’elaborazione appropriata.
>
>Pertanto, si consiglia di utilizzare i Componenti core.

## Definizione dei servizi avanzati che richiedono la configurazione {#definition-of-advanced-services-that-need-configuration}

I servizi che richiedono la registrazione di un componente sono:

* Determinare correttamente le dipendenze durante la pubblicazione (ovvero, assicurarsi che frammenti e modelli possano essere pubblicati automaticamente con una pagina se sono stati modificati dopo l’ultima pubblicazione).
* Supporto per frammenti di contenuto nella ricerca full-text.
* La gestione/gestione di *contenuto intermedio.*
* La gestione/gestione di *risorse multimediali diverse.*
* Svuotamento del Dispatcher per i frammenti di riferimento (se viene ripubblicata una pagina contenente un frammento).
* Utilizzo del rendering basato su paragrafi.

Se hai bisogno di una o più di queste funzioni, in genere è più facile utilizzare la funzionalità preconfigurata, invece di svilupparla da zero.

## Servizio OSGi - Configurazione del componente Frammento di contenuto {#osgi-service-content-fragment-component-configuration}

La configurazione deve essere associata al servizio OSGi **Configurazione del componente Frammento di contenuto**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli.

Ad esempio:

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
   <td>Tipo di risorsa da registrare, ad esempio <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Proprietà di riferimento</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nome della proprietà che contiene il riferimento al frammento, ad esempio <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà elemento/i</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Il nome della proprietà che contiene i nomi degli elementi da riprodurre; ad esempio<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà variante</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Il nome della proprietà che contiene il nome della variante da riprodurre; ad esempio<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Per alcune funzionalità (ad esempio, per eseguire il rendering solo di un intervallo di paragrafi) è necessario attenersi ad alcune convenzioni:

<table>
 <tbody>
  <tr>
   <td>Nome proprietà</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una proprietà stringa che definisce l’intervallo di paragrafi da restituire se in <em>modalità di rendering di un singolo elemento</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code></li>
     <li>valutato solo se <code>paragraphScope</code> è impostato su <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una proprietà stringa che definisce come devono essere generati i paragrafi se in <em>modalità di rendering di un singolo elemento</em>.</p> <p>Valori:</p>
    <ul>
     <li><code>all</code> : per eseguire il rendering di tutti i paragrafi</li>
     <li><code>range</code> : per riprodurre l’intervallo di paragrafi fornito da <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una proprietà booleana che definisce se le intestazioni (ad esempio, <code>h1</code>, <code>h2</code>, <code>h3</code>) vengono conteggiati come paragrafi (<code>true</code>) o meno (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Questo potrebbe cambiare nelle fasi cardine successive di 6.5.

## Esempio {#example}

Ad esempio, consulta quanto segue (su un’istanza di AEM preconfigurata):

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
