---
title: "Ricerca dello strumento di chiave privata (FindPrivateKey.exe) | Microsoft Docs"
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
ms.assetid: b8846a95-3fcc-4e8c-b9c0-128d975a6307
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Ricerca dello strumento di chiave privata (FindPrivateKey.exe)
Questo strumento da riga di comando può essere usato per recuperare una chiave privata da un archivio certificati.  Ad esempio, FindPrivateKey.exe può essere usato per cercare il percorso e il nome del file di chiave privata associati a un certificato X.509 specifico nell'archivio certificati.  
  
> [!IMPORTANT]
>  Lo strumento FindPrivateKey viene fornito come esempio WCF.  Per altre informazioni sull'ubicazione dell'esempio e su come compilarlo, vedere  
  
## Sintassi  
  
```  
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]  
```  
  
## Note  
 Nelle tabelle seguenti vengono descritti gli argomenti e le opzioni che possono essere usati con lo strumento di Ricerca della Chiave Privata \(FindPrivateKey.exe\).  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`storeName`|Nome dell'archivio certificati.|  
|`storeLocation`|Percorso dell'archivio certificati.|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`/n <` *subjectName* `>`|Specifica il nome dell’oggetto del certificato.|  
|`/t <` *Identificazione digitale* `>`|Specifica l'identificazione digitale del certificato.  Usare Certmgr.exe per recuperare l'identificazione digitale del certificato.|  
|`/f`|Restituisce soltanto il nome file.|  
|`/d`|Restituisce soltanto la directory.|  
|`/a`|Restituisce il nome file assoluto.|  
  
## Esempi  
 Il comando seguente consente di recuperare la chiave privata per John Doe.  
  
```  
FindPrivateKey My CurrentUser -n "CN=John Doe"  
```  
  
 Il comando seguente consente di recuperare la chiave privata per il computer locale.  
  
```  
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –a  
```