---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Einverständnis; Einverständnis; Voreinstellungen; Voreinstellungen; privacyOptOuts; marketingPreferences; optOutType; baseOfProcessing; Einverständnis; Einverständnis
title: Datentyp "Einwilligungen und Voreinstellungen"
description: Der Datentyp Einverständnis für Datenschutz, Personalisierung und Marketing-Voreinstellungen soll die Erfassung von Kundenberechtigungen und -präferenzen unterstützen, die von CMPs (Consent Management Platform) und anderen Quellen aus Ihren Datenvorgängen generiert werden.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 2%

---

# [!UICONTROL Einverständnis und Voreinstellungen] Datentyp

Die [!UICONTROL Einverständnis für Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen] Datentyp (nachstehend &quot;Datentyp&quot; genannt)[!UICONTROL Einverständnis und Voreinstellungen] Datentyp&quot;) ist ein [!DNL Experience Data Model] (XDM)-Datentyp, der die Erfassung von Kundenberechtigungen und -voreinstellungen unterstützt, die von Consent Management Platform (CMPs) und anderen Quellen aus Ihren Datenvorgängen generiert werden.

In diesem Dokument werden die Struktur und die beabsichtigte Verwendung der Felder beschrieben, die von der [!UICONTROL Einverständnis und Voreinstellungen] Datentyp.

## Voraussetzungen {#prerequisites}

Dieses Dokument erfordert ein Verständnis von XDM und die Verwendung der Schemas in [!DNL Experience Platform]. Lesen Sie die folgende Dokumentation, bevor Sie fortfahren:

* [XDM-System – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de)
* [Grundlagen der Schemakomposition](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Datentypstruktur {#structure}

>[!IMPORTANT]
>
>Die [!UICONTROL Einverständnis und Voreinstellungen] Der Datentyp ist für eine Reihe von Nutzungsszenarios im Zusammenhang mit der Einwilligungs- und Vorgabenverwaltung konzipiert. In diesem Dokument wird daher die Verwendung der Felder des Datentyps allgemein beschrieben und es werden nur Vorschläge zur Interpretation der Verwendung dieser Felder gemacht. Wenden Sie sich an Ihr Datenschutzrechtsteam, um die Struktur des Datentyps an die Interpretation und Präsentation dieser Zustimmungs- und Auswahlmöglichkeiten für Ihre Kunden anzupassen.

Die [!UICONTROL Einverständnis und Voreinstellungen] Datentyp bietet mehrere Felder, die zum Erfassen von **Einverständnis** und **Voreinstellung** Informationen.

Eine Einwilligung ist eine Option, mit der ein Kunde festlegen kann, wie seine Daten verwendet werden können. Die meisten Einverständniserklärungen haben einen rechtlichen Aspekt, da in einigen Rechtsordnungen eine Erlaubnis erforderlich ist, bevor Daten in einer bestimmten Weise verwendet werden können, oder der Kunde die Möglichkeit hat, diese Verwendung zu stoppen (Opt-out), wenn keine Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde festlegen kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke behandelt werden sollen. Diese Kategorien fallen in zwei Kategorien:

* **Personalisierungseinstellungen**: Voreinstellungen bezüglich der Personalisierung von Erlebnissen, die für einen Kunden bereitgestellt werden.
* **Marketing-Voreinstellungen**: Einstellungen, die angeben, ob eine Marke einen Kunden über verschiedene Kanäle kontaktieren darf.

Der folgende Screenshot zeigt, wie die Struktur des Datentyps in der Platform-Benutzeroberfläche dargestellt wird:

![](../images/data-types/consents.png)

>[!TIP]
>
>Siehe Handbuch unter [Erkunden von XDM-Ressourcen](../ui/explore.md) zu finden, wie Sie eine beliebige XDM-Ressource nachschlagen und ihre Struktur in der Platform-Benutzeroberfläche überprüfen können.

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, bei dem die [!UICONTROL Einverständnis und Voreinstellungen] Datentyp verarbeitet werden kann. Informationen zur spezifischen Verwendung dieser Felder finden Sie in den folgenden Abschnitten.

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
>* [Beispieldaten in der API generieren](../api/sample-data.md)


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

`collect` stellt die Einwilligung des Kunden zur Erfassung seiner Daten dar.

```json
"collect": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `adID`

`adID` stellt die Zustimmung des Kunden dar, ob eine Advertiser-ID verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `idType` | Der Anzeigen-ID-Typ, entweder `IDFA` für Apple ID für Advertiser oder `GAID` für die Advertiser-ID von Google, auch Android Advertiser ID (AAID) genannt. |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `share`

`share` stellt die Einwilligung des Kunden dar, ob seine Daten an Zweit- oder Dritte weitergegeben (oder an Dritte verkauft) werden können.

```json
"share": {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` erfasst Kundenpräferenzen darüber, auf welche Weise ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Anwendungsfälle der Personalisierung deaktivieren oder die Personalisierung vollständig deaktivieren.

>[!IMPORTANT]
>
>`personalize` umfasst keine Marketing-Anwendungsfälle. Wenn beispielsweise ein Kunde die Personalisierung für alle Kanäle ablehnt, sollte er nicht aufhören, Nachrichten über diese Kanäle zu empfangen. Stattdessen sollten die Nachrichten, die sie empfangen, generisch sein und nicht auf ihrem Profil basieren.
>
>Im selben Beispiel, wenn ein Kunde das direkte Marketing für alle Kanäle (über `marketing`, erläutert im Abschnitt [nächster Abschnitt](#marketing)), sollte dieser Kunde keine Nachrichten erhalten, selbst wenn eine Personalisierung zulässig ist.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `content` | Stellt die Voreinstellungen des Kunden für personalisierte Inhalte auf Ihrer Website oder in Ihrer Anwendung dar. |
| `val` | Die vom Kunden bereitgestellte Personalisierungseinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht zur Einwilligung aufgefordert werden muss, sollte der Wert dieses Felds die Grundlage angeben, auf der die Personalisierung erfolgen soll. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |

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
| `preferred` | Gibt den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an. Siehe [Anhang](#preferred-values) für gültige Werte. |
| `any` | Stellt die Voreinstellungen des Kunden für Direktmarketing als Ganzes dar. Die in diesem Feld bereitgestellte Zustimmungsvoreinstellung gilt als &quot;Standardeinstellung&quot;für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder überschrieben, die unter `marketing`. Wenn Sie planen, detailliertere Zustimmungsoptionen zu verwenden, wird empfohlen, dieses Feld auszuschließen.<br><br>Wenn der Wert auf `n`festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y`festgelegt ist, sollten alle genaueren Personalisierungsoptionen ebenfalls wie folgt behandelt werden: `y`, es sei denn, explizit auf `n`. Wenn der Wert nicht festgelegt ist, sollten die Werte für jede Personalisierungsoption wie angegeben berücksichtigt werden. |
| `email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. |
| `push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen gestattet. |
| `sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. |
| `val` | Die vom Kunden angegebene Voreinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht aufgefordert werden muss, seine Zustimmung zu erteilen, sollte der Wert dieses Felds die Grundlage angeben, auf der der Marketing-Anwendungsfall stattfinden soll. Siehe [Anhang](#choice-values) für akzeptierte Werte und Definitionen. |
| `time` | Ein ISO 8601-Zeitstempel, mit dem die Marketing-Voreinstellung geändert wurde (falls zutreffend). Beachten Sie Folgendes: Wenn der Zeitstempel für eine individuelle Voreinstellung mit dem unter `metadata`festgelegt ist, wird dieses Feld nicht für diese Voreinstellung festgelegt. |
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
| `time` | Ein ISO 8601-Zeitstempel zum letzten Mal, wenn die Zustimmungen und Voreinstellungen des Kunden aktualisiert wurden. Dieses Feld kann verwendet werden, anstatt Zeitstempel auf individuelle Voreinstellungen anzuwenden, um Belastung und Komplexität zu reduzieren. Bereitstellung einer `time` Wert unter einer individuellen Voreinstellung setzt die `metadata` Zeitstempel für diese bestimmte Voreinstellung. |

{style="table-layout:auto"}

## Daten mithilfe des Datentyps erfassen {#ingest}

Um die [!UICONTROL Einverständnis und Voreinstellungen] -Datentyp verwenden, um Einwilligungsdaten von Ihren Kunden zu erfassen, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diesen Datentyp enthält.

Siehe Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) für Schritte zum Zuweisen von Datentypen zu Feldern. Nachdem Sie ein Schema erstellt haben, das ein Feld mit der [!UICONTROL Einverständnis und Voreinstellungen] Datentyp, siehe Abschnitt . [Erstellen eines Datensatzes](../../catalog/datasets/user-guide.md#create) Führen Sie im Benutzerhandbuch zu Datensätzen die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema aus.

>[!IMPORTANT]
>
>Wenn Sie Einwilligungsdaten an senden möchten [!DNL Real-Time Customer Profile]müssen Sie eine [!DNL Profile]-aktiviertes Schema basierend auf dem [!DNL XDM Individual Profile] -Klasse, die die [!UICONTROL Einverständnis und Voreinstellungen] Datentyp. Der Datensatz, den Sie auf Grundlage dieses Schemas erstellen, muss auch für [!DNL Profile]. Spezifische Schritte zu [!DNL Real-Time Customer Profile] Anforderungen für Schemas und Datensätze.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass sie die Datensätze priorisieren, die die neuesten Zustimmungs- und Voreinstellungsdaten enthalten, damit Kundenprofile korrekt aktualisiert werden. Siehe Übersicht unter [Zusammenführungsrichtlinien](../../rtcdp/profile/merge-policies.md) für weitere Informationen.

## Handhabung von Zustimmungs- und Vorgabenänderungen

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort mit der [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Wenn ein Kunde die Datenerfassung ablehnt, muss die Datenerfassung sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten besuchten Seite keine Personalisierung vorhanden sein.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zu den [!UICONTROL Einverständnis und Voreinstellungen] Datentyp.

### Akzeptierte Werte für `val` {#choice-values}

In der folgenden Tabelle sind die für `val`:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja (Opt-in) | Der Kunde hat sich für die Zustimmung oder Präferenz entschieden. Mit anderen Worten, sie **do** Zustimmung zur Verwendung ihrer Daten, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `n` | Nein (Opt-out) | Der Kunde hat sich von der Zustimmung oder Präferenz abgemeldet. Mit anderen Worten, sie **nicht** Zustimmung zur Verwendung ihrer Daten, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungs- oder Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf `p` bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat; an diesem Punkt würde die Zustimmung auf `y`.<br><br>Wenn dieses Einverständnis oder diese Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, wird die `p` choice kann stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einverständnisaufforderung reagiert hat. Sie können beispielsweise den Wert automatisch auf `p` auf der ersten Seite einer Website, bevor der Kunde auf die Einwilligungsaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
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

In der folgenden Tabelle sind die für `preferred`:

| Wert | Beschreibung |
| --- | --- |
| `email` | E-Mail-Nachrichten. |
| `push` | Push-Benachrichtigungen. |
| `inApp` | In-App-Nachrichten. |
| `sms` | SMS-Nachrichten. |
| `phone` | Interaktionen mit Telefonaufrufen. |
| `phyMail` | Physische Post. |
| `inVehicle` | In-Vehicle-Nachrichten. |
| `inHome` | In-Home-Nachrichten. |
| `iot` | Internet der Nachrichten (IoT). |
| `social` | Social-Media-Inhalte. |
| `other` | Ein Kanal, der nicht in eine Standardkategorie passt. |
| `none` | Kein bevorzugter Kanal. |
| `unknown` | Der bevorzugte Kanal ist unbekannt. |

{style="table-layout:auto"}

### Voll [!UICONTROL Einverständnis und Voreinstellungen] schema {#full-schema}

So zeigen Sie das vollständige Schema für die [!UICONTROL Einverständnis und Voreinstellungen] Datentyp, siehe [Offizielles XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
