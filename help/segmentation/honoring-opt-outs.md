---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anerkennung von Ausschlussmöglichkeiten
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---


# Berücksichtigung von Ausschlussanträgen in Segmenten

Mit der Experience Platform können Ihre Kunden Abmeldeanfragen zur Nutzung und Datenspeicherung ihrer Daten innerhalb des Echtzeit-Profils des Kunden senden. Diese Ausschlussanträge sind Teil des California Consumer Privacy Act (CCPA), das kalifornischen Bürgern das Recht einräumt, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen und zu wissen, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und wem).

Nachdem ein Kunde sich für die Teilnahme entschieden hat, ist es wichtig, dass Ihr Unternehmen diese Ausschlussmöglichkeiten bei der Generierung von Audiencen für Marketing-Aktivitäten berücksichtigt. In diesem Dokument werden wichtige Details zur Erfüllung von Abmeldeanträgen beschrieben.

## Erste Schritte

Die Erfüllung von Abmeldeanforderungen erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste. Bevor Sie mit Abmeldeanfragen arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Adobe Experience Platform Segmentation Service](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [Erlebnisdatenmodell (XDM)](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Hilft Unternehmen, die Einhaltung von Datenschutzbestimmungen zu automatisieren, die Kundendaten innerhalb der Plattform einbeziehen. Zu diesen Verordnungen gehören:
   - California Consumer Privacy Act (CCPA): Datenschutzrechte für Einwohner Kaliforniens, einschließlich des Rechts, auf personenbezogene Daten zuzugreifen und sie zu löschen und zu wissen, ob personenbezogene Daten verkauft oder offen gelegt werden (und wem).
   - Allgemeine Datenschutzverordnung: Datenschutzrechte für Mitglieder der Europäischen Vereinigung, einschließlich des Rechts auf Zugang und des Rechts auf Vergessenheit.

## Ausschluss-Mixins

Um CCPA-Abmeldeanforderungen nachzukommen, muss eines der Schema, das zum Vereinigung-Schema gehört, die erforderlichen XDM-Abmeldefelder (Experience Data Model) enthalten. Es gibt zwei Mixins, die verwendet werden können, um einem Schema Ausschluss-Felder hinzuzufügen. Die folgenden Abschnitte werden ausführlicher behandelt:

- [Profil-Datenschutz](#profile-privacy): Dient zur Erfassung verschiedener Ausschluss-Typen (Allgemein oder Vertrieb/Freigabe).
- [Details](#profile-preferences-details)zu Profil-Voreinstellungen: Dient zum Erfassen von Abmeldeanforderungen für bestimmte XDM-Kanal.

Eine schrittweise Anleitung zum Hinzufügen eines Mixins zu einem Schema finden Sie im Abschnitt &quot;Hinzufügen eines Mixins&quot;in der folgenden XDM-Dokumentation:
- [Lernprogramm](../xdm/api/getting-started.md)zur API zur Registrierung von Schemas.: Erstellen eines Schemas mit der Schema Registry API.
- [Schema-Editor-Lernprogramm](../xdm/tutorials/create-schema-ui.md): Erstellen eines Schemas mithilfe der Plattform-Benutzeroberfläche

Im Folgenden finden Sie ein Beispielbild mit den Ausschluss-Mixins, die einem Schema in der Benutzeroberfläche hinzugefügt wurden:

![](images/opt-outs/opt-out-mixins-user-interface.png)

Die Struktur der einzelnen Mixins sowie eine Beschreibung der Felder, die sie zum Schema beitragen, sind in den folgenden Abschnitten detaillierter dargestellt.

### Profil-Datenschutz

Mit dem Profil Privacy-Mixin können Sie zwei Arten von CCPA-Ausschluss-Anfragen von Kunden erfassen:

1. Allgemeines Opt-out
2. Abmeldeoption für Verkauf/Freigabe

![](images/opt-outs/profile-privacy.png)

Das Profil Privacy mixin enthält die folgenden Felder:

- Opt-Outs für Datenschutz (`privacyOptOuts`): Ein Array, das eine Liste von Ausschluss-Objekten enthält.
- Ausschluss-Typ (`optOutType`): Die Art der Abmeldung. Dieses Feld ist ein Enum mit zwei möglichen Werten:
   - Allgemeine Abmeldung (`general_opt_out`)
   - Abwahl für Freigabe im Vertrieb (`sales_sharing_opt_out`)
- Ausschluss-Wert (`optOutValue`): Der aktive Status des Opt-out, auch als Wert des Opt-out-Signals bezeichnet, basierend auf dem angegebenen Opt-out-Typ. Dieses Feld ist ein Enum mit vier möglichen Werten:
   - nicht angegeben (`not_provided`): Es wurde kein Ausschluss-Antrag gestellt.
   - Ausstehende Überprüfung (`pending`): Die Abmeldeanforderung steht noch aus.
   - Ausschluss (`out`): Der Kunde hat sich abgemeldet.
   - Teilnahme (`in`): Der Kunde hat sich entschieden.
- Ausschluss-Zeitstempel (`timestamp`): Zeitstempel des empfangenen Ausschluss-Signals.

Zur Ansicht der vollständigen Struktur des Profil Privacy Mixins, lesen Sie bitte das öffentliche [XDM GitHub Repository](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) oder Vorschau des Mixins über die Plattform-Benutzeroberfläche.

### Details zu Profil-Voreinstellungen

Das Profil Voreinstellungsdetails-Mixin enthält mehrere Felder, die Voreinstellungen für Profil des Kunden darstellen (z. B. E-Mail-Format, bevorzugte Sprache und Zeitzone). In einem der Felder, die in diesem Mixin enthalten sind, können &quot;OptInOut&quot;(`optInOut`)-Werte für die Abmeldung für einzelne Kanal festgelegt werden.

![](images/opt-outs/profile-preferences-details.png)

Das Dialogfeld &quot;Details zu Profil-Voreinstellungen&quot;enthält die folgenden Felder zum Ausschluss:

- OptInOut (`optInOut`): Ein Objekt, bei dem jeder Schlüssel einen gültigen und bekannten URI für einen Kommunikations-Kanal und den aktiven Status des Ausschluss für jeden Kanal darstellt. Jeder Kanal kann einen von vier möglichen Werten haben:
   - nicht angegeben (`not_provided`): Für diesen Kanal wurde kein Ausschluss beantragt.
   - Ausstehende Überprüfung (`pending`): Die Abmeldeanforderung für diesen Kanal steht noch aus.
   - Ausschluss (`out`): Der Kunde hat sich gegen diesen Kanal entschieden.
   - Teilnahme (`in`): Der Kunde hat sich für diesen Kanal entschieden.
- Globale Ausschlussoption (`globalOptout`): Ein boolescher Wert, der bei Festlegung auf &quot;true&quot;eine globale Ausschluss-Außerkraftsetzung für das Profil einstellt. Der Standardwert für dieses Feld ist &quot;false&quot;.

Im folgenden JSON-Beispiel wird gezeigt, wie das OptInOut-Objekt mehrere Abmeldesignale für verschiedene Kommunikationssignale erfassen kann:

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Zur Ansicht der vollständigen Struktur des Profil Preferences Details Mixins besuchen Sie bitte das öffentliche GitHub-Repository [von](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM oder die Vorschau des Mixins über die Plattform-Benutzeroberfläche.

## Handhabung von Ausschluss-Optionen in der Segmentierung

Um sicherzustellen, dass mit CCPA-Ausschluss-Flags markierte Profil nicht in Segmenten enthalten sind, müssen bestehende Segmente um spezielle Felder ergänzt oder bei der Segmenterstellung einbezogen werden.

Die folgenden Abschnitte zeigen, wie die entsprechenden Felder für die beiden Arten von Ausschluss-Flags hinzugefügt werden:
1. Allgemeines Opt-out
2. Abmeldeoption für Verkauf/Freigabe

### Allgemeines Opt-out

Bei der Segmentierung werden automatisch alle Profil berücksichtigt, die das Flag &quot;Allgemeine Abmeldung&quot;enthalten. Das bedeutet, dass diese Profil standardmäßig nicht in Audiencen oder Exporten enthalten sind. Es empfiehlt sich jedoch, die entsprechenden Felder hinzuzufügen, um sicherzustellen, dass ausgeschlossene Profil nicht in Audiencen und Marketing-Aktivitäten enthalten sind.

Dies kann über die Benutzeroberfläche des Segmentaufbaus durch Hinzufügen von Attributen für die **Datenschutzoption** erfolgen. In diesem Fall ist das Segment so eingestellt, dass es nur diejenigen einbezieht, die sich für das Segment entschieden haben (d. h., sie haben keine allgemeine Ausschluss-Flag auf ihrem Profil. Dies geschieht durch die Erklärung, dass der &quot;Ausschluss-Typ&quot;gleich &quot;Allgemein-Ausschluss&quot;und der &quot;Ausschluss-Wert&quot;gleich &quot;Ausschluss-Teilnahme&quot;ist.

![](images/opt-outs/segment-general-opt-out.png)

### Abmeldeoption für Verkauf/Freigabe

Wenn ein Benutzer auf seinem Profil ein Ausschluss-/Freigabekennzeichen gesetzt hat, sollte dieses Profil nicht mehr für die Segmenterstellung oder Marketing-Aktivitäten verwendet werden. Um sicherzustellen, dass dieses Flag berücksichtigt wird, muss der Ausschluss-Typ &quot;Abmeldeart&quot;gleich &quot;Abmeldeoption&quot;und der Abmeldewert gleich &quot;Abmeldeoption&quot;sein.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Nächste Schritte

Weitere Informationen zur Segmentierung, einschließlich der Arbeit mit Segmentdefinitionen und Audiencen über die API und die Benutzeroberfläche, erhalten Sie zunächst in der Übersicht über die [Segmentierung](./home.md).

Weitere Informationen zum Datenschutz innerhalb der Plattform, einschließlich der Art und Weise, wie der Datenschutzdienst die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert, finden Sie in der Dokumentation [zum](../privacy-service/home.md)Datenschutzdienst.
