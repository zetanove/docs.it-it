---
title: "Mapping dei tipi di dati Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec34ae21-bbbb-4adb-b672-83865e2a8451
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Mapping dei tipi di dati Oracle
Nella tabella seguente sono elencati i tipi di dati Oracle e i relativi mapping al tipo <xref:System.Data.OracleClient.OracleDataReader>.  
  
|Tipo di dati Oracle|Tipo di dati .NET Framework restituito da OracleDataReader.GetValue|Tipo di dati OracleClient restituito da OracleDataReader.GetOracleValue|Note|  
|-------------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------|----------|  
|**BFILE**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBFile>||  
|**BLOB**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleLob>||  
|**CHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**CLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**DATE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**FLOAT**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|Questo tipo di dati è un alias del tipo di dati **NUMBER** ed è progettato in modo tale che <xref:System.Data.OracleClient.OracleDataReader> restituisca un oggetto **System.Decimal** o <xref:System.Data.OracleClient.OracleNumber> anziché un valore a virgola mobile.  L'utilizzo del tipo di dati .NET Framework può provocare un overflow.|  
|**INTEGER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|Questo tipo di dati è un alias del tipo di dati **NUMBER** ed è progettato in modo tale che <xref:System.Data.OracleClient.OracleDataReader> restituisca un valore **System.Decimal** o <xref:System.Data.OracleClient.OracleNumber> anziché un valore intero.  L'utilizzo del tipo di dati .NET Framework può provocare un overflow.|  
|**INTERVAL YEAR TO MONTH**|**Int32**|<xref:System.Data.OracleClient.OracleMonthSpan>||  
|**INTERVAL DAY TO SECOND**|**TimeSpan**|<xref:System.Data.OracleClient.OracleTimeSpan>||  
|**LONG**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**LONG RAW**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**NCHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**NCLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**NUMBER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|L'utilizzo del tipo di dati .NET Framework può provocare un overflow.|  
|**NVARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**RAW**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**REF CURSOR**|||Il tipo di dati **REF CURSOR** di Oracle non è supportato dall'oggetto <xref:System.Data.OracleClient.OracleDataReader>.|  
|**ROWID**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**TIMESTAMP**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**UNSIGNED INTEGER**|**Numero**|<xref:System.Data.OracleClient.OracleNumber>|Questo tipo di dati è un alias del tipo di dati **NUMBER\(38\)** ed è progettato in modo tale che <xref:System.Data.OracleClient.OracleDataReader> restituisca un oggetto **System.Decimal** o <xref:System.Data.OracleClient.OracleNumber> anziché un valore Unsigned Integer.  L'utilizzo del tipo di dati .NET Framework può provocare un overflow.|  
|**VARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
  
 Nella seguente tabella sono elencati i tipi di data Oracle e .NET Framework \(**System.Data.DbType** e <xref:System.Data.OracleClient.OracleType>\) da usare durante l'associazione come parametri.  
  
|Tipo di dati Oracle|Enumerazione DbType da associare come parametro|Enumerazione OracleType da associare come parametro|Note|  
|-------------------------|-----------------------------------------------------|---------------------------------------------------------|----------|  
|**BFILE**||**BFile**|Oracle consente di associare solo un tipo di dati **BFILE** come parametro **BFILE**.  Il provider di dati .NET per Oracle non ne crea automaticamente uno se si tenta di associare un valore diverso da **BFILE**, ad esempio **byte\[\]** o <xref:System.Data.OracleClient.OracleBinary>.|  
|**BLOB**||**Blob**|Oracle consente di associare solo un tipo di dati **BLOB** come parametro **BLOB**.  Il provider di dati .NET per Oracle non ne crea automaticamente uno se si tenta di associare un valore diverso da **BLOB**, ad esempio **byte\[\]** o <xref:System.Data.OracleClient.OracleBinary>.|  
|**CHAR**|**AnsiStringFixedLength**|**Char**||  
|**CLOB**||**Clob**|Oracle consente di associare solo un tipo di dati **CLOB** come parametro **CLOB**.  Il provider di dati .NET per Oracle non ne crea automaticamente uno se si tenta di associare un valore diverso da **CLOB**, ad esempio **System.String** o <xref:System.Data.OracleClient.OracleString>.|  
|**DATE**|**DateTime**|**DateTime**||  
|**FLOAT**|**Single, Double, Decimal**|**Float, Double, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina **System.Data.DBType** e <xref:System.Data.OracleClient.OracleType>.|  
|**INTEGER**|**SByte, Int16, Int32, Int64, Decimal**|**SByte, Int16, Int32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina **System.Data.DBType** e <xref:System.Data.OracleClient.OracleType>.|  
|**INTERVAL YEAR TO MONTH**|**Int32**|**IntervalYearToMonth**|<xref:System.Data.OracleClient.OracleType> è disponibile solo se si usa il software Oracle 9i sia per il client che per il server.|  
|**INTERVAL DAY TO SECOND**|**Oggetto**|**IntervalDayToSecond**|<xref:System.Data.OracleClient.OracleType> è disponibile solo se si usa il software Oracle 9i sia per il client che per il server.|  
|**LONG**|**AnsiString**|**LongVarChar**||  
|**LONG RAW**|**Binario**|**LongRaw**||  
|**NCHAR**|**StringFixedLength**|**NChar**||  
|**NCLOB**||**NClob**|Oracle consente di associare solo un tipo di dati **NCLOB** come parametro **NCLOB**.  Il provider di dati .NET per Oracle non ne crea automaticamente uno se si tenta di associare un valore diverso da **NCLOB**, ad esempio **System.String** o <xref:System.Data.OracleClient.OracleString>.|  
|**NUMBER**|**VarNumeric**|**Numero**||  
|**NVARCHAR2**|**String**|**NVarChar**||  
|**RAW**|**Binario**|**Raw**||  
|**REF CURSOR**||**Cursore**|Per altre informazioni, vedere [REF CURSOR Oracle](../../../../docs/framework/data/adonet/oracle-ref-cursors.md).|  
|**ROWID**|**AnsiString**|**Rowid**||  
|**TIMESTAMP**|**DateTime**|**Timestamp**|<xref:System.Data.OracleClient.OracleType> è disponibile solo se si usa il software Oracle 9i sia per il client che per il server.|  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|**TimestampLocal**|<xref:System.Data.OracleClient.OracleType> è disponibile solo se si usa il software Oracle 9i sia per il client che per il server.|  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|**TimestampWithTz**|<xref:System.Data.OracleClient.OracleType> è disponibile solo se si usa il software Oracle 9i sia per il client che per il server.|  
|**UNSIGNED INTEGER**|**Byte, UInt16, UInt32, UInt64, Decimal**|**Byte, UInt16, Uint32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina **System.Data.DBType** e <xref:System.Data.OracleClient.OracleType>.|  
|**VARCHAR2**|**AnsiString**|**VarChar**||  
  
 I valori **ParameterDirection** di **InputOutput**, **Output** e **ReturnValue** usati dalla proprietà <xref:System.Data.OracleClient.OracleParameter.Value%2A> dell'oggetto <xref:System.Data.OracleClient.OracleParameter> sono tipi di dati .NET Framework, a meno che il valore di input non sia un tipo di dati Oracle, ad esempio <xref:System.Data.OracleClient.OracleNumber> o <xref:System.Data.OracleClient.OracleString>.  Questo non si applica ai tipi di dati **REF CURSOR**, **BFILE** o **LOB**.  
  
## Vedere anche  
 [Oracle e ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)