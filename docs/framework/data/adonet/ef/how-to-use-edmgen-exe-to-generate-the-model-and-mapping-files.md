---
title: "Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping | Microsoft Docs"
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
ms.assetid: 40db462d-2fd2-4cc1-ad86-d280403e63fa
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping
In questo argomento viene illustrato come usare lo strumento Generatore EDM \(EdmGen.exe\) per generare i seguenti file in base al database School:  
  
-   Modello concettuale \(file con estensione csdl\).  
  
-   Modello di archiviazione \(file con estensione ssdl\).  
  
-   Mapping tra i modelli concettuali e di archiviazione \(file con estensione msl\).  
  
-   Codice del livello oggetti in Visual Basic o C\#.  
  
-   File di visualizzazione.  
  
 Lo strumento EdmGen.exe usa \/mode:FullGeneration per la generazione dei file elencati in precedenza.  Per altre informazioni sui comandi di EdmGen.exe, vedere [Generatore EDM \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md).  
  
 Se si usa EdmGen.exe per generare i file di modello e di mapping, sarà comunque necessario configurare il progetto di [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e).  
  
> [!NOTE]
>  Un modello concettuale generato da EdmGen.exe include tutti gli oggetti del database.  Per generare un modello concettuale che include solo oggetti specifici, usare la Procedura guidata Entity Data Model.  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
### Per generare il modello School per un progetto Visual Basic usando EdmGen.exe  
  
1.  Creare il database School.  Per altre informazioni, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0).  
  
2.  Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration   
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"   
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:VB  
  
    ```  
  
### Per generare il modello School per un progetto C\# usando EdmGen.exe  
  
1.  Creare il database School.  Per altre informazioni, vedere [Creating the School Sample Database](http://msdn.microsoft.com/it-it/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0).  
  
2.  Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration   
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"   
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:CSharp  
    ```  
  
## Vedere anche  
 [Modellazione e mapping](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)   
 [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/it-it/b18a9d16-e10b-4043-ba91-b632f85a2579)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527)   
 [Procedura: utilizzare EdmGen.exe per convalidare i file di modello e di mapping](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)