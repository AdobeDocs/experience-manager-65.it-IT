---
title: Estrazione di stringhe per la conversione
seo-title: Estrazione di stringhe per la conversione
description: Utilizzate xgettext-maven-plugin per estrarre le stringhe dal codice sorgente che devono essere tradotte
seo-description: Utilizzate xgettext-maven-plugin per estrarre le stringhe dal codice sorgente che devono essere tradotte
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Estrazione di stringhe per tradurre{#extracting-strings-for-translating}

Utilizzate xgettext-maven-plugin per estrarre le stringhe dal codice sorgente che devono essere tradotte. Il plugin Maven estrae le stringhe in un file XLIFF che si invia per la traduzione. Le stringhe vengono estratte dalle seguenti posizioni:

* File sorgente Java
* File sorgente JavaScript
* Rappresentazioni XML delle risorse SVN (nodi JCR)

## Configurazione dell&#39;estrazione della stringa {#configuring-string-extraction}

Configurate il modo in cui lo strumento xgettext-maven-plugin estrae le stringhe per il progetto.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| Sezione | Descrizione |
|---|---|
| /filter | Identifica i file analizzati. |
| /parser/vaultxml | Configura l&#39;analisi dei file Vault. Identifica i nodi JCR che contengono stringhe esternalizzate e suggerimenti per la localizzazione. Identifica anche i nodi JCR da ignorare. |
| /parser/javascript | Identifica le funzioni JavaScript che esternalizzano le stringhe. Non è necessario modificare questa sezione. |
| /parser/regexp | Configura l’analisi dei file Java, JSP e ExtJS Template. Non è necessario modificare questa sezione. |
| /potenziale | Formula per il rilevamento di stringhe da internazionalizzare. |

### Identificazione dei file da analizzare {#identifying-the-files-to-parse}

La sezione /filter del file i18n.any identifica i file analizzati dallo strumento xgettext-maven-plugin. Aggiungete diverse regole di inclusione ed esclusione che identificano i file analizzati e ignorati, rispettivamente. Includete tutti i file ed escludete quelli che non desiderate analizzare. In genere, si escludono i tipi di file che non contribuiscono all’interfaccia utente o i file che definiscono l’interfaccia utente ma che non vengono convertiti. Le regole di inclusione ed esclusione hanno il formato seguente:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

La parte pattern di una regola viene utilizzata per corrispondere ai nomi dei file da includere o escludere. Il prefisso del pattern indica se il nodo JCR (la sua rappresentazione in Vault) o il file system corrisponde.

| Prefisso | Effetto |
|---|---|
| / | Indica un percorso JCR. Pertanto, questo prefisso corrisponde ai file sotto la directory jcr_root. |
| &amp;ast; | Indica un file regolare nel file system. |
| nessuno | Nessun prefisso o un pattern che inizia con un nome di cartella o file indica un file regolare nel file system. |

Se utilizzato all&#39;interno di un pattern, il carattere / indica una sottodirectory e &amp;ast; il carattere corrisponde a tutti. Nella tabella seguente sono elencate diverse regole di esempio.

<table>
 <tbody>
  <tr>
   <th>Regola di esempio</th>
   <th>Effetto</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Includi tutti i file.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Escludete tutti i file PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Escludere i file POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Escludete tutti i file sotto il nodo /content.</p> <p>Includete il nodo /content/catalog/geometrixx/templatepages.</p> <p>Includete tutti i nodi secondari di /content/catalog/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Estrazione delle stringhe {#extracting-the-strings}

nessun POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Con POM: Aggiungi questo a POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

il comando:

```shell
mvn xgettext:extract
```

### File di output {#output-files}

* `raw.xliff`: stringhe estratte
* `warn.log`: eventuali avvertenze, se l&#39; `CQ.I18n.getMessage()` API viene utilizzata in modo errato. Questi hanno sempre bisogno di una correzione e poi di una nuova esecuzione.

* `parserwarn.log`: eventuali avvertenze del parser, ad esempio problemi del parser js
* `potentials.xliff`: candidati &quot;potenziali&quot; che non sono estratti, ma potrebbero essere stringhe leggibili dall&#39;uomo che necessitano di traduzione (possono essere ignorati, producono ancora una grande quantità di falsi positivi)
* `strings.xliff`: file xliff appiattito, da importare in ALF
* `backrefs.txt`: consente la ricerca rapida delle posizioni del codice sorgente per una determinata stringa

