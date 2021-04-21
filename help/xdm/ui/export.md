---
solution: Experience Platform
title: Exportieren von XDM-Schemas in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein vorhandenes Schema in eine andere Sandbox oder eine andere IMS-Organisation in der Adobe Experience Platform-Benutzeroberfläche exportieren.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Exportieren von XDM-Schemas in der Benutzeroberfläche

Alle Ressourcen in der Schema-Bibliothek sind in einer bestimmten Sandbox innerhalb einer IMS-Organisation enthalten. In einigen Fällen möchten Sie möglicherweise Experience Data Model-(XDM-)Ressourcen zwischen Sandboxen und IMS-Orgs freigeben.

Um diese Anforderung zu erfüllen, können Sie im Arbeitsbereich [!UICONTROL Schema] in der Adobe Experience Platform-Benutzeroberfläche eine Exportnutzlast für jedes Schema in der Schema-Bibliothek generieren. Diese Nutzlast kann dann in einem Aufruf an die Schema Registry API verwendet werden, um das Schema (und alle abhängigen Ressourcen) in eine Zielgruppe-Sandbox und IMS-Org zu importieren.

>[!NOTE]
>
>Sie können die Schema Registry-API auch verwenden, um neben Schemas, einschließlich Klassen, Mixins und Datentypen, weitere Ressourcen zu exportieren. Weitere Informationen finden Sie im Handbuch zu den [export/import-Endpunkten](../api/export-import.md).

## Voraussetzungen

Während die Plattform-Benutzeroberfläche den Export von XDM-Ressourcen ermöglicht, müssen Sie die Schema Registry-API verwenden, um diese Ressourcen in andere Sandboxes oder IMS-Orgs zu importieren, um den Workflow abzuschließen. Lesen Sie das Handbuch [Erste Schritte mit der Schema Registry API](../api/getting-started.md), um wichtige Informationen zu erforderlichen Authentifizierungsheader zu erhalten, bevor Sie diesem Handbuch folgen.

## Exportnutzlast generieren

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich **[!UICONTROL Schema]** aus. Suchen Sie im Arbeitsbereich [!UICONTROL Schema] das zu exportierende Schema und öffnen Sie es in [!DNL Schema Editor].

>[!TIP]
>
>Weitere Informationen zur Suche nach der gesuchten XDM-Ressource finden Sie im Handbuch [XDM-Ressourcen](./explore.md).

Nachdem Sie das Schema geöffnet haben, wählen Sie das Symbol **[!UICONTROL JSON kopieren]** (![Kopiersymbol](../images/ui/export/icon.png)) oben rechts auf der Arbeitsfläche aus.

![](../images/ui/export/copy-json.png)

Dadurch wird eine JSON-Nutzlast in Ihre Zwischenablage kopiert, die basierend auf der Schema-Struktur generiert wurde. Für das oben gezeigte Schema &quot;[!DNL Loyalty Members]&quot;wird folgende JSON generiert:

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

Die Nutzlast erfolgt in Form eines Arrays, wobei jedes Array-Element ein Objekt ist, das eine benutzerdefinierte XDM-Ressource darstellt, die exportiert werden soll. Im obigen Beispiel sind das benutzerdefinierte Mixin und das Schema &quot;[!DNL Loyalty Members]&quot;enthalten. [!DNL Loyalty details] Die vom Schema verwendeten Kernressourcen werden nicht in den Export einbezogen, da diese Ressourcen in allen Sandboxen und IMS-Organisationen verfügbar sind.

Beachten Sie, dass jede Instanz der Mandanten-ID Ihres Unternehmens in der Payload als `<XDM_TENANTID_PLACEHOLDER>` angezeigt wird. Diese Platzhalter werden automatisch durch den entsprechenden Wert für die Mandanten-ID ersetzt, je nachdem, wo Sie das Schema im nächsten Schritt importieren.

## Ressource mit der API importieren

Nachdem Sie die Export-JSON für das Schema kopiert haben, können Sie sie als Nutzlast für eine POST-Anforderung an den `/import`-Endpunkt in der Schema-Registrierungs-API verwenden. Weitere Informationen zum Konfigurieren des Aufrufs zum Senden des Schemas an das gewünschte IMS-Org und die Sandbox finden Sie im Abschnitt [Importieren einer XDM-Ressource in der API](../api/export-import.md#import).

## Nächste Schritte

Mit diesem Handbuch haben Sie ein XDM-Schema erfolgreich in ein anderes IMS-Org oder eine andere Sandbox exportiert. Weitere Informationen zu den Funktionen der Benutzeroberfläche [!UICONTROL Schema] finden Sie in der [[!UICONTROL Schema] UI-Übersicht](./overview.md).
