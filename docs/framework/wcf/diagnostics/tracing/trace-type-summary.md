---
title: "Riepilogo dei tipi di traccia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e639410b-d1d1-479c-b78e-a4701d4e4085
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Riepilogo dei tipi di traccia
Nella pagina relativa all'[enumerazione SourceLevels](http://go.microsoft.com/fwlink/?LinkID=94943) vengono definiti i vari livelli di traccia, ovvero Critical, Error, Warning, Information e Verbose, e viene descritto il flag `ActivityTracing` che attiva o disattiva l'output del limite di traccia e gli eventi di trasferimento attività.  
  
 È anche possibile esaminare l'enumerazione [TraceEventType](http://go.microsoft.com/fwlink/?LinkId=95169) per i tipi di traccia che possono essere emessi da <xref:System.Diagnostics>.  
  
 Nella tabella seguente sono elencati quelli più importanti.  
  
|Tipo di traccia|Descrizione|  
|---------------------|-----------------|  
|Critical|Errore irreversibile o arresto anomalo dell'applicazione.|  
|Errore|Errore risolvibile.|  
|Avviso|Messaggio informativo.|  
|Informazioni|Problema non critico.|  
|Dettagliato|Debug della traccia.|  
|Start|Avvio di un'unità logica di elaborazione.|  
|Sospendi|Sospensione di un'unità logica di elaborazione.|  
|Riprendi|Ripresa di un'unità logica di elaborazione..|  
|Interrompi|Arresto di un'unità logica di elaborazione.|  
|Trasferimento|Modifica dell'identità di correlazione.|  
  
 Un'attività è definita come una combinazione dei tipi di traccia riportati sopra.  
  
 Quella che segue è un'espressione regolare che definisce un'attività ideale in un ambito locale \(origine di traccia\),  
  
 `R = Start (Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop`  
  
 Ciò significa che un'attività deve soddisfare le condizioni seguenti.  
  
-   Deve avviarsi e arrestarsi rispettivamente con tracce Start e Stop.  
  
-   Deve avere una traccia Transfer subito prima di una traccia Suspend o Resume  
  
-   Non deve avere nessuna traccia tra le tracce Suspend e Resume, se esistono  
  
-   Può avere un numero qualsiasi di tracce Critical\/Error\/Warning\/Information\/Verbose\/Transfer, a condizione che vengano rispettate le condizioni precedenti  
  
 Quella che segue è un'espressione regolare che definisce un'attività ideale in ambito globale,  
  
```  
R+   
```  
  
 con R che è l'espressione regolare per un'attività nell'ambito locale.  Ciò si traduce in,  
  
```  
[R+ = Start ( Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop]+  
```