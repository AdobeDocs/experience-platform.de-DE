---
solution: Experience Platform
title: Exportieren von XDM-Schemas in die Benutzeroberfläche
description: Erfahren Sie, wie Sie ein vorhandenes Schema in eine andere Sandbox oder IMS-Organisation in der Benutzeroberfläche von Adobe Experience Platform exportieren.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Exportieren von XDM-Schemas in die Benutzeroberfläche

Alle Ressourcen in der Schema Library sind in einer bestimmten Sandbox innerhalb einer IMS-Organisation enthalten. In einigen Fällen möchten Sie möglicherweise Experience-Datenmodell (XDM)-Ressourcen zwischen Sandboxes und IMS-Organisationen freigeben.

Um diesem Bedarf zu begegnen, muss die [!UICONTROL Schemas] Mit Workspace in der Adobe Experience Platform-Benutzeroberfläche können Sie eine Export-Payload für ein Schema in der Schema Library generieren. Diese Payload kann dann in einem Aufruf an die Schema Registry-API verwendet werden, um das Schema (und alle abhängigen Ressourcen) in eine Ziel-Sandbox und IMS-Organisation zu importieren.

>[!NOTE]
>
>Sie können die Schema Registry-API auch verwenden, um neben Schemas weitere Ressourcen zu exportieren, darunter Klassen, Schemafeldgruppen und Datentypen. Siehe [Export-Endpunkthandbuch](../api/export.md) für weitere Informationen.

## Voraussetzungen

Während die Platform-Benutzeroberfläche den Export von XDM-Ressourcen ermöglicht, müssen Sie die Schema Registry-API verwenden, um diese Ressourcen in andere Sandboxes oder IMS-Organisationen zu importieren und den Workflow abzuschließen. Weitere Informationen finden Sie im Handbuch [Erste Schritte mit der Schema Registry-API](../api/getting-started.md) wichtige Informationen zu erforderlichen Authentifizierungskopfzeilen erhalten, bevor Sie diesem Handbuch folgen.

## Exportnutzlast generieren

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Schemas]** in der linken Navigation. Innerhalb der [!UICONTROL Schemas] Suchen Sie im Arbeitsbereich das Schema, das Sie exportieren möchten, und öffnen Sie es im [!DNL Schema Editor].

>[!TIP]
>
>Siehe Handbuch unter [Erkunden von XDM-Ressourcen](./explore.md) für Details zum Auffinden der gesuchten XDM-Ressource.

Nachdem Sie das Schema geöffnet haben, wählen Sie die **[!UICONTROL JSON kopieren]** Symbol (![Kopiersymbol](../images/ui/export/icon.png)) oben rechts auf der Arbeitsfläche.

![](../images/ui/export/copy-json.png)

Dadurch wird eine JSON-Payload in die Zwischenablage kopiert, die basierend auf der Schemastruktur generiert wurde. Für &quot;[!DNL Loyalty Members]&quot; Schema oben gezeigt, wird die folgende JSON generiert:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

Die Payload hat die Form eines Arrays, wobei jedes Array-Element ein Objekt ist, das eine benutzerdefinierte XDM-Ressource darstellt, die exportiert werden soll. Im obigen Beispiel wird der[!DNL Loyalty details]&quot; benutzerdefinierte Feldergruppe und &quot;[!DNL Loyalty Members]&quot; Schema enthalten sind. Kernressourcen, die vom Schema verwendet werden, sind nicht im Export enthalten, da diese Ressourcen in allen Sandboxes und IMS-Organisationen verfügbar sind.

Beachten Sie, dass die Mandanten-ID jeder Instanz Ihres Unternehmens als `<XDM_TENANTID_PLACEHOLDER>` in der Payload. Diese Platzhalter werden automatisch durch den entsprechenden Mandanten-ID-Wert ersetzt, je nachdem, wo Sie das Schema im nächsten Schritt importieren.

## Importieren der Ressource mit der API

Nachdem Sie die Export-JSON für das Schema kopiert haben, können Sie sie als Payload für eine POST-Anfrage an die `/rpc/import` -Endpunkt in der Schema Registry-API. Siehe [Import-Endpunkthandbuch](../api/import.md) für Details zur Konfiguration des Aufrufs zum Senden des Schemas an die gewünschte IMS-Organisation und Sandbox.

## Nächste Schritte

In diesem Handbuch haben Sie erfolgreich ein XDM-Schema in eine andere IMS-Organisation oder Sandbox exportiert. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Benutzeroberfläche, siehe [[!UICONTROL Schemas] Übersicht über die Benutzeroberfläche](./overview.md).
