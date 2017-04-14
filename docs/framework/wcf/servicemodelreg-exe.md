---
title: "Strumento di registrazione ServiceModel (ServiceModelReg.exe) | Microsoft Docs"
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
ms.assetid: 396ec5ae-e34f-4c64-a164-fcf50e86b6ac
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Strumento di registrazione ServiceModel (ServiceModelReg.exe)
Lo strumento da riga di comando consente di gestire la registrazione di componenti WCF e WF in un singolo computer.In condizioni normali, non è consigliabile l'utilizzo di questo strumento poiché, se installati, i componenti WCF e WF sono configurati.Tuttavia, se si verificano problemi con l'attivazione del servizio, si può tentare la registrazione dei componenti tramite questo strumento.  
  
## Sintassi  
  
```  
  
ServiceModelReg.exe[(-ia|-ua|-r)|((-i|-u) -c:<command>)] [-v|-q] [-nologo] [-?]  
```  
  
## Note  
 Lo strumento si trova nel percorso seguente:  
  
 %SystemRoot%\\Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\  
  
> [!NOTE]
>  Quando lo strumento di registrazione ServiceModel viene eseguito su [!INCLUDE[wv](../../../includes/wv-md.md)], la finestra di dialogo **Funzionalità Windows** potrebbe non indicare l'attivazione dell'opzione **Attivazione di Windows Communication Foundation HTTP** in **Microsoft .NET Framework 3.0**.La finestra di dialogo **Funzionalità Windows** può essere utilizzata facendo clic su **Avvio**, quindi fare clic su **Esegui** e digitando **OptionalFeatures**.  
  
 Nella tabella riportata di seguito sono descritte le opzioni che possono essere utilizzate con ServiceModelReg.exe.  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`-ia`|Installa tutti i componenti WCF e WF.|  
|`-ua`|Disinstalla tutti i componenti WCF e WF.|  
|`-r`|Ripristina tutti i componenti WCF e WF.|  
|`-i`|Installa tutti i componenti WCF e WF specificati con –c.|  
|`-u`|Disinstalla tutti i componenti WCF e WF specificati con –c.|  
|`-c`|Installa o disinstalla un componente:<br /><br /> -   httpnamespace – prenotazione dello spazio dei nomi HTTP<br />-   tcpportsharing – servizio di condivisione delle porte TCP<br />-   tcpactivation – servizio di attivazione TCP \(non supportato in .NET 4 Client Profile\)<br />-   namedpipeactivation – servizio di attivazione named pipe \(non supportato in .NET 4 Client Profile\)<br />-   msmqactivation – servizio di attivazione MSMQ \(non supportato in .NET 4 Client Profile\)<br />-   etw – manifesti di traccia eventi ETW \(Windows Vista o versioni successive\)|  
|`-q`|Modalità non interattiva \(solo registrazione errori visualizzata\)|  
|`-v`|Modalità dettagliata.|  
|`-nologo`|Elimina le informazioni di copyright e il messaggio di avvio.|  
|`-?`|Visualizza il testo della Guida|  
  
## Correzione dell’errore FileLoadException  
 Se sono state installate versioni precedenti di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sul computer, è possibile che venga visualizzato un errore `FileLoadFoundException` durante l’esecuzione dello strumento ServiceModelReg per registrare una nuova installazione.Ciò può verificarsi anche se sono stati rimossi manualmente file dall’installazione precedente, ma sono state mantenute intatte le impostazioni machine.config.  
  
 Verrà visualizzato un messaggio di errore simile al seguente:  
  
```  
Error: System.IO.FileLoadException: Could not load file or assembly 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)  
File name: 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  
```  
  
 È necessario notare dal messaggio di errore che è stato installato l’assembly System.ServiceModel Versione 2.0.0.0 di una precedente versione di Customer Technology Preview \(CTP\).La versione corrente dell'assembly System.ServiceModel rilasciata è invece 3.0.0.0.Pertanto, è possibile incontrare questo problema quando si vuole installare la versione ufficiale [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] su un computer nel quale è stata installata una precedente versione di CTP [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], ma non completamente disinstallata.  
  
 ServiceModelReg.exe non può eseguire la pulizia di voci della versione precedente, né può registrare voci della versione nuova.L’unica soluzione alternativa è modificare manualmente machine.config.È possibile trovare questo file al percorso seguente.  
  
```  
%windir%\Microsoft.NET\Framework\v2.0.50727\config\machine.config   
```  
  
 Se si esegue [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] su un computer a 64 bit, è necessario modificare lo stesso file anche in questa posizione.  
  
```  
%windir%\Microsoft.NET\Framework64\v2.0.50727\config\machine.config   
```  
  
 Trovare qualsiasi nodo XML in questo file che fa riferimento a “System.ServiceModel, Versione\=2 .0.0.0”, eliminare tali nodi e qualsiasi nodo figlio.Per risolvere il problema, salvare il file e ripetere l'esecuzione di ServiceModelReg.exe.  
  
## Esempi  
 Negli esempi seguenti viene illustrato come utilizzare le opzioni più comuni dello strumento ServiceModelReg.exe.  
  
```  
ServiceModelReg.exe -ia  
  Installs all components  
ServiceModelReg.exe -i -c:httpnamespace -c:etw  
  Installs HTTP namespace reservation and ETW manifests  
ServiceModelReg.exe -u -c:etw  
  Uninstalls ETW manifests  
ServiceModelReg.exe -r  
  Repairs an extended install  
```