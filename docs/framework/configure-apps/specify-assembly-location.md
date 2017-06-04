---
title: "Specifica della posizione di un assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "configurazione di applicazioni [.NET Framework]"
  - "assembly [.NET Framework], specifica del percorso"
  - "configurazione [.NET Framework], applicazioni"
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Specifica della posizione di un assembly
È possibile specificare la posizione di un assembly utilizzando due elementi:  
  
-   Utilizzo dell'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md).  
  
-   Utilizzo dell'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md).  
  
 È possibile utilizzare anche lo [strumento .NET Framework Configuration \(Mscorcfg.msc\)](http://msdn.microsoft.com/it-it/a7106c52-68da-490e-b129-971b2c743764) per specificare le posizioni di assembly o le posizioni in cui Common Language Runtime possa verificare la presenza di assembly.  
  
## Utilizzo dell'elemento \<codeBase\>  
 È possibile utilizzare l'elemento **\<codeBase\>** solo all'interno dei file di configurazione del computer o dei criteri editore che contengono anche le impostazioni per il reindirizzamento della versione di assembly.  Quando determina la versione di assembly da utilizzare, il runtime applica le impostazioni di codebase contenute nel file che determina la versione.  Se non viene specificata alcuna codebase, il runtime verifica la presenza dell'assembly secondo la normale procedura.  Per ulteriori informazioni, vedere [Modalità di individuazione di assembly del runtime](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
 Nell'esempio riportato di seguito viene illustrato come specificare la posizione di un assembly.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 È necessario specificare l'attributo **version** per tutti gli assembly con nome sicuro, mentre è possibile ometterlo per gli assembly senza nome sicuro.  L'elemento **\<codeBase\>** richiede l'attributo **href**.  Non è possibile specificare intervalli di versioni nell'elemento **\<codeBase\>**.  
  
> [!NOTE]
>  Se viene fornito un suggerimento relativo alla codebase per un assembly senza nome sicuro, è necessario che tale suggerimento faccia riferimento alla base dell'applicazione o a una sottodirectory della directory della base dell'applicazione.  
  
## Utilizzo dell'elemento \<probing\>  
 Gli assembly privi di una codebase vengono individuati dal runtime mediante la ricerca.  Per ulteriori informazioni, vedere [Modalità di individuazione di assembly del runtime](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
 È possibile utilizzare l'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) all'interno del file di configurazione dell'applicazione per specificare le sottodirectory in cui il runtime deve eseguire la ricerca per l'individuazione di un assembly.  Nell'esempio riportato di seguito viene illustrato come specificare le directory in cui eseguire la ricerca.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 L'attributo **privatePath** contiene le directory nelle quali il runtime deve cercare gli assembly.  Se l'applicazione si trova nella directory C:\\Programmi\\MyApp, il runtime cercherà gli assembly nei quali non viene specificata una codebase nelle directory C:\\Programmi\\MyApp\\Bin, C:\\Programmi\\MyApp\\Bin2\\Subbin e C:\\Programmi\\MyApp\\Bin3.  Le directory specificate nell'attributo **privatePath** devono essere sottodirectory della directory della base applicativa.  
  
## Vedere anche  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/it-it/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)