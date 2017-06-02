---
title: "Mapping dei tipi di dati Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "02/15/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d2521bcc-0051-4f35-8be3-e8723edeaf6f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Mapping dei tipi di dati Oracle
Nella tabella seguente sono illustrati i tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dedotti per i tipi di dati dal provider di dati .NET Framework per Oracle \(<xref:System.Data.OracleClient>\). Sono elencati inoltre i metodi delle funzioni di accesso tipizzate per <xref:System.Data.OracleClient.OracleDataReader>.  
  
|Tipo Oracle|Tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|Funzione di accesso tipizzata [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|Funzione di accesso tipizzata OracleType|  
|-----------------|----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------|  
|BFILE|Byte\[\]|GetBytes\(\)|GetOracleBFile\(\)|  
|BLOB|Byte\[\]|GetBytes\(\)|GetOracleLob\(\)|  
|CHAR|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
|CLOB|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleLob\(\)|  
|DATE|DateTime|GetDateTime\(\)|GetOracleDateTime\(\)|  
|FLOAT|Decimal|GetDecimal\(\)|GetOracleNumber\(\) \*\*|  
|INTEGER|Decimal|GetDecimal\(\)|GetOracleNumber\(\) \*\*|  
|INTERVAL YEAR TO MONTH \*|Int32|GetInt32\(\)|GetOracleMonthSpan\(\)|  
|INTERVAL DAY TO SECOND \*|TimeSpan|GetTimeSpan\(\)|GetOracleTimeSpan\(\)|  
|LONG|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
|LONG RAW|Byte\[\]|GetBytes\(\)|GetOracleBinary\(\)|  
|NCHAR|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
|NCLOB|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleLob\(\)|  
|NUMBER|Decimal|GetDecimal\(\)|GetOracleNumber\(\) \*\*|  
|NVARCHAR2|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
|RAW|Byte\[\]|GetBytes\(\)|GetOracleBinary\(\)|  
|REF CURSOR||||  
|ROWID|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
|TIMESTAMP \*|DateTime|GetDateTime\(\)|GetOracleDateTime\(\)|  
|TIMESTAMP WITH LOCAL TIME ZONE \*|DateTime|GetDateTime\(\)|GetOracleDateTime\(\)|  
|TIMESTAMP WITH TIME ZONE \*|DateTime|GetDateTime\(\)|GetOracleDateTime\(\)|  
|UNSIGNED INTEGER|Decimal|GetDecimal\(\)|GetOracleNumber\(\) \*\*|  
|VARCHAR2|String<br /><br /> Char\[\]|GetString\(\)<br /><br /> GetChars\(\)|GetOracleString\(\)|  
  
 \* Il tipo Oracle specificato è disponibile solo quando si usa il software Oracle 9i sia per il client che per il server.  
  
 \*\* Un NUMBER Oracle può avere un massimo di 38 cifre significative. Il tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] di `decimal` è limitato a 28 cifre. Se si legge un NUMBER Oracle di più di 28 cifre in un tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]`decimal` verrà generata un'eccezione `OverflowException`. Se si legge un valore NUMBER Oracle da `OracleDataReader`, è consigliabile chiamare il metodo della funzione di accesso tipizzata `GetOracleNumber` per restituire i valori NUMBER Oracle come `OracleNumber`. Se si compila un oggetto `DataSet`, è possibile usare l'evento `FillError` per determinare se si è verificata un'eccezione `OverflowException` e, in caso affermativo, per eseguire l'azione appropriata. Per informazioni sull'evento `FillError`, vedere [Gestione degli eventi di DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md).  
  
## Vedere anche  
 [Oracle e ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)