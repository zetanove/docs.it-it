---
title: "Procedura: visualizzare il contenuto della Global Assembly Cache | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], Global Assembly Cache"
  - "GAC (Global Assembly Cache), visualizzazione di contenuto"
  - "Gacutil.exe"
  - "Global Assembly Cache (strumento)"
  - "Global Assembly Cache, visualizzazione di contenuto"
  - "elenchi di assembly nella Global Assembly Cache"
  - "assembly con nome sicuro, Global Assembly Cache"
  - "visualizzazione di assembly nella Global Assembly Cache"
ms.assetid: c5f786a0-969b-4f14-9f02-e77c3384d9af
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: visualizzare il contenuto della Global Assembly Cache
Usare lo strumento [Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) per visualizzare i contenuti della Global Assembly Cache.  
  
### Per visualizzare un elenco degli assembly presenti nella Global Assembly Cache  
  
1.  Al [prompt dei comandi di Visual Studio](../../../docs/framework/tools/developer-command-prompt-for-vs.md) digitare il comando seguente:  
  
     **gacutil \-l**   
     \-oppure\-               
     **gacutil \/l**  
  
 Nelle versioni precedenti di .NET Framework, l'estensione della shell di Windows [Shfusion.dll](http://msdn.microsoft.com/it-it/0d9464cf-ddba-4ca9-bbec-f678fb58f380) consente di visualizzare la Global Assembly Cache in Esplora risorse.  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Shfusion.dll è obsoleto.  
  
## Vedere anche  
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)