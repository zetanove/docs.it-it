---
title: "Procedura: utilizzare EdmGen.exe per generare il codice del livello oggetti | Microsoft Docs"
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
ms.assetid: c44d2ebe-f66f-42cb-9741-4a3f0c2dcffb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Procedura: utilizzare EdmGen.exe per generare il codice del livello oggetti
In questo argomento viene illustrato come usare lo strumento [Generatore EDM \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md) per generare il codice del livello oggetti in base al file csdl.  
  
### Per generare il codice del livello oggetti per il modello School per un progetto di Visual Basic usando EdmGen.exe  
  
1.  Creare il database School.  Per altre informazioni, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0).  
  
2.  Generare il modello School o ottenere il file School.csdl.  Per altre informazioni, vedere [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
3.  Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:EntityClassGeneration   
    /incsdl:.\School.csdl /outobjectlayer:.\School.Objects.vb /language:VB  
    ```  
  
### Per generare il codice del livello oggetti per il modello School per un progetto di C\# usando EdmGen.exe  
  
1.  Creare il database School.  Per altre informazioni, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0).  
  
2.  Generare il modello School o ottenere il file School.csdl.  Per altre informazioni, vedere [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
3.  Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:EntityClassGeneration   
    /incsdl:.\School.csdl /outobjectlayer:.\School.Objects.cs /language:CSharp  
    ```  
  
## Vedere anche  
 [Modellazione e mapping](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527)   
 [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/it-it/b18a9d16-e10b-4043-ba91-b632f85a2579)   
 [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)