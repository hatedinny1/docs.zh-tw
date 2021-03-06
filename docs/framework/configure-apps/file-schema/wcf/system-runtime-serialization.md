---
title: "&lt;system.runtime.serialization&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8cebf4c-06d2-4667-8f5b-c3e1fc90df6f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;system.runtime.serialization&gt;
代表 <xref:System.Runtime.Serialization> 命名空間區段的根項目，而且包含用來設定 <xref:System.Runtime.Serialization.DataContractSerializer> 選項的項目。  
  
 system.runtime.serialization  
  
## 語法  
  
```  
  
<configuration>  
  <system.runtime.serialization>  
    <dataContractSerializer ignoreExtensionDataObject="Boolean"  
      maxItemsInObjectGraph="Integer">  
      <declaredTypes>  
        <add type="String ">  
          <knownType type="String">  
             <parameter index="Integer"/>  
          </knownType>  
        </add>  
      </declaredTypes>  
    <dataContractSerializer>  
  </system.runtime.serialization>  
</configuration>  
```  
  
## 屬性和項目  
 下列各節說明屬性、子元素和父元素  
  
### 屬性  
 無。  
  
### 子項目  
  
|項目|描述|  
|--------|--------|  
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md)|能夠在還原序列化時，加入要使用的已知型別。|  
  
### 父項目  
  
|項目|描述|  
|--------|--------|  
|[\<configuration\> 項目](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|組態的最上層項目。|  
  
## 請參閱  
 <xref:System.Runtime.Serialization>   
 [使用資料合約](../../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [資料合約已知型別](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)