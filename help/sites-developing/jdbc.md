---
title: Connessione ai database SQL
description: Accedere a un database SQL esterno in modo che le applicazioni AEM possano interagire con i dati
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Connessione ai database SQL{#connecting-to-sql-databases}

Accedere a un database SQL esterno in modo che le applicazioni CQ possano interagire con i dati:

1. [Creare o ottenere un bundle OSGi che esporta il pacchetto driver JDBC](#bundling-the-jdbc-database-driver).
1. [Configurare un provider del pool di origini dati JDBC](#configuring-the-jdbc-connection-pool-service).
1. [Ottieni un oggetto origine dati e crea la connessione nel codice](#connecting-to-the-database).

## Bundling del driver di database JDBC {#bundling-the-jdbc-database-driver}

Alcuni fornitori di database forniscono driver JDBC in un bundle OSGi, ad esempio [MySQL](https://dev.mysql.com/downloads/connector/j/). Se il driver JDBC per il database non è disponibile come bundle OSGi, ottieni il JAR del driver e inseriscilo in un bundle OSGi. Il bundle deve esportare i pacchetti necessari per interagire con il server di database. Il bundle deve anche importare i pacchetti a cui fa riferimento.

Nell&#39;esempio seguente viene utilizzato il plug-in [Bundle per Maven](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html) per racchiudere il driver HSQLDB in un bundle OSGi. Il POM indica al plug-in di incorporare il file hsqldb.jar identificato come dipendenza. Tutti i pacchetti org.hsqldb vengono esportati.

Il plug-in determina automaticamente quali pacchetti importare e li elenca nel file MANIFEST.MF del bundle. Se uno dei pacchetti non è disponibile sul server CQ, il bundle non si avvia al momento dell’installazione. Due possibili soluzioni sono le seguenti:

* Indicare nel POM che i pacchetti sono facoltativi. Utilizzare questa soluzione quando la connessione JDBC non richiede effettivamente i membri del pacchetto. Utilizzare l&#39;elemento Import-Package per indicare pacchetti facoltativi come nell&#39;esempio seguente:

  `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Racchiudi i file JAR che contengono i pacchetti in un bundle OSGi che esporta i pacchetti e distribuisci il bundle. Utilizzare questa soluzione quando i membri del pacchetto sono necessari durante l&#39;esecuzione del codice.

La conoscenza del codice sorgente consente di decidere quale soluzione utilizzare. Puoi anche provare entrambe le soluzioni ed eseguire test per convalidarle.

### POM per il bundle di hsqldb.jar {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

I seguenti collegamenti aprono le pagine di download di alcuni prodotti di database più diffusi:

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### Configurazione del servizio connection pool JDBC {#configuring-the-jdbc-connection-pool-service}

Aggiungere una configurazione per il servizio pool connessioni JDBC che utilizza il driver JDBC per creare oggetti origine dati. Il codice dell&#39;applicazione utilizza questo servizio per ottenere l&#39;oggetto e connettersi al database.

Il pool di connessioni JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) è un servizio di fabbrica. Se hai bisogno di connessioni che utilizzano proprietà diverse, ad esempio accesso in sola lettura o in lettura/scrittura, crea più configurazioni.

Quando si lavora con CQ, sono disponibili diversi metodi di gestione delle impostazioni di configurazione per tali servizi. Per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Per configurare un servizio di connessione in pool sono disponibili le seguenti proprietà. I nomi delle proprietà vengono elencati così come vengono visualizzati nella console Web. Il nome corrispondente per un nodo `sling:OsgiConfig` viene visualizzato tra parentesi. Vengono visualizzati valori di esempio per un server HSQLDB e un database con alias `mydb`:

* Classe driver JDBC ( `jdbc.driver.class`): la classe Java™ da utilizzare che implementa l&#39;interfaccia java.sql.Driver, ad esempio `org.hsqldb.jdbc.JDBCDriver`. Il tipo di dati è `String`.

* URI connessione JDBC ( `jdbc.connection.uri`): URL del database da utilizzare per creare la connessione, ad esempio `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. Il formato dell&#39;URL deve essere valido per l&#39;utilizzo con il metodo getConnection della classe java.sql.DriverManager. Il tipo di dati è `String`.

* Nome utente ( `jdbc.username`): il nome utente da utilizzare per l&#39;autenticazione con il server di database. Il tipo di dati è `String`.

* Password ( `jdbc.password`): password da utilizzare per l&#39;autenticazione dell&#39;utente. Il tipo di dati è `String`.

* Query di convalida ( `jdbc.validation.query`): l&#39;istruzione SQL da utilizzare per verificare che la connessione sia riuscita, ad esempio `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. Il tipo di dati è `String`.

* Sola lettura per impostazione predefinita (default.readonly): selezionare questa opzione quando si desidera che la connessione fornisca l&#39;accesso in sola lettura. Il tipo di dati è `Boolean`.
* Commit automatico per impostazione predefinita ( `default.autocommit`): selezionare questa opzione per creare transazioni separate per ogni comando SQL inviato al database e per ogni transazione viene eseguito automaticamente il commit. Non selezionare questa opzione quando si esegue il commit esplicito delle transazioni nel codice. Il tipo di dati è `Boolean`.

* Dimensione pool ( `pool.size`): numero di connessioni simultanee da rendere disponibili per il database. Il tipo di dati è `Long`.

* Attesa del pool ( `pool.max.wait.msec`): il tempo che deve trascorrere prima che una richiesta di connessione venga interrotta. Il tipo di dati è `Long`.

* Nome origine dati ( `datasource.name`): nome dell&#39;origine dati. Il tipo di dati è `String`.

* Proprietà servizio aggiuntive ( `datasource.svc.properties`): un insieme di coppie nome/valore che si desidera aggiungere all&#39;URL di connessione. Il tipo di dati è `String[]`.

Il servizio del pool di connessioni JDBC è un servizio di fabbrica. Pertanto, se si utilizza un nodo `sling:OsgiConfig` per configurare il servizio di connessione, il nome del nodo deve includere il PID del servizio factory seguito da *`-alias`*. L’alias utilizzato deve essere univoco per tutti i nodi di configurazione per quel PID. Un esempio di nome di nodo è `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Connessione al database {#connecting-to-the-database}

Nel codice Java™, utilizzare il servizio DataSourcePool per ottenere un oggetto `javax.sql.DataSource` per la configurazione creata. Il servizio DataSourcePool fornisce il metodo `getDataSource` che restituisce un oggetto `DataSource` per un determinato nome di origine dati. Come argomento del metodo, utilizzare il valore della proprietà Nome origine dati (o `datasource.name`) specificata per la configurazione del pool di connessioni JDBC.

L&#39;esempio di codice JSP seguente ottiene un&#39;istanza dell&#39;origine dati hsqldbds, esegue una semplice query SQL e visualizza il numero di risultati restituiti.

#### JSP che esegue una ricerca di database {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>Se il metodo getDataSource genera un&#39;eccezione perché l&#39;origine dati non è stata trovata, verificare che la configurazione del servizio del pool di connessioni sia corretta. Verificare i nomi, i valori e i tipi di dati delle proprietà.
>

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
