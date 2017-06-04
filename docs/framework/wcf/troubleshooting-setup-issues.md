---
title: "Risoluzione dei problemi di installazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1644f885-c408-4d5f-a5c7-a1a907bc8acd
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Risoluzione dei problemi di installazione
In questo argomento viene descritto come risolvere i problemi di installazione di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].  
  
## Alcune chiavi del Registro di sistema di Windows Communication Foundation non vengono ripristinate eseguendo un'operazione di ripristino MSI in .NET Framework 3.0  
 Se si elimina una delle chiavi di Registro seguenti:  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelService 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelOperation 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\ServiceModelEndpoint 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\SMSvcHost 3.0.0.0  
  
-   HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\MSDTC Bridge 3.0.0.0  
  
 Le chiavi non vengono ricreate se il ripristino viene eseguito utilizzando il programma di installazione di .NET Framework 3.0 avviato dall'applet **Installazione applicazioni** in **Pannello di controllo**.Per ricreare correttamente queste chiavi, l'utente deve disinstallare e reinstallare .NET Framework 3.0.  
  
## Il danneggiamento del servizio WMI blocca l'installazione del provider WMI per Windows Communication Foundation durante l'installazione del pacchetto .NET Framework 3.0  
 È possibile che, a causa del danneggiamento del servizio WMI, l'installazione del provider WMI per Windows Communication Foundation venga bloccata.Durante l'installazione il programma di installazione di Windows Communication Foundation non è in grado di registrare il file WCF con estensione mof mediante il componente mofcomp.exe.Di seguito è riportato un elenco di sintomi:  
  
1.  L'installazione di .NET Framework 3.0 viene completata correttamente, ma il provider WMI per WCF non viene registrato.  
  
2.  Nel registro eventi dell'applicazione viene visualizzato un evento di errore che fa riferimento a problemi durante la registrazione del provider WMI per WCF o l'esecuzione di mofcomp.exe.  
  
3.  Il file di log dell'installazione denominato dd\_wcf\_retCA\* nella directory %temp% dell'utente contiene riferimenti all'impossibilità di registrare il provider WMI per WCF.  
  
4.  È possibile che nel registro eventi o nel file di log sia elencata un'eccezione simile a una delle seguenti:  
  
     ServiceModelReg \[11:09:59:046\]: System.ApplicationException: Risultato imprevisto 3 durante l'esecuzione di E:\\WINDOWS\\system32\\wbem\\mofcomp.exe con "E:\\WINDOWS\\Microsoft.NET\\Framework\\v3.0\\Windows Communication Foundation\\ServiceModel.mof"  
  
     o:  
  
     ServiceModelReg \[07:19:33:843\]: System.TypeInitializationException: L'inizializzatore di tipo di 'System.Management.ManagementPath' ha generato un'eccezione.\-\-\-\> System.Runtime.InteropServices.COMException \(0x80040154\): Recupero della class factory COM per il componente con CLSID {CF4CC405\-E2C5\-4DDD\-B3CE\-5E7582D8C9FA} non riuscito a causa del seguente errore: 80040154.  
  
     o:  
  
     ServiceModelReg \[07:19:32:750\]: System.IO.FileNotFoundException: Impossibile caricare il file o l'assembly 'C:\\WINDOWS\\system32\\wbem\\mofcomp.exe' o una delle relative dipendenze.Impossibile trovare il file specificato.  
  
     Nome file: 'C:\\WINDOWS\\system32\\wbem\\mofcomp.exe  
  
 Per risolvere il problema descritto in precedenza, è necessario eseguire la procedura seguente.  
  
1.  Eseguire l'[utilità di diagnostica di Strumentazione gestione Windows, versione 2.0](http://go.microsoft.com/fwlink/?LinkId=94685) per ripristinare il servizio WMI.[!INCLUDE[crabout](../../../includes/crabout-md.md)] utilizzo di questo strumento, vedere l'argomento relativo all'[utilità di diagnostica di Strumentazione gestione Windows](http://go.microsoft.com/fwlink/?LinkId=94686).  
  
 Ripristinare l'installazione di .NET Framework 3.0 utilizzando l'applet **Installazione applicazioni** situata in **Pannello di controllo** o disinstallare\/reinstallare .NET Framework 3.0.  
  
## Il ripristino di .NET Framework 3.0 in seguito all'installazione di .NET Framework 3.5 rimuove gli elementi di configurazione introdotti da .NET Framework 3.5 nel file machine.config  
 Il ripristino di .NET Framework 3.0 in seguito all'installazione di [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)], gli elementi di configurazione introdotti da [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] nel file machine.config vengono rimossi.Tuttavia, la config web rimane invariata.La soluzione alternativa consiste nel ripristinare [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] al termine di questa operazione mediante ARP, o utilizzare lo strumento [Strumento di registrazione dei servizi di Windows Workflow \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) con l'opzione `/c`.  
  
 [Strumento di registrazione dei servizi di Windows Workflow \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) si trova in %windir%\\Microsoft.NET\\framework\\v3.5\\ o in %windir%\\Microsoft.NET\\framework64\\v3.5\\  
  
## Configurare IIS correttamente per WCF\/WF Webhost dopo aver installato .NET Framework 3.5  
 Quando l'installazione di [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] non riesce a configurare impostazioni di configurazione IIS [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] aggiuntive, registra un errore nel log di installazione e continua con l'operazione corrente.Qualsiasi tentativo di eseguire applicazioni WorkflowServices avrà esito negativo in quanto le impostazioni di configurazione richieste risultano mancanti.Ad esempio, il caricamento di xoml o del servizio regole potrebbe avere esito negativo.  
  
 Per evitare questo problema, utilizzare lo [Strumento di registrazione dei servizi di Windows Workflow \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) con l'opzione `/c` per configurare correttamente i mapping dello script IIS nel computer.[Strumento di registrazione dei servizi di Windows Workflow \(WFServicesReg.exe\)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) si trova in %windir%\\Microsoft.NET\\framework\\v3.5\\ o in %windir%\\Microsoft.NET\\framework64\\v3.5\\  
  
## Impossibile caricare il tipo ‘System.ServiceModel.Activation.HttpModule’ dall'assembly ‘System.ServiceModel, Version 3.0.0.0, Culture\=neutral, PublicKeyToken\=b77a5c561934e089’  
 Questo errore si verifica se viene installato [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] e quindi viene abilitata l'attivazione HTTP [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)][!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Per risolvere il problema eseguire la riga di comando seguente dal prompt dei comandi di [!INCLUDE[vs2010](../../../includes/vs2010-md.md)]:  
  
```Output  
aspnet_regiis.exe -i -enable  
```  
  
## Vedere anche  
 [Istruzioni di configurazione](../../../docs/framework/wcf/samples/set-up-instructions.md)