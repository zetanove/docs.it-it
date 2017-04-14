---
title: "Principal and Identity Objects | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "WindowsIdentity objects"
  - "GenericIdentity objects"
  - "GenericPrincipal objects"
  - "identity objects, about identity objects"
  - "security [.NET Framework], identity objects"
  - "principal objects, about principal objects"
  - "security [.NET Framework], principals"
  - "WindowsPrincipal objects"
ms.assetid: aa5930ad-f3d7-40aa-b6f6-c6edcd5c64f7
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Principal and Identity Objects
Il codice gestito è in grado di appurare l'identità o il ruolo di un principale tramite un oggetto [Principal](frlrfSystemSecurityPrincipalIPrincipalClassTopic), che contiene un riferimento a un oggetto [Identity](frlrfSystemSecurityPrincipalIIdentityClassTopic).  Può essere utile paragonare oggetti Identity e Principal a concetti familiari quali account utente e di gruppo.  Nella maggior parte degli ambienti di rete, gli account utente rappresentano utenti o programmi, mentre gli account di gruppo rappresentano determinate categorie di utenti e i diritti che essi detengono.  Analogamente, gli oggetti Identity di .NET Framework rappresentano utenti, mentre i ruoli rappresentano appartenenze e contesti di sicurezza.  In .NET Framework l'oggetto Principal incapsula sia un oggetto Identity che un ruolo. Le applicazioni di .NET Framework concedono diritti al principale sulla base dell'identità che esso presenta oppure, più comunemente, al ruolo che esso riveste.  
  
## Oggetti Identity  
 L'oggetto Identity incapsula informazioni sull'utente o sull'entità da convalidare.  Nella forma più semplice, gli oggetti Identity contengono un nome e un tipo di autenticazione.  Il nome può essere quello di un utente o di un account Windows, mentre il tipo di autenticazione può corrispondere a un protocollo di accesso supportato, quale Kerberos V5, oppure a un valore personalizzato.  In .NET Framework viene definito un oggetto <xref:System.Security.Principal.GenericIdentity> utilizzabile per la maggior parte degli scenari di accesso personalizzato e un oggetto <xref:System.Security.Principal.WindowsIdentity> più specializzato utilizzabile quando si desidera che l'applicazione si basi sull'autenticazione di Windows.  È inoltre possibile definire una classe di identità personalizzata che contenga informazioni utente personalizzate.  
  
 L'interfaccia <xref:System.Security.Principal.IIdentity> definisce proprietà per l'accesso a un nome e a un tipo di autenticazione. Ad esempio, Kerberos V5 o NTLM.  Tutte le classi **Identity** implementano l'interfaccia **IIdentity**.  Non è necessaria alcuna relazione tra un oggetto **Identity** e il token di processo di Windows NT sotto cui un thread è in esecuzione.  Se tuttavia l'oggetto **Identity** è un oggetto **WindowsIdentity**, si presupporrà che l'identità rappresenti un token di sicurezza di Windows NT.  
  
## Oggetti Principal  
 L'oggetto Principal rappresenta il contesto di sicurezza in cui viene eseguito il codice.  Le applicazioni che implementano la sicurezza basata sui ruoli concedono diritti sulla base del ruolo associato all'oggetto Principal.  Analogamente agli oggetti Identity, in .NET Framework viene fornito un oggetto <xref:System.Security.Principal.GenericPrincipal> e un oggetto <xref:System.Security.Principal.WindowsPrincipal>.  È inoltre possibile definire classi di principali personalizzate.  
  
 L'interfaccia <xref:System.Security.Principal.IPrincipal> definisce una proprietà che consente di accedere a un oggetto **Identity** associato nonché un metodo che consente di determinare se l'utente identificato dall'oggetto **Principal** è membro di un determinato ruolo.  Tutte le classi **Principal** implementano l'interfaccia **IPrincipal** nonché ulteriori proprietà e metodi eventualmente necessari.  Common Language Runtime fornisce ad esempio la classe **WindowsPrincipal**, che implementa funzionalità aggiuntive per il mapping tra l'appartenenza a un gruppo di Windows NT o Windows 2000 e i ruoli.  
  
 Un oggetto **Principal** è legato a un oggetto <xref:System.Runtime.Remoting.Messaging.CallContext> che rappresenta il contesto di chiamata all'interno di un dominio dell'applicazione <xref:System.AppDomain>.  Viene sempre creato un contesto di chiamata predefinito con ciascun nuovo **AppDomain**, così esiste sempre un contesto di chiamata disponibile per accettare l'oggetto **Principal**.  Quando viene creato un nuovo thread, per tale thread viene creato anche un oggetto **CallContext**.  Il riferimento all'oggetto **Principal** viene automaticamente copiato dal thread di origine al **CallContext** del nuovo thread.  Se il runtime non è in grado di determinare quale oggetto **Principal** appartiene al creatore del thread, si atterrà ai criteri predefiniti per la creazione di oggetti **Principal** e **Identity**.  
  
 Dei criteri configurabili specifici di un dominio applicazione definiscono le regole in base alle quali decidere quale tipo di oggetto **Principal** associare a un nuovo dominio applicazione.  Dove consentito dai criteri di sicurezza, il runtime può creare oggetti **Principal** e **Identity** che riflettono il token del sistema operativo associato al thread di esecuzione corrente.  In base all'impostazione predefinita, il runtime utilizza oggetti **Principal** e **Identity** che rappresentano utenti non autenticati.  Il runtime non crea questi oggetti **Principal** e **Identity** predefiniti finché il codice non tenta di accedervi.  
  
 Il codice attendibile che crea un dominio applicazione può impostare i criteri di sicurezza del dominio applicazione che controllano la costruzione degli oggetti **Principal** e **Identity** predefiniti.  Questi criteri specifici del dominio applicazione si applicano a tutti i thread di esecuzione di tale dominio applicazione.  Un host attendibile non gestito ha implicitamente la capacità di impostare questi criteri, mentre è necessario che il codice gestito che imposta tali criteri disponga dell'autorizzazione <xref:System.Security.Permissions.SecurityPermission?displayProperty=fullName> per il controllo dei criteri di dominio.  
  
 Quando si trasmette un oggetto **Principal** tra più domini applicazione, ma all'interno dello stesso processo e quindi sullo stesso computer, l'infrastruttura remota consente di copiare nel contesto del chiamato un riferimento all'oggetto **Principal** associato al contesto del chiamante.  
  
## Vedere anche  
 [How to: Create a WindowsPrincipal Object](../../../docs/standard/security/how-to-create-a-windowsprincipal-object.md)   
 [How to: Create GenericPrincipal and GenericIdentity Objects](../../../docs/standard/security/how-to-create-genericprincipal-and-genericidentity-objects.md)   
 [Replacing a Principal Object](../../../docs/standard/security/replacing-a-principal-object.md)   
 [Impersonating and Reverting](../../../docs/standard/security/impersonating-and-reverting.md)   
 [Role\-Based Security](../../../docs/standard/security/role-based-security.md)   
 [Key Security Concepts](../../../docs/standard/security/key-security-concepts.md)