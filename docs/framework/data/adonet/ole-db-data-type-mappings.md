---
title: "Mapping dei tipi di dati OLE DB | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04bcb259-59d3-4fd7-894d-4f0dd0c68069
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mapping dei tipi di dati OLE DB
Nella tabella seguente sono illustrati i tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dedotti per i tipi di dati dal provider di dati .NET Framework per ADO e OLE DB \(<xref:System.Data.OleDb>\).  Sono elencati inoltre i metodi delle funzioni di accesso tipizzate per <xref:System.Data.OleDb.OleDbDataReader>.  
  
|Tipo ADO|Tipo OLE DB|Tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|Funzione di accesso tipizzata [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|  
|--------------|-----------------|----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|  
|adBigInt|DBTYPE\_I8|Int64|GetInt64\(\)|  
|adBinary|DBTYPE\_BYTES|Byte\[\]|GetBytes\(\)|  
|adBoolean|DBTYPE\_BOOL|Boolean|GetBoolean\(\)|  
|adBSTR|DBTYPE\_BSTR|String|GetString\(\)|  
|adChapter|DBTYPE\_HCHAPTER|Supportato mediante `DataReader`.  Vedere [Recupero di dati mediante un DataReader](../../../../docs/framework/data/adonet/retrieving-data-using-a-datareader.md).|GetValue\(\)|  
|adChar|DBTYPE\_STR|String|GetString\(\)|  
|adCurrency|DBTYPE\_CY|Decimal|GetDecimal\(\)|  
|adDate|DBTYPE\_DATE|DateTime|GetDateTime\(\)|  
|adDBDate|DBTYPE\_DBDATE|DateTime|GetDateTime\(\)|  
|adDBTime|DBTYPE\_DBTIME|DateTime|GetDateTime\(\)|  
|adDBTimeStamp|DBTYPE\_DBTIMESTAMP|DateTime|GetDateTime\(\)|  
|adDecimal|DBTYPE\_DECIMAL|Decimal|GetDecimal\(\)|  
|adDouble|DBTYPE\_R8|Double|GetDouble\(\)|  
|adError|DBTYPE\_ERROR|ExternalException|GetValue\(\)|  
|adFileTime|DBTYPE\_FILETIME|DateTime|GetDateTime\(\)|  
|adGUID|DBTYPE\_GUID|Guid|GetGuid\(\)|  
|adIDispatch|DBTYPE\_IDISPATCH \*|Oggetto|GetValue\(\)|  
|adInteger|DBTYPE\_I4|Int32|GetInt32\(\)|  
|adIUnknown|DBTYPE\_IUNKNOWN \*|Oggetto|GetValue\(\)|  
|adNumeric|DBTYPE\_NUMERIC|Decimal|GetDecimal\(\)|  
|adPropVariant|DBTYPE\_PROPVARIANT|Oggetto|GetValue\(\)|  
|adSingle|DBTYPE\_R4|Single|GetFloat\(\)|  
|adSmallInt|DBTYPE\_I2|Int16|GetInt16\(\)|  
|adTinyInt|DBTYPE\_I1|Byte|GetByte\(\)|  
|adUnsignedBigInt|DBTYPE\_UI8|UInt64|GetValue\(\)|  
|adUnsignedInt|DBTYPE\_UI4|UInt32|GetValue\(\)|  
|adUnsignedSmallInt|DBTYPE\_UI2|UInt16|GetValue\(\)|  
|adUnsignedTinyInt|DBTYPE\_UI1|Byte|GetByte\(\)|  
|adVariant|DBTYPE\_VARIANT|Oggetto|GetValue\(\)|  
|adWChar|DBTYPE\_WSTR|String|GetString\(\)|  
|adUserDefined|DBTYPE\_UDT|Non supportato||  
|adVarNumeric|DBTYPE\_VARNUMERIC|Non supportato||  
  
 \* Per i tipi OLE DB `DBTYPE_IUNKNOWN` e `DBTYPE_IDISPATCH`, il riferimento all'oggetto è una rappresentazione con marshalling del puntatore.  
  
## Vedere anche  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)