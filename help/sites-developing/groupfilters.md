---
title: Creazione di filtri per gruppi di dispositivi
seo-title: Creating Device Group Filters
description: Creare un filtro gruppo di dispositivi per definire un set di requisiti di funzionalità dei dispositivi
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Creazione di filtri per gruppi di dispositivi{#creating-device-group-filters}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Crea un filtro per gruppi di dispositivi per definire un set di requisiti di funzionalità per dispositivi. Crea tutti i filtri necessari per eseguire il targeting dei gruppi necessari di funzionalità del dispositivo.

Progetta i filtri in modo da poterne utilizzare le combinazioni per definire i gruppi di funzionalità. In genere, le funzionalità dei diversi gruppi di dispositivi si sovrappongono. Pertanto, è possibile utilizzare alcuni filtri con più definizioni di gruppi di dispositivi.

Dopo aver creato un filtro, puoi utilizzarlo in [configurazione del gruppo.](/help/sites-developing/mobile.md#creating-a-device-group)

## Classe Java Filter {#the-filter-java-class}

Un filtro per gruppo di dispositivi è un componente OSGi che implementa [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) di rete. Quando distribuita, la classe di implementazione fornisce un servizio di filtro disponibile per le configurazioni dei gruppi di dispositivi.

La soluzione descritta in questo articolo utilizza il plug-in Apache Felix Maven SCR per facilitare lo sviluppo del componente e del servizio. Pertanto, la classe Java di esempio utilizza `@Component`e `@Service` annotazioni. La classe ha la seguente struttura:

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

Devi fornire il codice per i seguenti metodi:

* `getDescription`: restituisce la descrizione del filtro. La descrizione viene visualizzata nella finestra di dialogo di configurazione del gruppo di dispositivi.
* `getTitle`: restituisce il nome del filtro. Il nome viene visualizzato quando si selezionano i filtri per il gruppo di dispositivi.
* `matches`: determina se il dispositivo dispone delle funzionalità richieste.

### Inserimento del nome e della descrizione del filtro {#providing-the-filter-name-and-description}

Il `getTitle` e `getDescription` i metodi restituiscono rispettivamente il nome e la descrizione del filtro. Il codice seguente illustra l’implementazione più semplice:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

Per gli ambienti di authoring unilingua è sufficiente codificare il nome e il testo descrittivo. Prendere in considerazione l&#39;esternalizzazione delle stringhe per l&#39;utilizzo multilingue o per consentire la modifica delle stringhe senza ricompilare il codice sorgente.

### Valutazione in base ai criteri di filtro {#evaluating-against-filter-criteria}

Il `matches` restituisce funzione `true` se le funzionalità del dispositivo soddisfano tutti i criteri del filtro. Valutare le informazioni fornite negli argomenti del metodo per determinare se il dispositivo appartiene al gruppo. I seguenti valori vengono forniti come argomenti:

* Un oggetto DeviceGroup
* Nome dell’agente utente
* Oggetto Map contenente le funzionalità del dispositivo. Le chiavi della mappa sono i nomi delle funzionalità WURFL™ e i valori sono i valori corrispondenti del database WURFL™.

Il [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) L&#39;interfaccia contiene un sottoinsieme dei nomi delle funzionalità WURFL™ nei campi statici. Utilizza queste costanti di campo come chiavi per recuperare i valori dalla mappa delle funzionalità del dispositivo.

Ad esempio, il seguente esempio di codice determina se il dispositivo supporta i fogli di stile CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

Il `org.apache.commons.lang.math` fornisce il `NumberUtils` classe.

>[!NOTE]
>
>Assicurarsi che il database WURFL™ distribuito all&#39;AEM includa le funzionalità utilizzate come criteri di filtro. (vedere [Rilevamento dispositivo](/help/sites-developing/mobile.md#server-side-device-detection).)

### Esempio Di Filtro Per Le Dimensioni Dello Schermo {#example-filter-for-screen-size}

L&#39;esempio di implementazione di DeviceGroupFilter riportato di seguito determina se la dimensione fisica del dispositivo soddisfa i requisiti minimi. Questo filtro ha lo scopo di aggiungere granularità al gruppo di dispositivi touch. Le dimensioni dei pulsanti nell’interfaccia utente dell’applicazione devono essere uguali, indipendentemente dalle dimensioni fisiche dello schermo. Le dimensioni di altri elementi, ad esempio il testo, possono variare. Il filtro consente la selezione dinamica di un particolare CSS che controlla le dimensioni degli elementi dell’interfaccia utente.

Questo filtro applica i criteri di dimensione al `physical_screen_height` e `physical_screen_width` Nomi di proprietà WURFL™.

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

Il valore String restituito dal metodo getTitle viene visualizzato nell&#39;elenco a discesa delle proprietà del gruppo di dispositivi.

![filteraddtogroup](assets/filteraddtogroup.png)

I valori String restituiti dai metodi getTitle e getDescription sono inclusi nella parte inferiore della pagina di riepilogo del gruppo di dispositivi.

![filterdescription](assets/filterdescription.png)

### Il file POM Maven {#the-maven-pom-file}

Il seguente codice POM è utile se utilizzi Maven per creare le applicazioni. Il POM fa riferimento a diversi plug-in e dipendenze richiesti.

**Plug-in:**

* Plug-in del compilatore Apache Maven: compila le classi Java dal codice sorgente.
* Plug-in Apache Felix Maven Bundle: crea il bundle e il manifesto
* Plug-in Apache Felix Maven SCR: crea il file del descrittore del componente e configura l’intestazione del manifesto del servizio-componente.

**Dipendenze:**

* `cq-wcm-mobile-api-5.5.2.jar`: fornisce le interfacce DeviceGroup e DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`: fornisce le annotazioni del componente e del servizio.

Le interfacce DeviceGroup e DeviceGroupFilter sono incluse nel bundle Day Communique 5 WCM Mobile API. Le annotazioni Felix sono incluse nel bundle Apache Felix Declarative Services. Puoi ottenere questo file JAR dall’archivio di Adobi pubblico.

Al momento dell’authoring, 5.5.2 è la versione del bundle WCM Mobile API che si trova nell’ultima versione dell’AEM. Utilizza la console web di Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) per assicurarti che questa sia la versione del bundle implementata nell’ambiente.

**POM:** Il POM utilizzerà un groupId e una versione diversi.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

Aggiungi il profilo che [Ottenere il plug-in Maven del pacchetto di contenuti](/help/sites-developing/vlt-mavenplugin.md) fornisce al file delle impostazioni maven di utilizzare l’archivio di Adobi pubblico.
