---
title: "Elemento &lt;codeBase&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#codeBase"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/codeBase"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<codeBase> (elemento)"
  - "codeBase (elemento)"
  - "tag contenitore, <codeBase> (elemento)"
ms.assetid: d48a3983-2297-43ff-a14d-1f29d3995822
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Elemento &lt;codeBase&gt;
Specifica la posizione in cui Common Language Runtime può individuare un assembly.  
  
## Sintassi  
  
```  
  
   <codeBase    
version="Assembly version"  
href="URL of assembly"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`href`|Attributo obbligatorio.<br /><br /> Specifica l'URL in cui la versione dell'assembly specificata può essere individuata dall'ambiente di esecuzione.|  
|`version`|Attributo obbligatorio.<br /><br /> Specifica la versione dell'assembly a cui si applica l'elemento codeBase.  Il formato di un numero di versione di assembly è *principale.secondaria.build.revisione*.|  
  
## Attributo version  
  
|Valore|Descrizione|  
|------------|-----------------|  
|I valori validi per ogni parte del numero di versione sono compresi tra 0 e 65535.|Non applicabile.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`buildproviders`|Definisce una raccolta di provider di compilazione utilizzati per compilare file di risorse personalizzati.  Possono essere presenti più provider di compilazione.|  
|`compilation`|Consente di configurare tutte le impostazioni di compilazione utilizzate in ASP.NET.|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`System.web`|Specifica l'elemento radice per la sezione di configurazione ASP.NET.|  
  
## Note  
 Per fare in modo che dall'ambiente di esecuzione venga utilizzata l'impostazione **\<codeBase\>** in un file di configurazione del computer o nel file dei criteri dell'editore, il file deve eseguire anche il reindirizzamento della versione dell'assembly.  I file di configurazione dell'applicazione possono includere un'impostazione di codeBase senza eseguire il reindirizzamento della versione dell'assembly.  Dopo avere determinato la versione dell'assembly da utilizzare, nell'ambiente di esecuzione viene applicata l'impostazione di codeBase presente nel file che determina la versione.  Se non è indicato alcun elemento codeBase, nell'ambiente di esecuzione viene eseguita la ricerca dell'assembly seguendo la procedura standard.  
  
 Se l'assembly dispone di un nome sicuro, l'elemento codeBase può trovarsi in un punto qualsiasi sulla rete Intranet locale o su Internet.  Se l'assembly è di tipo privato, l'impostazione di codeBase deve specificare un percorso relativo alla directory dell'applicazione.  
  
 Per gli assembly senza un nome sicuro, la versione viene ignorata e il caricatore utilizza la prima occorrenza di \<codebase\> in \<dependentAssembly\>.  Se nel file di configurazione dell'applicazione è presente una voce che reindirizza l'associazione verso un altro assembly, il reindirizzamento avrà la precedenza anche se la versione dell'assembly non corrisponde alla richiesta di associazione.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare la posizione in cui un assembly può essere individuato dall'ambiente di esecuzione.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Specifica della posizione di un assembly](../../../../../docs/framework/configure-apps/specify-assembly-location.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)