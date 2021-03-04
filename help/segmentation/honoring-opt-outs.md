---
keywords: Experience Platform;Startseite;beliebte Themen;Ausschluss;Segmentierung;Segmentierungsdienst;Segmentierungsdienst;Ausschlussoption;Opt-out;Ausschluss;
solution: Experience Platform
title: Abrufen von Abmeldeanforderungen in Segmenten
topic: Übersicht
description: 'Adobe Experience Platform ermöglicht es Ihren Kunden, Abmeldeanfragen zur Nutzung und Datenspeicherung ihrer Daten innerhalb des Echtzeit-Profils des Kunden zu senden.] Diese Opt-out-Anfragen sind Teil des California Consumer Privacy Act (CCPA), der kalifornischen Bürgern das Recht einräumt, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen und zu wissen, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und wem). '
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 60%

---


# Erfüllen von Opt-out-Anfragen in Segmenten

Mit Adobe Experience Platform können Ihre Kunden Abmeldeanfragen zur Nutzung und Datenspeicherung ihrer Daten innerhalb von [!DNL Real-time Customer Profile] senden. Diese Abmeldeanträge sind Teil des [!DNL California Consumer Privacy Act] (CCPA), das kalifornischen Bürgern das Recht einräumt, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen und zu wissen, ob ihre personenbezogenen Daten verkauft oder offen gelegt werden (und wem).

Nachdem ein Kunde sich für ein Opt-out entschieden hat, muss Ihr Unternehmen diese Ausschlussmöglichkeiten bei der Generierung von Zielgruppen für Marketing-Aktivitäten berücksichtigen. In diesem Dokument werden wichtige Details zur Erfüllung von Opt-out-Anfragen beschrieben.

## Erste Schritte

Die Berücksichtigung von Abmeldeanfragen erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste, die involviert sind. Bevor Sie mit Opt-out-Anfragen arbeiten, lesen Sie die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Hilft Unternehmen, die Einhaltung von Datenschutzbestimmungen zu automatisieren, die Kundendaten in  [!DNL Platform]die Daten einbeziehen.

## Opt-out-Mixins

Um CCPA-Abmeldeanforderungen nachzukommen, muss eines der Schema, das Bestandteil des Vereinigung-Schemas ist, die erforderlichen Abmeldefelder für [!DNL Experience Data Model] (XDM) enthalten. Es gibt zwei Mixins, die verwendet werden können, um einem Schema Opt-out-Felder hinzuzufügen. Sie werden in den folgenden Abschnitten ausführlicher behandelt:

- [Profildatenschutz](#profile-privacy): Dient zur Erfassung verschiedener Opt-out-Typen (allgemein oder Vertrieb/Freigabe).
- [Profilvoreinstellungsdetails](#profile-preferences-details): Dient zum Erfassen von Opt-out-Anfragen für bestimmte XDM-Kanäle.

Eine schrittweise Anleitung zum Hinzufügen eines Mixins zu einem Schema finden Sie im Abschnitt „Hinzufügen eines Mixins“ in der folgenden XDM-Dokumentation:
- [Tutorial zur Schema Registry-API](../xdm/api/getting-started.md).: Erstellen eines Schemas mit der Schema Registry-API.
- [Schema Editor-Tutorial](../xdm/tutorials/create-schema-ui.md): Erstellen eines Schemas mithilfe der Platform-Benutzeroberfläche.

Im Folgenden finden Sie ein Beispielbild mit den Opt-out-Mixins, die einem Schema in der Benutzeroberfläche hinzugefügt wurden:

![](images/opt-outs/opt-out-mixins-user-interface.png)

Die Struktur der einzelnen Mixins sowie eine Beschreibung der Felder, die sie zum Schema beitragen, sind in den folgenden Abschnitten detaillierter dargestellt.

### [!DNL Profile Privacy] {#profile-privacy}

Mit dem [!DNL Profile Privacy]-Mixin können Sie zwei Arten von CCPA-Ausschluss-Anfragen von Kunden erfassen:

1. Allgemeines Opt-out
2. Opt-out für Vertrieb/Freigabe

![](images/opt-outs/profile-privacy.png)

Das Mixin [!DNL Profile Privacy] enthält die folgenden Felder:

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

Die vollständige Ansicht des [!DNL Profile Privacy]-Mixins finden Sie im öffentlichen [XDM GitHub-Repository](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) oder Vorschau des Mixins mithilfe der Plattform-Benutzeroberfläche.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

Das [!DNL Profile Preferences Details]-Mixin enthält mehrere Felder, die die Voreinstellungen für Profil des Kunden darstellen (z. B. E-Mail-Format, bevorzugte Sprache und Zeitzone). In einem der Felder, die in diesem Mixin enthalten sind, erlaubt „OptInOut“ (`optInOut`) das Festlegen von Opt-out-Werten für einzelne Kanäle.

![](images/opt-outs/profile-preferences-details.png)

Das [!DNL Profile Preferences Details]-Mixin enthält die folgenden Felder zum Ausschluss:

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

Zur Ansicht der vollständigen Struktur des Profil Preferences Details mixins besuchen Sie bitte das [XDM public GitHub repository](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) oder die Vorschau des mixins mithilfe der [!DNL Platform]-Benutzeroberfläche.

## Handhabung von Opt-out-Optionen in der Segmentierung

Um sicherzustellen, dass mit CCPA-Opt-out-Markierungen gekennzeichnete Profile nicht in Segmenten enthalten sind, müssen bestehende Segmente um spezielle Felder ergänzt oder bei der Segmenterstellung einbezogen werden.

Die nachstehenden Abschnitte zeigen, wie die entsprechenden Felder für die beiden Arten von Opt-out-Markierungen hinzugefügt werden:
1. Allgemeines Opt-out
2. Opt-out für Vertrieb/Freigabe

### Allgemeines Opt-out

[!DNL Segmentation] berücksichtigt automatisch alle Profil, die das Flag &quot;[!UICONTROL Allgemein-Ausschluss]&quot;enthalten, d. h., diese Profil werden standardmäßig nicht in Audiencen oder Exporten eingeschlossen. Es empfiehlt sich jedoch, die entsprechenden Felder hinzuzufügen, um sicherzustellen, dass Opt-out-Profile nicht in Zielgruppen und Marketing-Aktivitäten enthalten sind.

Dies kann über die Benutzeroberfläche erfolgen, indem Sie die Attribute **[!UICONTROL Privacy Opt-Outs]** hinzufügen. In diesem Fall ist das Segment so eingestellt, dass es nur diejenigen einschließt, die sich dafür entschieden haben (d. h., sie haben keine allgemeine Ausschluss-Flag auf ihrem Profil. Hierzu wird erklärt, dass &quot;[!UICONTROL Ausschluss-Typ]&quot;gleich &quot;[!UICONTROL Allgemeiner Ausschluss]&quot;und &quot;[!UICONTROL Ausschluss-Wert]&quot;gleich &quot;[!UICONTROL Ausschluss-in]&quot;ist.

![](images/opt-outs/segment-general-opt-out.png)

### Opt-out für Vertrieb/Freigabe

Wenn ein Benutzer auf seinem Profil eine Opt-out-Markierung für Vertrieb/Freigabe gesetzt hat, sollte dieses Profil nicht mehr für die Segmenterstellung oder Marketing-Aktivitäten verwendet werden. Um sicherzustellen, dass dieses Flag berücksichtigt wird, muss der Abmeldetyp &quot;[!UICONTROL Opt-out-Typ]&quot;gleich &quot;[!UICONTROL Abmeldeoption]&quot;und der Abmeldewert[!UICONTROL &quot;gleich &quot;[!UICONTROL Opt-in]&quot;sein.]

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Nächste Schritte

Weitere Informationen zur Segmentierung, einschließlich der Arbeit mit Segmentdefinitionen und Zielgruppen über die API und die Benutzeroberfläche, erhalten Sie im [Segmentierungsüberblick](./home.md).

Weitere Informationen zum Datenschutz in [!DNL Platform], einschließlich der Frage, wie [!DNL Privacy Service] die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert, finden Sie in der Dokumentation zu [[!DNL Privacy Service]](../privacy-service/home.md).
