---
title: "Procedura: creare criteri editore | Microsoft Docs"
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
  - "GAC (Global Assembly Cache), assembly dei criteri editore"
  - "Global Assembly Cache, assembly dei criteri editore"
  - "assembly dei criteri editore"
  - "file dei criteri editore"
ms.assetid: 8046bc5d-2fa9-4277-8a5e-6dcc96c281d9
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Procedura: creare criteri editore
È possibile che i fornitori di assembly consiglino l'utilizzo di una versione più recente di un assembly per l'esecuzione delle applicazioni fornendo un file dei criteri editore con l'assembly aggiornato.  Il file dei criteri editore contiene le impostazioni della codebase e per il reindirizzamento degli assembly e utilizza lo stesso formato del file di configurazione dell'applicazione.  Il file dei criteri editore viene compilato in un assembly e inserito nella Global Assembly Cache.  
  
 La creazione dei criteri editore si articola in tre passaggi.  
  
1.  Creazione di un file dei criteri editore.  
  
2.  Creazione di un assembly dei criteri editore.  
  
3.  Aggiunta dell'assembly dei criteri editore alla Global Assembly Cache.  
  
 Lo schema per i criteri editore viene descritto nella sezione [Reindirizzamento delle versioni degli assembly](../../../docs/framework/configure-apps/redirect-assembly-versions.md).  Nell'esempio riportato di seguito viene illustrato un file dei criteri editori che consente di reindirizzare una versione di `myAssembly`.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <!-- Redirecting to version 2.0.0.0 of the assembly. -->  
         <bindingRedirect oldVersion="1.0.0.0"  
                          newVersion="2.0.0.0"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 Per informazioni su come specificare una codebase, vedere [Specifica della posizione di un assembly](../../../docs/framework/configure-apps/specify-assembly-location.md).  
  
## Creazione dell'assembly dei criteri editore  
 Utilizzare [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) per creare l'assembly dei criteri editore.  
  
#### Per creare un assembly dei criteri editore  
  
1.  Digitare il seguente comando al prompt dei comandi:  
  
     **al \/link:** *publisherPolicyFile* **\/out:** *publisherPolicyAssemblyFile* **\/keyfile:** *keyPairFile* **\/platform:** *processorArchitecture*  
  
     In questo comando:  
  
    -   L'argomento *publisherPolicyFile* è il nome del file dei criteri editore.  
  
    -   L'argomento *publisherPolicyAssemblyFile* è il nome dell'assembly dei criteri editore risultante da questo comando.  Il nome del file di assembly deve seguire il formato:  
  
         **policy.** *majorNumber* **.** *minorNumber* **.** *mainAssemblyName* **.dll**  
  
    -   L'argomento *keyPairFile* è il nome del file che contiene la coppia di chiavi.  È necessario utilizzare la stessa coppia di chiavi per firmare l'assembly e l'assembly dei criteri editore.  
  
    -   L'argomento *processorArchitecture* identifica la piattaforma di destinazione di un assembly specifico di un processore,  
  
        > [!NOTE]
        >  La possibilità di utilizzare come destinazione un'architettura specifica di un processore è una nuova funzionalità di .NET Framework versione 2.0.  
  
     Mediante il comando riportato di seguito viene creato un assembly dei criteri editore denominato `policy.1.0.myAssembly` da un file dei criteri editore denominato `pub.config`. Viene inoltre assegnato all'assembly un nome sicuro mediante la coppia di chiavi presente nel file `sgKey.snk` e viene specificata come destinazione dell'assembly l'architettura del processore x86.  
  
    ```  
    al /link:pub.config /out:policy.1.0.myAssembly.dll /keyfile:sgKey.snk /platform:x86  
    ```  
  
     L'assembly dei criteri editore deve corrispondere all'architettura del processore dell'assembly a cui si applica.  Se pertanto il valore <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A> dell'assembly è impostato su <xref:System.Reflection.ProcessorArchitecture>, l'assembly dei criteri editore per tale assembly deve essere creato con `/platform:anycpu`.  È necessario specificare un assembly dei criteri editore separato per ogni assembly specifico di un processore.  
  
     Come conseguenza di questa regola, per modificare l'architettura del processore per un assembly, è necessario modificare il componente principale o secondario del numero di versione, in modo da poter fornire a un nuovo assembly dei criteri editore l'architettura di processore corretta.  Non è più possibile utilizzare l'assembly dei criteri editore precedente per l'assembly dopo aver specificato un'architettura di processore diversa.  
  
     Un'altra conseguenza è che non è possibile utilizzare il linker della versione 2.0 per creare un assembly dei criteri editore per un assembly compilato utilizzando versioni precedenti di .NET Framework, poiché viene specificata l'architettura del processore.  
  
## Aggiunta dell'assembly dei criteri editore alla Global Assembly Cache  
 Utilizzare lo [strumento Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) per aggiungere l'assembly dei criteri editore alla Global Assembly Cache.  
  
#### Per aggiungere l'assembly dei criteri editore alla Global Assembly Cache  
  
1.  Digitare il seguente comando al prompt dei comandi:  
  
     **gacutil \/i**  *publisherPolicyAssemblyFile*  
  
     Mediante il seguente comando viene aggiunto l'assembly `policy.1.0.myAssembly.dll` alla Global Assembly Cache.  
  
    ```  
    gacutil /i policy.1.0.myAssembly.dll  
    ```  
  
    > [!IMPORTANT]
    >  L'assembly dei criteri editore non può essere aggiunto alla Global Assembly Cache a meno che il file dei criteri editore originale non sia contenuto nella stessa directory dell'assembly.  
  
## Vedere anche  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configurazione di app](../../../docs/framework/configure-apps/index.md)   
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/it-it/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Reindirizzamento delle versioni di assembly](../../../docs/framework/configure-apps/redirect-assembly-versions.md)