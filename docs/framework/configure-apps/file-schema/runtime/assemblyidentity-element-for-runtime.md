---
title: "Elemento &lt;assemblyIdentity&gt; per &lt;runtime&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/assemblyIdentity"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#assemblyIdentity"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assemblyIdentity> (elemento)"
  - "assemblyIdentity (elemento)"
  - "tag contenitore, <assemblyIdentity> (elemento)"
ms.assetid: cea4d187-6398-4da4-af09-c1abc6a349c1
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Elemento &lt;assemblyIdentity&gt; per &lt;runtime&gt;
Contiene le informazioni di identificazione relative all'assembly.  
  
## Sintassi  
  
```  
  
   <assemblyIdentity    
name="assembly name"  
publicKeyToken="public key token"  
culture="assembly culture"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo obbligatorio.<br /><br /> Nome dell'assembly.|  
|`culture`|Attributo facoltativo.<br /><br /> Stringa che specifica la lingua e il paese relativi all'assembly.|  
|`publicKeyToken`|Attributo facoltativo.<br /><br /> Valore esadecimale che specifica il nome sicuro dell'assembly.|  
|`processorArchitecture`|Attributo facoltativo.<br /><br /> Uno dei valori di "x86", "amd64", "msil" o "ia64" che specificano l'architettura del processore per un assembly contenente codice specifico del processore.  Per tali valori non viene rilevata la distinzione tra maiuscole e minuscole.  Se all'attributo viene assegnato qualsiasi altro valore, verrà ignorato l'intero elemento `<assemblyIdentity>`.  Vedere <xref:System.Reflection.ProcessorArchitecture>.|  
  
## Attributo ProcessorArchitecture  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`amd64`|Solo processori AMD a 64 bit.|  
|`ia64`|Solo processore Intel a 64 bit.|  
|`msil`|Neutro per quanto riguarda il processore e i bit per parola.|  
|`x86`|Processore Intel a 32 bit, nativo o in ambiente WOW \(Windows on Windows\) su una piattaforma a 64 bit.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`dependentAssembly`|Incapsula i criteri di associazione e il percorso dell'assembly per ciascun assembly.  Utilizzare un elemento `<dependentAssembly>` per ciascun assembly.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Ciascun elemento **\<dependentAssembly\>** deve disporre di un elemento figlio **\<assemblyIdentity\>**.  
  
 Se l'attributo `processorArchitecture` è presente, l'elemento `<assemblyIdentity>` si applica solo all'assembly con l'architettura di processore corrispondente.  Se invece l'attributo `processorArchitecture` non è presente, l'elemento `<assemblyIdentity>` si applica a un assembly con qualsiasi architettura di processore.  
  
 Nell'esempio riportato di seguito viene illustrato un file di configurazione per due assembly con lo stesso nome che hanno come destinazione due architetture di processore diverse e le cui versioni non sono state mantenute sincronizzate.  Se l'applicazione viene eseguita sulla piattaforma x86, verrà applicato il primo elemento `<assemblyIdentity>` e verrà ignorato l'altro.  Se invece l'applicazione viene eseguita su una piattaforma diversa da x86 o ia64, verranno ignorati entrambi.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"  
                  processorArchitecture="x86" />  
            <bindingRedirect oldVersion= "1.0.0.0"   
                  newVersion="1.1.0.0" />  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"   
                  processorArchitecture="ia64" />  
            <bindingRedirect oldVersion="1.0.0.0"   
                  newVersion="2.0.0.0" />  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 Se in un file di configurazione è contenuto l'elemento `<assemblyIdentity>` senza l'attributo `processorArchitecture` e non è contenuto un elemento che corrisponde alla piattaforma, verrà utilizzato l'elemento senza attributo `processorArchitecture`.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come fornire le informazioni su un assembly.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)