---
title: "Elemento &lt;compilers&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#compilers"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<compilers> (elemento)"
  - "elementi di configurazione del compilatore, <compilers> (elemento)"
  - "compilers (elemento)"
ms.assetid: d40fba59-98f9-4783-ae0c-2ebea27ce77b
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;compilers&gt;
Il contenitore degli elementi di configurazione del compilatore; contiene zero o più elementi [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).  
  
## Sintassi  
  
```  
<compilers>  
  <compiler ... />  
</compilers>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)|Specifica gli attributi di configurazione del compilatore per un provider di linguaggio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|[Elemento \<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|Specifica le impostazioni di configurazione del compilatore per i provider di linguaggi disponibili.|  
  
## Note  
 L'elemento [\<compilers\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md) contiene le impostazioni di configurazione del compilatore per i provider di linguaggi su un computer.  Ciascun elemento [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md) specifica gli attributi di configurazione del compilatore per un provider di linguaggi specifico.  
  
 In .NET Framework le impostazioni iniziali del compilatore e del provider di linguaggi vengono definite nei file di configurazione del computer \(Machine.config\).  Gli sviluppatori e i fornitori di compilatori possono aggiungere impostazioni di configurazione per una nuova implementazione di <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=fullName>.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> per enumerare a livello di codice le impostazioni di configurazione del compilatore e del provider di linguaggio su un computer.  
  
## File di configurazione  
 Questo elemento può essere utilizzato nel file di configurazione del computer e nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato un elemento di configurazione del compilatore.  
  
```  
<configuration>  
   <system.codedom>  
     <compilers>  
       <!-- zero or more compiler elements -->  
       <compiler   
          language="c#;cs;csharp"   
          extension=".cs"  
          type="Microsoft.CSharp.CSharpCodeProvider, System, Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
          compilerOptions=""    
          warningLevel="1" />  
     </compilers>  
   </system.codedom>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.CodeDom.Compiler.CompilerInfo>   
 <xref:System.CodeDom.Compiler.CodeDomProvider>   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Schema di impostazioni del compilatore e del provider di linguaggi](../../../../../docs/framework/configure-apps/file-schema/compiler/index.md)   
 [Elemento \<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)