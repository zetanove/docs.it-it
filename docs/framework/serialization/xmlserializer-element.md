---
title: "Elemento &lt;xmlSerializer&gt; | Microsoft Docs"
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
helpviewer_keywords: 
  - "Elemento <xmlSerializer>"
  - "serializzazione XML, configurazione"
  - "Elemento xmlSerializer"
ms.assetid: d129d10c-3eb7-45d9-8098-5fa853825e47
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Elemento &lt;xmlSerializer&gt;
Specifica se effettuare un controllo aggiuntivo dello stato di avanzamento di <xref:System.Xml.Serialization.XmlSerializer>.  
  
## Sintassi  
  
```  
  
<xmlSerializer checkDeserializerAdvance = "true"|"false" />  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**checkDeserializeAdvances**|Specifica se controllare lo stato di avanzamento di <xref:System.Xml.Serialization.XmlSerializer>.  Impostare l'attributo su "true" o "false".  Il valore predefinito è "true".|  
|**useLegacySerializationGeneration**|Specifica se <xref:System.Xml.Serialization.XmlSerializer> usa la generazione legacy di serializzazione che genera assembly scrivendo un codice C\# in un file e quindi compilandola in un assembly.  Il valore predefinito è **false**.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)|Contiene le impostazioni di configurazione per le classi <xref:System.Xml.Serialization.XmlSerializer> e <xref:System.Xml.Serialization.XmlSchemaImporter>.|  
  
## Note  
 Per impostazione predefinita, <xref:System.Xml.Serialization.XmlSerializer> fornisce un livello aggiuntivo di sicurezza contro potenziali attacchi di tipo Denial of Service durante la deserializzazione di dati non attendibili.  Per ottenere questo risultato, tenta di rilevare cicli infiniti durante la deserializzazione.  Se si verifica tale condizione, viene generata un'eccezione con un messaggio che comunica che a causa di un errore interno, la deserializzazione non è in grado di procedere su un flusso sottostante.  
  
 Se si riceve questo messaggio, non significa che è necessariamente in corso un attacco di tipo Denial of Service.  In rare circostanze, il meccanismo di rilevamento di ciclo infinito produce un falso positivo e l'eccezione viene generata pur trattandosi di un messaggio in arrivo valido.  Nel caso in cui i messaggi validi della propria applicazione vengano rifiutati da tale livello aggiuntivo di protezione, impostare l'attributo **checkDeserializeAdvances** su "false".  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come impostare l'attributo **checkDeserializeAdvances** su "false".  
  
```  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
  </system.xml.serialization>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Xml.Serialization.XmlSerializer>   
 [Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)