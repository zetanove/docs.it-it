---
title: "Attributo GUID_ManagedName | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "reference"
apiname: 
  - "GUID_ManagedName"
apilocation: 
  - "alink.dll"
apitype: "COM"
f1_keywords: 
  - "GUID_ManagedName"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "GUID_ManagedName (attributo)"
ms.assetid: 11e18095-e444-47bc-aff6-b887ac5dc01e
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Attributo GUID_ManagedName
Definisce un attributo personalizzato dell'interfaccia che specifica il nome dello spazio dei nomi gestito per una raccolta di componente oggetto model \(COM\).  
  
## Sintassi  
  
```  
[  
   custom(GUID_ManagedName, value)  
]  
```  
  
#### Parametri  
 `value`  
 Il nome dello spazio dei nomi gestito per la libreria.  
  
## Definizione  
 `GUID_ManagedName` viene definita nel Cor. h come segue:  
  
```  
// {0F21F359-AB84-41e8-9A78-36D110E6D2F9}  
EXTERN_GUID(GUID_ManagedName, 0xf21f359, 0xab84, 0x41e8, 0x9a, 0x78, 0x36, 0xd1, 0x10, 0xe6, 0xd2, 0xf9);  
```  
  
## Note  
 Un attributo personalizzato dell'interfaccia definisce i metadati per un oggetto nella libreria dei tipi.  
  
 Utilizzare <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetCustData%2A?displayProperty=fullName> o <xref:System.Runtime.InteropServices.ComTypes.ITypeLib2.GetCustData%2A?displayProperty=fullName> per recuperare il nome gestito dall'attributo.  
  
 Per ulteriori informazioni, vedere [Interface Attributes](../Topic/Interface%20Attributes.md) in Visual C\+\+ fare riferimento alla documentazione.  
  
## Esempio  
 Nell'esempio seguente viene illustrata una definizione di libreria utilizzando il `GUID_ManagedName` attributo.  
  
```  
[  
   ...  
   custom(GUID_ManagedName, Microsoft.VisualStudio.CommandBars.dll")  
]  
library Microsoft_VisualStudio_CommandBars  
{  
   ...  
}  
```  
  
## Requisiti  
 **Intestazione:** Cor.h