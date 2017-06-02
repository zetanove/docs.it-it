---
title: "Gerarchia delle eccezioni | Microsoft Docs"
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
  - "eccezioni, tipi"
  - "fase di esecuzione, le eccezioni"
  - "eccezioni di base"
  - "ApplicationException (classe)"
  - "eccezioni Common language runtime"
  - "Interoperabilità COM, eccezioni"
  - "eccezioni, le gerarchie"
ms.assetid: f7d68675-be06-40fb-a555-05f0c5a6f66b
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# Gerarchia delle eccezioni
Esistono due tipi di eccezioni: eccezioni generate da un programma in esecuzione ed eccezioni generate dal motore Common Language Runtime. Esiste inoltre una gerarchia di eccezioni che possono essere generate da un'applicazione o dal runtime.  
  
 Il <xref:System.Exception?displayProperty=fullName> classe è la classe base per le eccezioni. Varie classi di eccezione ereditano direttamente da <xref:System.Exception>, tra cui <xref:System.ApplicationException> e <xref:System.SystemException>. Queste due classi costituiscono la base per quasi tutte le eccezioni di runtime.  
  
 La maggior parte delle eccezioni che derivano da <xref:System.Exception> aggiungervi alcuna funzionalità e non i nuovi membri. Ad esempio, il <xref:System.InvalidCastException> gerarchia di classi sia come indicato di seguito:  
  
 <xref:System.Object> <xref:System.Exception> <xref:System.SystemException> <xref:System.InvalidCastException>  
  
 Il runtime viene generato nella classe derivata appropriata di <xref:System.SystemException> quando si verificano errori. Questi errori derivano da controlli di runtime non riusciti, ad esempio errori di matrice fuori dal limite, e possono verificarsi durante l'esecuzione di qualsiasi metodo. Se si progetta un'applicazione che crea nuove eccezioni, è necessario derivare tali eccezioni dal <xref:System.Exception> (classe). Non è consigliabile intercettare un <xref:System.SystemException>, non è buona norma di programmazione per generare un <xref:System.SystemException> nell'applicazione.  
  
 Le eccezioni più gravi, ovvero quelle generate dal runtime o nelle condizioni di errore, includere <xref:System.ExecutionEngineException>, <xref:System.StackOverflowException>, e <xref:System.OutOfMemoryException>.  
  
 Le eccezioni di interoperabilità derivano da <xref:System.SystemException> e sono ulteriormente estese da <xref:System.Runtime.InteropServices.ExternalException>. Ad esempio, <xref:System.Runtime.InteropServices.COMException> è l'eccezione generata durante le operazioni di interoperabilità COM e deriva da <xref:System.Runtime.InteropServices.ExternalException>. <xref:System.ComponentModel.Win32Exception> e <xref:System.Runtime.InteropServices.SEHException> anche derivare da <xref:System.Runtime.InteropServices.ExternalException>.  
  
## <a name="hierarchy-of-runtime-exceptions"></a>Gerarchia delle eccezioni del runtime  
 Il runtime dispone di un set di base di eccezioni derivate da <xref:System.SystemException> che viene generato all'esecuzione di singole istruzioni. Nella tabella seguente sono elencate in ordine gerarchico le eccezioni standard fornite dal runtime e le condizioni nelle quali è necessario creare una classe derivata.  
  
|Tipo di eccezione|Tipo base|Descrizione|Esempio|  
|--------------------|---------------|-----------------|-------------|  
|[(Eccezione)](../../../docs/standard/exceptions/exception-class-and-properties.md)|<xref:System.Object>|Classe base per tutte le eccezioni.|Nessuno (usare una classe derivata di questa eccezione).|  
|<xref:System.SystemException>|<xref:System.Exception>|Classe base per tutti gli errori generati dal runtime.|Nessuno (usare una classe derivata di questa eccezione).|  
|<xref:System.IndexOutOfRangeException>|<xref:System.SystemException>|Generata dal runtime solo quando una matrice viene indicizzata in modo non corretto.|Indicizzazione di una matrice esternamente al relativo intervallo valido:<br /><br /> `var i = arr[arr.Length + 1];`<br /><br /> `Dim i = arr(arr.Length + 1)`|  
|<xref:System.NullReferenceException>|<xref:System.SystemException>|Generata dal runtime solo quando viene fatto riferimento a un oggetto Null.|`object o = null; string s = o.ToString();`<br /><br /> `Dim o As Object = Nothing Dim s As String = o.ToString()`|  
|<xref:System.AccessViolationException>|<xref:System.SystemException>|Generata dal runtime solo quando si accede alla memoria non valida.|Si verifica quando si usa l'interoperabilità con codice non gestito o codice gestito non sicuro e un puntatore non valido.|  
|<xref:System.InvalidOperationException>|<xref:System.SystemException>|Generata dai metodi con uno stato non valido.|La chiamata dell'enumeratore `GetNext` metodo dopo la rimozione di un elemento dalla raccolta sottostante.|  
|<xref:System.ArgumentException>|<xref:System.SystemException>|Classe base per tutte le eccezioni di argomento.|Nessuno (usare una classe derivata di questa eccezione).|  
|<xref:System.ArgumentNullException>|<xref:System.ArgumentException>|Generata dai metodi che non consentono un argomento Null.|`String s = null; int i = "Calculate".IndexOf(s);`<br /><br /> `Dim s As String = Nothing Dim i As Integer = "Calculate".IndexOf(s)`|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.ArgumentException>|Generata dai metodi che verificano se gli argomenti sono compresi in un determinato intervallo.|`String s = "string"; s = s.Substring(s.Length + 1);`<br /><br /> `Dim s As String = "string" s = s.Substring(s.Length + 1)`|  
|<xref:System.Runtime.InteropServices.ExternalException>|<xref:System.SystemException>|Classe base per le eccezioni che si verificano in o sono destinate ad ambienti esterni al runtime.|Nessuno (usare una classe derivata di questa eccezione).|  
|<xref:System.Runtime.InteropServices.COMException>|<xref:System.Runtime.InteropServices.ExternalException>|Eccezione durante l'incapsulamento delle informazioni COM HRESULT.|Usata nell'interoperabilità COM.|  
|<xref:System.Runtime.InteropServices.SEHException>|<xref:System.Runtime.InteropServices.ExternalException>|Eccezione durante l'incapsulamento delle informazioni sulla gestione delle eccezioni strutturate Win32.|Usata nell'interoperabilità del codice non gestito.|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe di eccezione e proprietà](../../../docs/standard/exceptions/exception-class-and-properties.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [Procedure consigliate per le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Eccezioni](../../../docs/standard/exceptions/index.md)