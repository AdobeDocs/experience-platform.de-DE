---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erfüllen von Opt-outs
topic: overview
translation-type: tm+mt
source-git-commit: f156679601c2ed0bb933a66a56661c29c1b9c778
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 65%

---


# Erfüllen von Opt-out-Anfragen in Segmenten

[!DNL Experience Platform] ermöglicht es Ihren Kunden, Abmeldeanfragen zur Nutzung und Datenspeicherung ihrer Daten innerhalb von [!DNL Real-time Customer Profile]zu senden. These opt-out requests are part of the [!DNL California Consumer Privacy Act] (CCPA), which provides California residents with the right to access and delete their personal data and to know whether their personal data is sold or disclosed (and to whom).

Nachdem ein Kunde sich für ein Opt-out entschieden hat, muss Ihr Unternehmen diese Ausschlussmöglichkeiten bei der Generierung von Zielgruppen für Marketing-Aktivitäten berücksichtigen. In diesem Dokument werden wichtige Details zur Erfüllung von Opt-out-Anfragen beschrieben.

## Erste Schritte

Honoring opt-out requests requires an understanding of the various [!DNL Adobe Experience Platform] services involved. Bevor Sie mit Opt-out-Anfragen arbeiten, lesen Sie die Dokumentation für die folgenden Dienste:

- [!DNL Real-time Customer Profile](../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [!DNL Adobe Experience Platform Segmentation Service](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus [!DNL Real-time Customer Profile] Daten.
- [!DNL Experience Data Model (XDM)](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [!DNL Adobe Experience Platform Privacy Service](../privacy-service/home.md): Hilft Unternehmen, die Einhaltung von Datenschutzbestimmungen zu automatisieren, die Kundendaten in [!DNL Platform]die Daten einbeziehen.

## Opt-out-Mixins

In order to honor CCPA opt-out requests, one of the schemas that is a part of the union schema must contain the necessary [!DNL Experience Data Model] (XDM) opt-out fields. Es gibt zwei Mixins, die verwendet werden können, um einem Schema Opt-out-Felder hinzuzufügen. Sie werden in den folgenden Abschnitten ausführlicher behandelt:

- [Profildatenschutz](#profile-privacy): Dient zur Erfassung verschiedener Opt-out-Typen (allgemein oder Vertrieb/Freigabe).
- [Profilvoreinstellungsdetails](#profile-preferences-details): Dient zum Erfassen von Opt-out-Anfragen für bestimmte XDM-Kanäle.

Eine schrittweise Anleitung zum Hinzufügen eines Mixins zu einem Schema finden Sie im Abschnitt „Hinzufügen eines Mixins“ in der folgenden XDM-Dokumentation:
- [Tutorial zur Schema Registry-API](../xdm/api/getting-started.md).: Erstellen eines Schemas mit der Schema Registry-API.
- [Schema Editor-Tutorial](../xdm/tutorials/create-schema-ui.md): Erstellen eines Schemas mithilfe der Platform-Benutzeroberfläche.

Im Folgenden finden Sie ein Beispielbild mit den Opt-out-Mixins, die einem Schema in der Benutzeroberfläche hinzugefügt wurden:

![](images/opt-outs/opt-out-mixins-user-interface.png)

Die Struktur der einzelnen Mixins sowie eine Beschreibung der Felder, die sie zum Schema beitragen, sind in den folgenden Abschnitten detaillierter dargestellt.

### [!DNL Profile Privacy]

The [!DNL Profile Privacy] mixin allows you to capture two kinds of CCPA opt-out requests from customers:

1. Allgemeines Opt-out
2. Opt-out für Vertrieb/Freigabe

![](images/opt-outs/profile-privacy.png)

Das [!DNL Profile Privacy] Mixin enthält die folgenden Felder:

- Datenschutz-Opt-outs (`privacyOptOuts`): Ein Array, das eine Liste von Opt-out-Objekten enthält.
- Opt-out-Typ (`optOutType`): Die Art des Opt-outs. Dieses Feld ist ein Enum mit zwei möglichen Werten:
   - Allgemeines Opt-out (`general_opt_out`)
   - Opt-out für Freigabe/Vertrieb (`sales_sharing_opt_out`)
- Opt-out-Wert (`optOutValue`): Der aktive Status des Opt-outs, auch als Wert des Opt-out-Signals bezeichnet, basierend auf dem angegebenen Opt-out-Typ. Dieses Feld ist ein Enum mit vier möglichen Werten:
   - Nicht angegeben (`not_provided`): Es wurde keine Opt-out-Anfrage gestellt.
   - Ausstehende Überprüfung (`pending`): Die Opt-out-Anfrage steht noch aus.
   - Opt-out (`out`): Der Kunde hat sich abgemeldet.
   - Opt-in (`in`): Der Kunde hat sich angemeldet.
- Opt-out-Zeitstempel (`timestamp`): Zeitstempel des empfangenen Opt-out-Signals.

To view the full structure of the [!DNL Profile Privacy] mixin, please refer to the [XDM public GitHub repository](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) or preview the mixin using the Platform UI.

### Profilvoreinstellungsdetails

Das Profilvoreinstellungsdetails-Mixin enthält mehrere Felder, die Voreinstellungen für Kundenprofile darstellen (z. B. E-Mail-Format, bevorzugte Sprache und Zeitzone). In einem der Felder, die in diesem Mixin enthalten sind, erlaubt „OptInOut“ (`optInOut`) das Festlegen von Opt-out-Werten für einzelne Kanäle.

![](images/opt-outs/profile-preferences-details.png)

Das Profilvoreinstellungsdetails-Mixin enthält die folgenden Felder bezüglich Opt-outs:

- OptInOut (`optInOut`): Ein Objekt, bei dem jeder Schlüssel einen gültigen und bekannten URI für einen Kommunikationskanal und den aktiven Status des Opt-outs für jeden Kanal darstellt. Jeder Kanal kann einen von vier möglichen Werten haben:
   - Nicht angegeben (`not_provided`): Für diesen Kanal wurde keine Opt-out-Anfrage gesendet.
   - Ausstehende Überprüfung (`pending`): Die Opt-out-Anfrage für diesen Kanal muss noch geprüft werden.
   - Opt-out (`out`): Der Kunde hat sich von diesem Kanal abgemeldet.
   - Opt-in (`in`): Der Kunde hat sich bei diesem Kanal angemeldet.
- Globales Opt-out (`globalOptout`): Ein boolescher Wert, der bei Festlegung auf „true“ eine globale Opt-out-Regelung für das Profil einstellt. Der Standardwert für dieses Feld ist „false“.

Im folgenden JSON-Beispiel wird gezeigt, wie das OptInOut-Objekt mehrere Opt-out-Signale für verschiedene Kommunikationssignale erfassen kann:

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

To view the full structure of the Profile Preferences Details mixin, please visit the [XDM public GitHub repository](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) or preview the mixin using the [!DNL Platform] UI.

## Handhabung von Opt-out-Optionen in der Segmentierung

Um sicherzustellen, dass mit CCPA-Opt-out-Markierungen gekennzeichnete Profile nicht in Segmenten enthalten sind, müssen bestehende Segmente um spezielle Felder ergänzt oder bei der Segmenterstellung einbezogen werden.

Die nachstehenden Abschnitte zeigen, wie die entsprechenden Felder für die beiden Arten von Opt-out-Markierungen hinzugefügt werden:
1. Allgemeines Opt-out
2. Opt-out für Vertrieb/Freigabe

### Allgemeines Opt-out

[!DNL Segmentation] berücksichtigt automatisch alle Profil, die das Flag &quot;[!UICONTROL Allgemein-Ausschluss]&quot;enthalten, d. h., diese Profil werden standardmäßig nicht in Audiencen oder Exporten eingeschlossen. Es empfiehlt sich jedoch, die entsprechenden Felder hinzuzufügen, um sicherzustellen, dass Opt-out-Profile nicht in Zielgruppen und Marketing-Aktivitäten enthalten sind.

This can be done using the user interface by adding **[!UICONTROL Privacy Opt-Outs]** attributes. In diesem Fall ist das Segment so eingestellt, dass es nur diejenigen einschließt, die sich dafür entschieden haben (d. h., sie haben keine allgemeine Ausschluss-Flag auf ihrem Profil. This is done by declaring that the &quot;[!UICONTROL Opt-Out Type]&quot; equals &quot;[!UICONTROL General Opt-Out]&quot; and the &quot;[!UICONTROL Opt-Out Value]&quot; equals &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Opt-out für Vertrieb/Freigabe

Wenn ein Benutzer auf seinem Profil eine Opt-out-Markierung für Vertrieb/Freigabe gesetzt hat, sollte dieses Profil nicht mehr für die Segmenterstellung oder Marketing-Aktivitäten verwendet werden. To ensure this flag is honored, the &quot;[!UICONTROL Opt-Out Type]&quot; must equal &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; and the &quot;[!UICONTROL Opt-Out Value]&quot; must equal &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Nächste Schritte

Weitere Informationen zur Segmentierung, einschließlich der Arbeit mit Segmentdefinitionen und Zielgruppen über die API und die Benutzeroberfläche, erhalten Sie im [Segmentierungsüberblick](./home.md).

To learn more about data privacy within [!DNL Platform], including how [!DNL Privacy Service] helps to facilitate automated compliance with legal and organizational privacy regulations, please refer to the documentation on [!DNL Privacy Service](../privacy-service/home.md).
