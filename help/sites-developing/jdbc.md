---
title: Connessione ai database SQL
seo-title: Connessione ai database SQL
description: Accedere a un database SQL esterno in modo che le applicazioni AEM possano interagire con i dati
seo-description: Accedere a un database SQL esterno in modo che le applicazioni AEM possano interagire con i dati
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Connessione ai database SQL{#connecting-to-sql-databases}

Accedete a un database SQL esterno in modo che le applicazioni CQ possano interagire con i dati:

1. [Create o ottenete un bundle OSGi che esporta il pacchetto](#bundling-the-jdbc-database-driver) driver JDBC.
1. [Configurare un provider](#configuring-the-jdbc-connection-pool-service) di pool di origini dati JDBC.
1. [Ottenere un oggetto origine dati e creare la connessione nel codice](#connecting-to-the-database).

## Bundling del driver del database JDBC {#bundling-the-jdbc-database-driver}

Alcuni fornitori di database forniscono driver JDBC in un bundle OSGi, ad esempio [MySQL](https://www.mysql.com/downloads/connector/j/). Se il driver JDBC per il database non è disponibile come bundle OSGi, ottenere il driver JAR e inserirlo in un bundle OSGi. Il bundle deve esportare i pacchetti necessari per interagire con il server del database. Il bundle deve anche importare i pacchetti a cui fa riferimento.

L&#39;esempio seguente utilizza il plug-in [Bundle per Maven](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) per mandare a capo il driver HSQLDB in un bundle OSGi. Il POM indica al plug-in di incorporare il file hsqldb.jar identificato come dipendenza. Vengono esportati tutti i pacchetti org.hsqldb.

Il plug-in determina automaticamente quali pacchetti importare ed elenca tali pacchetti nel file MANIFEST.MF del bundle. Se uno qualsiasi dei pacchetti non è disponibile sul server CQ, il bundle non verrà avviato al momento dell&#39;installazione. Due possibili soluzioni sono le seguenti:

* Indicare nel POM che i pacchetti sono facoltativi. Utilizzate questa soluzione quando la connessione JDBC non richiede effettivamente i membri del pacchetto. Utilizzate l&#39;elemento Import-Package per indicare i pacchetti facoltativi come nell&#39;esempio seguente:

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Racchiudete i file JAR che contengono i pacchetti in un bundle OSGi che esporta i pacchetti e distribuite il bundle. Utilizzate questa soluzione quando i membri del pacchetto sono richiesti durante l&#39;esecuzione del codice.

La conoscenza del codice sorgente consente di decidere quale soluzione utilizzare. È inoltre possibile provare entrambe le soluzioni ed eseguire test per convalidare la soluzione.

### POM che include hsqldb.jar {#pom-that-bundles-hsqldb-jar}

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

I seguenti collegamenti aprono le pagine di download per alcuni prodotti di database più diffusi:

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [ Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### Configurazione del servizio del pool di connessioni JDBC {#configuring-the-jdbc-connection-pool-service}

Aggiungete una configurazione per il servizio JDBC Connections Pool che utilizza il driver JDBC per creare oggetti origine dati. Il codice dell&#39;applicazione utilizza questo servizio per ottenere l&#39;oggetto e connettersi al database.

Il pool di connessioni JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) è un servizio di fabbrica. Se sono necessarie connessioni che utilizzano proprietà diverse, ad esempio l&#39;accesso in sola lettura o in lettura/scrittura, creare più configurazioni.

Quando si lavora con CQ esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Per configurare un servizio di connessione in pool sono disponibili le seguenti proprietà. I nomi delle proprietà sono elencati così come sono visualizzati nella console Web. Il nome corrispondente per un nodo `sling:OsgiConfig` viene visualizzato tra parentesi. I valori di esempio sono mostrati per un server HSQLDB e un database con alias `mydb`:

* Classe driver JDBC ( `jdbc.driver.class`): La classe Java da utilizzare che implementa l&#39;interfaccia java.sql.Driver, ad esempio `org.hsqldb.jdbc.JDBCDriver`. Il tipo di dati è `String`.

* URI connessione JDBC ( `jdbc.connection.uri`): L&#39;URL del database da utilizzare per creare la connessione, ad esempio `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. Il formato dell&#39;URL deve essere valido per l&#39;utilizzo con il metodo getConnection della classe java.sql.DriverManager. Il tipo di dati è `String`.

* Nome utente ( `jdbc.username`): Nome utente da utilizzare per l&#39;autenticazione con il server del database. Il tipo di dati è `String`.

* Password ( `jdbc.password`): La password da utilizzare per l&#39;autenticazione dell&#39;utente. Il tipo di dati è `String`.

* Query convalida ( `jdbc.validation.query`): Istruzione SQL da utilizzare per verificare che la connessione abbia esito positivo, ad esempio `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. Il tipo di dati è `String`.

* Sola lettura per impostazione predefinita (default.readonly): Selezionate questa opzione quando desiderate che la connessione fornisca l&#39;accesso in sola lettura. Il tipo di dati è `Boolean`.
* Autocommit per impostazione predefinita ( `default.autocommit`): Selezionare questa opzione per creare transazioni separate per ogni comando SQL inviato al database e ogni transazione viene automaticamente impegnata. Non selezionare questa opzione quando si esegue il commit esplicito delle transazioni nel codice. Il tipo di dati è `Boolean`.

* Dimensione pool ( `pool.size`): Numero di connessioni simultanee da rendere disponibili al database. Il tipo di dati è `Long`.

* Attesa pool ( `pool.max.wait.msec`): Il tempo trascorso prima del timeout di una richiesta di connessione. Il tipo di dati è `Long`.

* Nome origine dati ( `datasource.name`): Nome dell&#39;origine dati. Il tipo di dati è `String`.

* Ulteriori proprietà del servizio ( `datasource.svc.properties`): Set di coppie nome/valore da aggiungere all’URL della connessione. Il tipo di dati è `String[]`.

Il servizio del pool di connessioni JDBC è una fabbrica. Pertanto, se si utilizza un nodo `sling:OsgiConfig` per configurare il servizio di connessione, il nome del nodo deve includere il PID del servizio factory seguito da *`-alias`*. L&#39;alias utilizzato deve essere univoco per tutti i nodi di configurazione per tale PID. Il nome di un nodo di esempio è `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Connessione al database {#connecting-to-the-database}

Nel codice Java, utilizzate il servizio DataSourcePool per ottenere un oggetto `javax.sql.DataSource` per la configurazione creata. Il servizio DataSourcePool fornisce il metodo `getDataSource` che restituisce un oggetto `DataSource` per un determinato nome di origine dati. Come argomento del metodo, utilizzate il valore della proprietà Nome origine dati (o `datasource.name`) specificata per la configurazione del pool di connessioni JDBC.

L&#39;esempio seguente codice JSP ottiene un&#39;istanza dell&#39;origine dati hsqldbds, esegue una semplice query SQL e visualizza il numero di risultati restituiti.

#### JSP che esegue una ricerca nel database {#jsp-that-performs-a-database-lookup}

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
>Se il metodo getDataSource genera un&#39;eccezione perché l&#39;origine dati non è trovata, assicurarsi che la configurazione del servizio del pool di connessioni sia corretta. Verificare i nomi, i valori e i tipi di dati delle proprietà.


>[!NOTE]
>
>Per informazioni su come inserire un DataSourcePool in un bundle OSGi, vedere [Injection a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html) (Iniezione di un servizio DataSourcePool in un bundle OSGi di).

