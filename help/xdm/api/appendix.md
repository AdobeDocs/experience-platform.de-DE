---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Entwickleranhang für Schema Registry
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Schema Registry-API.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 73%

---


# Anhang

This document provides supplemental information related to working with the [!DNL Schema Registry] API.

## Kompatibilitätsmodus

[!DNL Experience Data Model]Das  (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quell-Code und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemas verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich das Standard-XDM von dem unterscheidet, das Sie in Adobe Experience Platform sehen. What you are seeing in [!DNL Experience Platform] is called Compatibility Mode, and it provides a simple mapping between standard XDM and the way it is used within [!DNL Platform].

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemas in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken, ist die Entfernung des Präfix „xdm:“ für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM als auch im Kompatibilitätsmodus geburtstagsbezogene Felder (mit entfernten „Beschreibungsattributen“) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen „meta:xdmField“ und „meta:xdmType“ enthalten.

<table>
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767,
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Warum ist der Kompatibilitätsmodus erforderlich?

Adobe Experience Platform ist für die Verwendung mit mehreren Lösungen und Diensten konzipiert, die jeweils eigene technische Herausforderungen und Einschränkungen aufweisen (z. B. wie bestimmte Technologien Sonderzeichen handhaben). Um diese Einschränkungen zu überwinden, wurde der Kompatibilitätsmodus entwickelt.

Die meisten [!DNL Experience Platform] Dienste einschließlich [!DNL Catalog], [!DNL Data Lake]und [!DNL Real-time Customer Profile] Verwendung als Standard-XDM [!DNL Compatibility Mode] . Die [!DNL Schema Registry] API verwendet auch [!DNL Compatibility Mode]und die Beispiele in diesem Dokument werden alle mit verwendet [!DNL Compatibility Mode].

It is worthwhile to know that a mapping takes place between standard XDM and the way it is operationalized in [!DNL Experience Platform], but it should not affect your use of [!DNL Platform] services.

The open source project is available to you, but when it comes to interacting with resources through the [!DNL Schema Registry], the API examples in this document provide the best practices you should know and follow.