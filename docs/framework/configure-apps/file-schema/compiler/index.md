---
title: "Schema di impostazioni del compilatore e del provider di linguaggi | Microsoft Docs"
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
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "elementi di configurazione del compilatore"
  - "elementi di configurazione del compilatore, schema"
  - "impostazioni di configurazione del compilatore"
  - "impostazioni di configurazione del compilatore, schema"
  - "schema di configurazione [.NET Framework], impostazioni del compilatore"
  - "impostazioni di configurazione [.NET Framework], compilatori"
  - "provider di linguaggi"
  - "provider di linguaggi, schema di impostazioni"
ms.assetid: c020b139-8699-4f0d-9ac9-70d0c5b2a8c8
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Schema di impostazioni del compilatore e del provider di linguaggi
Nelle impostazioni del compilatore e del provider di linguaggi sono specificati gli elementi di configurazione del compilatore per i provider di linguaggi disponibili.  Ogni elemento di configurazione del compilatore specifica il nome del tipo del provider di codice, i parametri del compilatore, le estensioni di file e i nomi dei linguaggi supportati.  
  
 In .NET Framework le impostazioni iniziali del compilatore vengono definite nel file di configurazione del computer \(Machine.config\).  Gli sviluppatori e i fornitori di compilatori possono aggiungere impostazioni di configurazione per una nuova implementazione di <xref:System.CodeDom.Compiler.CodeDomProvider>.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=fullName> per enumerare a livello di codice le impostazioni di configurazione del compilatore e del provider di linguaggio su un computer.  
  
 [Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)  
  
 [\<compilatori\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)  
  
 [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.codedom\>](../../../../../docs/framework/configure-apps/file-schema/compiler/system-codedom-element.md)|Specifica le impostazioni di configurazione del compilatore per i provider di linguaggi disponibili.|  
|[\<compilatori\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compilers-element.md)|Il contenitore degli elementi di configurazione del compilatore; contiene zero o più elementi [\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md).|  
|[\<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)|Specifica gli attributi di configurazione del compilatore per un provider di linguaggio.|  
  
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
 [Elemento \<compiler\>](../../../../../docs/framework/configure-apps/file-schema/compiler/compiler-element.md)