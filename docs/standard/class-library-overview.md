---
title: "Cenni preliminari sulla libreria di classi .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "libreria di classi .NET Framework, informazioni"
  - ".NET Framework, libreria di classi"
  - "tipi di base, libreria di classi"
  - "tipi incorporati"
  - "libreria di classi [.NET Framework]"
  - "tipo di valori degli oggetti classe"
  - "classi [.NET Framework], cenni preliminari sulla libreria"
  - "CLS (Common Language Specification)"
  - "Common Language Specification"
  - "tipi di dati [.NET Framework]"
  - "tipi di dati [.NET Framework], C#"
  - "tipi di dati [.NET Framework], C++"
  - "tipi di dati [.NET Framework], JScript"
  - "tipi di dati [.NET Framework], Visual Basic"
  - "tipo di valore a virgola mobile"
  - "tipo di valore Integer"
  - "JScript, tipi di dati"
  - "librerie, libreria di classi .NET Framework"
  - "tipo di valore logico"
  - "membri [.NET Framework], tipo"
  - "spazi dei nomi [.NET Framework]"
  - "spazi dei nomi [.NET Framework], informazioni sugli spazi dei nomi"
  - "convenzioni di denominazione [.NET Framework]"
  - "spazio dei nomi di sistema"
  - "type system [.NET Framework]"
  - "tipi, .NET Framework"
  - "tipi definiti dall'utente"
  - "tipi di valori"
  - "Visual Basic, tipi di dati"
  - "Visual C#, tipi di dati"
  - "Visual C++, tipi di dati"
ms.assetid: 7e4c5921-955d-4b06-8709-101873acf157
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Cenni preliminari sulla libreria di classi .NET Framework
[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] include classi, interfacce e tipi di valore che consentono di ottimizzare il processo di sviluppo rendendolo più rapido e che forniscono accesso alle funzionalità di sistema.  Per facilitare l'interoperabilità tra i linguaggi, la maggior parte dei tipi .NET Framework è compatibile con la specifica CLS \(Common Language Specification\) e può pertanto essere utilizzata da qualsiasi linguaggio di programmazione dotato di compilatore conforme a tale specifica.  
  
 I tipi di .NET Framework rappresentano gli elementi fondamentali per la compilazione di applicazioni, componenti e controlli .NET.  In [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] sono inclusi tipi che consentono di eseguire le funzioni seguenti:  
  
-   Rappresentare tipi di dati ed eccezioni di base.  
  
-   Incapsulare strutture di dati.  
  
-   Eseguire I\/O.  
  
-   Accedere a informazioni su tipi caricati.  
  
-   Richiamare i controlli di sicurezza di .NET Framework.  
  
-   Offrire l'accesso ai dati, un'elaborata interfaccia GUI \(Graphical User Interface, interfaccia grafica utente\) per il lato client e una GUI per il lato client controllata dal server.  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] offre una vasta gamma di interfacce, nonché di classi astratte e concrete \(non astratte\).  È possibile utilizzare le classi concrete così come sono oppure, in molti casi, derivare da esse classi personalizzate.  Per avvalersi delle funzionalità di un'interfaccia è possibile creare, oppure derivare da una delle classi di .NET Framework, una classe che consenta di implementare l'interfaccia.  
  
## Convenzioni di denominazione  
 Nei tipi di .NET Framework è utilizzato uno schema di denominazione con sintassi a punti che definisce una gerarchia.  Secondo questa tecnica i tipi correlati vengono raggruppati in spazi dei nomi, in modo da semplificarne le ricerche e i riferimenti.  La prima parte del nome completo, fino al primo punto da destra, è il nome dello spazio dei nomi.  L'ultima parte del nome è il nome del tipo.  **System.Collections.ArrayList**, ad esempio, rappresenta il tipo **ArrayList**, appartenente allo spazio dei nomi **System.Collections**.  I tipi di **System.Collections** possono essere utilizzati per manipolare raccolte di oggetti.  
  
 Questo schema di denominazione è vantaggioso per gli sviluppatori di librerie che desiderano estendere [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] poiché consente di creare gruppi gerarchici di tipi e denominarli in modo coerente utilizzando nomi di immediata comprensione.  Consente inoltre l'identificazione non ambigua dei tipi mediante il relativo nome completo, ovvero mediante il relativo spazio dei nomi e nome di tipo, in modo da evitare conflitti tra i nomi di tipo.  Nella denominazione degli spazi dei nomi è opportuno che gli sviluppatori di librerie rispettino la seguente convenzione:  
  
 *NomeSocietà*.*NomeTecnologia*  
  
 Lo spazio dei nomi Microsoft.Word, ad esempio, è conforme a questa convenzione.  
  
 Il ricorso a schemi di denominazione per raggruppare dei tipi correlati all'intero di spazi dei nomi è un metodo estremamente utile per compilare e documentare librerie di classi.  Questo schema di denominazione non ha tuttavia alcun effetto sulla visibilità, sull'accesso ai membri, sull'ereditarietà, sulla sicurezza o sull'associazione.  Gli spazi dei nomi possono essere ripartiti tra più assembly e un singolo assembly può contenere tipi provenienti da spazi dei nomi differenti.  L'assembly fornisce la struttura formale per la creazione di versioni successive, la distribuzione, la sicurezza, il caricamento e la visibilità in Common Language Runtime.  
  
 Per ulteriori informazioni sugli spazi dei nomi e sui nomi dei tipi, vedere [Sistema di tipi comuni](../../docs/standard/base-types/common-type-system.md).  
  
## Spazio dei nomi System  
 Lo spazio dei nomi <xref:System> è lo spazio dei nomi di primo livello per i tipi fondamentali di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  Questo spazio dei nomi include classi che rappresentano i tipi di dati di base utilizzati da tutte le applicazioni: <xref:System.Object> \(il primo livello della gerarchia di ereditarietà\), <xref:System.Byte>, <xref:System.Char>, <xref:System.Array>, <xref:System.Int32>, <xref:System.String> e così via.  Molti di questi tipi corrispondono ai tipi di dati primitivi utilizzati dal linguaggio di programmazione.  Quando si scrive il codice utilizzando tipi di .NET Framework è possibile utilizzare la corrispondente parola chiave del linguaggio utilizzato dove è previsto un tipo di dati di base di .NET Framework.  
  
 Nella tabella riportata di seguito sono elencati i tipi di base disponibili in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] con una breve descrizione di ciascun tipo e viene inoltre indicato il tipo corrispondente in Visual Basic, C\#, C\+\+ e JScript.  
  
|Categoria|Nome di classe|Descrizione|Tipo di dati di Visual Basic|Tipo di dati di C\#|Tipo di dati C\+\+|Tipo di dati di JScript|  
|---------------|--------------------|-----------------|----------------------------------|-------------------------|------------------------|-----------------------------|  
|Integer|<xref:System.Byte>|Intero senza segno a 8 bit.|**Byte**|**byte**|**unsigned char**|**Byte**|  
||<xref:System.SByte>|Intero con segno a 8 bit.<br /><br /> Non conforme a CLS.|**SByte**|**sbyte**|**char**<br /><br /> \-o\-<br /><br /> **signed** **char**|**SByte**|  
||<xref:System.Int16>|Intero con segno a 16 bit.|**Short**|**short**|**short**|**short**|  
||<xref:System.Int32>|Intero con segno a 32 bit.|**Integer**|**int**|**int**<br /><br /> \-o\-<br /><br /> **long**|**int**|  
||<xref:System.Int64>|Signed Integer a 64 bit.|**Long**|**long**|**\_\_int64**|**long**|  
||<xref:System.UInt16>|Intero senza segno a 16 bit.<br /><br /> Non conforme a CLS.|**UShort**|**ushort**|**unsigned short**|**UInt16**|  
||<xref:System.UInt32>|Intero senza segno a 32 bit.<br /><br /> Non conforme a CLS.|**UInteger**|**uint**|**unsigned int**<br /><br /> \-oppure\-<br /><br /> **unsigned long**|**UInt32**|  
||<xref:System.UInt64>|Intero senza segno a 64 bit.<br /><br /> Non conforme a CLS.|**ULong**|**ulong**|**unsigned \_\_int64**|**UInt64**|  
|A virgola mobile|<xref:System.Single>|Un numero a virgola mobile e precisione singola a 32 bit.|**Single**|**float**|**float**|**float**|  
||<xref:System.Double>|Un numero a virgola mobile e precisione doppia a 64 bit.|**Double**|**double**|**double**|**double**|  
|Logica|<xref:System.Boolean>|Un valore Boolean \(true o false\).|**Boolean**|**bool**|**bool**|**bool**|  
|Altro|<xref:System.Char>|Un carattere Unicode a 16 bit.|**Char**|**char**|**wchar\_t**|**char**|  
||<xref:System.Decimal>|Un valore decimale a 128 bit.|**Decimal**|**decimal**|**Decimal**|**Decimal**|  
||<xref:System.IntPtr>|Un intero con segno la cui dimensione dipende dalla piattaforma sottostante \(un valore a 32 bit su una piattaforma a 32 bit e un valore a 64 bit su una piattaforma a 64 bit\).|**IntPtr**<br /><br /> Nessun tipo incorporato.|**IntPtr**<br /><br /> Nessun tipo incorporato.|**IntPtr**<br /><br /> Nessun tipo incorporato.|**IntPtr**|  
||<xref:System.UIntPtr>|Un intero senza segno la cui dimensione dipende dalla piattaforma sottostante \(un valore a 32 bit su una piattaforma a 32 bit e un valore a 64 bit su una piattaforma a 64 bit\).<br /><br /> Non conforme a CLS.|**UIntPtr**<br /><br /> Nessun tipo incorporato.|**UIntPtr**<br /><br /> Nessun tipo incorporato.|**UIntPtr**<br /><br /> Nessun tipo incorporato.|**UIntPtr**|  
|Oggetti Class|<xref:System.Object>|Il primo livello della gerarchia di oggetti.|**Object**|**object**|**Object\***|**Object**|  
||<xref:System.String>|Una stringa di caratteri Unicode immutabile e a lunghezza fissa.|**String**|**string**|**String\***|**String**|  
  
 Oltre ai tipi di dati di base, lo spazio dei nomi <xref:System> contiene oltre 100 classi, da quelle che gestiscono le eccezioni a quelle correlate a concetti fondamentali della fase di esecuzione, quali i domini di applicazione e Garbage Collector.  Lo spazio dei nomi <xref:System> contiene inoltre numerosi spazi dei nomi di secondo livello..  
  
 Per ulteriori informazioni sugli spazi dei nomi, sfogliare la [libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkID=227195).  Nella documentazione di riferimento viene fornita una breve panoramica di ciascuno spazio dei nomi nonché una descrizione formale di ogni tipo e dei relativi membri.  
  
## Vedere anche  
 [Common Type System](../../docs/standard/base-types/common-type-system.md)   
 [Libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkID=227195)   
 [Panoramica](../../docs/framework/get-started/overview.md)