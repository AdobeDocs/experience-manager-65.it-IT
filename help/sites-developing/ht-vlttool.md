---
title: Come utilizzare lo strumento VLT
seo-title: How to use the VLT Tool
description: Lo strumento Jackrabbit FileVault (VLT) è sviluppato da The Apache Foundation che mappa il contenuto di un’istanza Jackrabbit/AEM sul file system
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 1%

---

# Come utilizzare lo strumento VLT {#how-to-use-the-vlt-tool}

Lo strumento Jackrabbit FileVault (VLT) è uno strumento sviluppato da [Apache Foundation](https://www.apache.org/) che mappa il contenuto di un’istanza Jackrabbit/AEM sul file system. Lo strumento VLT ha funzioni simili a quelle del client del sistema di controllo del codice sorgente (ad esempio un client SVN), che fornisce le normali operazioni di check-in, check-out e gestione, nonché opzioni di configurazione per una rappresentazione flessibile del contenuto del progetto.

Lo strumento VLT viene eseguito dalla riga di comando. Questo documento descrive come utilizzare lo strumento, tra cui come iniziare e ottenere assistenza, nonché un elenco di tutti [comandi](#vlt-commands) e disponibili [opzioni](#vlt-global-options).

## Concetti e architettura {#concepts-and-architecture}

Consulta la [Panoramica di Filevault](https://jackrabbit.apache.org/filevault/overview.html) e [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) pagina del funzionario [Documentazione di Apache Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/index.html) per una panoramica completa dei concetti e della struttura dello strumento Filevault.

## Guida introduttiva a VLT {#getting-started-with-vlt}

Per iniziare a utilizzare VLT, è necessario effettuare le seguenti operazioni:

1. Installa VLT, aggiorna le variabili di ambiente e aggiorna i file di sovversione globali ignorati.
1. Configurare l’archivio AEM (se non lo si è già fatto).
1. Consulta l’archivio dell’AEM.
1. Sincronizza con l’archivio.
1. Verifica del funzionamento della sincronizzazione.

### Installazione dello strumento VLT {#installing-the-vlt-tool}

Per utilizzare lo strumento VLT, è innanzitutto necessario installarlo. Non viene installato per impostazione predefinita in quanto è uno strumento aggiuntivo. Inoltre, è necessario impostare la variabile di ambiente del sistema.

1. Scaricare il file di archivio FileVault dalla [Archivio di artefatti Maven.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >L&#39;origine dello strumento VLT è [disponibile su GitHub.](https://github.com/apache/jackrabbit-filevault)
1. Estrai l’archivio.
1. Aggiungi `<archive-dir>/vault-cli-<version>/bin` nell&#39;ambiente `PATH` in modo che i file di comando `vlt` o `vlt.bat` sono accessibili a seconda delle necessità. Ad esempio:

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Apri una shell della riga di comando ed esegui `vlt --help`. Assicurati che l’output sia simile alla seguente schermata della guida:

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

Dopo averlo installato, è necessario aggiornare i file di sovversione ignorati globali. Modifica le impostazioni svn e aggiungi quanto segue:

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### Configurazione del carattere di fine riga {#configuring-the-end-of-line-character}

VLT gestisce automaticamente la fine della linea (EOF) in base alle seguenti regole:

* righe di file estratte in Windows terminano con un `CRLF`
* righe di file estratte su Linux/Unix con una `LF`
* righe di file di cui è stato eseguito il commit nel repository che terminano con un `LF`

Per garantire la corrispondenza tra la configurazione VLT e SVN, è necessario impostare `svn:eol-style` proprietà a `native` per l’estensione dei file memorizzati nell’archivio. Modifica le impostazioni svn e aggiungi quanto segue:

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### Estrazione dell&#39;archivio {#checking-out-the-repository}

Estrarre l&#39;archivio utilizzando il sistema di controllo del codice sorgente. In svn, ad esempio, digita quanto segue (sostituendo l’URI e il percorso con l’archivio):

```shell
svn co https://svn.server.com/repos/myproject
```

### Sincronizzazione con l’archivio {#synchronizing-with-the-repository}

È necessario sincronizzare filevault con l&#39;archivio. Per effettuare questo collegamento:

1. Nella riga di comando, passa a `content/jcr_root`.
1. Estrarre l&#39;archivio digitando quanto segue (sostituendo il numero di porta con **4502** e password amministratore):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >Le credenziali devono essere specificate una sola volta al momento del check-out iniziale. Vengono quindi archiviati nella home directory all’interno di `.vault/auth.xml`.

### Verifica del funzionamento della sincronizzazione {#testing-whether-the-synchronization-worked}

Dopo aver estratto il repository e averlo sincronizzato, è necessario eseguire un test per verificare che tutto funzioni correttamente. Un modo semplice per farlo è modificare una **.jsp** e verifica se le modifiche vengono applicate dopo il commit delle modifiche.

Per verificare la sincronizzazione:

1. Accedi a `.../jcr_content/libs/foundation/components/text`.
1. Modificare un elemento in `text.jsp`.
1. Visualizza i file modificati digitando `vlt st`
1. Visualizza le modifiche digitando `vlt diff text.jsp`
1. Eseguire il commit delle modifiche: `vlt ci test.jsp`.
1. Ricarica una pagina contenente un componente testo e verifica se le modifiche sono presenti.

## Come trovare assistenza con lo strumento VLT {#getting-help-with-the-vlt-tool}

Dopo aver installato lo strumento VLT, è possibile accedere al relativo file della Guida dalla riga di comando:

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

Per informazioni della Guida su un comando specifico, digitare il comando help seguito dal nome del comando. Ad esempio:

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## Attività comuni eseguite in VLT {#common-tasks-performed-in-vlt}

Di seguito sono riportate alcune attività comuni eseguite in VLT. Per informazioni dettagliate su ciascun comando, vedere [comandi](#vlt-commands).

### Estrazione di una sottostruttura {#checking-out-a-subtree}

Se ad esempio si desidera estrarre solo una sottostruttura del repository, `/apps/geometrixx`, a tale scopo, digitare quanto segue:

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

In questo modo viene creata una nuova directory principale di esportazione `geo` con un `META-INF` e `jcr_root` e inserisce tutti i file sotto `/apps/geometrixx` in `geo/jcr_root`.

### Esecuzione di un Check-Out filtrato {#performing-a-filtered-checkout}

Se disponi di un filtro dell’area di lavoro esistente e desideri utilizzarlo per il pagamento, puoi prima creare il `META-INF/vault` e posizionare il filtro in tale directory oppure specificarlo nella riga di comando come indicato di seguito:

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

Esempio di filtro:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### Utilizzo di Import/Export al posto del controllo .vlt {#using-import-export-instead-of-vlt-control}

Puoi importare ed esportare contenuti tra un archivio JCR e il file system locale senza utilizzare i control file.

Per importare ed esportare contenuti senza utilizzare `.vlt` controllo:

1. Impostazione iniziale dell&#39;archivio:

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. Modifica la copia remota e aggiorna JCR:

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. Modificare la copia remota e aggiornare il file server:

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## Utilizzo di VLT {#using-vlt}

Per eseguire comandi in VLT, digitare quanto segue nella riga di comando:

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

Le opzioni e i comandi sono descritti in dettaglio nelle sezioni seguenti.

## Opzioni globali VLT {#vlt-global-options}

Di seguito è riportato un elenco di opzioni VLT disponibili per tutti i comandi. Per ulteriori informazioni sulle opzioni disponibili, vedere i singoli comandi.

|  |  |
|--- |--- |
| Opzione | Descrizione |
| `-Xjcrlog <arg>` | Opzioni JcrLog estese |
| `-Xdavex <arg>` | Opzioni remote JCR estese |
| `--credentials <arg>` | Credenziali predefinite da utilizzare |
| `--config <arg>` | Configurazione JcrFs da utilizzare |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `--version` | Stampa le informazioni sulla versione ed esce da VLT |
| `--log-level <level>` | Indica il livello di registro, ad esempio il livello di registro log4j. |
| `-h (--help) <command>` | Stampa la Guida per quel particolare comando |

## Comandi VLT {#vlt-commands}

Nella tabella seguente vengono descritti tutti i comandi VLT disponibili. Per informazioni dettagliate sulla sintassi, sulle opzioni disponibili e sugli esempi, vedere i singoli comandi.

|  |  |  |
|--- |--- |--- |
| Comando | Comando abbreviato | Descrizione |
| `export` |  | Esporta da un archivio JCR (vault file system) al file system locale senza control file. |
| `import` |  | Importa un file system locale in un archivio JCR (file system di Vault). |
| `checkout` | `co` | Estrae un file system Vault. Utilizzalo per un archivio JCR iniziale nel file system locale. (Nota: è innanzitutto necessario estrarre il repository in una versione secondaria.) |
| `analyze` |  | Analizza i pacchetti. |
| `status` | `st` | Stampa lo stato dei file e delle directory in copia di lavoro. |
| `update` | `up` | Importa le modifiche dal repository nella copia di lavoro. |
| `info` |  | Visualizza informazioni su un file locale. |
| `commit` | `ci` | Invia le modifiche dalla copia di lavoro all&#39;archivio. |
| `revert` | `rev` | Ripristina lo stato originale del file della copia di lavoro e annulla la maggior parte delle modifiche locali. |
| `resolved` | `res` | Rimuove lo stato in conflitto nei file o nelle directory di copia in corso. |
| `propget` | `pg` | Stampa il valore di una proprietà su file o directory. |
| `proplist` | `pl` | Stampa le proprietà su file o directory. |
| `propset` | `ps` | Imposta il valore di una proprietà su file o directory. |
| `add` |  | Inserisce i file e le directory sotto il controllo della versione. |
| `delete` | `del` oppure `rm` | Rimuove file e directory dal controllo delle versioni. |
| `diff` | `di` | Visualizza le differenze tra due percorsi. |
| `console` |  | Esegue una console interattiva. |
| `rcp` |  | Copia una struttura di nodi da un repository remoto a un altro. |
| `sync` |  | Consente di controllare il servizio di sincronizzazione di Vault. |

### Esporta {#export}

Esporta il file system Vault montato su &lt;uri> al file system locale in &lt;local-path>. Un&#39;opzione &lt;jcr-path> può essere specificato per esportare solo una sottostruttura.

#### Sintassi {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Opzioni {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-t (--type) <arg>` | specifica il tipo di esportazione, piattaforma o jar. |
| `-p (--prune-missing)` | specifica se eliminare i file locali mancanti |
| `<uri>` | uri punto di montaggio |
| `<jcrPath>` | Percorso JCR |
| `<localPath>` | percorso locale |

#### Esempi {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### Importa {#import}

Importa il file system locale (a partire da `<local-path>` nel file system di vaulting in `<uri>`. È possibile specificare un `<jcr-path>` come directory principale di importazione. Se `--sync` viene specificato, i file importati vengono automaticamente posti sotto il controllo di Vault.

#### Sintassi {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Opzioni {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-s (-- sync)` | mette i file locali sotto il controllo del vault |
| `<uri>` | uri punto di montaggio |
| `<jcrPath>` | Percorso JCR |
| `<localPath>` | percorso locale |

#### Esempi {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Pagamento (co) {#checkout-co}

Esegue un check-out iniziale da un archivio JCR al file system locale a partire da &lt;uri> al file system locale in &lt;local-path>. Puoi anche aggiungere una &lt;jcrpath> per estrarre una sottodirectory della struttura remota. È possibile specificare i filtri di Workspace da copiare nella directory META-INF.

#### Sintassi {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Opzioni {#options-2}

|  |  |
|--- |--- |
| `--force` | forza l&#39;estrazione per sovrascrivere i file locali se esistono già |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `-f (--filter) <file>` | specifica i filtri automatici se non ne è stato definito alcuno |
| `<uri>` | uri punto di montaggio |
| `<jcrPath>` | (facoltativo) percorso remoto |
| `<localPath>` | (facoltativo) percorso locale |

#### Esempi {#examples-2}

Utilizzo di JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

Con l&#39;area di lavoro predefinita:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

Se l’URI è incompleto, verrà espanso:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### Analizza {#analyze}

Analizza i pacchetti.

#### Sintassi {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### Opzioni {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | formato printf per i collegamenti hotfix (nome,id), ad esempio `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `<localPaths> [<localPaths> ...]` | percorso locale |

### Stato {#status}

Stampa lo stato dei file e delle directory in copia di lavoro.

Se `--show-update` viene specificato, ogni file viene controllato rispetto alla versione remota. La seconda lettera specifica quindi quale azione verrà eseguita da un&#39;operazione di aggiornamento.

#### Sintassi {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Opzioni {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `-u (--show-update)` | visualizza le informazioni di aggiornamento |
| `-N (--non-recursive)` | funziona su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory per visualizzare lo stato |

### Aggiornare {#update}

Copia le modifiche dal repository nella copia di lavoro.

#### Sintassi {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opzioni {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `--force` | forza la sovrascrittura dei file locali |
| `-N (--non-recursive)` | funziona su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory da aggiornare |

### Info {#info}

Visualizza informazioni su un file locale.

#### Sintassi {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### Opzioni {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | opera in modo ricorsivo |
| `<file> [<file> ...]` | file o directory per visualizzare le informazioni |

### Conferma {#commit}

Invia le modifiche dalla copia di lavoro all&#39;archivio.

#### Sintassi {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opzioni {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `--force` | forza il commit anche se la copia remota viene modificata |
| `-N (--non-recursive)` | funziona su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory di cui eseguire il commit |

### Versione precedente {#revert}

Ripristina lo stato originale del file della copia di lavoro e annulla la maggior parte delle modifiche locali.

#### Sintassi {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### Opzioni {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | discendente in modo ricorsivo |
| `<file> [<file> ...]` | file o directory di cui eseguire il commit |

### Risolto {#resolved}

Rimuovi **in conflitto** stato della copia di file o directory.

>[!NOTE]
>
>Questo comando non risolve semanticamente i conflitti o rimuove i marcatori di conflitto, ma rimuove semplicemente i file di artefatti correlati ai conflitti e consente di eseguire nuovamente il commit di PATH.

#### Sintassi {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Opzioni {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | discendente in modo ricorsivo |
| `--force` | risolve, anche in presenza di indicatori di conflitto |
| `<file> [<file> ...]` | file o directory da risolvere |

### Propget {#propget}

Stampa il valore di una proprietà su file o directory.

#### Sintassi {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### Opzioni {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | discendente in modo ricorsivo |
| `<propname>` | il nome della proprietà |
| `<file> [<file> ...]` | file o directory da cui ottenere la proprietà |

### Proplist {#proplist}

Stampa le proprietà su file o directory.

#### Sintassi {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### Opzioni {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | discendente in modo ricorsivo |
| `<file> [<file> ...]` | file o directory da cui elencare le proprietà |

### Propset {#propset}

Imposta il valore di una proprietà su file o directory.

>[!NOTE]
>
>VLT riconosce le seguenti proprietà speciali con versione:
>
>`vlt:mime-type`
>
>Il tipo MIME del file. Utilizzato per determinare se unire il file. Un tipo MIME che inizia con &#39;text/&#39; (o un tipo MIME assente) viene considerato come testo. Qualsiasi altra cosa viene trattata come binaria.

#### Sintassi {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Opzioni {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | stampa il meno possibile |
| `-R (--recursive)` | discendente in modo ricorsivo |
| `<propname>` | il nome della proprietà |
| `<propval>` | il valore della proprietà |
| `<file> [<file> ...]` | file o directory su cui impostare la proprietà |

### Aggiungi {#add}

Inserisce i file e le directory sotto il controllo della versione, pianificandoli per l&#39;aggiunta all&#39;archivio. Verranno aggiunti al prossimo commit.

#### Sintassi {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Opzioni {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `-N (--non-recursive)` | funziona su un&#39;unica directory |
| `--force` | forza l&#39;esecuzione dell&#39;operazione |
| `<file> [<file> ...]` | file o directory locale da aggiungere |

### Eliminare {#delete}

Rimuove file e directory dal controllo delle versioni.

#### Sintassi {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Opzioni {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il meno possibile |
| `--force` | forza l&#39;esecuzione dell&#39;operazione |
| `<file> [<file> ...]` | file o directory locale da eliminare |

### Diff. {#diff}

Visualizza le differenze tra due percorsi.

#### Sintassi {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Opzioni {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | funziona su un&#39;unica directory |
| `<file> [<file> ...]` | per visualizzare le differenze tra |

### Console {#console}

Esegue una console interattiva.

#### Sintassi {#syntax-16}

```shell
console -F <file>
```

#### Opzioni {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | specifica il file delle impostazioni della console. Il file predefinito è console.properties. |

### Rcp {#rcp}

Copia una struttura di nodi da un repository remoto a un altro. `<src>` punta al nodo di origine e `<dst>` specifica il percorso di destinazione, in cui deve esistere il nodo padre. Rcp elabora i nodi trasmettendo i dati in streaming.

#### Sintassi {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### Opzioni {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | Stampa il meno possibile. |
| `-r (--recursive)` | Discende in modo ricorsivo. |
| `-b (--batchSize) <size>` | Numero di nodi da elaborare prima di un salvataggio intermedio. |
| `-t (--throttle) <seconds>` | Numero di secondi di attesa dopo un salvataggio intermedio. |
| `-u (--update)` | Sovrascrivi/elimina nodi esistenti. |
| `-n (--newer)` | Rispetta le proprietà lastModified per l&#39;aggiornamento. |
| `-e (--exclude) <arg> [<arg> ...]` | Regexp dei percorsi sorgente esclusi. |
| `<src>` | Indirizzo dell&#39;archivio della struttura di origine. |
| `<dst>` | Indirizzo dell’archivio del nodo di destinazione. |

#### Esempi {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>Il `--exclude` devono essere seguite da un&#39;altra opzione prima della `<src>` e `<dst>` argomenti. Ad esempio:
>
>`vlt rcp -e ".*\.txt" -r`

### Sincronizza {#sync}

Consente di controllare il servizio di sincronizzazione di Vault. Senza argomenti, questo comando tenta di porre la directory di lavoro corrente sotto il controllo di sincronizzazione. Se viene eseguito all&#39;interno di un checkout VLT, utilizza il rispettivo filtro e host per configurare la sincronizzazione. Se viene eseguita all&#39;esterno di un&#39;estrazione VLT, registra la cartella corrente per la sincronizzazione solo se la directory è vuota.

#### Sintassi {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Opzioni {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato. |
| `--force` | forzare l&#39;esecuzione di determinati comandi. |
| `-u (--uri) <uri>` | specifica l&#39;URI dell&#39;host di sincronizzazione. |
| `<command>` | comando di sincronizzazione da eseguire. |
| `<localPath>` | cartella locale da sincronizzare. |

### Codici di stato {#status-codes}

I codici di stato utilizzati da VLT sono:

* &#39; &#39; nessuna modifica
* &#39;A&#39; aggiunto
* &#39;C&#39; In Conflitto
* &#39;D&#39; eliminato
* &#39;I&#39; ignorato
* &#39;M&#39; modificato
* &#39;R&#39; Sostituito
* &#39;?&#39; l&#39;elemento non è incluso nel controllo della versione
* &#39;!&#39; elemento mancante (rimosso da un comando non svn) o incompleto
* Elemento con versione &#39;~&#39; ostruito da un elemento di tipo diverso

## Impostazione della sincronizzazione di FileVault {#setting-up-filevault-sync}

Il servizio di sincronizzazione Vault viene utilizzato per sincronizzare il contenuto dell&#39;archivio con una rappresentazione del file system locale e viceversa. Ciò si ottiene installando un servizio OSGi che ascolta le modifiche dell’archivio e analizza periodicamente il contenuto del file system. Utilizza lo stesso formato di serializzazione dell’insieme di credenziali per la mappatura del contenuto dell’archivio su disco.

>[!NOTE]
>
>Il servizio di sincronizzazione di Vault è uno strumento di sviluppo ed è sconsigliato utilizzarlo su un sistema produttivo. Inoltre, il servizio può essere sincronizzato solo con il file system locale e non può essere utilizzato per lo sviluppo remoto.

### Installazione del servizio tramite vlt {#installing-the-service-using-vlt}

Il `vlt sync install` il comando può essere utilizzato per installare automaticamente il bundle e la configurazione del servizio di sincronizzazione di vault.

Il bundle è installato di seguito `/libs/crx/vault/install` e il nodo di configurazione viene creato alle `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. Inizialmente il servizio è abilitato, ma non sono configurate directory principali di sincronizzazione.

L&#39;esempio seguente installa il servizio di sincronizzazione nell&#39;istanza CRX accessibile dall&#39;URI specificato.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### Visualizzazione dello stato del servizio {#displaying-the-service-status}

Il `status` è possibile utilizzare il comando per visualizzare informazioni sul servizio sync in esecuzione. &quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>Il `status` Il comando non recupera dati live dal servizio, ma legge la configurazione in `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### Aggiunta di una cartella di sincronizzazione {#adding-a-sync-folder}

Il `register` viene utilizzato per aggiungere una cartella da sincronizzare alla configurazione.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>Il `register` non attiva una sincronizzazione finché non si configura il comando `sync-once` configurazione.

### Rimozione di una cartella di sincronizzazione {#removing-a-sync-folder}

Il `unregister` viene utilizzato per rimuovere una cartella da sincronizzare dalla configurazione.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>È necessario annullare la registrazione di una cartella di sincronizzazione prima di eliminarla.

### Configurazione della sincronizzazione {#configuring-synchronization}

#### Configurazione del servizio {#service-configuration}

Una volta in esecuzione, il servizio può essere configurato con i seguenti parametri:

* `vault.sync.syncroots`: uno o più percorsi del file system locale che definiscono le directory principali di sincronizzazione.

* `vault.sync.fscheckinterval`: frequenza (in secondi) di cui il file system deve essere analizzato per rilevare eventuali modifiche. Il valore predefinito è 5 secondi.
* `vault.sync.enabled`: flag generale che abilita/disabilita il servizio.

>[!NOTE]
>
>Il servizio può essere configurato con la console web o un `sling:OsgiConfig` nodo (con il nome `com.day.jcr.sync.impl.VaultSyncServiceImpl`) nell&#39;archivio.
>
>Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate.

#### Sincronizza configurazione cartelle {#sync-folder-configuration}

Ogni cartella di sincronizzazione memorizza la configurazione e lo stato in tre file:

* `.vlt-sync-config.properties`: file di configurazione.

* `.vlt-sync.log`: file di registro contenente informazioni sulle operazioni eseguite durante la sincronizzazione.
* `.vlt-sync-filter.xml`: filtri che definiscono quali parti dell’archivio vengono sincronizzate. Il formato di questo file è descritto da [Esecuzione di un&#39;estrazione filtrata](#performing-a-filtered-checkout) sezione.

Il `.vlt-sync-config.properties` consente di configurare le seguenti proprietà:

**disabilitato** Attiva o disattiva la sincronizzazione. Per impostazione predefinita, questo parametro è impostato su false per consentire la sincronizzazione.

**sync-once** Se non è vuoto, la scansione successiva sincronizzerà la cartella nella direzione specificata, quindi il parametro verrà cancellato. Sono supportati due valori:

* `JCR2FS`: esporta tutto il contenuto nell’archivio JCR e scrive sul disco locale.
* `FS2JCR`: importa tutto il contenuto dal disco all’archivio JCR.

**sync-log** Definisce il nome del file di registro. Il valore predefinito è .vlt-sync.log

### Utilizzo della sincronizzazione VLT per lo sviluppo {#using-vlt-sync-for-development}

Per impostare un ambiente di sviluppo basato su una cartella di sincronizzazione, procedere come segue:

1. Estrai l’archivio con la riga di comando vlt:

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >Puoi utilizzare i filtri per estrarre solo i percorsi appropriati. Consulta la [Esecuzione di un&#39;estrazione filtrata](#performing-a-filtered-checkout) sezione per informazioni.

1. Passa alla cartella principale della copia di lavoro:

   ```shell
   $ cd dev/jcr_root/
   ```

1. Installare il servizio di sincronizzazione nel repository:

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. Inizializza il servizio di sincronizzazione:

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. Modifica il `.vlt-sync-config.properties` file nascosto e configura la sincronizzazione per sincronizzare il contenuto dell’archivio:

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >Questo passaggio scarica l’intero archivio in base alla configurazione del filtro.

1. Controlla il file di registro `.vlt-sync.log` per visualizzare lo stato di avanzamento:

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

La cartella locale è ora sincronizzata con l’archivio. La sincronizzazione è bidirezionale, pertanto la modifica dall’archivio verrà applicata alla cartella di sincronizzazione locale e viceversa.

>[!NOTE]
>
>La funzione di sincronizzazione VLT supporta solo file e cartelle semplici, ma rileva i file serializzati con archivio speciale (con estensione content.xml, dialog.xml e così via) e li ignora automaticamente. Pertanto, è possibile utilizzare la sincronizzazione di Vault in un checkout predefinito di Vault.
