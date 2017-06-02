---
title: "Accessing Custom Attributes | Microsoft Docs"
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
  - "custom attributes, accessibility"
  - "attributes [.NET Framework], accessing"
  - "reflection, custom attributes"
ms.assetid: 1d8e3398-00d8-47d5-a084-214f9859d3d7
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Accessing Custom Attributes
Dopo che gli attributi sono stati associati a elementi del programma, è possibile verificarne l'esistenza ed esaminarne il valore tramite reflection.  In .NET Framework versioni 1.0 e 1.1 gli attributi personalizzati vengono esaminati nel contesto di esecuzione.  In .NET Framework versione 2.0 è disponibile un nuovo contesto di caricamento, Reflection\-Only, che consente di esaminare il codice che non è possibile caricare per l'esecuzione.  
  
## Contesto Reflection\-Only  
 Il codice caricato nel contesto Reflection\-Only non può essere eseguito.  Non è pertanto possibile creare istanze di attributi personalizzati, operazione per cui è richiesta l'esecuzione dei costruttori.  Per caricare ed esaminare gli attributi personalizzati nel contesto Reflection\-Only, utilizzare la classe <xref:System.Reflection.CustomAttributeData>.  È possibile ottenere istanze di questa classe utilizzando l'overload appropriato del metodo statico <xref:System.Reflection.CustomAttributeData.GetCustomAttributes%2A?displayProperty=fullName>.  Per informazioni al riguardo, vedere [How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
## Contesto di esecuzione  
 I principali metodi di reflection per l'esecuzione di query sugli attributi nel contesto di esecuzione sono <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=fullName> e <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName>.  
  
 L'accessibilità di un attributo personalizzato viene controllata in riferimento all'assembly a cui l'attributo è collegato.  In altri termini, si verifica se un metodo di un tipo dell'assembly a cui è collegato l'attributo personalizzato può chiamare il costruttore dell'attributo personalizzato.  
  
 I metodi come <xref:System.Reflection.Assembly.GetCustomAttributes%28System.Boolean%29?displayProperty=fullName> consentono di controllare la visibilità e l'accessibilità dell'argomento di tipo.  È possibile recuperare un attributo personalizzato del tipo definito dall'utente tramite **GetCustomAttributes** solo nel codice dell'assembly che contiene tale tipo.  
  
 Nell'esempio in C\# riportato di seguito viene rappresentato un tipico modello di progettazione di attributi personalizzati.  Viene illustrato il modello di reflection degli attributi personalizzati adottato dal runtime.  
  
```  
System.DLL  
public class DescriptionAttribute : Attribute  
{  
}  
  
System.Web.DLL  
internal class MyDescriptionAttribute : DescriptionAttribute  
{  
}  
  
public class LocalizationExtenderProvider  
{  
    [MyDescriptionAttribute(...)]  
    public CultureInfo GetLanguage(...)  
    {  
    }  
}  
```  
  
 Se il runtime tenta di recuperare gli attributi personalizzati del tipo di attributo personalizzato pubblico <xref:System.ComponentModel.DescriptionAttribute> associato al metodo **GetLanguage**, effettua le seguenti operazioni:  
  
1.  Controlla che l'argomento di tipo **DescriptionAttribute** per **Type.GetCustomAttributes**\(Type *tipo*\) sia pubblico e quindi visibile e accessibile.  
  
2.  Controlla che il tipo definito dall'utente **MyDescriptionAttribute** derivato da **DescriptionAttribute** sia visibile e accessibile all'interno dell'assembly **System.Web.DLL**, in cui è collegato al metodo **GetLanguage**\(\).  
  
3.  Controlla che il costruttore di **MyDescriptionAttribute** sia visibile e accessibile all'interno dell'assembly **System.Web.DLL**.  
  
4.  Chiama il costruttore di **MyDescriptionAttribute** con i parametri dell'attributo personalizzato e restituisce il nuovo oggetto al chiamante.  
  
 Il modello di reflection degli attributi personalizzati può perdere istanze di tipi definiti dall'utente all'esterno dell'assembly in cui il tipo è definito.  Questo modello non differisce da quello in cui si inquadrano i membri della libreria di sistema del runtime, che restituiscono istanze di tipi definiti dall'utente, quali [Type.GetMethods\(\)](frlrfSystemTypeClassGetMethodsTopic), che restituisce una matrice di oggetti **RuntimeMethodInfo**.  Per impedire a un client di rilevare informazioni su un attributo personalizzato definito dall'utente, definire i membri del tipo come non pubblici.  
  
 Nell'esempio che segue viene illustrato il metodo principale per accedere agli attributi personalizzati tramite reflection.  
  
 [!code-cpp[CustomAttributeData#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CustomAttributeData/CPP/source2.cpp#2)]
 [!code-csharp[CustomAttributeData#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CustomAttributeData/CS/source2.cs#2)]
 [!code-vb[CustomAttributeData#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CustomAttributeData/VB/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A?displayProperty=fullName>   
 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName>   
 [Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)   
 [Security Considerations for Reflection](../../../docs/framework/reflection-and-codedom/security-considerations-for-reflection.md)