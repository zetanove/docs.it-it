---
title: "&lt;add&gt; di &lt;baseAddressPrefixFilter&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b226bede-8459-4de9-b2ac-3d39604ce2bc
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;add&gt; di &lt;baseAddressPrefixFilter&gt;
Rappresenta un elemento di configurazione che specifica un filtro pass\-through che fornisce un meccanismo per scegliere le associazioni di Internet Information Services \(IIS\) appropriate quando un'applicazione [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] è ospitata in IIS.  
  
## Sintassi  
  
```  
  
<serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="string"/>  
     </baseAddressPrefixFilters>  
</serviceHostingEnvironment>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|prefix|URI usato per la corrispondenza a una parte di un indirizzo di base.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<FiltriPrefissoIndirizzoBase\>](../../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md)|Raccolta di elementi di configurazione che specificano filtri pass\-through, che forniscono un meccanismo per scegliere le associazioni di IIS appropriate quando un'applicazione [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] è ospitata in IIS.|  
  
## Note  
 Un filtro dei prefissi fornisce ai provider di hosting condiviso una modalità per specificare quali URI devono essere usati dal servizio.  Consente agli host condivisi di ospitare più applicazioni con indirizzi di base diversi per lo stesso schema nello stesso sito.  
  
 I siti Web IIS sono contenitori di applicazioni virtuali che contengono directory virtuali.  È possibile accedere all'applicazione in un sito tramite una o più associazioni IIS.  Le associazioni IIS forniscono due tipi di informazioni: un protocollo di associazione e informazioni di associazione.  Il protocollo di associazione, ad esempio HTTP, definisce lo schema in base al quale viene stabilita la comunicazione, mentre le informazioni di associazione, ad esempio l'indirizzo IP, la porta, l'intestazione host, contengono i dati usati per accedere al sito.  
  
 IIS supporta la definizione di più associazioni IIS per ogni sito, che si traduce in più indirizzi di base per ogni schema.  Poiché un servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] ospitato in un sito consente l'associazione a un solo indirizzo di base per ogni schema, è possibile usare la funzionalità di filtro dei prefissi per scegliere l'indirizzo di base necessario per il servizio ospitato.  Gli indirizzi di base in ingresso forniti da IIS sono filtrati in base all'elenco di prefissi facoltativo.  
  
 Un sito può ad esempio contenere gli indirizzi di base seguenti.  
  
```  
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 È possibile usare il file di configurazione seguente per specificare un filtro dei prefissi a livello di AppDomain.  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix=”net.tcp://test1.fabrikam.com:8000”/>  
        <add prefix=”http://test2.fabrikam.com:9000”/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 In questo esempio `net.tcp://test1.fabrikam.com:8000` e `http://test2.fabrikam.com:9000` sono i soli indirizzi di base che è consentito attraversare per i rispettivi schemi.  
  
 Per impostazione predefinita, quando non è specificato un prefisso, vengono passati tutti gli indirizzi.  La definizione del prefisso fa in modo che venga passato solo l'indirizzo di base corrispondente allo schema specifico.  
  
> [!NOTE]
>  Il filtro non supporta caratteri jolly.  Gli indirizzi di base forniti da IIS possono inoltre disporre di indirizzi associati ad altri schemi non presenti nell'elenco `baseAddressPrefixFilters`.  Questi indirizzi non vengono filtrati.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElement>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>   
 [Hosting](../../../../../docs/framework/wcf/feature-details/hosting.md)