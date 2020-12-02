---
title: Creazione di filtri per gruppi di dispositivi
seo-title: Creazione di filtri per gruppi di dispositivi
description: Creare un filtro gruppo di dispositivi per definire un set di requisiti di funzionalità dispositivo
seo-description: Creare un filtro gruppo di dispositivi per definire un set di requisiti di funzionalità dispositivo
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---


# Creazione di filtri per gruppi di dispositivi{#creating-device-group-filters}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Create un filtro gruppo di dispositivi per definire un set di requisiti di funzionalità dei dispositivi. Create tutti i filtri necessari per eseguire il targeting dei gruppi necessari di funzionalità dei dispositivi.

Progettate i filtri in modo da poter utilizzare combinazioni di essi per definire i gruppi di funzionalità. In genere, esiste una sovrapposizione delle capacità di diversi gruppi di dispositivi. Di conseguenza, potete utilizzare alcuni filtri con più definizioni di gruppi di dispositivi.

Dopo aver creato un filtro, è possibile utilizzarlo nella configurazione [gruppo.](/help/sites-developing/mobile.md#creating-a-device-group)

## Classe Java del filtro {#the-filter-java-class}

Un filtro gruppo di dispositivi è un componente OSGi che implementa l&#39;interfaccia [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html). Quando viene distribuita, la classe di implementazione fornisce un servizio filtro disponibile per le configurazioni di gruppi di dispositivi.

La soluzione descritta in questo articolo utilizza il plugin Apache Felix Maven SCR per facilitare lo sviluppo del componente e del servizio. Di conseguenza, la classe Java di esempio utilizza le annotazioni `@Component`e `@Service`. La classe ha la struttura seguente:

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

È necessario fornire il codice per i metodi seguenti:

* `getDescription`: Restituisce la descrizione del filtro. La descrizione viene visualizzata nella finestra di dialogo di configurazione del gruppo di dispositivi.
* `getTitle`: Restituisce il nome del filtro. Il nome viene visualizzato quando si selezionano i filtri per il gruppo di dispositivi.
* `matches`: Determina se il dispositivo dispone delle funzionalità richieste.

### Nome e descrizione del filtro {#providing-the-filter-name-and-description}

I metodi `getTitle` e `getDescription` restituiscono rispettivamente il nome e la descrizione del filtro. Il codice seguente illustra l&#39;implementazione più semplice:

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

La codifica rigida del testo di nome e descrizione è sufficiente per gli ambienti di authoring in lingue diverse. Si consideri l&#39;esternalizzazione delle stringhe per uso multilingue, o per abilitare la modifica delle stringhe senza ricompilare il codice sorgente.

### Valutazione in base ai criteri del filtro {#evaluating-against-filter-criteria}

La funzione `matches` restituisce `true` se le funzionalità del dispositivo soddisfano tutti i criteri del filtro. Valutare le informazioni fornite negli argomenti del metodo per determinare se il dispositivo appartiene al gruppo. I seguenti valori sono forniti come argomenti:

* Un oggetto DeviceGroup
* Nome dell’agente utente
* Un oggetto Map che contiene le funzionalità del dispositivo. Le chiavi Mappa sono i nomi delle funzionalità WURFL™ e i valori sono i valori corrispondenti del database WURFL™.

L&#39;interfaccia [com.day.cq.wcm.mobile.api.devicvisti.DeviceSpecsCostanti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) contiene un sottoinsieme dei nomi delle funzionalità WURFL™ nei campi statici. Utilizzate queste costanti di campo come chiavi per il recupero dei valori dalla Mappa delle funzionalità dei dispositivi.

Ad esempio, il seguente esempio di codice determina se il dispositivo supporta CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

Il pacchetto `org.apache.commons.lang.math` fornisce la classe `NumberUtils`.

>[!NOTE]
>
>Assicurarsi che il database WURFL™ distribuito per AEM includa le funzionalità utilizzate come criteri di filtro. (Vedere [Rilevamento dispositivo](/help/sites-developing/mobile.md#server-side-device-detection).)

### Esempio di filtro per le dimensioni dello schermo {#example-filter-for-screen-size}

L&#39;implementazione di esempio DeviceGroupFilter che segue determina se la dimensione fisica del dispositivo soddisfa i requisiti minimi. Questo filtro consente di aggiungere granularità al gruppo di dispositivi touch. Le dimensioni dei pulsanti nell’interfaccia utente dell’applicazione devono essere uguali, indipendentemente dalle dimensioni fisiche dello schermo. Le dimensioni di altri elementi, come il testo, possono variare. Il filtro abilita la selezione dinamica di un particolare CSS che controlla le dimensioni degli elementi dell&#39;interfaccia utente.

Questo filtro applica i criteri di dimensione ai nomi delle proprietà `physical_screen_height` e `physical_screen_width` WURFL™.

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

![filteradtogroup](assets/filteraddtogroup.png)

I valori String restituiti dai metodi getTitle e getDescription sono inclusi nella parte inferiore della pagina di riepilogo del gruppo di dispositivi.

![filterdescription](assets/filterdescription.png)

### Il file POM Maven {#the-maven-pom-file}

Il seguente codice POM è utile se utilizzate Maven per creare le applicazioni. Il POM fa riferimento a diversi plug-in e dipendenze richiesti.

**Plug-in:**

* Plug-in Apache Maven Compiler: Compila le classi Java dal codice sorgente.
* Plug-in Apache Felix Maven Bundle: Crea il bundle e il manifesto
* Plugin Apache Felix Maven SCR: Crea il file descrittore del componente e configura l’intestazione del manifesto service-component.

**Dipendenze:**

* `cq-wcm-mobile-api-5.5.2.jar`: Fornisce le interfacce DeviceGroup e DeviceGroupFilter.

* `org.apache.felix.scr.annotations.jar`: Fornisce le annotazioni dei componenti e dei servizi.

Le interfacce DeviceGroup e DeviceGroupFilter sono incluse nel bundle API WCM Mobile Day Communique 5. Le annotazioni Felix sono incluse nel bundle Apache Felix Dichiarative Services. È possibile ottenere questo file JAR dal repository pubblico  Adobe.

Al momento dell&#39;authoring, 5.5.2 è la versione del bundle API WCM Mobile che si trova nell&#39;ultima versione di AEM. Utilizzate  console Web di Adobe ([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)) per verificare che si tratti della versione del bundle distribuita nell&#39;ambiente in uso.

**POM:** (il POM utilizzerà un ID e una versione groupId diversi).

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

Aggiungete il profilo che la sezione [Acquisizione del plug-in di Content Package Maven](/help/sites-developing/vlt-mavenplugin.md) fornisce al file delle impostazioni del cielo per utilizzare l&#39;archivio pubblico  Adobe.
