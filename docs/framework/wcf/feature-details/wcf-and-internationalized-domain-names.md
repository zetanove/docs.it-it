---
title: "WCF e nomi IDN (Internationalized Domain Name) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8a3e10a-8bc2-4a78-8d86-a562ba6e65fa
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# WCF e nomi IDN (Internationalized Domain Name)
È stato aggiunto il supporto per i servizi WCF con gli IDN \(Internationalized Domain Name\).  Un IDN è un nome di dominio che contiene caratteri non ASCII.  Questo supporto include sia la possibilità di ospitare un servizio WCF con un nome IDN sia un client WCF per comunicare con un servizio Web con un nome IDN.  
  
## System.Uri e IDN  
 All'oggetto <xref:System.Uri> sono associate due proprietà: <xref:System.Uri.Host%2A> e <xref:System.Uri.DnsSafeHost%2A>.  Queste proprietà contengono valori Unicode o Punycode in base alle impostazioni di configurazione IDN.  
  
 IDN viene abilitato nel file di configurazione di un'applicazione usando il seguente codice XML  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All/AllExceptIntranet/None" />  
  </uri>  
</configuration>  
  
```  
  
 L'elemento \<idn\> contiene l'attributo abilitato che può essere impostato su uno dei valori seguenti:  
  
1.  “None”  
  
2.  "AllExceptIntranet"  
  
3.  “All”  
  
 Quando l'impostazione IDN è impostata su "None", non viene effettuata alcuna conversione da Uri.Host o Uri.DnsSafeHost.  Quando l'impostazione IDN è impostata su "All", uri.Host rimane Unicode e uri.DnsSafeHost viene convertito in Punycode.  Quando l'impostazione IDN è impostata su "AllExceptIntranet", uri.DnsSafeHost viene convertito in Punycode per gli indirizzi Internet e rimane Unicode per gli indirizzi Intranet.  Questa impostazione è importante per una corretta risoluzione dei nomi DNS.  Si noti che questa impostazione non deve essere configurata per Windows 8 e versioni più recenti.  
  
> [!WARNING]
>  È consigliabile non impostare mai come hardcoded un indirizzo in cui viene usato Punycode.  WCF lo convertirà in base alle impostazioni di configurazione che vengano applicate.  
  
> [!WARNING]
>  Quando si aggiungono caratteri Unicode ad applicationHost.exe.config, salvare il file usando la codifica UTF\-8.  
  
## Vedere anche  
 [System.Uri](http://msdn.microsoft.com/library/system.uri.aspx)