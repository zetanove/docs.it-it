---
title: "Reflection in the .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assemblies [.NET Framework], reflection"
  - "EventInfo class, reflection"
  - "common language runtime, reflection"
  - "FieldInfo class, reflection"
  - "ParameterInfo class, reflection"
  - "ConstructorInfo class, reflection"
  - "Assembly class, reflection"
  - "value types, reflection"
  - "reflection, about reflection"
  - "modules, reflection"
  - "runtime, reflection"
  - "Module class, reflection"
  - "MethodInfo class, reflection"
  - "PropertyInfo class, reflection"
  - "type browsers"
  - "reflection"
  - "discovering type information at run time"
  - "type system, reflection"
ms.assetid: d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Reflection in the .NET Framework
Le classi nello spazio dei nomi <xref:System.Reflection>, insieme a <xref:System.Type?displayProperty=fullName>, consentono di ottenere informazioni sugli [assembly](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md) caricati e sui tipi in essi definiti, ad esempio [classi](http://msdn.microsoft.com/it-it/ad7d3561-271e-4546-82fc-e00b059f27a9), [interfacce](http://msdn.microsoft.com/it-it/fd9d5975-5363-4bc9-b883-609f887895e5) e [tipi di valore](http://msdn.microsoft.com/it-it/c9c567f8-8ab1-4d88-834d-00f7d92418de).  È anche possibile usare la reflection per creare istanze di tipi in fase di esecuzione, richiamarle e accedervi.  Per argomenti su aspetti specifici della reflection, vedere [Argomenti correlati](#related_topics) al termine di questa panoramica.  
  
 Il caricatore di [Common Language Runtime](../../../docs/standard/clr.md) gestisce i [domini applicazione](../../../docs/framework/app-domains/application-domains.md), che costituiscono limiti definiti intorno a oggetti con lo stesso ambito di applicazione.  La gestione include il caricamento di ciascun assembly nel dominio applicazione appropriato e il controllo della disposizione in memoria della gerarchia dei tipi di ciascun assembly.  
  
 Gli [assembly](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md) contengono moduli, che contengono tipi, che a loro volta contengono membri.  La reflection fornisce oggetti che incapsulano assembly, moduli e tipi.  È possibile usare la reflection per creare in modo dinamico un'istanza di un tipo, associare il tipo a un oggetto esistente od ottenere il tipo da un oggetto esistente.  È quindi possibile richiamare i metodi del tipo o accedere ai relativi campi e proprietà.  Gli impieghi tipici della reflection includono:  
  
-   L'uso di <xref:System.Reflection.Assembly> per definire e caricare gli assembly, per caricare i moduli elencati nel manifesto dell'assembly e per individuare un tipo di tale assembly e crearne un'istanza.  
  
-   L'uso di <xref:System.Reflection.Module> per individuare informazioni riguardanti ad esempio l'assembly che contiene il modulo e le classi incluse nel modulo.  È anche possibile ottenere tutti i metodi globali o altri metodi specifici non globali definiti nel modulo.  
  
-   L'uso di <xref:System.Reflection.ConstructorInfo> per individuare informazioni quali il nome, i parametri, i modificatori di accesso \(ad esempio `public` o `private`\) e i dettagli di implementazione \(ad esempio `abstract` o `virtual`\) di un costruttore.  L'uso del metodo <xref:System.Type.GetConstructors%2A> o <xref:System.Type.GetConstructor%2A> di un oggetto <xref:System.Type> per richiamare un costruttore specifico.  
  
-   L'uso di <xref:System.Reflection.MethodInfo> per individuare informazioni quali il nome, il tipo restituito, i parametri, i modificatori di accesso \(ad esempio `public` o `private`\) e i dettagli di implementazione \(ad esempio `abstract` o `virtual`\) di un metodo.  L'uso del metodo <xref:System.Type.GetMethods%2A> o <xref:System.Type.GetMethod%2A> di un oggetto <xref:System.Type> per richiamare un metodo specifico.  
  
-   L'uso di <xref:System.Reflection.FieldInfo> per individuare informazioni quali il nome, i modificatori di accesso \(ad esempio `public` o `private`\) e i dettagli di implementazione \(ad esempio `static`\) di un campo, nonché per ottenere o impostare i valori dei campi.  
  
-   L'uso di <xref:System.Reflection.EventInfo> per individuare informazioni quali nome, tipo di dati del gestore eventi, attributi personalizzati, tipo dichiarante e tipo riflesso di un evento, nonché per aggiungere o rimuovere i gestori eventi.  
  
-   L'uso di <xref:System.Reflection.PropertyInfo> per ottenere informazioni quali nome, tipo di dati, tipo dichiarante, tipo riflesso e stato modificabile o di sola lettura di una proprietà nonché per ottenere o impostare i valori della proprietà.  
  
-   L'uso di <xref:System.Reflection.ParameterInfo> per ottenere informazioni quali nome di un parametro, tipo di dati, tipo di parametro \(se di input o di output\) e posizione del parametro in una firma di un metodo.  
  
-   L'uso di <xref:System.Reflection.CustomAttributeData> per individuare informazioni sugli attributi personalizzati in caso di uso del contesto Reflection\-Only di un dominio applicazione.  <xref:System.Reflection.CustomAttributeData> consente di esaminare gli attributi senza crearne istanze.  
  
 Le classi dello spazio dei nomi <xref:System.Reflection.Emit> forniscono un tipo specializzato di reflection che consente di compilare tipi in fase di esecuzione.  
  
 La reflection può essere usata anche per creare applicazioni definite visualizzatori di tipi, che consentono agli utenti di selezionare i tipi e visualizzarne quindi le relative informazioni.  
  
 Esistono anche altri impieghi per la reflection.  I compilatori di linguaggi come JScript usano la reflection per creare tabelle di simboli.  Le classi dello spazio dei nomi <xref:System.Runtime.Serialization> usano la reflection per accedere ai dati e determinare quali campi rendere persistenti.  Le classi dello spazio dei nomi <xref:System.Runtime.Remoting> usano la reflection in modo indiretto attraverso la serializzazione.  
  
## Tipi di runtime nella reflection  
 La reflection fornisce classi, ad esempio <xref:System.Type> e <xref:System.Reflection.MethodInfo>, per rappresentare tipi, membri, parametri e altre entità di codice.  Tuttavia, quando si usa la reflection non si opera direttamente su queste classi, la maggior parte delle quali è astratta \(`MustInherit` in Visual Basic\).  Si opera invece con tipi fornito da Common Language Runtime \(CLR\).  
  
 Ad esempio, quando si usa l'operatore `typeof` di C\# \(`GetType` in Visual Basic\) per ottenere un oggetto <xref:System.Type>, l'oggetto è in realtà un `RuntimeType`.  `RuntimeType` deriva da <xref:System.Type> e fornisce le implementazioni di tutti i metodi astratti.  
  
 Queste classi runtime sono `internal` \(`Friend` in Visual Basic\).  Non sono documentate separatamente rispetto alle relative classi base, poiché il loro comportamento è descritto nella documentazione della classe base.  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)|Viene illustrata la classe <xref:System.Type> e vengono forniti esempi di codice in cui viene descritto l'uso di <xref:System.Type> con diverse classi di reflection per ottenere informazioni su costruttori, metodi, campi, proprietà ed eventi.|  
|[Reflection and Generic Types](../../../docs/framework/reflection-and-codedom/reflection-and-generic-types.md)|Vengono illustrate le modalità con cui la reflection gestisce i parametri e gli argomenti di tipo di metodi e tipi generici.|  
|[Security Considerations for Reflection](../../../docs/framework/reflection-and-codedom/security-considerations-for-reflection.md)|Vengono illustrate le regole che determinano in che misura è possibile usare la reflection per recuperare informazioni sui tipi e accedere a essi.|  
|[Dynamically Loading and Using Types](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md)|Viene illustrata l'interfaccia di associazione personalizzata della reflection che supporta l'associazione tardiva.|  
|[How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|Viene descritto il contesto di caricamento Reflection\-Only.  Viene illustrato come caricare un assembly, verificare il contesto ed esaminare gli attributi applicati a un assembly nel contesto Reflection\-Only.|  
|[Accessing Custom Attributes](../../../docs/framework/reflection-and-codedom/accessing-custom-attributes.md)|Viene illustrato l'uso della reflection per ottenere informazioni sull'esistenza degli attributi e sui relativi valori.|  
|[Specifying Fully Qualified Type Names](../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)|Vengono illustrati il formato dei nomi di tipo completi, secondo i canoni BNF \(Backus\-Naur Form\), e la sintassi richiesta per specificare nomi di assembly, puntatori, riferimenti, matrici e caratteri speciali.|  
|[How to: Hook Up a Delegate Using Reflection](../../../docs/framework/reflection-and-codedom/how-to-hook-up-a-delegate-using-reflection.md)|Viene illustrato come creare un delegato per un metodo e associarlo a un evento.  Viene illustrato come creare un metodo di gestione degli eventi in fase di esecuzione usando <xref:System.Reflection.Emit.DynamicMethod>.|  
|[Emitting Dynamic Methods and Assemblies](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)|Viene illustrato come generare assembly e metodi generici.|  
  
## Riferimento  
 <xref:System.Type?displayProperty=fullName>  
  
 <xref:System.Reflection>  
  
 <xref:System.Reflection.Emit>  
  
 [Torna all'inizio](#top)