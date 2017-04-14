---
title: "Tipi di dati comuni (riferimenti alle API non gestite) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "reference"
dev_langs: 
  - "C++"
ms.assetid: e4ab2c4c-9433-4eba-9e9a-096de406cafb
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Tipi di dati comuni (riferimenti alle API non gestite)
In questo argomento sono elencati i tipi di dati semplici usati dalle API non gestite per .NET Framework e definiti dalle istruzioni `typedef` di C\/C\+\+. Questi tipi di dati sono in genere alias di tipi di dati primitivi di C\/C\+\+. I valori di questi tipi di dati normalmente sono opachi, cioè vengono restituiti da una determinata funzione o metodo in modo da poter essere passati ad altre funzioni o metodi senza modifiche.  
  
|Tipo di dati|Definizione|Definito in|Descrizione|  
|------------------|-----------------|-----------------|-----------------|  
|AppDomainID|`typedef UINT_PTR AppDomainID;`|corprof.h|Identificatore di un dominio di applicazione.|  
|AssemblyID|`typedef UINT_PTR AssemblyID;`|corprof.h|Identificatore di un assembly.|  
|ClassID|`typedef UINT_PTR ClassID;`|corprof.h|Identificatore di una classe gestita.|  
|CONNID|`typedef DWORD CONNID;`|cordebug.h, mscoree.h|Identificatore della connessione per un thread connesso a un'istanza di Microsoft SQL Server.|  
|ContextID|`typedef UINT_PTR ContextID;`|corprof.h|Identificatore del contesto associato a un thread gestito specifico.|  
|COR\_PRF\_ELT\_INFO|`typedef UINT_PTR COR_PRF_ELT_INFO;`|corprof.h|Handle opaco che rappresenta le informazioni su un determinato stack frame.|  
|COR\_PRF\_FRAME\_INFO|`typedef UINT_PTR COR_PRF_FRAME_INFO;`|corprof.h|Handle opaco che punta a uno stack frame. È valido solo durante il callback a cui viene passato.|  
|CORDB\_ADDRESS|`typedef ULONG64 CORDB_ADDRESS;`|cordebug.h|Indirizzo in memoria.|  
|CORDB\_CONTINUE\_STATUS|`typedef DWORD CORDB_CONTINUE_STATUS;`|cordebug.h|Stato di continuazione.|  
|CORDB\_REGISTER|`typedef ULONG64 CORDB_REGISTER;`|cordebug.h|Valore di un registro della CPU.|  
|FunctionID|`typedef UINT_PTR FunctionID;`|corprof.h|Identificatore di una funzione o di un metodo.|  
|GCHandleID|`typedef UINT_PTR GCHandleID;`|corprof.h|Handle di Garbage Collection.|  
|mdToken|`typedef UINT32 mdToken;`|corprof.h|Token di metadati \(una riga in una tabella di metadati\).|  
|ModuleID|`typedef UINT_PTR ModuleID;`|corprof.h|Identificatore di un modulo di assembly.|  
|ObjectID|`typedef UINT_PTR ObjectID;`|corprof.h|Identificatore di un oggetto.|  
|ProcessID|`typedef UINT_PTR ProcessID;`|corprof.h|Identificatore di un processo gestito.|  
|ReJITID|`typedef UINT_PTR ReJITID;`|corprof.h|Identificatore di una funzione Just\-In\-Time.|  
|TASKID|`typedef UINT64 TASKID;`|cordebug.h, mscoree.h|Identificatore di un'istanza di [ICLRTask](../../../ocs/framework/unmanaged-api/hosting/iclrtask-interface.md).|  
|ThreadID|`typedef UINT_PTR ThreadID;`|corprof.h|Identificatore di un thread gestito.|  
  
## Vedere anche  
 [Riferimenti alle API non gestite](../../../docs/framework/unmanaged-api/index.md)