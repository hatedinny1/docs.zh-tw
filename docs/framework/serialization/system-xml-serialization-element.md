---
title: "&lt;system.xml.serialization&gt; 項目 | Microsoft Docs"
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
  - "<system.xml.serialization> 項目"
  - "system.xml.serialization 項目"
  - "XML 序列化, 設定"
ms.assetid: 3ce45919-388a-418c-8968-6df0372c73ec
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;system.xml.serialization&gt; 項目
用來控制 XML 序列化的最上層項目。  如需有關組態檔的詳細資訊，請參閱 [組態檔結構描述](../../../docs/framework/configure-apps/file-schema/index.md)。  
  
## 語法  
  
```  
  
<system.xml.serialization>  
</system.xml.serialization>  
```  
  
## 屬性和項目  
 下列章節說明屬性、子項目和父項目。  
  
### 屬性  
 無。  
  
### 子項目  
  
|項目|描述|  
|--------|--------|  
|[\<dateTimeSerialization\> 項目](../../../docs/framework/serialization/datetimeserialization-element.md)|判斷 <xref:System.DateTime> 物件的序列化模式。|  
|[\<schemaImporterExtensions\> 項目](../../../docs/framework/serialization/schemaimporterextensions-element.md)|包含 <xref:System.Xml.Serialization.XmlSchemaImporter> 用來對應 XSD 型別至 .NET Framework 型別的型別。|  
  
### 父項目  
  
|項目|描述|  
|--------|--------|  
|[\<configuration\> 項目](../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Common Language Runtime 與 .NET Framework 應用程式使用的所有組態檔中的根項目。|  
  
## 範例  
 下列程式碼範例描述如何指定 <xref:System.DateTime> 物件的序列化模式，以及在對應 XSD 型別至 .NET Framework 型別時 <xref:System.Xml.Serialization.XmlSchemaImporter> 使用的新增型別。  
  
```  
<system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
    <dateTimeSerialization mode = "Local" />  
    <schemaImporterExtensions>  
        <add   
        name = "MobileCapabilities"   
        type = "System.Web.Mobile.MobileCapabilities,   
        System.Web.Mobile, Version - 2.0.0.0, Culture = neuutral,   
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
</system.sxml.serialization>  
```  
  
## 請參閱  
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>   
 [組態檔結構描述](../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<dateTimeSerialization\> 項目](../../../docs/framework/serialization/datetimeserialization-element.md)   
 [\<schemaImporterExtensions\> 項目](../../../docs/framework/serialization/schemaimporterextensions-element.md)   
 [\<xmlSchemaImporterExtensions\> 的 \<add\> 項目](../../../docs/framework/serialization/add-element-for-xmlschemaimporterextensions.md)