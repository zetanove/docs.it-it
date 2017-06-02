---
title: "&lt;service&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 13123dd6-c4a9-4a04-a984-df184b851788
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# &lt;service&gt;
L'elemento `service` contiene le impostazioni di un servizio Windows Communication Foundation \(WCF\).  Contiene anche endpoint che espongono il servizio.  
  
## Sintassi  
  
```  
  
<service behaviorConfiguration=String"  
        name="String"  
</service>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|behaviorConfiguration|Stringa che contiene il nome del comportamento da usare per creare l'istanza del servizio.  Il nome del comportamento deve essere nell'ambito del punto in cui il servizio è definito.  Il valore predefinito è una stringa vuota.|  
|name|Attributo stringa obbligatorio che specifica il tipo del servizio per cui creare un'istanza.  Questa impostazione deve corrispondere a un tipo valido.  Il formato deve essere `Namespace.Class.`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<endpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)|Raccolta di elementi `endpoint` che espongono questo servizio.|  
|[\<host\>](../../../../../docs/framework/configure-apps/file-schema/wcf/host.md)|Specifica l'host dell'istanza del servizio.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.HostElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<servizi\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md)|Elemento radice di tutti gli elementi di configurazione WCF.|  
  
## Note  
 I servizi vengono definiti nella sezione `services` del file di configurazione.  Un assembly può contenere un numero qualsiasi di servizi.  Ogni servizio dispone di una propria sezione di configurazione `service`.  Questa sezione e il relativo contenuto definiscono il contratto di servizio, il comportamento e gli endpoint del particolare servizio.  
  
 L'elemento `behaviorConfiguration` è anche facoltativo.  Identifica il comportamento usato dal servizio.  Il comportamento specificato in questo attributo deve collegarsi a un comportamento nell'ambito nello stesso file di configurazione.  
  
 Ogni servizio espone uno o più endpoint, i quali sono provvisti di un proprio indirizzo e associazione.  Tutte le associazioni usate all'interno del file di configurazione devono essere definite nell'ambito del file.  Le associazioni sono collegate agli endpoint tramite la combinazione di attributi `name` e `bindingConfiguration`.  L'attributo `name` descrive la sezione in cui è definita l'associazione.  L'attributo `bindingConfiguration` definisce quale configurazione viene usata tra quelle contenute nella sezione di associazione.  In una sezione di associazione è possibile definire diverse configurazioni.  
  
## Esempio  
 Di seguito è riportato un esempio di una configurazione di servizio.  
  
```  
<service behaviorConfiguration="testChannelBehavior"   
     name="HelloWorld">  
     <endpoint   
        address="/HelloWorld2/"  
        name="test"  
        bindingNamespace="http://www.cohowinery.com/"  
        binding="basicHttpBinding"  
        contract="IHelloWorld" />  
</service>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceElement>   
 [Configurazione dei servizi](../../../../../docs/framework/wcf/configuring-services.md)