---
title: "Procedura: rimuovere un assembly dalla Global Assembly Cache | Microsoft Docs"
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
  - "eliminazione di assembly in Global Assembly Cache"
  - "GAC (Global Assembly Cache), rimozione di assembly"
  - "Gacutil.exe"
  - "Global Assembly Cache (strumento)"
  - "Global Assembly Cache, rimozione di assembly"
  - "rimozione di assembly dalla Global Assembly Cache"
  - "assembly con nome sicuro, Global Assembly Cache"
ms.assetid: acdcc588-b458-436d-876c-726de68244c1
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: rimuovere un assembly dalla Global Assembly Cache
Esistono due modi per rimuovere un assembly dalla Global Assembly Cache \(GAC\):  
  
-   Uso dello strumento [Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  È possibile usare questa opzione per disinstallare gli assembly inseriti nella GAC durante le fasi di sviluppo e test.  
  
-   Uso di [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx).  È possibile usare questa opzione per disinstallare gli assembly quando si esegue il test dei pacchetti di installazione o per i sistemi di produzione.  
  
### Rimozione di un assembly con Gacutil.exe  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     **gacutil –u** \<*nome assembly*\>  
  
     In questo comando *nome assembly* rappresenta il nome dell'assembly da rimuovere dalla Global Assembly Cache.  
  
    > [!WARNING]
    >  Evitare di usare Gacutil.exe per rimuovere assembly nei sistemi di produzione, perché è possibile che un assembly sia ancora richiesto da qualche applicazione.  Usare invece Windows Installer che mantiene un conteggio dei riferimenti per ogni assembly installato nella GAC.  
  
 L'esempio seguente rimuove un assembly denominato `hello.dll` dalla Global Assembly Cache.  
  
```  
gacutil -u hello  
```  
  
### Rimozione di un assembly con Windows Installer  
  
1.  In **Programmi e funzionalità** nel **Pannello di controllo** selezionare l'app da disinstallare.  Se il pacchetto di installazione ha inserito assembly nella GAC, questi saranno rimossi da Windows Installer se non vengono usati da altre applicazioni.  
  
    > [!NOTE]
    >  Windows Installer mantiene un conteggio dei riferimenti per gli assembly installati nella GAC.  La rimozione di un assembly dalla Global Assembly Cache avviene solo quando il conteggio dei riferimenti raggiunge zero. Ciò indica che non viene usato da altre applicazioni installate da un pacchetto di Windows Installer.  
  
## Vedere anche  
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Procedura: Installare un assembly nella Global Assembly Cache](../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)