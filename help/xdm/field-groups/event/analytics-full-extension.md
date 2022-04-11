---
title: Adobe Analytics ExperienceEvent Full Extension – Schemafeldgruppe
description: Dieses Dokument bietet einen Überblick über die Schemafeldgruppe „Adobe Analytics ExperienceEvent Full Extension“.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: ht
source-wordcount: '894'
ht-degree: 100%

---

# Schemafeldgruppe [!UICONTROL Adobe Analytics ExperienceEvent Full Extension]

[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die allgemeine von Adobe Analytics erfasste Metriken erfasst.

In diesem Dokument werden die Struktur und der Anwendungsfall der Feldgruppe der Analytics-Erweiterung beschrieben.

>[!NOTE]
>
>Aufgrund des Umfangs und der Anzahl der sich wiederholenden Elemente in dieser Feldgruppe wurden viele der in diesem Handbuch angezeigten Felder reduziert, um Platz zu sparen. Um die gesamte Struktur dieser Feldgruppe zu untersuchen, können Sie [sie in der Platform-Benutzeroberfläche nachschlagen ](../../ui/explore.md) oder das vollständige Schema im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) anzeigen.

## Feldgruppenstruktur

Die Feldgruppe stellt ein einzelnes `_experience`-Objekt für ein Schema bereit, das selbst ein einzelnes `analytics`-Objekt enthält.

![Felder der obersten Ebene für die Analytics-Feldgruppe](../../images/field-groups/analytics-full-extension/full-schema.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `customDimensions` | Objekt | Erfasst benutzerdefinierte Dimensionen, die von Analytics verfolgt werden. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#custom-dimensions). |
| `endUser` | Objekt | Erfasst die Web-Interaktionsdetails für den Endbenutzer, der das Ereignis ausgelöst hat. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#end-user). |
| `environment` | Objekt | Erfasst Informationen über den Browser und das Betriebssystem, die das Ereignis ausgelöst haben. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#environment). |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Objekt | Die Feldgruppe stellt Objektfelder bereit, mit denen bis zu 1.000 benutzerspezifische Ereignisse erfasst werden können. Weitere Informationen zu diesen Feldern finden Sie im [nachfolgenden Unterabschnitt](#events). |
| `session` | Objekt | Erfasst Informationen über die Sitzung, die das Ereignis ausgelöst hat. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#session). |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` erfasst benutzerdefinierte [Dimensionen](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=de), die von Analytics verfolgt werden.

![customDimensions-Feld](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `eVars` | Objekt | Ein Objekt, das bis zu 250 Konvertierungsvariablen ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=de)) erfasst. Die Eigenschaften dieses Objekts sind von `eVar1` bis `eVar250` nummeriert und akzeptieren nur Zeichenfolgen für ihren Datentyp. |
| `hierarchies` | Objekt | Ein Objekt, das bis zu fünf benutzerdefinierte Hierarchievariablen ([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=de)) erfasst. Die Eigenschaften dieses Objekts werden als `hier1` bis `hier5` verschlüsselt. Dies sind selbst Objekte mit den folgenden Untereigenschaften:<ul><li>`delimiter`: Das ursprüngliche Trennzeichen, das zur Erstellung der Liste unter `values` verwendet wurde.</li><li>`values`: Eine durch Trennzeichen getrennte Liste von Namen der Hierarchieebenen, dargestellt als Zeichenfolge.</li></ul> |
| `listProps` | Objekt | Ein Objekt, das bis zu 75 [Listen-Props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=de#listen-props) erfasst. Die Eigenschaften dieses Objekts werden als `prop1` bis `prop75` verschlüsselt. Dies sind selbst Objekte mit den folgenden Untereigenschaften:<ul><li>`delimiter`: Das ursprüngliche Trennzeichen, das zur Erstellung der Liste unter `values` verwendet wurde.</li><li>`values`: Eine durch Trennzeichen getrennte Liste von Werten für die Eigenschaft, dargestellt als Zeichenfolge.</li></ul> |
| `lists` | Objekt | Ein Objekt, das bis zu drei [Listen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=de) erfasst. Die Eigenschaften dieses Objekts werden als `list1` bis `list3` verschlüsselt. Jede dieser Eigenschaften enthält ein `list`-Array von Datentypen für [[!UICONTROL Schlüssel-Wert-Paare]](../../data-types/key-value-pair.md). |
| `props` | Objekt | Ein Objekt, das bis zu 75 [Eigenschaften](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=de) erfasst. Die Eigenschaften dieses Objekts werden als `prop1` bis `prop75` verschlüsselt und akzeptieren als Datentyp nur Zeichenfolgen. |
| `postalCode` | Zeichenfolge | Eine vom Kunden bereitgestellte Postleitzahl. |
| `stateProvince` | Zeichenfolge | Ein vom Kunden bereitgestellter Bundeslands- oder Regionsstandort. |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` erfasst die Web-Interaktionsdetails für den Endbenutzer, der das Ereignis ausgelöst hat.

![endUser-Feld](../../images/field-groups/analytics-full-extension/endUser.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web-Informationen]](../../data-types/web-information.md) | Die Informationen zu Web-Seite, Link und Referrer aus dem ersten Erlebnisereignis für diesen Endbenutzer. |
| `firstTimestamp` | Ganzzahl | Ein Unix-Zeitstempel für das erste Erlebnisereignis für diesen Endbenutzer. |

## `environment` {#environment}

`environment` erfasst Informationen über den Browser und das Betriebssystem, die das Ereignis ausgelöst haben.

![Umgebungsfeld](../../images/field-groups/analytics-full-extension/environment.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `browserIDStr` | Zeichenfolge | Die Adobe Analytics-Kennung für den verwendeten Browser (wird auch als [Dimension „Browser-Typ“](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=de) bezeichnet). |
| `operatingSystemIDStr` | Zeichenfolge | Die Adobe Analytics-Kennung für das verwendete Betriebssystem (wird auch als [Dimension „Betriebssystemtyp“](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=de) bezeichnet). |

## Benutzerdefinierte Ereignisfelder {#events}

Die Feldergruppe der Analytics-Erweiterung enthält zehn Objektfelder, die jeweils bis zu 100 [benutzerdefinierte Ereignismetriken](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=de) erfassen, insgesamt 1000 für die Feldergruppe.

Jedes Ereignisobjekt der obersten Ebene enthält die einzelnen Ereignisobjekte für den jeweiligen Bereich. Beispiel: `event101to200` enthält die Ereignisse, die von `event101` bis `event200` verschlüsselt wurden.

Jedes lineare Objekt verwendet den Datentyp [[!UICONTROL Kennzahl]](../../data-types/measure.md) und stellt eine eindeutige Kennung und einen quantifizierbaren Wert bereit.

![Feld für benutzerdefiniertes Ereignis](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` erfasst Informationen über die Sitzung, die das Ereignis ausgelöst hat.

![Sitzungsfeld](../../images/field-groups/analytics-full-extension/session.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `search` | [[!UICONTROL Durchsuchen]](../../data-types/search.md) | Erfasst Informationen zur Web- oder Mobile-Suche nach dem Sitzungseintrag. |
| `web` | [[!UICONTROL Web-Informationen]](../../data-types/web-information.md) | Erfasst Informationen zu Link-Klicks, Web-Seitendetails, Informationen zur verweisenden Stelle sowie Browser-Details für den Sitzungseintrag. |
| `depth` | Ganzzahl | Die aktuelle Sitzungstiefe (z. B. die Seitenzahl) für den Endbenutzer. |
| `num` | Ganzzahl | Die aktuelle Sitzungsnummer für den Endbenutzer. |
| `timestamp` | Ganzzahl | Ein Unix-Zeitstempel für den Sitzungseintrag. |

## Nächste Schritte

In diesem Dokument wurden die Struktur und der Anwendungsfall für die Feldgruppe der Analytics-Erweiterung behandelt. Weitere Informationen zur Feldgruppe selbst finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Wenn Sie diese Feldgruppe verwenden, um Analytics-Daten mithilfe des Adobe Experience Platform Web SDK zu erfassen, erfahren Sie in der Anleitung unter [Konfigurieren eines Datenstroms](../../../edge/fundamentals/datastreams.md), wie Sie Daten Server-seitig XDM zuordnen.
