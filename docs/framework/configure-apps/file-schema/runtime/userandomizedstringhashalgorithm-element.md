---
title: "Elemento &lt;UseRandomizedStringHashAlgorithm&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<UseRandomizedStringHashAlgorithm> (elemento)"
  - "UseRandomizedStringHashAlgorithm (elemento)"
ms.assetid: c08125d6-56cc-4b23-b482-813ff85dc630
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Elemento &lt;UseRandomizedStringHashAlgorithm&gt;
Specifica se Common Language Runtime calcola i codici hash per le stringhe in base al dominio dell'applicazione.  
  
## Sintassi  
  
```  
<UseRandomizedStringHashAlgorithm   
   enabled=0|1 />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se i codici hash per le stringhe sono calcolati in base al dominio dell'applicazione.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`0`|Common Language Runtime non calcola i codici hash per le stringhe in base al dominio dell'applicazione; viene utilizzato un singolo algoritmo per calcolare i codici hash della stringa.  Impostazione predefinita.|  
|`1`|Common Language Runtime esegue il calcolo dei codici hash per le stringhe in base al dominio dell'applicazione.  Le stringhe identiche in domini applicazione diversi e in processi diversi disporranno di codici hash differenti.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 Per impostazione predefinita, la classe <xref:System.StringComparer> e il metodo <xref:System.String.GetHashCode%2A?displayProperty=fullName> utilizzano un singolo algoritmo di hash che produce un codice hash coerente tra i domini applicazione.  Questo equivale a impostare l'attributo `enabled` dell'elemento `<UseRandomizedStringHashAlgorithm>` su `0`.  Algoritmo di hash utilizzato in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)].  
  
 La classe <xref:System.StringComparer> e il metodo <xref:System.String.GetHashCode%2A?displayProperty=fullName> possono inoltre utilizzare un algoritmo di hash diverso che calcola i codici hash in base al dominio applicazione.  Di conseguenza, i codici hash per le stringhe equivalenti risulteranno diversi tra i domini applicazione.  Si tratta di una funzionalità su scelta esplicita; per approfittarne, è necessario impostare l'attributo `enabled` dell'elemento `<UseRandomizedStringHashAlgorithm>` su `1`.  
  
 La ricerca di stringhe in una tabella hash in genere rappresenta un'operazione O\(1\).  Tuttavia, quando si verificano numerosi conflitti, la ricerca può diventare un'operazione O\(n<sup>2</sup>\).  È possibile utilizzare l'elemento di configurazione `<UseRandomizedStringHashAlgorithm>` per generare un algoritmo di hash casuale per dominio applicazione, che a sua volta limita il numero di conflitti potenziali, in particolare quando le chiavi da cui i codici hash vengono calcolati sono basate su immissione dei dati dagli utenti.  
  
## Esempio  
 Nell'esempio seguente viene definita una classe `DisplayString` che include una costante di stringa privata, `s`, il cui valore è "Questa è una stringa." Viene inoltre incluso un metodo `ShowStringHashCode` tramite cui vengono visualizzati il valore stringa e il codice hash con il nome del dominio applicazione in cui il metodo è in esecuzione.  
  
 [!code-csharp[System.String.GetHashCode#2](../../../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.String.GetHashCode/CS/perdomain.cs#2)]
 [!code-vb[System.String.GetHashCode#2](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.String.GetHashCode/VB/perdomain.vb#2)]  
  
 Quando si esegue l'esempio senza fornire un file di configurazione, restituisce un output analogo al seguente.  Si noti che i codici hash per la stringa sono identici nei due domini applicazione.  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 941BCEAC  
String 'This is a string.' in domain 'NewDomain': 941BCEAC  
  
```  
  
 Tuttavia, se si aggiunge il file di configurazione seguente alla directory di esempio e, successivamente, si esegue l'esempio, i codici hash per la stessa stringa risulteranno diversi dal dominio dell'applicazione.  
  
```  
  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <UseRandomizedStringHashAlgorithm enabled="1" />  
   </runtime>  
</configuration>  
  
```  
  
 Quando il file di configurazione è presente, l'esempio visualizza il seguente output:  
  
```  
  
String 'This is a string.' in domain 'PerDomain.exe': 5435776D  
String 'This is a string.' in domain 'NewDomain': 75CC8236  
  
```  
  
## Vedere anche  
 <xref:System.StringComparer.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.String.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.Object.GetHashCode%2A?displayProperty=fullName>