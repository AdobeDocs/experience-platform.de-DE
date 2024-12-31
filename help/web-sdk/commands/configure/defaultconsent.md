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

Die `defaultConsent`-Eigenschaft bestimmt, wie das Einverständnis zur Datenerfassung verarbeitet wird, bevor der [`setConsent`](../setconsent.md) aufgerufen wird. Diese Eigenschaft ist nützlich, wenn Sie nicht versehentlich Daten von Personen erfassen möchten, die in Bereichen wohnen, in denen vor der Datenerfassung ein Einverständnis erforderlich ist.

Standardmäßig werden Benutzende für alle Zwecke angemeldet und die Web-SDK darf die folgenden Aufgaben ausführen:

* Senden an und Empfangen von Daten von Adobe-Servern.
* Lesen und Schreiben von Cookies oder Web-Speicherelementen.

Wenn Benutzende sich aus allen Gründen abmelden, führt die Web-SDK keine dieser Aufgaben aus.

Die `defaultConsent`-Eigenschaft unterstützt drei Werte:

* **`in`**: Die Datenerfassung wird wie gewohnt durchgeführt, bis der Benutzer eine Abwahl trifft.
* **`out`**: Daten werden dauerhaft verworfen, bis sich der Benutzer anmeldet.
* **`pending`**: Daten werden lokal gespeichert, bis sich der Benutzer mithilfe des [`setConsent`](../setconsent.md)-Befehls anmeldet. Wenn das Standardeinverständnis für den allgemeinen Zweck auf `pending` festgelegt ist, führt der Versuch, Befehle auszuführen, die von den Voreinstellungen für das Opt-in des Benutzers abhängen (z. B. den [`sendEvent`](../sendevent/overview.md)-Befehl), dazu, dass der Befehl in die Warteschlange der Web-SDK gestellt wird. Befehle in der Warteschlange werden erst verarbeitet, nachdem die Opt-in-Voreinstellungen des Benutzers an die Web-SDK weitergegeben wurden.

>[!NOTE]
>
> Einverständnisdaten bleiben zwischen dem Laden der Seite nicht erhalten.

Wenn Sie einen Besucher haben, der nicht unter die Datenschutz-Grundverordnung (DSGVO) fällt, kann die standardmäßige Einwilligung auf `in` gesetzt werden. Für Besucher innerhalb der Gerichtsbarkeit der DSGVO kann das standardmäßige Einverständnis auf `pending` festgelegt werden. Ihre Consent Management Platform (CMP) kann die Region des Kunden erkennen und das Flag `gdprApplies` IAB TCF 2.0 bereitstellen. Diese Markierung kann verwendet werden, um das Standardeinverständnis festzulegen.

Wenn Sie keine Ereignisse erfassen möchten, die vor dem Festlegen der Opt-in-Voreinstellungen des Benutzers aufgetreten sind, können Sie während der Konfiguration von Web SDK `"defaultConsent": "out"` übergeben. Der Versuch, Befehle auszuführen, die von den Opt-in-Voreinstellungen des Benutzers abhängen, hat keine Auswirkungen, bis Sie die Opt-in-Voreinstellungen des Benutzers an die Web-SDK weitergeleitet haben.

>[!NOTE]
>
>Derzeit unterstützt Web SDK nur einen einzigen Alles-oder-Nichts-Zweck. Obwohl wir planen, einen robusteren Satz von Zwecken oder Kategorien zu erstellen, die den verschiedenen Adobe-Funktionen und Produktangeboten entsprechen, ist die aktuelle Implementierung ein Alles-oder-Nichts-Ansatz für das Opt-in.  Dies gilt nur für [!DNL Web SDK] und NICHT für andere Adobe JavaScript-Bibliotheken.

## Verwenden von `defaultConsent` zusammen mit `setConsent` {#using-consent}

Web SDK bietet zwei komplementäre Einverständniskonfigurationsbefehle:

* [`defaultConsent`](defaultconsent.md): Dieser Befehl soll die Einverständnisvoreinstellungen von Adobe-Kunden erfassen, die Web-SDK verwenden.
* [`setConsent`](../setconsent.md): Dieser Befehl soll die Einverständnisvoreinstellungen Ihrer Site-Besucher erfassen.

Wenn diese Einstellungen zusammen verwendet werden, können sie je nach den konfigurierten Werten zu unterschiedlichen Ergebnissen bei der Datenerfassung und der Cookie-Einstellung führen.

In der folgenden Tabelle erfahren Sie, wann eine Datenerfassung erfolgt und wann Cookies gesetzt werden, basierend auf den Einstellungen für das Einverständnis.

| defaultConsent | setConsent | Datenerfassung findet statt | Web SDK setzt Browser-Cookies |
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

Die folgenden Cookies werden gesetzt, wenn die Einverständniskonfiguration Folgendes zulässt:

| Name | Maximales Alter | Beschreibung |
|---|---|---|
| **AMCV_##@AdobeOrg** | 34128000 (395 Tage) | Bei aktiviertem [`idMigrationEnabled`](../configure/idmigrationenabled.md) vorhanden. Dies ist hilfreich bei der Umstellung auf Web SDK, während einige Teile der Site noch `visitor.js` verwenden. |
| **Demdex-Cookie** | 15552000 (180 Tage) | Vorhanden, wenn ID-Synchronisierung aktiviert ist. Audience Manager legt dieses Cookie fest, um einem Site-Besucher eine eindeutige ID zuzuweisen. Das demdex -Cookie hilft Audience Manager bei der Ausführung grundlegender Funktionen wie Besucheridentifizierung, ID-Synchronisierung, Segmentierung, Modellierung, Berichterstellung usw. |
| **kndctr_orgid_cluster** | 1800 (30 Minuten) | Speichert den Edge Network-Bereich, der den Anfragen des aktuellen Benutzers dient. Die Region wird im URL-Pfad verwendet, damit das Edge Network die Anfrage an die richtige Region weiterleiten kann. Wenn ein(e) Benutzende(r) eine Verbindung mit einer anderen IP-Adresse oder in einer anderen Sitzung herstellt, wird die Anfrage erneut an die nächstgelegene Region weitergeleitet. |
| **kndct_orgid_identity** | 34128000 (395 Tage) | Speichert die ECID sowie andere Informationen im Zusammenhang mit der ECID. |
| **kndctr_orgid_consent** | 15552000 (180 Tage) | Speichert die Einverständnisvoreinstellungen der Benutzer für die Website. |
| **s_ecid** | 63115200 (2 Jahre) | Enthält eine Kopie der Experience Cloud-ID ([!DNL ECID]) oder der MID. Die MID wird in einem Schlüssel-Wert-Paar gespeichert, das dieser Syntax folgt: `s_ecid=MCMID\|<ECID>`. |

## Festlegen des Standardeinverständnisses mit der Tag-Erweiterung „Web SDK&quot;

Wählen Sie beim Konfigurieren der Tag **[!UICONTROL Erweiterung die gewünschte Optionsschaltfläche unter]** Standardeinverständnis[ aus](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenschutz] und wählen Sie dann die gewünschte **[!UICONTROL Standardeinwilligung]** aus.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Festlegen des Standardeinverständnisses mit der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `configure`-Befehls die `defaultConsent`-Zeichenfolgeneigenschaft auf die gewünschte Einverständnisstufe fest. Bei dieser Eigenschaft wird zwischen Groß- und Kleinschreibung unterschieden und sie unterstützt nur die folgenden drei Werte: `"in"`, `"out"` und `"pending"`. Wenn Sie versuchen, einen anderen Wert zu verwenden, gibt die Bibliothek einen Fehler aus.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
