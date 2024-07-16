---
keywords: Experience Platform; profile; Echtzeit-Kundenprofil; Fehlerbehebung; API; Einverständnis; Einverständnis; Voreinstellungen; Voreinstellungen; privacyOptOuts; marketingPreferences; optOutType; baseOfProcessing; consent; Consent
title: Datentyp "Einwilligungen und Voreinstellungen"
description: Der Datentyp Einverständnis für Datenschutz, Personalization und Marketing-Voreinstellungen soll die Erfassung von Kundenberechtigungen und -präferenzen unterstützen, die von Consent Management Platform (CMPs) und anderen Quellen aus Ihren Datenvorgängen generiert werden.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 1%

---

# Datentyp [!UICONTROL Zustimmungen und Voreinstellungen]

Der Datentyp [!UICONTROL Einverständnis für Datenschutz, Personalization und Marketing-Voreinstellungen] (im Folgenden als &quot;[!UICONTROL Einverständnis und Voreinstellungen]&quot; bezeichnet) ist ein [!DNL Experience Data Model] (XDM)-Datentyp, der die Erfassung von Kundenberechtigungen und -präferenzen unterstützt, die von Consent Management Platform (CMPs) und anderen Quellen aus Ihren Datenvorgängen generiert werden.

Dieses Dokument behandelt die Struktur und die vorgesehene Verwendung der Felder, die vom Datentyp [!UICONTROL Einverständnisse und Voreinstellungen] bereitgestellt werden.

## Voraussetzungen {#prerequisites}

Dieses Dokument setzt ein Verständnis von XDM und der Verwendung der Schemas in [!DNL Experience Platform] voraus. Lesen Sie die folgende Dokumentation, bevor Sie fortfahren:

* [XDM-System – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de)
* [Grundlagen der Schemakomposition](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Datentypstruktur {#structure}

>[!IMPORTANT]
>
>Der Datentyp [!UICONTROL Einverständnisse und Voreinstellungen] deckt eine Reihe von Nutzungsszenarien für die Einwilligungs- und Vorzugsverwaltung ab. In diesem Dokument wird daher die Verwendung der Felder des Datentyps allgemein beschrieben und es werden nur Vorschläge zur Interpretation der Verwendung dieser Felder gemacht. Wenden Sie sich an Ihr Datenschutzrechtsteam, um die Struktur des Datentyps an die Interpretation und Präsentation dieser Zustimmungs- und Auswahlmöglichkeiten für Ihre Kunden anzupassen.

Der Datentyp [!UICONTROL Einverständnisse und Voreinstellungen] enthält mehrere Felder, mit denen **Einverständnis** und **Vorlieben** erfasst werden.

Eine Einwilligung ist eine Option, mit der ein Kunde festlegen kann, wie seine Daten verwendet werden können. Die meisten Einverständniserklärungen haben einen rechtlichen Aspekt, da in einigen Rechtsordnungen eine Erlaubnis erforderlich ist, bevor Daten in einer bestimmten Weise verwendet werden können, oder der Kunde die Möglichkeit hat, diese Verwendung zu stoppen (Opt-out), wenn keine Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde festlegen kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke behandelt werden sollen. Diese Kategorien fallen in zwei Kategorien:

* **Personalization-Voreinstellungen**: Voreinstellungen dazu, wie die Marke Erlebnisse personalisieren soll, die einem Kunden bereitgestellt werden.
* **Marketing-Voreinstellungen**: Voreinstellungen dazu, ob eine Marke einen Kunden über verschiedene Kanäle kontaktieren darf.

Der folgende Screenshot zeigt, wie die Struktur des Datentyps in der Platform-Benutzeroberfläche dargestellt wird:

![](../images/data-types/consents.png)

>[!TIP]
>
>Anweisungen zum Nachschlagen einer beliebigen XDM-Ressource und zum Überprüfen ihrer Struktur in der Platform-Benutzeroberfläche finden Sie im Handbuch zu [Erkunden von XDM-Ressourcen](../ui/explore.md) zu .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp &quot;[!UICONTROL Einverständnisse und Voreinstellungen]&quot;. Informationen zur spezifischen Verwendung dieser Felder finden Sie in den folgenden Abschnitten.

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
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in Experience Platform definieren, um zu veranschaulichen, wie Ihre Kundenzustimmungs- und -bevorzugte Daten zugeordnet werden sollen. Weitere Informationen finden Sie in der folgenden Dokumentation:
>
>* [Generieren von Beispieldaten in der Benutzeroberfläche](../ui/sample.md)
>* [Generieren von Beispieldaten in der API](../api/sample-data.md)

## `consents` {#choices}

`consents` enthält mehrere Felder, die die Zustimmung und Voreinstellungen eines Kunden beschreiben. Diese Felder werden in den folgenden Unterabschnitten ausführlicher beschrieben.

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

`collect` entspricht der Einwilligung des Kunden zur Erfassung seiner Daten.

```json
"collect": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style="table-layout:auto"}

### `adID`

`adID` steht für die Zustimmung des Kunden, ob eine Advertiser-ID verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `idType` | Der Anzeigen-ID-Typ, entweder `IDFA` für die Apple-ID für Advertiser oder `GAID` für die Google Advertiser-ID, die auch als Android Advertiser ID (AAID) bezeichnet wird. |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style="table-layout:auto"}

### `share`

`share` steht für die Einwilligung des Kunden, ob seine Daten an Zweit- oder Dritte weitergegeben (oder an Dritte verkauft) werden können.

```json
"share": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` erfasst Kundenpräferenzen darüber, wie ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Anwendungsfälle der Personalisierung deaktivieren oder die Personalisierung vollständig deaktivieren.

>[!IMPORTANT]
>
>`personalize` deckt keine Marketing-Anwendungsfälle ab. Wenn beispielsweise ein Kunde die Personalisierung für alle Kanäle ablehnt, sollte er nicht aufhören, Nachrichten über diese Kanäle zu empfangen. Stattdessen sollten die Nachrichten, die sie empfangen, generisch sein und nicht auf ihrem Profil basieren.
>
>Wenn ein Kunde sich im selben Beispiel vom Direktmarketing für alle Kanäle abmeldet (über `marketing`, wie im Abschnitt [nächster Abschnitt](#marketing) erläutert), sollte dieser Kunde keine Nachrichten erhalten, selbst wenn eine Personalisierung zulässig ist.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `content` | Stellt die Voreinstellungen des Kunden für personalisierte Inhalte auf Ihrer Website oder Anwendung dar. |
| `val` | Die vom Kunden bereitgestellte Personalisierungseinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht zur Einwilligung aufgefordert werden muss, sollte der Wert dieses Felds die Grundlage angeben, auf der die Personalisierung erfolgen soll. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` erfasst Kundenpräferenzen in Bezug darauf, für welche Marketing-Zwecke ihre Daten verwendet werden können. Kunden können bestimmte Marketing-Anwendungsfälle abwählen oder Direktmarketing vollständig deaktivieren.

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
| `preferred` | Gibt den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an. Akzeptierte Werte finden Sie im [Anhang](#preferred-values) . |
| `any` | Stellt die Voreinstellungen des Kunden für Direktmarketing als Ganzes dar. Die in diesem Feld angegebene Zustimmungsvoreinstellung gilt als &quot;Standardeinstellung&quot;für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder überschrieben, die unter `marketing` angegeben sind. Wenn Sie planen, detailliertere Zustimmungsoptionen zu verwenden, wird empfohlen, dieses Feld auszuschließen.<br><br>Wenn der Wert auf `n` festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y` gesetzt ist, sollten alle feineren Personalisierungsoptionen ebenfalls als `y` behandelt werden, es sei denn, dies ist explizit auf `n` festgelegt. Wenn der Wert nicht festgelegt ist, sollten die Werte für jede Personalisierungsoption wie angegeben berücksichtigt werden. |
| `email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. |
| `push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen gestattet. |
| `sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. |
| `val` | Die vom Kunden angegebene Voreinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht aufgefordert werden muss, seine Zustimmung zu erteilen, sollte der Wert dieses Felds die Grundlage angeben, auf der der Marketing-Anwendungsfall stattfinden soll. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |
| `time` | Ein ISO 8601-Zeitstempel, mit dem die Marketing-Voreinstellung geändert wurde (falls zutreffend). Beachten Sie, dass, wenn der Zeitstempel für eine individuelle Voreinstellung mit dem unter `metadata` angegebenen Zeitstempel übereinstimmt, dieses Feld nicht für diese Voreinstellung festgelegt werden darf. |
| `reason` | Wenn ein Kunde einen Marketing-Anwendungsfall ablehnt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |

{style="table-layout:auto"}

### `metadata`

`metadata` erfasst allgemeine Metadaten über die Zustimmung und Voreinstellungen des Kunden, wann immer sie zuletzt aktualisiert wurden.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `time` | Ein ISO 8601-Zeitstempel zum letzten Mal, wenn die Zustimmungen und Voreinstellungen des Kunden aktualisiert wurden. Dieses Feld kann verwendet werden, anstatt Zeitstempel auf individuelle Voreinstellungen anzuwenden, um Belastung und Komplexität zu reduzieren. Wenn Sie unter einer individuellen Voreinstellung einen `time` -Wert angeben, wird der `metadata`-Zeitstempel für diese Voreinstellung überschrieben. |

{style="table-layout:auto"}

## Daten mithilfe des Datentyps erfassen {#ingest}

Um den Datentyp [!UICONTROL Zustimmungen und Voreinstellungen] zum Erfassen der Zustimmungsdaten Ihrer Kunden zu verwenden, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diesen Datentyp enthält.

Anweisungen zum Zuweisen von Datentypen zu Feldern finden Sie im Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) . [ Nachdem Sie ein Schema erstellt haben, das ein Feld mit dem Datentyp [!UICONTROL Einverständnisse und Voreinstellungen] enthält, lesen Sie den Abschnitt zum Erstellen eines Datensatzes [3} im Benutzerhandbuch zum Datensatz und befolgen Sie die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema.](../../catalog/datasets/user-guide.md#create)

>[!IMPORTANT]
>
>Wenn Sie Einwilligungsdaten an [!DNL Real-Time Customer Profile] senden möchten, müssen Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile] -Klasse basiert, die den Datentyp [!UICONTROL Einverständnis und Voreinstellungen] enthält. Der Datensatz, den Sie auf Grundlage dieses Schemas erstellen, muss auch für [!DNL Profile] aktiviert sein. Spezifische Schritte bezüglich der [!DNL Real-Time Customer Profile]-Anforderungen für Schemas und Datensätze finden Sie in den oben genannten Tutorials.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass sie die Datensätze priorisieren, die die neuesten Zustimmungs- und Voreinstellungsdaten enthalten, damit Kundenprofile korrekt aktualisiert werden. Weitere Informationen finden Sie in der Übersicht zu [Zusammenführungsrichtlinien](../../rtcdp/profile/merge-policies.md) .

## Handhabung von Zustimmungs- und Vorgabenänderungen

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort mit dem [Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md) erzwungen werden. Wenn ein Kunde die Datenerfassung ablehnt, muss die Datenerfassung sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten besuchten Seite keine Personalisierung vorhanden sein.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zum Datentyp [!UICONTROL Einverständnisse und Voreinstellungen].

### Akzeptierte Werte für `val` {#choice-values}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für die Zustimmung oder Präferenz entschieden. Mit anderen Worten, sie stimmen **do** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat sich von der Zustimmung oder Präferenz abgemeldet. Mit anderen Worten, sie stimmen **nicht** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungs- oder Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf &quot;`p`&quot;gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf &quot;`y`&quot;aktualisiert.<br><br>Wenn diese Einwilligung oder Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, kann stattdessen die Option `p` verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einwilligungsaufforderung reagiert hat. Sie können beispielsweise den Wert auf der ersten Seite einer Website automatisch auf &quot;`p`&quot;setzen, bevor der Kunde auf die Einwilligungsaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | Unbekannt | Die Einwilligungs- oder Präferenzinformationen des Kunden sind unbekannt. |
| `dy` | Standardwert Ja (Opt-in) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-in (&quot;Ja&quot;) behandelt. Mit anderen Worten, die Zustimmung wird angenommen, bis der Kunde etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `dn` | Standardwert Nein (Opt-out) | Der Kunde hat selbst keinen Zustimmungswert angegeben und wird standardmäßig als Opt-out (&quot;Nein&quot;) behandelt. Mit anderen Worten, es wird angenommen, dass der Kunde die Zustimmung verweigert hat, bis er etwas Anderes angibt.<br><br>Beachten Sie, dass Sie alle Profile, die Standardwerte enthalten, manuell aktualisieren müssen, wenn die Datenschutzrichtlinien Ihres Unternehmens Änderungen an den Standardeinstellungen einiger oder aller Benutzer zur Folge haben. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style="table-layout:auto"}

### Akzeptierte Werte für `preferred` {#preferred-values}

In der folgenden Tabelle sind die für `preferred` zulässigen Werte aufgeführt. Die Werte `preferred` geben den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an, über den er über Datenerfassung, Datenschutzrichtlinien und Personalisierungsoptionen informiert wird.

| Wert | Beschreibung |
| --- | --- |
| `email` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten per E-Mail an. |
| `push` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Push-Benachrichtigungen an. Hierbei handelt es sich um Nachrichten oder Warnhinweise, die direkt an ihr Gerät, häufig eine mobile Anwendung, gesendet werden. |
| `inApp` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von In-App-Nachrichten an. Diese Nachrichten werden in einer Mobile- oder Webanwendung bereitgestellt und geben Informationen an, während der Benutzer aktiv mit der App interagiert. |
| `sms` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten per SMS (Short Message Service) an. Dies sind Textnachrichten, die an ihr Mobiltelefon gesendet werden. |
| `phone` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten über Telefongespräche an. |
| `phyMail` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Materialien über physische Post an. |
| `inVehicle` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Erhalt von Benachrichtigungen während seiner Fahrt an. Diese Nachrichten können über Informationssysteme des Fahrzeugs oder andere Kommunikationskanäle im Fahrzeug übermittelt werden. |
| `inHome` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Empfang von Nachrichten zu Hause an. Diese Nachrichten können über intelligente Heimgeräte oder andere heimische Kommunikationskanäle bereitgestellt werden. |
| `iot` | Diese Voreinstellung bezeichnet die Zustimmung des Kunden zum Empfang von Nachrichten im Zusammenhang mit dem Internet der Dinge (IoT). Diese Nachrichten können über verbundene Geräte und Systeme in ihrer Umgebung bereitgestellt werden. |
| `social` | Diese Voreinstellung gibt die Zustimmung des Kunden zum Erhalt von Nachrichten über soziale Medienplattformen an. |
| `other` | Diese Voreinstellung umfasst Kanäle, die nicht in Standardkategorien passen. Es stellt alternative oder spezialisierte Kommunikationskanäle dar, die für ein bestimmtes Unternehmen oder eine bestimmte Branche spezifisch sein können. |
| `none` | Diese Voreinstellung zeigt an, dass der Kunde keinen bevorzugten Kommunikationskanal hat. |
| `unknown` | Diese Voreinstellung bedeutet, dass der bevorzugte Kommunikationskanal des Kunden nicht bekannt oder nicht angegeben ist. Dies kann vorkommen, wenn der Kunde keine ausdrückliche Einwilligung oder Präferenzinformationen erteilt hat. |

{style="table-layout:auto"}

### Vollständiges Schema für [!UICONTROL Einverständnisse und Voreinstellungen] {#full-schema}

Um das vollständige Schema für den Datentyp [!UICONTROL Zustimmungen und Voreinstellungen] anzuzeigen, lesen Sie das [offizielle XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
