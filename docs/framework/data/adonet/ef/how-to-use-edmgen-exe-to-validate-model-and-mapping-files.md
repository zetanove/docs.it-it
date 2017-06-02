---
title: "Procedura: utilizzare EdmGen.exe per convalidare i file di modello e di mapping | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: 2641906a-971a-4d0b-8aee-13fabc02a1cc
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Procedura: utilizzare EdmGen.exe per convalidare i file di modello e di mapping
In questo argomento viene illustrato come usare lo strumento [Generatore EDM \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md) per convalidare i file di modello e di mapping.  Per altre informazioni, vedere [Entity Data Model](../../../../../docs/framework/data/adonet/entity-data-model.md).  
  
### Per convalidare il modello School usando EdmGen.exe  
  
1.  Creare il database School.  Per altre informazioni, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0).  
  
2.  Generare il modello School.  Per altre informazioni, vedere [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
3.  Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```scr  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:ValidateArtifacts /inssdl:.\School.ssdl /inmsl:.\School.msl /incsdl:.\School.csdl  
    ```  
  
## Vedere anche  
 [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527)   
 [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/it-it/b18a9d16-e10b-4043-ba91-b632f85a2579)   
 [Procedura: utilizzare EdmGen.exe per generare il codice del livello oggetti](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md)