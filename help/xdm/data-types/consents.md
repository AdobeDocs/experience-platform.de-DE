---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einverständnis;Einverständnis;Voreinstellungen;Voreinstellungen;DatenschutzOptOuts;MarketingPreferences;OptOutType;basisOfProcessing;Einverständnis;Einverständnis
title: Datentyp „Einverständnis und Voreinstellungen“
description: Der Datentyp Einverständnis für Datenschutz, Personalization und Marketing-Voreinstellungen unterstützt die Erfassung von Kundenberechtigungen und -einstellungen, die von Einverständnisverwaltungsplattformen (CMPs) und anderen Quellen aus Ihren Datenvorgängen generiert wurden.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '2305'
ht-degree: 1%

---

# [!UICONTROL Consents and Preferences] Datentyp

Der [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]-Datentyp (im Folgenden als &quot;[!UICONTROL Consents and Preferences]-Datentyp“ bezeichnet) ist ein [!DNL Experience Data Model] (XDM)-Datentyp, der die Erfassung von Kundenberechtigungen und -präferenzen unterstützt, die von Einverständnisverwaltungsplattformen (CMPs) und anderen Quellen aus Ihren Datenvorgängen generiert werden.

In diesem Dokument werden die Struktur und der Verwendungszweck der Felder beschrieben, die vom Datentyp [!UICONTROL Consents and Preferences] bereitgestellt werden.

## Voraussetzungen {#prerequisites}

Dieses Dokument setzt ein Verständnis von XDM und der Verwendung der Schemata in [!DNL Experience Platform] voraus. Bitte lesen Sie die folgende Dokumentation, bevor Sie fortfahren:

* [XDM-System – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de)
* [Grundlagen der Schemakomposition](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Datentypstruktur {#structure}

>[!IMPORTANT]
>
>Der [!UICONTROL Consents and Preferences] Datentyp wurde entwickelt, um eine Reihe von Anwendungsfällen für die Einverständnis- und Präferenzverwaltung abzudecken. Daher beschreibt dieses Dokument die Verwendung der Felder des Datentyps allgemein und macht nur Vorschläge, wie Sie die Verwendung dieser Felder interpretieren sollten. Wenden Sie sich an Ihre Rechtsabteilung, um die Struktur des Datentyps an die Interpretation anzupassen und Ihren Kunden diese Einverständnis- und Präferenzentscheidungen zu präsentieren.

Der Datentyp [!UICONTROL Consents and Preferences] enthält mehrere Felder, mit denen **(Einverständnis** und **Voreinstellungen** erfasst werden.

Eine Einwilligung ist eine Option, mit der ein Kunde angeben kann, wie seine Daten verwendet werden dürfen. Die meisten Einverständnisse haben einen rechtlichen Aspekt, da einige Gerichtsbarkeiten die Einholung einer Genehmigung verlangen, bevor Daten auf eine bestimmte Weise verwendet werden können, oder verlangen, dass der Kunde die Möglichkeit hat, diese Verwendung zu stoppen (Opt-out), wenn keine bejahende Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde angeben kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke gehandhabt werden sollen. Diese sind in zwei Kategorien unterteilt:

* **Personalization-Voreinstellungen**: Voreinstellungen dafür, wie die Marke die einem Kunden bereitgestellten Erlebnisse personalisieren soll.
* **Marketing-**: Voreinstellungen dazu, ob eine Marke über verschiedene Kanäle Kontakt mit einem Kunden aufnehmen darf.

Der folgende Screenshot zeigt, wie die Struktur des Datentyps in der Experience Platform-Benutzeroberfläche dargestellt wird:

![](../images/data-types/consents.png)

>[!TIP]
>
>Anweisungen zum Suchen einer XDM[Ressource und Überprüfen ihrer Struktur in der Benutzeroberfläche von Experience Platform finden Sie im Handbuch &#x200B;](../ui/explore.md)Erkunden von XDM-Ressourcen“ zu .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den der [!UICONTROL Consents and Preferences]-Datentyp verarbeiten kann. Informationen zur spezifischen Verwendung der einzelnen Felder finden Sie in den folgenden Abschnitten.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in Experience Platform definieren, um zu visualisieren, wie Ihre Kundeneinwilligungs- und Präferenzdaten zugeordnet werden sollten. In der folgenden Dokumentation finden Sie weitere Informationen:
>
>* [Generieren von Beispieldaten in der Benutzeroberfläche](../ui/sample.md)
>* [Generieren von Beispieldaten in der API](../api/sample-data.md)

## `consents` {#choices}

`consents` enthält mehrere Felder, die die Einverständnisse und Voreinstellungen eines Kunden beschreiben. Diese Felder werden in den folgenden Unterabschnitten näher beschrieben.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` stellt das Einverständnis des Kunden mit der Erfassung seiner Daten dar.

```json
"collect": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Einverständnisentscheidung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `adID`

`adID` stellt das Einverständnis des Kunden dar, ob eine Advertiser-ID verwendet werden kann, um den Kunden über Apps hinweg auf diesem Gerät zu verknüpfen.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `idType` | Der Anzeigen-ID-Typ, entweder `IDFA` für die Apple-ID für Advertiser oder `GAID` für die Google-Advertiser-ID, auch bekannt als Android Advertiser-ID (AAID). |
| `val` | Die vom Kunden bereitgestellte Einverständnisentscheidung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `share`

`share` stellt die Zustimmung des Kunden dazu dar, ob seine Daten an Zweite oder Dritte weitergegeben (oder an Dritte verkauft) werden können.

```json
"share": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Einverständnisentscheidung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` erfasst Kundenpräferenzen bezüglich der Möglichkeiten, wie ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Anwendungsfälle der Personalisierung deaktivieren oder sich ganz von der Personalisierung abmelden.

>[!IMPORTANT]
>
>`personalize` deckt keine Marketing-Anwendungsfälle ab. Wenn sich ein Kunde beispielsweise gegen die Personalisierung für alle Kanäle entscheidet, sollte er den Empfang von Nachrichten über diese Kanäle nicht einstellen. Stattdessen sollten die Nachrichten, die sie erhalten, generisch sein und nicht auf ihrem Profil basieren.
>
>Wenn ein Kunde sich im selben Beispiel für das Direkt-Marketing für alle Kanäle entscheidet (durch `marketing`, wie im [nächsten Abschnitt](#marketing) erläutert), sollte dieser Kunde keine Nachrichten erhalten, selbst wenn Personalisierung zulässig ist.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `content` | Gibt die Kundenpräferenzen für personalisierte Inhalte auf Ihrer Website oder in Ihrem Programm an. |
| `val` | Die vom Kunden bereitgestellte Personalisierungseinstellung für den angegebenen Anwendungsfall. Wenn der Kunde nicht zur Einwilligung aufgefordert werden muss, sollte der Wert dieses Felds die Grundlage angeben, auf der die Personalisierung erfolgen soll. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` erfasst Kundenpräferenzen bezüglich der Frage, zu welchen Marketing-Zwecken ihre Daten verwendet werden können. Kunden können bestimmte Marketing-Anwendungsfälle abwählen oder sich vollständig vom Direkt-Marketing abmelden.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `preferred` | Gibt den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an. Siehe [Anhang](#preferred-values) für gültige Werte. |
| `any` | Stellt die Kundenpräferenzen für das direkte Marketing als Ganzes dar. Die in diesem Feld angegebene Einverständnisvoreinstellung gilt als Standardvoreinstellung für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder überschrieben, die unter `marketing` bereitgestellt werden. Wenn Sie granularere Einverständnisoptionen verwenden möchten, wird empfohlen, dieses Feld auszuschließen.<br><br>Wenn der Wert auf `n` festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y` festgelegt ist, sollten auch alle detaillierteren Personalisierungsoptionen als `y` behandelt werden, es sei denn, die Einstellung wird explizit auf `n` festgelegt. Wenn der Wert nicht festgelegt ist, sollten die Werte für jede Personalisierungsoption wie angegeben berücksichtigt werden. |
| `email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. |
| `push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen erlaubt. |
| `sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. |
| `val` | Die vom Kunden bereitgestellte Voreinstellung für den angegebenen Anwendungsfall. Wenn der Kunde nicht zur Einwilligung aufgefordert werden muss, sollte der Wert dieses Felds die Grundlage angeben, auf der der Marketing-Anwendungsfall stattfinden soll. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |
| `time` | Ein ISO 8601-Zeitstempel, der angibt, wann sich die Marketing-Voreinstellung geändert hat, falls zutreffend. Beachten Sie, dass, wenn der Zeitstempel für eine einzelne Voreinstellung mit dem unter `metadata` angegebenen Zeitstempel übereinstimmt, dieses Feld nicht für diese Voreinstellung festgelegt werden muss. |
| `reason` | Wenn ein Kunde sich von einem Marketing-Anwendungsfall abmeldet, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |

{style="table-layout:auto"}

### `metadata`

`metadata` erfasst allgemeine Metadaten zu den Einverständnissen und Voreinstellungen des Kunden, wann immer diese zuletzt aktualisiert wurden.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `time` | Ein ISO 8601-Zeitstempel für das letzte Mal, dass eines der Einverständnisse und Voreinstellungen des Kunden aktualisiert wurde. Dieses Feld kann verwendet werden, anstatt Zeitstempel auf individuelle Voreinstellungen anzuwenden, um die Last und Komplexität zu reduzieren. Wenn Sie unter einer individuellen Voreinstellung einen `time` Wert angeben, wird der `metadata` Zeitstempel für diese bestimmte Voreinstellung überschrieben. |

{style="table-layout:auto"}

## Aufnehmen von Daten mit dem Datentyp {#ingest}

Um den Datentyp [!UICONTROL Consents and Preferences] zum Aufnehmen von Einverständnisdaten von Ihren Kunden zu verwenden, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diesen Datentyp enthält.

Anweisungen zum Zuweisen von Datentypen zu Feldern [&#x200B; Sie im Tutorial &#x200B;](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)Erstellen eines Schemas in der Benutzeroberfläche“. Nachdem Sie ein Schema erstellt haben, das ein Feld mit dem Datentyp [!UICONTROL Consents and Preferences] enthält, lesen Sie den Abschnitt [Erstellen eines Datensatzes](../../catalog/datasets/user-guide.md#create) im Benutzerhandbuch zu Datensätzen, indem Sie die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema befolgen.

>[!IMPORTANT]
>
>Wenn Sie Einverständnisdaten an [!DNL Real-Time Customer Profile] senden möchten, müssen Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile]-Klasse basiert, die den [!UICONTROL Consents and Preferences] Datentyp enthält. Der Datensatz, den Sie basierend auf diesem Schema erstellen, muss auch für die [!DNL Profile] aktiviert sein. Die einzelnen Schritte im Zusammenhang mit den [!DNL Real-Time Customer Profile] für Schemata und Datensätze finden Sie in den oben verlinkten Tutorials.
>
>Darüber hinaus müssen Sie auch sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass die Datensätze, die die neuesten Einverständnis- und Präferenzdaten enthalten, priorisiert werden, damit Kundenprofile korrekt aktualisiert werden. Weitere Informationen finden Sie in der Übersicht [Zusammenführungsrichtlinien](../../rtcdp/profile/merge-policies.md) .

## Umgang mit Einverständnis- und Voreinstellungsänderungen

Wenn ein Kunde sein Einverständnis oder seine Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort durchgesetzt werden, indem das Einverständnis in der verwendeten Datenerfassungsbibliothek festgelegt wird. Wenn ein Kunde die Datenerfassung ablehnt, muss diese sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten Seite, die er besucht, keine Personalisierung vorhanden sein. Siehe [`setConsent`](/help/collection/js/commands/setconsent.md) mit der JavaScript-Bibliothek oder die [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) Aktion mit der Tag-Erweiterung.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zum [!UICONTROL Consents and Preferences] Datentyp.

### Akzeptierte Werte für `val` {#choice-values}

In der folgenden Tabelle sind die akzeptierten Werte für `val` aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für das Einverständnis oder die Voreinstellung entschieden. Mit anderen Worten, sie **nicht** der Verwendung ihrer Daten, wie in der betreffenden Einwilligung oder Präferenz angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat die Zustimmung oder Voreinstellung abgelehnt. Mit anderen Worten, sie **nicht** der Verwendung ihrer Daten, wie in der betreffenden Einwilligung oder Präferenz angegeben. |
| `p` | Überprüfung ausstehend | Das System hat noch keinen endgültigen Einverständnis- oder Präferenzwert erhalten. Dies wird am häufigsten im Rahmen einer Einwilligung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird dieses Einverständnis auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Ab diesem Zeitpunkt wird das Einverständnis auf `y` aktualisiert.<br><br>Wenn für diese Einwilligung oder Voreinstellung kein zweistufiger Verifizierungsprozess verwendet wird, kann stattdessen die `p` verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einverständnisaufforderung reagiert hat. Beispielsweise können Sie den Wert auf der ersten Seite einer Website automatisch auf `p` setzen, bevor der Kunde auf die Einverständnisaufforderung reagiert hat. In Rechtssystemen, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde nicht explizit widersprochen hat (mit anderen Worten, eine Zustimmung wird vorausgesetzt).<br><br> Dieser Wert kann zwar über andere Mechanismen wie Streaming-Aufnahme in die [!DNL Profile] aufgenommen werden, wird aber **für die Datenerfassung oder** auf [!DNL Edge Network] nicht unterstützt. Der `p` kann zwar nicht explizit gesendet werden, aber die Ereigniswarteschlange wird weiterhin vom [[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md) verarbeitet und das Ereignis wird an [!DNL Edge Network] gesendet, sobald das Einverständnis des Endbenutzers explizit `in` wurde. |
| `u` | Unbekannt | Die Einverständnis- oder Voreinstellungsinformationen des Kunden sind unbekannt. |
| `dy` | Standard von „Ja“ (Opt-in) | Der Kunde hat selbst keinen Einverständniswert angegeben und wird standardmäßig als Opt-in („Ja„) behandelt. Mit anderen Worten wird die Einwilligung so lange vorausgesetzt, bis der Kunde etwas Anderes angibt.<br><br>Beachten Sie, dass Sie, wenn Gesetze oder Änderungen an den Datenschutzrichtlinien Ihres Unternehmens zu Änderungen an den Standardwerten einiger oder aller Benutzer führen, alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen. |
| `dn` | Standard von „Nein“ (Opt-out) | Der Kunde hat selbst keinen Einverständniswert angegeben und wird standardmäßig als Opt-out („Nein„) behandelt. Mit anderen Worten wird davon ausgegangen, dass der Kunde seine Zustimmung verweigert hat, bis er etwas Anderes angibt.<br><br>Beachten Sie, dass Sie, wenn Gesetze oder Änderungen an den Datenschutzrichtlinien Ihres Unternehmens zu Änderungen an den Standardwerten einiger oder aller Benutzer führen, alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen. |
| `LI` | berechtigtes Interesse | Das berechtigte geschäftliche Interesse an der Erhebung und Verarbeitung dieser Daten für den angegebenen Zweck überwiegt den potenziellen Schaden, den sie für den Einzelnen darstellen. |
| `CT` | Vertrag | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Lebensnotwendiges Interesse des Einzelnen | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | öffentliches Interesse | Die Erhebung von Daten für den genannten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style="table-layout:auto"}

### Akzeptierte Werte für `preferred` {#preferred-values}

In der folgenden Tabelle sind die akzeptierten Werte für `preferred` aufgeführt. Die `preferred` Werte geben den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an, die ihn über die Datenerfassung, Datenschutzrichtlinien und Personalisierungsoptionen informieren würden.

| Wert | Beschreibung |
| --- | --- |
| `email` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten per E-Mail an. |
| `push` | Diese Voreinstellung zeigt die Zustimmung des Kunden zum Empfang von Push-Benachrichtigungen an. Hierbei handelt es sich um Nachrichten oder Warnhinweise, die direkt an ihr Gerät, häufig eine Mobile App, gesendet werden. |
| `inApp` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von In-App-Nachrichten an. Diese Nachrichten werden innerhalb einer mobilen oder Web-Anwendung gesendet und enthalten Informationen, während der Benutzer aktiv mit der App interagiert. |
| `sms` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten per SMS (Short Message Service) an. Dies sind Textnachrichten, die an ihr Mobiltelefon gesendet werden. |
| `phone` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten durch Telefoninteraktionen an. |
| `phyMail` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Materialien per Post an. |
| `inVehicle` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Benachrichtigungen im Fahrzeug an. Diese Nachrichten können über Fahrzeuginformationssysteme oder andere bordeigene Kommunikationskanäle versendet werden. |
| `inHome` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten zu Hause an. Diese Nachrichten können über Smart-Home-Geräte oder andere heimbasierte Kommunikationskanäle gesendet werden. |
| `iot` | Diese Voreinstellung bezeichnet die Zustimmung des Kunden zum Empfang von Nachrichten im Zusammenhang mit dem Internet der Dinge (IoT). Diese Nachrichten können über verbundene Geräte und Systeme in ihrer Umgebung gesendet werden. |
| `social` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten über Social-Media-Plattformen an. |
| `other` | Diese Voreinstellung umfasst Kanäle, die nicht zu Standardkategorien passen. Es stellt alternative oder spezialisierte Kommunikationskanäle dar, die für ein bestimmtes Unternehmen oder eine bestimmte Branche spezifisch sein können. |
| `none` | Diese Voreinstellung zeigt an, dass der Kunde keinen bevorzugten Kommunikationskanal hat. |
| `unknown` | Diese Voreinstellung bedeutet, dass der bevorzugte Kommunikationskanal des Kunden unbekannt ist oder nicht angegeben wurde. Dies kann vorkommen, wenn der Kunde keine expliziten Einverständnis- oder Voreinstellungsinformationen angegeben hat. |

{style="table-layout:auto"}

### Vollständiges [!UICONTROL Consents and Preferences] {#full-schema}

Das vollständige Schema für den [!UICONTROL Consents and Preferences] Datentyp finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
