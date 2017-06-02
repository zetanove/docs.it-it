---
title: "Interpretazione della traccia di rete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "TraceMode (attributo)"
  - "dati esadecimali, output della traccia di rete"
  - "traccia di rete, analisi"
  - "protocolonly"
  - "testo, output della traccia di rete"
  - "includehex"
ms.assetid: ad22b4b8-00af-4778-9cca-cb609ce1f8ff
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Interpretazione della traccia di rete
Quando la tracciatura della rete è abilitato, è possibile utilizzare la tracciatura per acquisire le chiamate dell'applicazione a vari <xref:System.Net> i membri della classe.  L'output di queste chiamate può essere simile agli esempi seguenti.  
  
```  
[588]   (4357)   Entering Socket#33574638::Send()  
[588]   (4387)   Exiting Socket#33574638::Send()-> 61#61  
```  
  
 Nell'esempio precedente, \[588\] è l'identificatore univoco del thread corrente.  \(4357\) e \(4387\) sono i timestamp che indicano il numero di millisecondi trascorsi dopo che l'applicazione ha avviato.  I dati che seguono il timestamp mostrano l'applicazione che fornisce e proveniente il metodo **Socket.Send**.  L'oggetto che esegue il metodo **Send** dispone di 33574638 come relativo identificatore univoco.  L'analisi dell'uscita di metodo include il valore restituito \(61 nell'esempio precedente\).  
  
 La tracciatura della rete possono acquisire il traffico di rete da cui viene inviato o viene ricevuto dall'applicazione tramite protocolli a livello di applicazione come protocollo HTTP \(HTTP\).  Questi dati possono essere acquisiti come testo e, facoltativamente, dati esadecimali.  I dati esadecimali sono disponibili quando si specifica **includehex** come valore dell'attributo **tracemode**.  \(Per informazioni dettagliate su questo attributo, vedere [Procedura: Configurare la tracciatura della rete](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)\). Nell'analisi di esempio è stata generata utilizzando **includehex**.  
  
 `[1692]   (1142)   00000000 : 47 45 54 20 2F 77 70 61-64 2E 64 61 74 20 48 54 : GET /wpad.dat HT`  
  
 `[1692]   (1142)   00000010 : 54 50 2F 31 2E 31 0D 0A-48 6F 73 74 3A 20 69 74 : TP/1.1..Host: it`  
  
 `[1692]   (1142)   00000020 : 67 70 72 6F 78 79 0D 0A-43 6F 6E 6E 65 63 74 69 : gproxy..Connecti`  
  
 `[1692]   (1142)   00000030 : 6F 6E 3A 20 43 6C 6F 73-65 0D 0A 0D 0A     : on: Close....`  
  
 Per omettere i dati esadecimali, specificare **protocolonly** come valore per l'attributo **tracemode**.  Nell'esempio seguente viene illustrata la tracciatura quando **protocolonly** è specificato.  
  
 `[2444]   (594)   Data from ConnectStream#33574638::WriteHeaders<<GET /wpad.dat HTTP/1.1`  
  
 `Host: itgproxy`  
  
 `Connection: Close`  
  
## Vedere anche  
 [Abilitazione della traccia di rete](../../../docs/framework/network-programming/enabling-network-tracing.md)   
 [Procedura: Configurare la tracciatura della rete](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)   
 [Tracciatura di rete in .NET Framework](../../../docs/framework/network-programming/network-tracing.md)