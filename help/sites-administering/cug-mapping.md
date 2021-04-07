---
title: Mappatura di gruppi di utenti personalizzati in AEM 6.5
seo-title: Mappatura di gruppi di utenti personalizzati in AEM 6.5
description: Scopri come funziona la Mappatura di gruppi di utenti personalizzati in AEM.
seo-description: Scopri come funziona la Mappatura di gruppi di utenti personalizzati in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Sicurezza
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# Mappatura di gruppi di utenti personalizzati in AEM 6.5 {#custom-user-group-mapping-in-aem}

## Confronto del contenuto JCR relativo al CUG {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versioni precedenti AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugEnabled</p> <p>Dichiarazione del tipo di nodo: N/D, proprietà residua</p> </td>
   <td><p>Autorizzazione:</p> <p>Nodo: rep:cugPolicy del tipo di nodo rep:CugPolicy</p> <p>Dichiarazione del tipo di nodo: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticazione:</p> <p>Tipo di miscela: granite:AuthenticationRequired</p> </td>
   <td><p>Per limitare l’accesso in lettura, al nodo di destinazione viene applicata una policy CUG dedicata.</p> <p>NOTA: I criteri possono essere applicati solo ai percorsi supportati configurati.</p> <p>I nodi con nome rep:cugPolicy e tipo rep:CugPolicy sono protetti e non possono essere scritti utilizzando normali chiamate API JCR; utilizza invece la gestione del controllo accessi JCR.</p> <p>Per ulteriori informazioni, consulta <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">questa pagina</a> .</p> <p>Per applicare i requisiti di autenticazione su un nodo è sufficiente aggiungere il tipo mixin granite:AuthenticationRequired.</p> <p>NOTA: Solo rispettati sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugPrincipals</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: rep:principalNames</p> <p>Dichiarazione del tipo di nodo: rep:CugPolicy</p> </td>
   <td><p>La proprietà contenente i nomi delle entità autorizzate a leggere il contenuto al di sotto del gruppo di utenti chiuso è protetta e non può essere scritta utilizzando normali chiamate API JCR; utilizza invece la gestione del controllo accessi JCR.</p> <p>Per ulteriori informazioni sull’implementazione, consulta <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">questa pagina</a> .</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugLoginPage</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: granite:loginPath (facoltativo)</p> <p>Dichiarazione del tipo di nodo: granite:AuthenticationRequired</p> </td>
   <td><p>Un nodo JCR con il tipo mixin granite:AuthenticationRequired definito, può facoltativamente definire un percorso di accesso alternativo.</p> <p>NOTA: Solo rispettati sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugRealm</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td>ND</td>
   <td>Non più supportato con la nuova implementazione.</td>
  </tr>
 </tbody>
</table>

## Confronto dei servizi OSGi {#comparison-of-osgi-services}

**Versioni precedenti AEM**

Etichetta: Supporto di Adobe Granite Closed User Group (CUG)

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Etichetta: Configurazione CUG Apache Jackrabbit Oak

   Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = OBBLIGATORIO

* Etichetta: Elenco di esclusione di Apache Jackrabbit Oak CUG

   Nome: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = OBBLIGATORIO

* Nome: com.adobe.granite.auth.requirements.impl.RequirementService
* Etichetta: Adobe Granite Authentication Requirements e Login Path Handler

   Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

   ConfigurationPolicy = OBBLIGATORIO

**Commenti**

* Configurazione dell’autorizzazione CUG e attivazione/disattivazione della valutazione.
Servizio per configurare l’elenco di esclusione delle entità che non dovrebbero essere interessate dall’autorizzazione CUG.

   >[!NOTE]
   > 
   >Se il `CugExcludeImpl` non è configurato, il `CugConfiguration` torna al valore predefinito.

   È possibile collegare un’implementazione personalizzata di CugExclude in caso di esigenze specifiche.

* Componente OSGi che implementa LoginPathProvider che espone un percorso di accesso corrispondente a LoginSelectorHandler. Ha un riferimento obbligatorio a un RequirementHandler che viene utilizzato per registrare l&#39;osservatore che ascolta i requisiti di autenticazione modificati memorizzati nel contenuto tramite il tipo di mixin granite:AuthenticationRequired.
* Componente OSGi che implementa RequirementHandler che notifica a SlingAuthenticator le modifiche ai requisiti di autenticazione.

   Poiché il criterio di configurazione per questo componente è REQUIRE, verrà attivato solo se è specificato un set di percorsi supportati.

   L&#39;abilitazione del servizio avvia il servizio RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
