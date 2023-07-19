---
title: Estrazione di stringhe per la traduzione
seo-title: Extracting Strings for Translating
description: Utilizza xgettext-maven-plugin per estrarre le stringhe dal codice sorgente che richiedono la traduzione
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Estrazione di stringhe per la traduzione{#extracting-strings-for-translating}

Utilizza xgettext-maven-plugin per estrarre le stringhe dal codice sorgente che devono essere tradotte. Il plug-in Maven estrae le stringhe in un file XLIFF che invii per la traduzione. Le stringhe vengono estratte dalle seguenti posizioni:

* File Java di origine
* File sorgente JavaScript
* Rappresentazioni XML delle risorse SVN (nodi JCR)

## Configurazione dell’estrazione della stringa {#configuring-string-extraction}

Configura il modo in cui lo strumento xgettext-maven-plugin estrae le stringhe per il progetto.

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
| /parsers/vaultxml | Configura l&#39;analisi dei file Vault. Identifica i nodi JCR che contengono stringhe esternalizzate e hint di localizzazione. Identifica anche i nodi JCR da ignorare. |
| /parsers/javascript | Identifica le funzioni JavaScript che esternalizzano le stringhe. Non è necessario modificare questa sezione. |
| /parsers/regexp | Configura l’analisi dei file Java, JSP e del modello ExtJS. Non è necessario modificare questa sezione. |
| /potenziali | Formula per il rilevamento delle stringhe da internazionalizzare. |

### Identificazione dei file da analizzare {#identifying-the-files-to-parse}

La sezione /filter del file i18n.any identifica i file analizzati dallo strumento xgettext-maven-plugin. Aggiungi diverse regole di inclusione ed esclusione che identificano i file analizzati e ignorati, rispettivamente. È necessario includere tutti i file e quindi escludere i file che non si desidera analizzare. In genere, vengono esclusi i tipi di file che non contribuiscono all’interfaccia utente o i file che definiscono l’interfaccia utente ma che non vengono tradotti. Le regole di inclusione ed esclusione hanno il seguente formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

La parte pattern di una regola viene utilizzata per far corrispondere i nomi dei file da includere o escludere. Il prefisso del pattern indica se stai facendo corrispondere un nodo JCR (la sua rappresentazione in Vault) o il file system.

| Prefisso | Effetto |
|---|---|
| / | Indica un percorso JCR. Pertanto, questo prefisso corrisponde ai file sotto la directory jcr_root. |
| &amp;ast; | Indica un file normale nel file system. |
| nessuno | Nessun prefisso o pattern che inizia con una cartella o un nome di file indica un file normale nel file system. |

Se utilizzato all’interno di un pattern, il carattere / indica una sottodirectory e il carattere &amp;ast; corrisponde a tutto. Nella tabella seguente sono elencati diversi esempi di regole.

<table>
 <tbody>
  <tr>
   <th>Esempio di regola</th>
   <th>Effetto</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Includi tutti i file.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Escludi tutti i file PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Escludere i file POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Escludi tutti i file sotto il nodo /content.</p> <p>Includi il nodo /content/catalogs/geometrixx/templatepages.</p> <p>Includi tutti i nodi figlio di /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Estrazione delle stringhe  {#extracting-the-strings}

nessun POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Con POM: aggiungi a POM:

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
* `warn.log`: avvertenze (se presenti), se `CQ.I18n.getMessage()` L’API non viene utilizzata correttamente. Per queste operazioni è sempre necessaria una correzione e quindi una nuova esecuzione.

* `parserwarn.log`: avvisi del parser (se presenti), ad esempio problemi del parser js
* `potentials.xliff`: candidati &quot;potenziali&quot; che non vengono estratti, ma che potrebbero essere stringhe leggibili dall’uomo che necessitano di traduzione (possono essere ignorati, producono comunque una quantità enorme di falsi positivi)
* `strings.xliff`: file xliff appiattito, da importare in ALF
* `backrefs.txt`: consente la ricerca rapida delle posizioni del codice sorgente per una determinata stringa
