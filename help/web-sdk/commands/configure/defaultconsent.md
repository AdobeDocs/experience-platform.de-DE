---
title: defaultConsent
description: Legen Sie die standardmäßige Methode zur Einverständniserfassung für Ihre Web-Eigenschaft fest.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

Die `defaultConsent` -Eigenschaft bestimmt, wie Sie die Datenerfassungs-Zustimmung verarbeiten, bevor Sie den [`setConsent`](../setconsent.md) -Befehl aufrufen. Diese Eigenschaft ist nützlich, wenn Sie nicht versehentlich Daten von Einzelpersonen erfassen möchten, die sich in Bereichen befinden, in denen vor der Datenerfassung eine Einwilligung erforderlich ist.

Standardmäßig sind Benutzer für alle Zwecke angemeldet und das Web SDK darf die folgenden Aufgaben ausführen:

* Senden an und Empfangen von Daten von Adobe-Servern.
* Cookies oder Elemente des Webspeichers lesen und schreiben.

Wenn Benutzer sich von allen Zwecken abmelden, führt das Web SDK keine dieser Aufgaben aus.

Die `defaultConsent` -Eigenschaft unterstützt drei Werte:

* **`in`**: Die Datenerfassung wird wie gewohnt fortgesetzt, bis sich der Benutzer abmeldet.
* **`out`**: Die Daten werden dauerhaft verworfen, bis sich der Benutzer anmeldet.
* **`pending`**: Die Daten werden lokal gespeichert, bis sich der Benutzer mit dem Befehl [`setConsent`](../setconsent.md) anmeldet. Wenn die Standardzustimmung für den allgemeinen Zweck auf &quot;`pending`&quot;festgelegt ist, führt der Versuch, Befehle auszuführen, die von den Anmeldeeinstellungen des Benutzers abhängen (z. B. dem Befehl &quot;[`sendEvent`](../sendevent/overview.md)&quot;), dazu, dass der Befehl im Web SDK in die Warteschlange gestellt wird. In der Warteschlange befindliche Befehle werden erst verarbeitet, nachdem Sie die Opt-in-Voreinstellungen des Benutzers an das Web SDK übermittelt haben.

>[!NOTE]
>
> Die Einwilligungsdaten bleiben nicht zwischen den Seitenladevorgängen erhalten.

Wenn Sie einen Besucher haben, der nicht unter die Datenschutz-Grundverordnung (DSGVO) fällt, kann die Standardzustimmung auf `in` gesetzt werden. Besucher innerhalb der Gerichtsbarkeit der DSGVO können ihre standardmäßige Einwilligung auf `pending` setzen lassen. Ihre Consent Management Platform (CMP) kann die Region des Kunden erkennen und das Flag `gdprApplies` für IAB TCF 2.0 bereitstellen. Mit diesem Flag können Sie die Standardzustimmung festlegen.

Wenn Sie keine Ereignisse erfassen möchten, die vor dem Festlegen der Opt-in-Voreinstellungen des Benutzers aufgetreten sind, können Sie `"defaultConsent": "out"` während der Web SDK-Konfiguration übergeben. Der Versuch, Befehle auszuführen, die von den Anmeldeeinstellungen des Benutzers abhängen, hat keine Auswirkungen, bis Sie die Anmeldeeinstellungen des Benutzers an das Web SDK übermittelt haben.

>[!NOTE]
>
>Derzeit unterstützt das Web SDK nur einen einzigen All-or-Nichts-Zweck. Obwohl wir planen, einen robusteren Satz von Zielen oder Kategorien zu entwickeln, die den verschiedenen Adobe-Funktionen und Produktangeboten entsprechen, ist die aktuelle Implementierung ein Alles-oder-Nichts-Ansatz zum Opt-in.  Dies gilt nur für [!DNL Web SDK] und NICHT für andere Adobe JavaScript-Bibliotheken.

## Verwenden von `defaultConsent` zusammen mit `setConsent` {#using-consent}

Das Web SDK bietet zwei komplementäre Konfigurationsbefehle für die Zustimmung:

* [`defaultConsent`](defaultconsent.md): Dieser Befehl dient zum Erfassen der Zustimmungsvoreinstellungen von Adobe-Kunden, die das Web SDK verwenden.
* [`setConsent`](../setconsent.md): Mit diesem Befehl können Sie die Zustimmungsvoreinstellungen Ihrer Site-Besucher erfassen.

Wenn diese Einstellungen zusammen verwendet werden, können sie je nach konfigurierten Werten zu unterschiedlichen Ergebnissen bei der Datenerfassung und Cookie-Einstellung führen.

Die nachstehende Tabelle zeigt, wann und wann Cookies basierend auf den Zustimmungseinstellungen erfasst werden.

| defaultConsent | setConsent | Datenerfassung | Web SDK setzt Browser-Cookies |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nein | Ja |
| `in` | Nicht festgelegt | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nein | Ja |
| `pending` | Nicht festgelegt | Nein | Nein |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nein | Ja |
| `out` | Nicht festgelegt | Nein | Nein |

Die folgenden Cookies werden gesetzt, wenn die Konfiguration der Zustimmung Folgendes zulässt:

| Name | Max. Alter | Beschreibung |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 Tage) | Vorhanden, wenn [`idMigrationEnabled`](../configure/idmigrationenabled.md) aktiviert ist. Dies ist beim Übergang zum Web SDK hilfreich, während einige Teile der Site weiterhin `visitor.js` verwenden. |
| **Demdex-Cookie** | 15552000 (180 Tage) | Vorhanden bei aktivierter ID-Synchronisierung. Audience Manager setzt dieses Cookie, um Site-Besuchern eine eindeutige ID zuzuweisen. Das demdex-Cookie hilft Audience Manager bei der Ausführung grundlegender Funktionen wie Besucheridentifizierung, ID-Synchronisierung, Segmentierung, Modellierung, Berichterstellung usw. |
| **kndctr_orgid_cluster** | 1800 (30 Minuten) | Speichert den Edge Network-Bereich, der den Anforderungen des aktuellen Benutzers entspricht. Der Bereich wird im URL-Pfad verwendet, damit das Edge Network die Anfrage an den richtigen Bereich weiterleiten kann. Wenn ein Benutzer eine Verbindung mit einer anderen IP-Adresse oder in einer anderen Sitzung herstellt, wird die Anforderung erneut an den nächsten Bereich weitergeleitet. |
| **kndct_orgid_identity** | 34128000 (395 Tage) | Speichert die ECID sowie andere Informationen zur ECID. |
| **kndctr_orgid_consent** | 15552000 (180 Tage) | Speichert die Voreinstellung der Benutzerzustimmung für die Website. |
| **s_ecid** | 63115200 (2 Jahre) | Enthält eine Kopie der Experience Cloud-ID ([!DNL ECID]) oder MID. Die MID wird in einem Schlüssel-Wert-Paar gespeichert, das dieser Syntax folgt: `s_ecid=MCMID\|<ECID>`. |

## Festlegen der Standardzustimmung mit der Web SDK-Tag-Erweiterung

Wählen Sie die gewünschte Optionsschaltfläche unter **[!UICONTROL Standardzustimmung]** aus, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenschutz] und wählen Sie dann die gewünschte **[!UICONTROL Standardzustimmung]** aus.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Festlegen der Standardzustimmung mit der Web SDK JavaScript-Bibliothek

Legen Sie die String-Eigenschaft `defaultConsent` beim Ausführen des Befehls `configure` auf die gewünschte Zustimmungsebene fest. Diese Eigenschaft unterscheidet zwischen Groß- und Kleinschreibung und unterstützt nur die folgenden drei Werte: `"in"`, `"out"` und `"pending"`. Wenn Sie versuchen, einen anderen Wert zu verwenden, gibt die Bibliothek einen Fehler aus.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
