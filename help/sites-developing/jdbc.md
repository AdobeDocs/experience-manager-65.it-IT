---
title: Connessione ai database SQL
seo-title: Connecting to SQL Databases
description: Accedere a un database SQL esterno in modo che le applicazioni AEM possano interagire con i dati
seo-description: Access an external SQL database to so that your AEM applications can interact with the data
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Connessione ai database SQL{#connecting-to-sql-databases}

Accedi a un database SQL esterno in modo che le applicazioni CQ possano interagire con i dati:

1. [Crea o ottieni un bundle OSGi che esporta il pacchetto del driver JDBC](#bundling-the-jdbc-database-driver).
1. [Configurare un provider di pool di origini dati JDBC](#configuring-the-jdbc-connection-pool-service).
1. [Ottenere un oggetto origine dati e creare la connessione nel codice](#connecting-to-the-database).

## Bundling del driver di database JDBC {#bundling-the-jdbc-database-driver}

Alcuni fornitori di database forniscono driver JDBC in un bundle OSGi, per esempio [MySQL](https://www.mysql.com/downloads/connector/j/). Se il driver JDBC per il database non è disponibile come bundle OSGi, ottieni il driver JAR e inseriscilo in un bundle OSGi. Il bundle deve esportare i pacchetti necessari per interagire con il server di database. Il bundle deve anche importare i pacchetti a cui fa riferimento.

Nell&#39;esempio seguente viene utilizzato il [Plug-in bundle per Maven](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) avvolgere il driver HSQLDB in un bundle OSGi. Il POM indica al plug-in di incorporare il file hsqldb.jar identificato come dipendenza. Vengono esportati tutti i pacchetti org.hsqldb.

Il plugin determina automaticamente quali pacchetti importare ed elenca nel file MANIFEST.MF del bundle. Se uno qualsiasi dei pacchetti non è disponibile sul server CQ, il bundle non si avvia al momento dell&#39;installazione. Due possibili soluzioni sono le seguenti:

* Indicare nel POM che i pacchetti sono facoltativi. Utilizza questa soluzione quando la connessione JDBC non richiede effettivamente i membri del pacchetto. Utilizza l’elemento Import-Package per indicare pacchetti facoltativi come nell’esempio seguente:

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Racchiudi i file JAR che contengono i pacchetti in un bundle OSGi che esporta i pacchetti e distribuisci il bundle. Utilizza questa soluzione quando i membri del pacchetto sono richiesti durante l&#39;esecuzione del codice.

La conoscenza del codice sorgente consente di decidere quale soluzione utilizzare. Puoi anche provare entrambe le soluzioni ed eseguire test per convalidare la soluzione.

### POM che raggruppa hsqldb.jar {#pom-that-bundles-hsqldb-jar}

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

I seguenti collegamenti consentono di aprire le pagine di download per alcuni dei più comuni prodotti di database:

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### Configurazione del servizio del pool di connessioni JDBC {#configuring-the-jdbc-connection-pool-service}

Aggiungi una configurazione per il servizio JDBC Connections Pool che utilizza il driver JDBC per creare oggetti di origine dati. Il codice dell&#39;applicazione utilizza questo servizio per ottenere l&#39;oggetto e connettersi al database.

Pool di connessioni JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) è un servizio di fabbrica. Se hai bisogno di connessioni che utilizzano proprietà diverse, ad esempio accesso in sola lettura o in lettura/scrittura, crea più configurazioni.

Quando si lavora con CQ esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete.

Per configurare un servizio di connessione in pool sono disponibili le seguenti proprietà. I nomi delle proprietà vengono elencati come visualizzati nella console Web. Nome corrispondente per un `sling:OsgiConfig` viene visualizzato tra parentesi. Vengono visualizzati valori di esempio per un server HSQLDB e un database con un alias di `mydb`:

* Classe del driver JDBC ( `jdbc.driver.class`): Classe Java da utilizzare che implementa l&#39;interfaccia java.sql.Driver, ad esempio `org.hsqldb.jdbc.JDBCDriver`. Il tipo di dati è `String`.

* URI di connessione JDBC ( `jdbc.connection.uri`): URL del database da utilizzare per creare la connessione, ad esempio `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. Il formato dell&#39;URL deve essere valido per l&#39;uso con il metodo getConnection della classe java.sql.DriverManager. Il tipo di dati è `String`.

* Nome utente ( `jdbc.username`): Nome utente da utilizzare per l&#39;autenticazione con il server di database. Il tipo di dati è `String`.

* Password ( `jdbc.password`): Password da utilizzare per l&#39;autenticazione dell&#39;utente. Il tipo di dati è `String`.

* Query di convalida ( `jdbc.validation.query`): Istruzione SQL da utilizzare per verificare che la connessione abbia esito positivo, ad esempio `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. Il tipo di dati è `String`.

* Sola lettura per impostazione predefinita (default.readonly): Selezionare questa opzione quando si desidera che la connessione fornisca l&#39;accesso in sola lettura. Il tipo di dati è `Boolean`.
* Autocommit per impostazione predefinita ( `default.autocommit`): Selezionare questa opzione per creare transazioni separate per ogni comando SQL inviato al database e ogni transazione viene impegnata automaticamente. Non selezionare questa opzione quando esegui transazioni in modo esplicito nel codice. Il tipo di dati è `Boolean`.

* Dimensione pool ( `pool.size`): Numero di connessioni simultanee da rendere disponibili al database. Il tipo di dati è `Long`.

* Attesa pool ( `pool.max.wait.msec`): Tempo di attesa prima del timeout di una richiesta di connessione. Il tipo di dati è `Long`.

* Nome origine dati ( `datasource.name`): Nome dell&#39;origine dati. Il tipo di dati è `String`.

* Proprietà del servizio aggiuntive ( `datasource.svc.properties`): Set di coppie nome/valore da aggiungere all&#39;URL di connessione. Il tipo di dati è `String[]`.

Il servizio JDBC Connections Pool è una fabbrica. Pertanto, se utilizzi un `sling:OsgiConfig` nodo per configurare il servizio di connessione, il nome del nodo deve includere il PID del servizio di fabbrica seguito da *`-alias`*. L&#39;alias utilizzato deve essere univoco per tutti i nodi di configurazione per quel PID. Un nome di nodo di esempio è `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Connessione al database {#connecting-to-the-database}

Nel codice Java, utilizza il servizio DataSourcePool per ottenere un `javax.sql.DataSource` oggetto per la configurazione creata. Il servizio DataSourcePool fornisce la variabile `getDataSource` metodo che restituisce un `DataSource` oggetto per un nome di origine dati specificato. Come argomento del metodo, utilizza il valore del Nome origine dati (o `datasource.name`) specificata per la configurazione del pool di connessioni JDBC.

Nell&#39;esempio seguente il codice JSP ottiene un&#39;istanza dell&#39;origine dati hsqldbds, esegue una semplice query SQL e visualizza il numero di risultati restituiti.

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
>Se il metodo getDataSource genera un&#39;eccezione perché l&#39;origine dati non è trovata, verificare che la configurazione del servizio del pool connessioni sia corretta. Verifica i nomi, i valori e i tipi di dati delle proprietà.

>[!NOTE]
>
>Per scoprire come inserire un DataSourcePool in un bundle OSGi, vedi [Inserimento di un servizio DataSourcePool in un bundle OSGi di Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/datasourcepool.html).
