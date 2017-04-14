---
title: "Modifiche al runtime in .NET Framework 4.6 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5262bcfa-6e48-416b-8972-69cb4002d386
caps.latest.revision: 34
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Modifiche al runtime in .NET Framework 4.6
In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework, ma eseguite in una versione successiva del runtime di .NET Framework. Includono anche le differenze di comportamento tra le applicazioni eseguite in diversi ambienti di runtime di .NET Framework. Sono incluse le modifiche apportate nelle seguenti aree:  
  
-   [Base](#Core)  
  
-   [Servizi di rete](#Networking)  
  
-   [Windows Presentation Foundation \(WPF\)](#WPF)  
  
-   [Installazione e distribuzione](#Setup)  
  
-   [ClickOnce](#ClickOnce)  
  
-   [Nuovo compilatore JIT a 64 bit](#RyuJIT)  
  
<a name="Core"></a>   
## Base  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.Globalization.PersianCalendar?displayProperty=fullName>|A partire da [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], la classe <xref:System.Globalization.PersianCalendar> usa l'algoritmo solare Hijri.|L'algoritmo solare Hijri produce risultati identici a quelli del calendario persiano attualmente in uso in Iran e Afghanistan. Produce anche risultati identici all'algoritmo precedente per le date dal 1800 al 2023 del calendario gregoriano. Le date non incluse in questo intervallo possono essere interessate se la classe <xref:System.Globalization.PersianCalendar> viene usata per eseguire conversioni di data, ad esempio tra date del calendario gregoriano e date del calendario persiano, o per determinare se un anno specifico è bisestile.<br /><br /> A causa della modifica, il valore della proprietà <xref:System.Globalization.PersianCalendar.MinSupportedDateTime%2A?displayProperty=fullName> è cambiato da 21, 0622 a March 22, 0622 per i sistemi su cui è installato [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].<br /><br /> Per altre informazioni, vedere l'argomento <xref:System.Globalization.PersianCalendar>.|Secondario|  
|<xref:System.Runtime.Versioning.TargetFrameworkAttribute>|Per il dominio di applicazione predefinito, il valore della proprietà <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName> è derivato dal <xref:System.Runtime.Versioning.TargetFrameworkAttribute>, se presente, a meno che non sia definito in modo esplicito tramite l'assegnazione di un nome alla proprietà <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName>.  Nelle versioni precedenti di .NET Framework, il valore dell'attributo <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName> è `null` a meno che non venga eseguito un numero di percorsi di codice speciale o un dominio dell'applicazione non predefinita viene creato senza specificare in modo esplicito il framework di destinazione nella proprietà <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName>.<br /><br /> Per i domini dell'applicazione non predefiniti, non è presente alcuna modifica in modo che sia determinato il valore della proprietà <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName>. Se non viene assegnato alcun valore in modo esplicito alla proprietà <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName>, il dominio dell'applicazione non predefinito eredita il nome del framework di destinazione dal dominio dell'applicazione predefinito.|Per il dominio dell'applicazione predefinito, <xref:System.AppDomainSetup.TargetFrameworkName%2A?displayProperty=fullName> può restituire un valore non null quando in precedenza restituiva `null`. Questo è il comportamento auspicabile.|Marginale|  
|<xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString%28System.Boolean%29?displayProperty=fullName>|Se i certificati installati nel sistema non sono supportati da .NET Framework, passando il valore `True` per l'argomento `verbose` viene restituita una stringa valida. Nelle versioni precedenti di .NET Framework, il tentativo di accedere alle informazioni sulla chiave pubblica per i certificati non supportati in alcuni casi genera un'eccezione.|Questo metodo è esclusivamente informativo; le note della documentazione di prodotte potrebbero non essere coerenti in tutte le versioni di .NET Framework. Questa modifica interessa solo le app che chiamano il metodo `ToString(True)` e hanno installato i certificati che non sono supportati da .NET Framework. Restituendo una stringa invece di generare un'eccezione, questa modifica rende il metodo più affidabile.|Marginale|  
|Reflection e Distributed COM \(DCOM\)|Gli oggetti di reflection non possono essere più passati dal codice gestito ai client DCOM out\-of\-process. Sono interessati i tipi seguenti: <xref:System.Reflection.Assembly>; <xref:System.Reflection.MemberInfo> e i tipi derivati, tra cui <xref:System.Reflection.FieldInfo>, <xref:System.Reflection.MethodInfo>, <xref:System.Type> e <xref:System.Reflection.TypeInfo>; <xref:System.Reflection.MethodBody>; <xref:System.Reflection.Module> e <xref:System.Reflection.ParameterInfo>.|Chiamate a [IMarshal](http://msdn.microsoft.com/library/windows/desktop/dd542707.aspx) per l'oggetto restituiscono `E_NOINTERFACE`.|Secondario|  
  
<a name="Networking"></a>   
## Servizi di rete  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Valori di data e ora nella classe <xref:System.Net.Mime.ContentDisposition?displayProperty=fullName>.|Per essere conformi a [RFC822](http://www.ietf.org/rfc/rfc0822.txt) e [RFC2822](http://www.ietf.org/rfc/rfc2822.txt), il valore di una data e ora formattato adesso è caratterizzato da un'ora a due cifre. In precedenza, era caratterizzato da un'ora a una cifra per i valori prima delle 10.00.|Questa modifica influisce sui seguenti scenari di utilizzo:<br /><br /> -   Confronto tra le lunghezze o i codici hash degli oggetti <xref:System.Net.Mime.ContentDisposition> serializzati tra le versioni di .NET Framework.<br />-   Confronto tra il valore restituito del metodo <xref:System.Net.Mime.ContentDisposition.ToString%2A> o la rappresentazione di stringa dei valori delle proprietà data e ora <xref:System.Net.Mime.ContentDisposition> tra le versioni di .NET Framework.|Secondario|  
  
<a name="WPF"></a>   
## Windows Presentation Foundation \(WPF\)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Rendering di finestre in uno scenario di utilizzo di più monitor|Viene eseguito il rendering dell'intera finestra senza ritaglio quando la finestra si estende al di fuori di uno schermo in uno scenario di utilizzo di più monitor.|Vedere [Attenuazione: Rendering di finestre WPF](../../../docs/framework/migration-guide/mitigation-wpf-window-rendering.md).|Secondario|  
|Controllo ortografico nei controlli WPF abilitati per il testo|In Windows 10 il controllo ortografico potrebbe non funzionare poiché le funzionalità di controllo ortografico della piattaforma sono disponibili solo per le lingue presenti nell'elenco delle lingue di input.|In Windows 10, quando una lingua viene aggiunta all'elenco di tastiere disponibili, Windows scarica e installa automaticamente un pacchetto di funzionalità su richiesta corrispondente che fornisce funzionalità di controllo ortografico. Aggiungendo la lingua all'elenco di lingue di input, il controllo ortografico sarà supportato.|Secondario|  
  
<a name="Setup"></a>   
## Installazione e distribuzione  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Controllo delle versioni del prodotto|Il controllo delle versioni del prodotto è cambiato rispetto alle versioni precedenti di .NET Framework, in particolare .NET Framework 4, 4.5, 4.5.1 e 4.5.2. Per altre informazioni, vedere [Attenuazione: Controllo delle versioni del prodotto](../../../docs/framework/migration-guide/mitigation-product-versioning.md).|Vedere [Attenuazione: Controllo delle versioni del prodotto](../../../docs/framework/migration-guide/mitigation-product-versioning.md).|Medium|  
  
<a name="ClickOnce"></a>   
## ClickOnce  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|App pubblicate con ClickOnce che usano un certificato per la firma del codice SHA\-256.|Le app ClickOnce destinate alle versioni [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] o precedenti e firmati con un certificato SHA\-256 non hanno più una dipendenza di runtime in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] o versione successiva.|In precedenza, la firma di un'app ClickOnce destinata a [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] o alle versioni precedenti con un certificato SHA\-256 richiedeva la presenza di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] o una versione successiva sul sistema di destinazione. Ciò produceva errori nei casi in cui non era presente. Questa modifica rimuove tale dipendenza e consente di usare i certificati SHA\-256 per firmare le app ClickOnce destinate a [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] e versioni precedenti.|Secondario|  
  
<a name="RyuJIT"></a>   
## Nuovo compilatore JIT a 64 bit  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Gestione delle eccezioni \(restituzione da un'area `try`\)|A differenza del compilatore JIT precedente, JIT64, il nuovo compilatore JIT a 64 bit non consente un'istruzione IL [ret](http://msdn.microsoft.com/library/system.reflection.emit.opcodes.ret.aspx) in un'area `try`.|Restituzione da un'area `try` non è consentita dalla specifica ECMA\-335 e nessun compilatore gestito noto genera tale livello di integrità. Tuttavia, il compilatore JIT64 eseguirà tale livello di integrità se viene generato tramite reflection emit.|Marginale|