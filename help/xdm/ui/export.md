---
solution: Experience Platform
title: Exportieren von XDM-Schemas in die Benutzeroberfläche
description: Erfahren Sie, wie Sie ein vorhandenes Schema in eine andere Sandbox oder IMS-Organisation in der Benutzeroberfläche von Adobe Experience Platform exportieren.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Exportieren von XDM-Schemas in die Benutzeroberfläche

Alle Ressourcen in der Schema Library sind in einer bestimmten Sandbox innerhalb einer IMS-Organisation enthalten. In einigen Fällen möchten Sie möglicherweise Experience-Datenmodell (XDM)-Ressourcen zwischen Sandboxes und IMS-Organisationen freigeben.

Um dies zu erreichen, können Sie mit dem Arbeitsbereich [!UICONTROL Schemas] in der Adobe Experience Platform-Benutzeroberfläche eine Export-Payload für ein beliebiges Schema in der Schema Library generieren. Diese Payload kann dann in einem Aufruf an die Schema Registry-API verwendet werden, um das Schema (und alle abhängigen Ressourcen) in eine Ziel-Sandbox und IMS-Organisation zu importieren.

>[!NOTE]
>
>Sie können die Schema Registry-API auch verwenden, um neben Schemas weitere Ressourcen zu exportieren, darunter Klassen, Schemafeldgruppen und Datentypen. Weitere Informationen finden Sie im Handbuch zu den [Export-/Import-Endpunkten](../api/export-import.md) .

## Voraussetzungen  

Während die Platform-Benutzeroberfläche den Export von XDM-Ressourcen ermöglicht, müssen Sie die Schema Registry-API verwenden, um diese Ressourcen in andere Sandboxes oder IMS-Organisationen zu importieren und den Workflow abzuschließen. Wichtige Informationen zu erforderlichen Authentifizierungskopfzeilen finden Sie im [Erste Schritte mit der Schema Registry-API](../api/getting-started.md) , bevor Sie dieses Handbuch befolgen.

## Exportnutzlast generieren

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Schemas]** aus. Suchen Sie im Arbeitsbereich [!UICONTROL Schemas] das Schema, das Sie exportieren möchten, und öffnen Sie es im Arbeitsbereich [!DNL Schema Editor].

>[!TIP]
>
>Weitere Informationen zum Auffinden der gesuchten XDM-Ressource finden Sie im Handbuch [Erkunden von XDM-Ressourcen](./explore.md) .

Nachdem Sie das Schema geöffnet haben, wählen Sie das Symbol **[!UICONTROL JSON kopieren]** (![Kopiersymbol](../images/ui/export/icon.png)) oben rechts auf der Arbeitsfläche aus.

![](../images/ui/export/copy-json.png)

Dadurch wird eine JSON-Payload in die Zwischenablage kopiert, die basierend auf der Schemastruktur generiert wurde. Für das oben dargestellte Schema &quot;[!DNL Loyalty Members]&quot;wird die folgende JSON generiert:

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

Die Payload hat die Form eines Arrays, wobei jedes Array-Element ein Objekt ist, das eine benutzerdefinierte XDM-Ressource darstellt, die exportiert werden soll. Im obigen Beispiel sind die benutzerdefinierte Feldergruppe &quot;[!DNL Loyalty details]&quot;und das Schema &quot;[!DNL Loyalty Members]&quot;enthalten. Kernressourcen, die vom Schema verwendet werden, sind nicht im Export enthalten, da diese Ressourcen in allen Sandboxes und IMS-Organisationen verfügbar sind.

Beachten Sie, dass jede Instanz der Mandanten-ID Ihres Unternehmens in der Payload als `<XDM_TENANTID_PLACEHOLDER>` angezeigt wird. Diese Platzhalter werden automatisch durch den entsprechenden Mandanten-ID-Wert ersetzt, je nachdem, wo Sie das Schema im nächsten Schritt importieren.

## Importieren der Ressource mit der API

Nachdem Sie die Export-JSON für das Schema kopiert haben, können Sie sie als Payload für eine POST-Anfrage an den `/import`-Endpunkt in der Schema Registry-API verwenden. Weitere Informationen zum Konfigurieren des Aufrufs zum Senden des Schemas an die gewünschte IMS-Organisation und Sandbox finden Sie im Abschnitt [Importieren einer XDM-Ressource in die API](../api/export-import.md#import) .

## Nächste Schritte

In diesem Handbuch haben Sie erfolgreich ein XDM-Schema in eine andere IMS-Organisation oder Sandbox exportiert. Weitere Informationen zu den Funktionen der [!UICONTROL Schemas]-Benutzeroberfläche finden Sie in der [[!UICONTROL Übersicht über Schemas] der Benutzeroberfläche](./overview.md).
