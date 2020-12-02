---
title: Come utilizzare lo strumento VLT
seo-title: Come utilizzare lo strumento VLT
description: Lo strumento Jackrabbit FileVault (VLT) è sviluppato da Apache Foundation che mappa il contenuto di un'istanza Jackrabbit/AEM al file system
seo-description: Lo strumento Jackrabbit FileVault (VLT) è sviluppato da Apache Foundation che mappa il contenuto di un'istanza Jackrabbit/AEM al file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
translation-type: tm+mt
source-git-commit: 2da3da1a36f074593e276ddd15ed8331239ab70f
workflow-type: tm+mt
source-wordcount: '2748'
ht-degree: 2%

---


# Come utilizzare lo strumento VLT {#how-to-use-the-vlt-tool}

Lo strumento Jackrabbit FileVault (VLT) è uno strumento sviluppato da [Apache Foundation](https://www.apache.org/) che mappa il contenuto di un&#39;istanza Jackrabbit/AEM al file system. Lo strumento VLT ha funzioni simili a quelle del client del sistema di controllo del codice sorgente (come un client Subversion (SVN)), che fornisce le normali operazioni di check-in, check-out e gestione, nonché opzioni di configurazione per una rappresentazione flessibile del contenuto del progetto.

Lo strumento VLT viene eseguito dalla riga di comando. Questo documento descrive come utilizzare lo strumento, incluso come iniziare e ottenere assistenza, nonché un elenco di tutti i [comandi](#vlt-commands) e le opzioni [disponibili](#vlt-global-options).

## Concetti e architettura {#concepts-and-architecture}

Per una panoramica completa dei concetti e della struttura dello strumento Filevault, vedere la pagina [Filevault Overview](https://jackrabbit.apache.org/filevault/overview.html) and [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) della documentazione ufficiale [Apache Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/index.html).

## Guida introduttiva a VLT {#getting-started-with-vlt}

Per iniziare a utilizzare VLT, è necessario effettuare le seguenti operazioni:

1. Installate VLT, aggiornate le variabili di ambiente e aggiornate i file di sovversione ignorati globali.
1. Configurate l&#39;archivio AEM (se non lo avete già fatto).
1. Esaminare il repository AEM.
1. Sincronizzare con la directory archivio.
1. Verificare il funzionamento della sincronizzazione.

### Installazione dello strumento VLT {#installing-the-vlt-tool}

Per utilizzare lo strumento VLT, è prima necessario installarlo. Per impostazione predefinita, non è installato in quanto è uno strumento aggiuntivo. Inoltre, è necessario impostare la variabile di ambiente del sistema.

1. Scaricare il file di archivio FileVault dal repository degli artifact di [Maven.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >L&#39;origine dello strumento VLT è [disponibile su GitHub.](https://github.com/apache/jackrabbit-filevault)
1. Estrarre l&#39;archivio.
1. Aggiungere `<archive-dir>/vault-cli-<version>/bin` all&#39;ambiente `PATH` in modo che i file di comando `vlt` o `vlt.bat` siano accessibili a seconda delle necessità. Esempio:

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Aprite una shell della riga di comando ed eseguite `vlt --help`. Accertatevi che l&#39;output sia simile alla seguente schermata della guida:

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

Dopo averlo installato, è necessario aggiornare i file di subversione ignorati globali. Modificate le impostazioni di salvataggio e aggiungete quanto segue:

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### Configurazione del carattere di fine riga {#configuring-the-end-of-line-character}

VLT gestisce automaticamente End of Line (EOF) in base alle seguenti regole:

* righe di file estratti in Windows con un `CRLF`
* linee di file estratti su Linux/Unix con un `LF`
* righe di file inviate alla fine del repository con un `LF`

Per garantire la corrispondenza tra la configurazione VLT e SVN, impostare la proprietà `svn:eol-style` su `native` per l&#39;estensione dei file memorizzati nella directory archivio. Modificate le impostazioni di salvataggio e aggiungete quanto segue:

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

### Estrazione del repository {#checking-out-the-repository}

Estrarre il repository utilizzando il sistema di controllo del codice sorgente. In svn, ad esempio, digitare quanto segue (sostituendo l’URI e il percorso con il repository):

```shell
svn co https://svn.server.com/repos/myproject
```

### Sincronizzazione con il repository {#synchronizing-with-the-repository}

È necessario sincronizzare l&#39;archivio dei file con l&#39;archivio. Per effettuare ciò:

1. Nella riga di comando, passare a `content/jcr_root`.
1. Per controllare il repository, digitate il seguente numero di porta (sostituendo il numero **4502** con le password dell&#39;amministratore):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >Le credenziali devono essere specificate una sola volta al momento dell&#39;estrazione iniziale. Saranno quindi memorizzati nella directory principale all&#39;interno di `.vault/auth.xml`.

### Verifica del funzionamento della sincronizzazione {#testing-whether-the-synchronization-worked}

Dopo aver estratto l&#39;archivio e averlo sincronizzato, è necessario verificare che tutto funzioni correttamente. Un modo semplice per farlo è modificare un file **.jsp** e verificare se le modifiche vengono applicate dopo il commit delle modifiche.

Per verificare la sincronizzazione:

1. Accedi a `.../jcr_content/libs/foundation/components/text`.
1. Modificate un elemento in `text.jsp`.
1. Visualizzare i file modificati digitando `vlt st`
1. Visualizzare le modifiche digitando `vlt diff text.jsp`
1. Conferma le modifiche: `vlt ci test.jsp`.
1. Ricaricate una pagina contenente un componente di testo e verificate se le modifiche sono presenti.

## Assistenza per lo strumento VLT {#getting-help-with-the-vlt-tool}

Dopo aver installato lo strumento VLT, potete accedere al relativo file della Guida dalla riga di comando:

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

Per informazioni su un particolare comando, digitare il comando help seguito dal nome del comando. Esempio:

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

Di seguito sono riportate alcune attività comuni eseguite in VLT. Per informazioni dettagliate su ciascun comando, vedere i singoli [comandi](#vlt-commands).

### Estrazione di una sottostruttura {#checking-out-a-subtree}

Se si desidera estrarre solo una sottostruttura dell&#39;archivio, ad esempio `/apps/geometrixx`, è possibile eseguire questa operazione digitando quanto segue:

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

In questo modo si crea una nuova radice di esportazione `geo` con una directory `META-INF` e `jcr_root` e tutti i file vengono inseriti sotto `/apps/geometrixx` in `geo/jcr_root`.

### Esecuzione di un checkout filtrato {#performing-a-filtered-checkout}

Se disponete di un filtro dell&#39;area di lavoro esistente e desiderate utilizzarlo per il checkout, potete prima creare la directory `META-INF/vault` e inserire il filtro in tale area oppure specificarlo sulla riga di comando come segue:

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

### Utilizzo di Importa/Esporta invece del controllo .vlt {#using-import-export-instead-of-vlt-control}

È possibile importare ed esportare contenuti tra un repository JCR e il file system locale senza utilizzare file di controllo.

Per importare ed esportare contenuti senza utilizzare il controllo `.vlt`:

1. Configurare inizialmente la directory archivio:

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. Modificare la copia remota e aggiornare JCR:

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

Per eseguire i comandi in VLT, digitare quanto segue nella riga di comando:

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

Le opzioni e i comandi sono descritti dettagliatamente nelle sezioni seguenti.

## Opzioni globali VLT {#vlt-global-options}

Di seguito è riportato un elenco di opzioni VLT, disponibili per tutti i comandi. Per informazioni sulle opzioni aggiuntive disponibili, consultate i singoli comandi.

|  |  |
|--- |--- |
| Opzione | Descrizione |
| `-Xjcrlog <arg>` | Opzioni JcrLog estese |
| `-Xdavex <arg>` | Opzioni di rimozione JCR estese |
| `--credentials <arg>` | Credenziali predefinite da utilizzare |
| `--config <arg>` | Configurazione JcrFs da utilizzare |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | stampa il minor numero possibile |
| `--version` | Stampa le informazioni sulla versione ed esce da VLT |
| `--log-level <level>` | Indica il livello di registro, ad esempio il livello log4j. |
| `-h (--help) <command>` | Stampa l&#39;aiuto per quel particolare comando |

## Comandi VLT {#vlt-commands}

Nella tabella seguente sono descritti tutti i comandi VLT disponibili. Per informazioni dettagliate su sintassi, opzioni disponibili ed esempi, vedere i singoli comandi.

|  |  |  |
|--- |--- |--- |
| Comando | Abbreviazione, Comando | Descrizione |
| `export` |  | Esporta da un repository JCR (file system vault) al file system locale senza file di controllo. |
| `import` |  | Importa un file system locale in un archivio JCR (vault file system). |
| `checkout` | `co` | Estrai un file system Vault. Utilizzate questa opzione per un archivio JCR iniziale nel file system locale. (Nota: È innanzitutto necessario estrarre il repository in subversione. |
| `analyze` |  | Analizza i pacchetti. |
| `status` | `st` | Stampa lo stato dei file di copia di lavoro e delle directory. |
| `update` | `up` | Importa le modifiche dall&#39;archivio nella copia di lavoro. |
| `info` |  | Visualizza informazioni su un file locale. |
| `commit` | `ci` | Invia le modifiche dalla copia di lavoro alla directory archivio. |
| `revert` | `rev` | Ripristina lo stato originale del file della copia di lavoro e annulla le modifiche locali. |
| `resolved` | `res` | Rimuove lo stato in conflitto durante il lavoro di file o directory di copia. |
| `propget` | `pg` | Stampa il valore di una proprietà su file o directory. |
| `proplist` | `pl` | Stampa le proprietà su file o directory. |
| `propset` | `ps` | Imposta il valore di una proprietà su file o directory. |
| `add` |  | Posiziona i file e le directory sotto il controllo della versione. |
| `delete` | `del` o `rm` | Rimuove i file e le directory dal controllo della versione. |
| `diff` | `di` | Visualizza le differenze tra due percorsi. |
| `console` |  | Esegue una console interattiva. |
| `rcp` |  | Copia una struttura di nodi da un repository remoto a un altro. |
| `sync` |  | Consente di controllare il servizio di sincronizzazione dell&#39;archivio. |

### Esporta {#export}

Esporta il file system Vault montato su &lt;uri> nel file system locale in &lt;local-path>. È possibile specificare un &lt;percorso-jcr> facoltativo per esportare solo un sottoalbero.

#### Sintassi {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Opzioni {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-t (--type) <arg>` | specifica il tipo di esportazione, piattaforma o jar. |
| `-p (--prune-missing)` | specifica se i file locali mancanti devono essere eliminati |
| `<uri>` | uri di montagna |
| `<jcrPath>` | Percorso JCR |
| `<localPath>` | percorso locale |

#### Esempi {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### Importa {#import}

Importa il file system locale (a partire da `<local-path>` nel file system vault in corrispondenza di `<uri>`. È possibile specificare `<jcr-path>` come radice di importazione. Se si specifica `--sync`, i file importati vengono automaticamente sottoposti al controllo vault.

#### Sintassi {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Opzioni {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-s (-- sync)` | mette i file locali sotto controllo archivio |
| `<uri>` | uri di montagna |
| `<jcrPath>` | Percorso JCR |
| `<localPath>` | percorso locale |

#### Esempi {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Checkout (co) {#checkout-co}

Esegue un check-out iniziale da un repository JCR al file system locale a partire da &lt;uri> al file system locale in &lt;local-path>. È inoltre possibile aggiungere un argomento &lt;jcrPath> per estrarre una sottodirectory della struttura ad albero remota. È possibile specificare i filtri dell&#39;area di lavoro che vengono copiati nella directory META-INF.

#### Sintassi {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Opzioni {#options-2}

|  |  |
|--- |--- |
| `--force` | forza il checkout per sovrascrivere i file locali, se già esistenti |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-f (--filter) <file>` | specifica i filtri automatici se non ne sono definiti nessuno |
| `<uri>` | uri di montagna |
| `<jcrPath>` | (facoltativo) percorso remoto |
| `<localPath>` | (facoltativo) percorso locale |

#### Esempi {#examples-2}

Utilizzo di JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

Con l’area di lavoro predefinita:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

Se l&#39;URI è incompleto, verrà espanso:

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
| `-l (--linkFormat) <format>` | formato printf per i collegamenti con hotfix (nome,id), ad esempio `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `<localPaths> [<localPaths> ...]` | percorso locale |

### Stato {#status}

Stampa lo stato dei file di copia di lavoro e delle directory.

Se si specifica `--show-update`, ogni file viene controllato rispetto alla versione remota. La seconda lettera specifica quindi quale azione verrà eseguita da un&#39;operazione di aggiornamento.

#### Sintassi {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Opzioni {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-u (--show-update)` | visualizza informazioni di aggiornamento |
| `-N (--non-recursive)` | opera su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory per visualizzare lo stato |

### Aggiorna {#update}

Copia le modifiche dalla directory archivio nella copia di lavoro.

#### Sintassi {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opzioni {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `--force` | forza la sovrascrittura dei file locali |
| `-N (--non-recursive)` | opera su un&#39;unica directory |
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
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | opera ricorsiva |
| `<file> [<file> ...]` | file o directory per visualizzare le informazioni |

### Conferma {#commit}

Invia le modifiche dalla copia di lavoro alla directory archivio.

#### Sintassi {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opzioni {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `--force` | forza il commit anche se la copia remota viene modificata |
| `-N (--non-recursive)` | opera su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory da impegnare |

### Versione precedente {#revert}

Ripristina lo stato originale del file della copia di lavoro e annulla le modifiche locali.

#### Sintassi {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### Opzioni {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | discendenti ricorsivamente |
| `<file> [<file> ...]` | file o directory da impegnare |

### Risolto {#resolved}

Rimuove lo stato **in conflitto** per i file o le directory di copia di lavoro.

>[!NOTE]
>
>Questo comando non risolve in modo semantico i conflitti o rimuove i contrassegni di conflitto; elimina semplicemente i file di artifact correlati al conflitto e consente di eseguire nuovamente il commit di PATH.

#### Sintassi {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Opzioni {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | discendenti ricorsivamente |
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
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | discendenti ricorsivamente |
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
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | discendenti ricorsivamente |
| `<file> [<file> ...]` | file o directory per elencare le proprietà da |

### Progetti {#propset}

Imposta il valore di una proprietà su file o directory.

>[!NOTE]
>
>VLT riconosce le seguenti proprietà speciali con le versioni:
>
>`vlt:mime-type`
>
>Il tipo mimetrico del file. Utilizzato per determinare se unire il file. Un tipo mimetrico che inizia con &#39;text/&#39; (o un tipo mimetizzato assente) viene considerato come testo. Qualsiasi altra cosa viene trattata come binaria.

#### Sintassi {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Opzioni {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-R (--recursive)` | discendenti ricorsivamente |
| `<propname>` | il nome della proprietà |
| `<propval>` | il valore della proprietà |
| `<file> [<file> ...]` | file o directory su cui impostare la proprietà |

### Aggiungi {#add}

Posiziona i file e le directory sotto il controllo della versione, pianificandoli per l&#39;aggiunta alla directory archivio. Saranno aggiunti al prossimo commit.

#### Sintassi {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Opzioni {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `-N (--non-recursive)` | opera su un&#39;unica directory |
| `--force` | forza l&#39;esecuzione dell&#39;operazione |
| `<file> [<file> ...]` | file o directory locale da aggiungere |

### Elimina {#delete}

Rimuove i file e le directory dal controllo della versione.

#### Sintassi {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Opzioni {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato |
| `-q (--quiet)` | il minor numero possibile di stampe |
| `--force` | forza l&#39;esecuzione dell&#39;operazione |
| `<file> [<file> ...]` | file o directory locale da eliminare |

### Diff.{#diff}

Visualizza le differenze tra due percorsi.

#### Sintassi {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Opzioni {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | opera su un&#39;unica directory |
| `<file> [<file> ...]` | file o directory per visualizzare le differenze da |

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

Copia una struttura di nodi da un repository remoto a un altro. `<src>` punta al nodo di origine e  `<dst>` specifica il percorso di destinazione, dove deve esistere il nodo principale. Rcp elabora i nodi eseguendo lo streaming dei dati.

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
| `-n (--newer)` | Rispetta le proprietà lastModified per l’aggiornamento. |
| `-e (--exclude) <arg> [<arg> ...]` | Regolazione dei percorsi sorgente esclusi. |
| `<src>` | Indirizzo del repository della struttura di origine. |
| `<dst>` | L&#39;indirizzo del repository del nodo di destinazione. |

#### Esempi {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>Le opzioni `--exclude` devono essere seguite da un&#39;altra opzione prima degli argomenti `<src>` e `<dst>`. Esempio:
>
>`vlt rcp -e ".*\.txt" -r`

### Sincronizza {#sync}

Consente di controllare il servizio di sincronizzazione dell&#39;archivio. Senza argomenti, questo comando tenta di mettere la directory di lavoro corrente sotto il controllo di sincronizzazione. Se eseguito all’interno di un checkout vuoto, utilizza il rispettivo filtro e host per configurare la sincronizzazione. Se eseguito al di fuori di un checkout di convalida, registra la cartella corrente per la sincronizzazione solo se la directory è vuota.

#### Sintassi {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Opzioni {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | output dettagliato. |
| `--force` | forzare l&#39;esecuzione di alcuni comandi. |
| `-u (--uri) <uri>` | specifica l&#39;URI dell&#39;host di sincronizzazione. |
| `<command>` | comando di sincronizzazione da eseguire. |
| `<localPath>` | cartella locale da sincronizzare. |

### Codici di stato {#status-codes}

I codici di stato utilizzati da VLT sono:

* &#39; &#39; Nessuna modifica
* &#39;A&#39; Aggiunto
* &#39;C&#39; Conflitto
* &#39;D&#39; Eliminato
* &#39;I&#39; Ignorato
* &#39;M&#39; Modificato
* &#39;R&#39; Sostituito
* &#39;?&#39; l&#39;elemento non è sotto il controllo della versione
* &#39;!&#39; elemento mancante (rimosso dal comando non-svn) o incompleto
* Elemento con versione &#39;~&#39; ostruito da un elemento di un tipo diverso

## Impostazione della sincronizzazione di FileVault {#setting-up-filevault-sync}

Il servizio di sincronizzazione di archivi viene utilizzato per sincronizzare il contenuto del repository con una rappresentazione del file system locale e viceversa. Questo si ottiene installando un servizio OSGi che ascolterà le modifiche del repository e analizzerà periodicamente il contenuto del file system. Utilizza lo stesso formato di serializzazione di vault per la mappatura del contenuto del repository su disco.

>[!NOTE]
>
>Il servizio di sincronizzazione vault è uno strumento di sviluppo ed è altamente scoraggiato ad utilizzarlo su un sistema produttivo. Inoltre, il servizio può essere sincronizzato solo con il file system locale e non può essere utilizzato per lo sviluppo remoto.

### Installazione del servizio tramite vlt {#installing-the-service-using-vlt}

Il comando `vlt sync install` può essere utilizzato per installare automaticamente il bundle del servizio di sincronizzazione di archivi e la configurazione.

Il bundle viene installato sotto `/libs/crx/vault/install` e il nodo di configurazione viene creato in `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. Inizialmente il servizio è attivato ma non sono configurate radici di sincronizzazione.

L&#39;esempio seguente installa il servizio di sincronizzazione nell&#39;istanza CRX accessibile dall&#39;URI specificato.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### Visualizzazione dello stato del servizio {#displaying-the-service-status}

Il comando `status` può essere utilizzato per visualizzare informazioni sul servizio di sincronizzazione in esecuzione. &quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>Il comando `status` non recupera dati dal servizio, ma legge la configurazione in `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### Aggiunta di una cartella di sincronizzazione {#adding-a-sync-folder}

Il comando `register` viene utilizzato per aggiungere una cartella da sincronizzare alla configurazione.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>Il comando `register` non attiva la sincronizzazione finché non si configura la configurazione `sync-once`.

### Rimozione di una cartella di sincronizzazione {#removing-a-sync-folder}

Il comando `unregister` viene utilizzato per rimuovere dalla configurazione una cartella da sincronizzare.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>Prima di eliminare la cartella, è necessario annullare la registrazione di una cartella di sincronizzazione.

### Configurazione della sincronizzazione {#configuring-synchronization}

#### Configurazione del servizio {#service-configuration}

Una volta che il servizio è in esecuzione, può essere configurato con i seguenti parametri:

* `vault.sync.syncroots`: Uno o più percorsi di file system locali che definiscono le radici di sincronizzazione.

* `vault.sync.fscheckinterval`: Frequenza (in secondi) della quale il file system deve essere analizzato per rilevare eventuali modifiche. Il valore predefinito è 5 secondi.
* `vault.sync.enabled`: Flag generale che abilita/disabilita il servizio.

>[!NOTE]
>
>Il servizio può essere configurato con la console Web o con un nodo `sling:OsgiConfig` (con il nome `com.day.jcr.sync.impl.VaultSyncServiceImpl`) nella directory archivio.
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

#### Sincronizza configurazione cartella {#sync-folder-configuration}

Ogni cartella di sincronizzazione memorizza configurazione e stato in tre file:

* `.vlt-sync-config.properties`: file di configurazione.

* `.vlt-sync.log`: file di registro contenente informazioni sulle operazioni eseguite durante la sincronizzazione.
* `.vlt-sync-filter.xml`: filtri che definiscono quali porzioni del repository vengono sincronizzate. Il formato di questo file è descritto dalla sezione [Esecuzione di un checkout filtrato](#performing-a-filtered-checkout).

Il file `.vlt-sync-config.properties` consente di configurare le seguenti proprietà:

**** disabledAttiva o disattiva la sincronizzazione. Per impostazione predefinita, questo parametro è impostato su false per consentire la sincronizzazione.

**sync-** onceSe non è vuoto la scansione successiva sincronizzerà la cartella nella direzione specificata, il parametro verrà cancellato. Sono supportati due valori:

* `JCR2FS`: esporta tutto il contenuto nell&#39;archivio JCR e scrive sul disco locale.
* `FS2JCR`: importa tutto il contenuto dal disco nell&#39;archivio JCR.

**sync-** logDefinisce il nome del file di registro. Per impostazione predefinita, il valore è .vlt-sync.log

### Utilizzo della sincronizzazione VLT per lo sviluppo {#using-vlt-sync-for-development}

Per impostare un ambiente di sviluppo basato su una cartella di sincronizzazione, procedere come segue:

1. Estrarre il repository con la riga di comando vlt:

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >Potete utilizzare i filtri solo per estrarre i percorsi appropriati. Per informazioni, vedere la sezione [Esecuzione di un checkout filtrato](#performing-a-filtered-checkout).

1. Passate alla cartella principale della copia di lavoro:

   ```shell
   $ cd dev/jcr_root/
   ```

1. Installate il servizio di sincronizzazione nell’archivio:

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. Inizializzare il servizio di sincronizzazione:

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. Modificate il file nascosto `.vlt-sync-config.properties` e configurate la sincronizzazione per sincronizzare il contenuto del repository:

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >Questo passaggio scarica l’intero repository in base alla configurazione del filtro.

1. Controllare il file di registro `.vlt-sync.log` per vedere l&#39;avanzamento:

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

La cartella locale ora è sincronizzata con la directory archivio. La sincronizzazione è bidirezionale, quindi le modifiche dal repository verranno applicate alla cartella di sincronizzazione locale e viceversa.

>[!NOTE]
>
>La funzione di sincronizzazione VLT supporta solo file e cartelle semplici, ma rileva i file serializzati speciali (content.xml, dialog.xml, ecc.) e li ignora in modo invisibile. È quindi possibile utilizzare la sincronizzazione di volta in volta su un checkout di volume predefinito.
