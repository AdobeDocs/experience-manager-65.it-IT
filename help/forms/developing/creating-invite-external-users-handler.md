---
title: Creazione di un handler per l’invito di utenti esterni
description: Creazione di un handler per l’invito di utenti esterni
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# Creazione di un handler per l’invito di utenti esterni {#create-invite-external-users-handler}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Puoi creare un handler per l’invito di utenti esterni per il servizio di Rights Management. Un handler per l’invito di utenti esterni consente al servizio di Rights Management di invitare utenti esterni a diventare utenti del Rights Management. Quando un utente diventa un utente di Rights Management, può eseguire attività quali l&#39;apertura di un documento PDF protetto da policy. Dopo aver implementato in AEM Forms l’handler per l’invito di utenti esterni, puoi utilizzare la console di amministrazione per interagire con esso.

>[!NOTE]
>
>Un handler per l’invito di utenti esterni è un componente AEM Forms. Prima di creare un handler per l’invito di utenti esterni, è consigliabile acquisire familiarità con la creazione dei componenti.

**Riepilogo dei passaggi**

Per sviluppare un handler per l’invito di utenti esterni, esegui i seguenti passaggi:

1. Imposta l&#39;ambiente di sviluppo.
1. Definisci l’implementazione di Invita External Users Handler .
1. Definisci il file XML del componente.
1. Distribuisci il gestore di invito di utenti esterni.
1. Verifica il gestore di invito di utenti esterni.

## Configurazione dell&#39;ambiente di sviluppo {#setting-up-development-environment}

Per configurare l’ambiente di sviluppo, devi creare un nuovo progetto Java, ad esempio un progetto Eclipse. La versione di Eclipse supportata è `3.2.1` o successiva.

Il Rights Management SPI richiede che il file `edc-server-spi.jar` sia impostato nel percorso di classe del progetto. Se non si fa riferimento a questo file JAR, non è possibile utilizzare il Rights Management SPI nel progetto Java. Questo file JAR viene installato con AEM Forms SDK nella cartella `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` .

Oltre ad aggiungere il file `edc-server-spi.jar` al percorso della classe del progetto, devi anche aggiungere i file JAR necessari per utilizzare l’API del servizio Rights Management. Questi file sono necessari per utilizzare l’API del servizio di Rights Management all’interno del gestore di invito di utenti esterni.

## Definizione dell&#39;implementazione del gestore degli utenti esterni dell&#39;invito {#define-invite-external-users-handler}

Per sviluppare un gestore di utenti esterni per l’invito, è necessario creare una classe Java che implementi l’interfaccia `com.adobe.edc.server.spi.ersp.InvitedUserProvider`. Questa classe contiene un metodo denominato `invitedUser`, che il servizio di Rights Management richiama quando gli indirizzi e-mail vengono inviati utilizzando la pagina **Aggiungi utenti invitati** accessibile tramite la console di amministrazione.

Il metodo `invitedUser` accetta un&#39;istanza `java.util.List` che contiene indirizzi e-mail digitati in stringa inviati dalla pagina **Aggiungi utenti invitati**. Il metodo `invitedUser` restituisce una matrice di oggetti `InvitedUserProviderResult`, che in genere è una mappatura degli indirizzi e-mail agli oggetti Utente (non restituisce null).

>[!NOTE]
>
>Oltre a dimostrare come creare un gestore di utenti esterni per gli inviti, questa sezione utilizza anche l’API di AEM Forms.

L&#39;implementazione del gestore di utenti esterni per l&#39;invito contiene un metodo definito dall&#39;utente denominato `createLocalPrincipalAccount`. Questo metodo accetta un valore stringa che specifica un indirizzo e-mail come valore di parametro. Il metodo `createLocalPrincipalAccount` presuppone la preesistenza di un dominio locale denominato `EDC_EXTERNAL_REGISTERED`. Puoi configurare questo nome di dominio in modo che sia tutto ciò che desideri; tuttavia, per un&#39;applicazione di produzione, è possibile integrare con un dominio enterprise.

Il metodo `createUsers` esegue iterazioni su ogni indirizzo e-mail e crea un oggetto utente corrispondente (un utente locale nel dominio `EDC_EXTERNAL_REGISTERED`). Infine, viene chiamato il metodo `doEmails` . Questo metodo viene lasciato intenzionalmente come una stub nel campione. In un’implementazione di produzione, conterrebbe la logica dell’applicazione per inviare messaggi e-mail di invito agli utenti appena creati. Viene lasciato nell’esempio per dimostrare il flusso logico dell’applicazione di un’applicazione reale.

### Definizione dell&#39;implementazione del gestore degli utenti esterni dell&#39;invito {#user-handler-implementation}

L’implementazione del gestore di utenti esterni dell’invito seguente accetta gli indirizzi e-mail inviati dalla pagina Aggiungi utenti invitati accessibile tramite la console di amministrazione.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>Questa classe Java viene salvata come file JAVA denominato InviteExternalUsersSample.java.

## Definizione del file XML del componente per il gestore di autorizzazioni {#define-component-xml-authorization-handler}

È necessario definire un file XML del componente per distribuire il componente handler degli utenti esterni invitati. Esiste un file XML componente per ciascun componente e fornisce metadati sul componente.

Il seguente file `component.xml` viene utilizzato per il gestore di utenti esterni dell’invito. Il nome del servizio è `InviteExternalUsersSample` e l&#39;operazione esposta dal servizio è denominata `invitedUser`. Il parametro di input è un&#39;istanza `java.util.List` e il valore di output è una matrice di istanze `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`.

### Definizione del file XML del componente per il gestore di utenti esterni dell’invito {#component-xml-invite-external-users-handler}

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## Creazione del pacchetto del gestore di utenti esterni dell&#39;invito {#packaging-invite-external-users-handler}

Per distribuire il gestore di utenti esterni per l’invito in AEM Forms, devi creare un pacchetto del progetto Java in un file JAR. È necessario assicurarsi che i file JAR esterni da cui dipende la logica di business dell’handler degli utenti esterni invitati, come i file `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar`, siano inclusi anche nel file JAR. Anche il file XML del componente deve essere presente. Il file `component.xml` e i file JAR esterni devono trovarsi nella directory principale del file JAR.

>[!NOTE]
>
>Nell’illustrazione seguente, viene visualizzata una classe `BootstrapImpl` . Questa sezione non illustra come creare una classe `BootstrapImpl`.

L’illustrazione seguente mostra il contenuto del progetto Java incluso nel file JAR del gestore di utenti esterni per l’invito.

![Invitare gli utenti](assets/ci_ci_InviteUsers.png)

A. File JAR esterni richiesti dal file B. JAVA componente

Devi creare un pacchetto con l’handler degli utenti esterni per l’invito in un file JAR. Nel diagramma precedente, noterai che i file .JAVA sono elencati. Una volta inseriti in un file JAR, è necessario specificare anche i corrispondenti file .CLASS. Senza i file .CLASS, il gestore di autorizzazioni non funziona.

>[!NOTE]
>
>Dopo aver assemblato il gestore di autorizzazioni esterno in un file JAR, puoi distribuire il componente in AEM Forms. È possibile distribuire un solo gestore di utenti esterni invitati alla volta.

>[!NOTE]
>
>Puoi anche distribuire programmaticamente un componente.

## Verifica del gestore degli utenti esterni dell&#39;invito {#testing-invite-external-users-handler}

Per testare l’handler degli utenti esterni invitati, puoi aggiungere utenti esterni da invitare utilizzando la console di amministrazione.

Per aggiungere utenti esterni da invitare utilizzando la console di amministrazione:

1. Distribuisci il file JAR del gestore di utenti esterni dell’invito utilizzando Workbench.
1. Riavvia il server applicazioni.
1. Accedi alla console di amministrazione.
1. Fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configurazione]** > Invitati **[!UICONTROL Registrazione utente]**.
1. Abilita la registrazione degli utenti invitati selezionando la casella **[!UICONTROL Abilita registrazione degli utenti invitati]** . In **[!UICONTROL Usa sistema di registrazione incorporato]**, fare clic su **[!UICONTROL No]**. Salva le impostazioni.
1. Dalla home page della console di amministrazione, fai clic su **[!UICONTROL Impostazioni]** > **[!UICONTROL Gestione utente]** > **[!UICONTROL Gestione dominio]**.
1. Fare clic su **[!UICONTROL Nuovo dominio locale]**. Nella pagina seguente, crea un dominio con il nome e il valore dell’identificatore `EDC_EXTERNAL_REGISTERED`. Salva le modifiche.
1. Dalla home page della console di amministrazione, fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Utenti invitati e locali]**. Viene visualizzata la pagina **[!UICONTROL Aggiungi utente invitato]** .
1. Inserire gli indirizzi e-mail (poiché l’attuale gestore di utenti esterni per l’invito non invia effettivamente messaggi e-mail, l’indirizzo e-mail non deve essere valido). Fai clic su **[!UICONTROL OK]**. Gli utenti vengono invitati al sistema.
1. Dalla home page della console di amministrazione, fai clic su **[!UICONTROL Impostazioni]** > **[!UICONTROL Gestione utente]** > **[!UICONTROL Utenti e gruppi]**.
1. Nel campo **[!UICONTROL Trova]** , immetti un indirizzo e-mail specificato. Fare clic su **[!UICONTROL Trova]**. L’utente invitato viene visualizzato come utente nel dominio locale `EDC_EXTERNAL_REGISTERED` .

>[!NOTE]
>
>Il gestore degli utenti esterni invitati non riesce se il componente viene arrestato o disinstallato.
