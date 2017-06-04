---
title: "Procedura: installare un assembly nella Global Assembly Cache | Microsoft Docs"
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
  - "Gacutil.exe"
  - "Global Assembly Cache (strumento)"
  - "Global Assembly Cache, installazione di assembly"
  - "assembly con nome sicuro, Global Assembly Cache"
ms.assetid: a7e6f091-d02c-49ba-b736-7295cb0eb743
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Procedura: installare un assembly nella Global Assembly Cache
Esistono due modi per installare un assembly con nome sicuro nella Global Assembly Cache:  
  
> [!IMPORTANT]
>  Nella GAC possono essere installati solo assembly con nome sicuro.  Per informazioni sulla creazione di un assembly con nome sicuro, vedere [Procedura: firmare un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  
  
-   Uso di [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx).  
  
     Eseguire questa operazione in Visual Studio 2012 e Visual Studio 2013 creando un progetto InstallShield Limited Edition.  
  
     Si tratta della modalità consigliata e più comune per l'aggiunta di assembly alla Global Assembly Cache.  In tal modo si ottiene il conteggio dei riferimenti degli assembly nella Global Assembly Cache e altre utili funzionalità.  
  
-   Uso dello [strumento Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
     È possibile usare Gacutil.exe per aggiungere assembly con nome sicuro alla Global Assembly Cache e visualizzare il contenuto di tale cache.  
  
    > [!NOTE]
    >  È necessario usare Gacutil.exe solo in fase di sviluppo e non se ne consiglia l'uso per l'installazione di assembly di produzione nella Global Assembly Cache.  
  
> [!NOTE]
>  Nelle versioni precedenti di .NET Framework, l'estensione della shell di Windows Shfusion.dll consente di installare gli assembly trascinandoli in Esplora file.  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Shfusion.dll è obsoleto.  
  
### Per usare lo strumento Global Assembly Cache \(Gacutil.exe\).  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     **gacutil \-i** \<*nome assembly*\>  
  
     In questo comando *nome assembly* rappresenta il nome dell'assembly da installare nella Global Assembly Cache.  
  
 L'esempio seguente consente di installare un assembly con nome file `hello.dll` nella Global Assembly Cache.  
  
```  
gacutil -i hello.dll  
```  
  
 Per altre informazioni, vedere [Strumento Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
### Per usare un progetto InstallShield Limited Edition  
  
1.  Aggiungere un pacchetto di installazione e distribuzione alla soluzione aprendo il menu di scelta rapida per la soluzione e scegliendo **Aggiungi**, **Nuovo progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo progetto**, nella cartella **Installato**, scegliere **Altri tipi di progetto**,  **Installazione e distribuzione**, **InstallShield Limited Edition** e assegnare un nome al progetto.  \(Se richiesto, scaricare, installare e attivare InstallShield.\)  
  
3.  Eseguire la configurazione generale del progetto di installazione e di distribuzione usando Project Assistant in **Esplora soluzioni** oppure scegliendo i passaggi secondari dei passaggi numerati in **Esplora soluzioni**.  Configurare il programma di installazione come si farebbe se non si stessero aggiungendo assembly alla GAC.  
  
4.  Per avviare il processo di aggiunta di un assembly nella GAC, scegliere **File**, nel passaggio **Specifica dati applicazione** in **Esplora soluzioni**.  
  
5.  Nel riquadro **Cartelle computer di destinazione** aprire il menu di scelta rapida per **Computer di destinazione**, quindi scegliere **Mostra cartella predefinita**, **\[GlobalAssemblyCache\]**.  
  
6.  Per ogni progetto nella soluzione che contiene un assembly che si desidera installare nella Global Assembly Cache:  
  
    1.  Nel riquadro **Cartelle computer di origine** scegliere progetto.  
  
    2.  Nel riquadro **Cartelle computer di destinazione** scegliere **\[GlobalAssemblyCache\]**.  
  
    3.  Nel riquadro **File computer di origine** scegliere **Output primario da** *\<nome\_progetto\>*.  
  
    4.  Trascinare il file nel passaggio c al riquadro di **File computer di destinazione** \(oppure usare i comandi **Copia** e **Incolla** dal menu di scelta rapida del file\).  
  
## Vedere anche  
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Procedura: rimuovere un assembly dalla Global Assembly Cache](../../../docs/framework/app-domains/how-to-remove-an-assembly-from-the-gac.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)   
 [Procedura: firmare un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)   
 [Windows Installer Deployment](http://msdn.microsoft.com/it-it/121be21b-b916-43e2-8f10-8b080516d2a0)