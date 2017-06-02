---
title: "Procedura: individuare assembly mediante DEVPATH | Microsoft Docs"
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
  - "configurazione di applicazioni .NET Framework, assembly"
  - "app.config (file), posizioni degli assembly"
  - "file di configurazione dell'applicazione, specifica della posizione dell'assembly"
  - "assembly [.NET Framework], posizione"
  - "DEVPATH"
  - "individuazione di assembly"
ms.assetid: 44d2eadf-7eec-443c-a2ac-d601fd919e17
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Procedura: individuare assembly mediante DEVPATH
Per assicurare il corretto funzionamento dell'assembly condiviso che viene compilato con più applicazioni,  gli sviluppatori possono creare una variabile di ambiente DEVPATH che faccia riferimento alla directory di output di compilazione per l'assembly, anziché inserire continuamente l'assembly nella Global Assembly Cache durante le fasi di sviluppo.  
  
 Se ad esempio viene compilato un assembly condiviso denominato MySharedAssembly e la directory di output è C:\\MySharedAssembly\\Debug,  è possibile inserire tale directory nella variabile DEVPATH.  È quindi necessario specificare l'elemento [\<developmentMode\>](../../../docs/framework/configure-apps/file-schema/runtime/developmentmode-element.md) nel file di configurazione del computer.  In tal modo, Common Language Runtime utilizza la variabile DEVPATH per individuare gli assembly.  
  
 L'assembly condiviso deve essere individuabile da Common Language Runtime.  Per specificare una directory privata per la risoluzione dei riferimenti agli assembly, utilizzare l'[Elemento \<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) o l'[Elemento \<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) in un file di configurazione, come descritto in [Specifica della posizione di un assembly](../../../docs/framework/configure-apps/specify-assembly-location.md).  È anche possibile inserire l'assembly in una sottodirectory della directory dell'applicazione.  Per ulteriori informazioni, vedere [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
> [!NOTE]
>  Questa è una funzionalità avanzata, destinata solo allo sviluppo.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare la ricerca di assembly in fase di runtime nelle directory specificate dalla variabile di ambiente DEVPATH.  
  
## Esempio  
  
```  
<configuration>  
  <runtime>  
    <developmentMode developerInstallation="true"/>  
  </runtime>  
</configuration>  
```  
  
 L'impostazione predefinita è false.  
  
> [!NOTE]
>  Utilizzare questa impostazione solo in fase di sviluppo.  In fase di runtime non vengono controllate le versioni degli assembly con nome sicuro individuate mediante la variabile DEVPATH,  ma viene utilizzato il primo assembly individuato.  
  
## Vedere anche  
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/it-it/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)