---
title: "Supporto per IRI (International Resource Identifier) in System.Uri | Microsoft Docs"
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
ms.assetid: b5e994c3-3535-4aff-8e1b-b69be22e9a22
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Supporto per IRI (International Resource Identifier) in System.Uri
La classe <xref:System.Uri?displayProperty=fullName> è stata estesa a l International Resource Identifier \(IRI\) e il supporto per mercati internazionali \(IDN\) di nomi di dominio.  Questi miglioramenti disponibili in.NET Framework 3.5, 3,0 SP1 e 2,0 SP1.  
  
## Supporto IDN e IRI  
 Gli indirizzi Web in genere vengono espressi tramite URI \(Uniform Resource Identifier \(URI\) costituiti da un set di caratteri molto limitata:  
  
-   Lettere ASCII maiuscole e minuscole dell'alfabeto inglese.  
  
-   Cifre comprese tra 0 e 9.  
  
-   Un numero limitato di altri simboli ASCII.  
  
 Le specifiche per gli identificatori URI sono documentate negli standard RFC 2396 e RFC 3986 pubblicati dall'IETF \(Internet Engineering Task Force\).  
  
 Con la crescita di Internet, è aumentata l'esigenza di identificare le risorse utilizzando lingue diverse dall'inglese.  Gli identificatori che soddisfano questa esigenza e consentono l'utilizzo di caratteri non ASCII, ad esempio caratteri del set di caratteri Unicode\/ISO 10646, sono noti come identificatori IRI \(International Resource Identifier\).  Le specifiche per gli identificatori IRI sono documentate nello standard RFC 3987 pubblicato dall'IETF.  L'utilizzo degli identificatori IRI consente l'inclusione di caratteri Unicode in un URL.  
  
 La classe esistente <xref:System.Uri?displayProperty=fullName> è stata estesa per fornire supporto IRI in base allo standard RFC 3987.  Gli utenti correnti non noteranno alcuna variazione rispetto al comportamento di .NET Framework 2.0 a meno che non attivino in modo specifico l'IRI.  In questo modo viene assicurata la compatibilità dell'applicazione con le versioni precedenti di .NET Framework.  
  
 Un'applicazione può specificare se utilizzare è mercati internazionali analizzare \(IDN\) di nome di dominio applicato ai nomi di dominio e se le regole di analisi IRI.  Questa operazione può essere effettuata nel file machine.config o app.config.  
  
 Se si attiva IDN, tutte le etichette Unicode in un nome di dominio verranno convertite negli equivalenti nomi Punycode,  I nomi Punycode contengono solo caratteri ASCII e vengono sempre avviati con il prefisso xn\-\-  allo scopo di supportare i server DNS esistenti su Internet, poiché la maggior parte dei server DNS supporta solo caratteri ASCII \(vedere RFC 3940\).  
  
 L'attivazione di IRI e IDN influisce sul valore della proprietà <xref:System.Uri.DnsSafeHost%2A?displayProperty=fullName>.  L'attivazione di IRI e IDN può inoltre modificare il comportamento dei metodi <xref:System.Uri.Equals%2A?displayProperty=fullName>, <xref:System.Uri.OriginalString%2A?displayProperty=fullName>, <xref:System.Uri.GetComponents%2A?displayProperty=fullName> e <xref:System.Uri.IsWellFormedOriginalString%2A>.  
  
 La classe <xref:System.GenericUriParser?displayProperty=fullName> è stata estesa anche per consentire la creazione di un parser personalizzabile che supporti IRI e IDN.  Il comportamento di un oggetto <xref:System.GenericUriParser?displayProperty=fullName> viene specificato passando una combinazione bit per bit dei valori disponibili nell'enumerazione <xref:System.GenericUriParserOptions?displayProperty=fullName> al costruttore <xref:System.GenericUriParser?displayProperty=fullName>.  Il tipo <xref:System.GenericUriParserOptions?displayProperty=fullName> indica che il parser supporta le regole di analisi indicate nella specifica RFC 3987 per gli identificatori IRI \(International Resource Identifier\).  Se IRI è effettivamente utilizzato dipende da IRI è abilitato.  
  
 Il tipo <xref:System.GenericUriParserOptions?displayProperty=fullName> indica che il parser supporta l'analisi IDN \(Internationalized Domain Name\) dei nomi host.  Se l'oggetto specifico viene effettivamente utilizzato a seconda che specifico è abilitato.  
  
 Abilitare l'analisi IRI eseguirà la normalizzazione e il controllo dei caratteri in base alle regole IRI nello standard RFC 3987.  Il valore predefinito è per IRI che analizza per essere disabilitato in modo dalla normalizzazione e il controllo dei caratteri vengono effettuate secondo RFC 2396 e RFC 3986.  
  
 L'elaborazione IDN e IRI nella classe <xref:System.Uri?displayProperty=fullName> può essere controllata mediante le classi dell'impostazione di configurazione <xref:System.Configuration.IdnElement?displayProperty=fullName> e <xref:System.Configuration.IriParsingElement?displayProperty=fullName>.  L'impostazione <xref:System.Configuration.IriParsingElement?displayProperty=fullName> attiva o disabilita l'elaborazione IRI nella classe <xref:System.Uri?displayProperty=fullName>.  L'impostazione <xref:System.Configuration.IdnElement?displayProperty=fullName> attiva o disabilita l'elaborazione IDN nella classe <xref:System.Uri>.  L'impostazione <xref:System.Configuration.IriParsingElement?displayProperty=fullName> inoltre controlla indirettamente IDN.  Per consentire l'elaborazione IDN, è necessario attivare l'elaborazione IRI.  Se l'elaborazione IRI è disabilitata, l'elaborazione IDN verrà configurata sull'impostazione predefinita dove per la compatibilità viene utilizzato il comportamento di .NET Framework 2.0 e non vengono utilizzati nomi IDN.  
  
 L'impostazione di configurazione per le classi di configurazione <xref:System.Configuration.IdnElement?displayProperty=fullName> e <xref:System.Configuration.IriParsingElement?displayProperty=fullName> verrà letta una volta alla prima classe <xref:System.Uri?displayProperty=fullName> viene costruita.  Le successive modifiche alle impostazioni di configurazione verranno ignorate.  
  
## Vedere anche  
 <xref:System.Configuration.IdnElement?displayProperty=fullName>   
 <xref:System.Configuration.IriParsingElement?displayProperty=fullName>   
 <xref:System.Uri?displayProperty=fullName>   
 <xref:System.Uri.DnsSafeHost%2A?displayProperty=fullName>