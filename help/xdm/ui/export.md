---
solution: Experience Platform
title: Exportieren von XDM-Schemata über die Benutzeroberfläche
description: Erfahren Sie, wie Sie ein vorhandenes Schema in eine andere Sandbox oder Organisation in der Benutzeroberfläche von Adobe Experience Platform exportieren.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 11%

---

# Exportieren von XDM-Schemata in die Benutzeroberfläche {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Kopieren von JSON-Strukturen"
>abstract="Generieren Sie eine Export-Payload für Ihr ausgewähltes Schema, indem Sie die JSON-Struktur in die Zwischenablage kopieren. Verwenden Sie diese Funktion, um die Details eines beliebigen Schemas in die Schema-Bibliothek zu exportieren. Diese exportierte JSON-Datei kann dann zum Importieren des Schemas und der zugehörigen Ressourcen in eine andere Sandbox oder Organisation verwendet werden. Dadurch wird die Freigabe und Wiederverwendung von Schemata zwischen verschiedenen Umgebungen einfach und effizient."

Alle Ressourcen innerhalb der Schemabibliothek sind in einer bestimmten Sandbox in einer Organisation enthalten. In einigen Fällen empfiehlt es sich, Experience-Datenmodell (XDM)-Ressourcen zwischen Sandboxes und Organisationen freizugeben.

Um diese Anforderung zu erfüllen, können Sie mit dem [!UICONTROL Schemas] in der Adobe Experience Platform-Benutzeroberfläche eine Export-Payload für jedes Schema in der Schemabibliothek generieren. Diese Payload kann dann in einem Aufruf an die Schema Registry-API verwendet werden, um das Schema (und alle abhängigen Ressourcen) in eine Ziel-Sandbox und Organisation zu importieren.

>[!NOTE]
>
>Sie können die Schema Registry-API auch verwenden, um zusätzlich zu Schemata andere Ressourcen zu exportieren, einschließlich Klassen, Schemafeldgruppen und Datentypen. Weitere Informationen finden [&#x200B; im &#x200B;](../api/export.md) zum Exportieren von Endpunkten .

## Voraussetzungen

Auch wenn Sie über die Experience Platform-Benutzeroberfläche XDM-Ressourcen exportieren können, müssen Sie die Schema Registry-API verwenden, um diese Ressourcen in andere Sandboxes oder Organisationen zu importieren, um den Workflow abzuschließen. Lesen Sie das Handbuch [Erste Schritte mit der Schema Registry-API](../api/getting-started.md) um wichtige Informationen zu erforderlichen Authentifizierungskopfzeilen zu erhalten, bevor Sie dieses Handbuch befolgen.

## Export-Payload generieren {#generate-export-payload}

Export-Payloads können in der Experience Platform-Benutzeroberfläche über das Bedienfeld Details auf der Registerkarte [!UICONTROL Durchsuchen] oder direkt über die Arbeitsfläche des Schemas im Schema-Editor generiert werden.

Um eine Export-Payload zu generieren, wählen Sie **[!UICONTROL Schemata]** im linken Navigationsbereich aus. Wählen Sie im Arbeitsbereich [!UICONTROL Schemas] die Zeile für das Schema aus, das Sie exportieren möchten, um Schemadetails in der rechten Seitenleiste anzuzeigen.

>[!TIP]
>
>Weitere Informationen dazu, wie Sie die [&#x200B; XDM-Ressource finden, finden &#x200B;](./explore.md) im Handbuch zu XDM-Ressourcen .

Wählen Sie als Nächstes das **[!UICONTROL JSON kopieren]**-Symbol (![Kopiersymbol](/help/images/icons/copy.png)) aus den verfügbaren Optionen aus.

![Der Arbeitsbereich „Schemata“ mit einer Schemazeile und [!UICONTROL In JSON kopieren] hervorgehoben.](../images/ui/export/copy-json.png)

Dadurch wird eine JSON-Payload in die Zwischenablage kopiert, die basierend auf der Schemastruktur generiert wird. Für das oben dargestellte Schema &quot;[!DNL Loyalty Members]&quot; wird die folgende JSON generiert:

+++Auswählen, um eine Beispiel-JSON-Payload zu erweitern

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

+++

Sie können die Payload auch kopieren, indem Sie [!UICONTROL Mehr] oben rechts im Schema-Editor auswählen. Ein Dropdown-Menü bietet zwei Optionen: [!UICONTROL JSON-] kopieren und [!UICONTROL Schema löschen].

>[!NOTE]
>
>Ein Schema kann nicht gelöscht werden, wenn es für ein Profil aktiviert ist oder über verknüpfte Datensätze verfügt.

![Der Schema-Editor mit [!UICONTROL Mehr] und [!UICONTROL In JSON kopieren] hervorgehobenen &#x200B;](../images/ui/export/schema-editor-copy-json.png)

Die Payload hat die Form eines Arrays, wobei jedes Array-Element ein Objekt ist, das eine zu exportierende benutzerdefinierte XDM-Ressource darstellt. Im obigen Beispiel sind die benutzerdefinierte Feldergruppe &quot;[!DNL Loyalty details]&quot; und das Schema &quot;[!DNL Loyalty Members]&quot; enthalten. Alle vom Schema verwendeten Kernressourcen sind nicht im Export enthalten, da diese Ressourcen in allen Sandboxes und Organisationen verfügbar sind.

Beachten Sie, dass jede Instanz der Mandanten-ID Ihrer Organisation als `<XDM_TENANTID_PLACEHOLDER>` in der Payload angezeigt wird. Diese Platzhalter werden automatisch durch den entsprechenden Wert der Mandanten-ID ersetzt, je nachdem, wohin Sie das Schema im nächsten Schritt importieren.

## Ressource mit der API importieren {#import-resource-with-api}

Nachdem Sie die Export-JSON für das Schema kopiert haben, können Sie sie als Payload für eine POST-Anfrage an den `/rpc/import`-Endpunkt in der Schema Registry-API verwenden. Weitere Informationen [&#x200B; Konfigurieren des Aufrufs zum Senden des Schemas an &#x200B;](../api/import.md) gewünschte Organisation und Sandbox finden Sie im Handbuch zum des Importendpunkts .

## Nächste Schritte

Mithilfe dieses Handbuchs haben Sie ein XDM-Schema erfolgreich in eine andere Organisation oder Sandbox exportiert. Weitere Informationen zu den Funktionen der Benutzeroberfläche [!UICONTROL Schemata] finden Sie unter [[!UICONTROL Schemata] Benutzeroberfläche - Übersicht](./overview.md).
