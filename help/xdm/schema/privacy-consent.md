---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
title: Datentyp "Inhalt und Voreinstellungen"
description: Der Datentyp "Datenschutz/Marketing-Voreinstellungen (Zustimmung)"soll die Erfassung von Kundenberechtigungen und -einstellungen unterstützen, die von CMPs (Consent Management Platform) und anderen Quellen aus Ihren Datenvorgängen generiert werden.
topic: guide
translation-type: tm+mt
source-git-commit: 1a4dd167ecd4f4f61ffe26af786b355e4561b30d
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 1%

---


# [!DNL Consents & Preferences] Übersicht über den Datentyp

Der [!DNL Privacy/Marketing Preferences (Consent)] Datentyp (im Folgenden &quot;[!DNL Consents & Preferences] Datentyp&quot; genannt) ist ein [!DNL Experience Data Model] (XDM) Datentyp, der die Erfassung von Kundenberechtigungen und -einstellungen unterstützt, die von CMPs (Consent Management Platforms) und anderen Quellen aus Ihren Datenoperationen generiert werden.

Dieses Dokument umfasst die Struktur und die vorgesehene Verwendung der vom [!DNL Consents & Preferences] Datentyp bereitgestellten Felder.

## Voraussetzungen  {#prerequisites}

Dieses Dokument erfordert ein funktionierendes Verständnis von XDM und die Verwendung der Schema in [!DNL Experience Platform]. Bitte lesen Sie die folgende Dokumentation, bevor Sie fortfahren:

* [XDM-System – Übersicht](http://www.adobe.com/go/xdm-home-en)
* [Grundlagen der Schemakomposition](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Datentypstruktur {#structure}

>[!IMPORTANT]
>
>Der [!DNL Consents & Preferences] Datentyp deckt eine Reihe von Anwendungsfällen im Zusammenhang mit der Zustimmung und der Vorzugsverwaltung ab. In diesem Dokument wird daher die Verwendung der Felder des Datentyps allgemein beschrieben und es werden nur Vorschläge zur Interpretation der Verwendung dieser Felder gemacht. Bitte wenden Sie sich an Ihr Datenschutzrechtsteam, um die Struktur des Datentyps an die Interpretation und Präsentation dieser Einwilligung und Präferenz für Ihre Kunden anzupassen.

Der [!DNL Consents & Preferences] Datentyp enthält mehrere Felder, die zur Erfassung von **Informationen zur Einwilligung** und **Präferenz** verwendet werden.

Eine Einwilligung ist eine Option, mit der ein Kunde angeben kann, wie seine Daten verwendet werden können. Die meisten Zustimmungen haben einen rechtlichen Aspekt, da in einigen Rechtsordnungen eine Erlaubnis erforderlich ist, bevor Daten auf eine bestimmte Weise verwendet werden können, oder dass der Kunde die Möglichkeit hat, diese Verwendung zu beenden (Opt-out), wenn keine ausdrückliche Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde festlegen kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke behandelt werden sollen. Diese fallen in zwei Kategorien:

* **Voreinstellungen** für Personalisierung: Voreinstellungen für die Personalisierung der Erlebnisse, die ein Kunde von der Marke erhält.
* **Marketingvoreinstellungen**: Voreinstellungen, ob eine Marke über verschiedene Kanal mit einem Kunden in Kontakt treten darf.

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den der [!DNL Consents & Preferences] Datentyp verarbeiten kann. Informationen zur spezifischen Verwendung der einzelnen Felder finden Sie in den folgenden Abschnitten.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:any": {
        "xdm:val": "y",
      },
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Das obige Beispiel soll die Struktur der Daten veranschaulichen, die [!DNL Platform] über den [!DNL Consents & Preferences] Datentyp gesendet werden, um dem Rest dieses Dokuments einen Kontext zu geben, in dem die wichtigsten vom Datentyp bereitgestellten Felder erläutert werden. Das vollständige Schema für die Struktur des Datentyps finden Sie zu Referenzzwecken im [Anhang](#full-schema) .

## xdm:content {#choices}

`xdm:consents` enthält mehrere Felder, die die Zustimmung und Voreinstellungen eines Kunden beschreiben. Diese Felder werden in den Unterabschnitten weiter unten detailliert beschrieben.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:any": {
      "xdm:val": "y",
    },
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collection

`xdm:collect` die Einwilligung des Kunden zur Erfassung seiner Daten.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:val` | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

### xdm:adID

`xdm:adID` stellt die Zustimmung des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:val` | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

### xdm:share

`xdm:share` stellt die Zustimmung des Kunden dar, ob seine Daten an Dritte oder Zweitanbieter weitergegeben (oder an Dritte verkauft) werden können.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:val` | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

### xdm:personalize {#personalize}

`xdm:personalize` erfasst Kundenvoreinstellungen darüber, auf welche Weise ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Personalisierungs-Anwendungsfälle Opt-out oder ganz Opt-out Personalisierung.

>[!IMPORTANT]
>
>`xdm:personalize` umfasst nicht Anwendungsfälle für das Inverkehrbringen. Wenn ein Kunde beispielsweise die Personalisierung für alle Kanal ablehnt, sollte er nicht aufhören, über diese Kanal Nachrichten zu empfangen. Vielmehr sollten die Nachrichten, die sie erhalten, generisch sein und nicht auf ihrem Profil basieren.
>
>Wenn sich ein Kunde beispielsweise für alle Kanal (bis, `xdm:marketing`wie im [nächsten Abschnitt](#marketing)erläutert) vom Direktmarketing abmeldet, sollte er keine Nachrichten erhalten, selbst wenn eine Personalisierung zulässig ist.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:content` | Stellt die Voreinstellungen des Kunden für personalisierte Inhalte auf Ihrer Website oder in Ihrer Anwendung dar. |
| `xdm:val` | Die vom Kunden bereitgestellte Voreinstellung für die Personalisierung des angegebenen Anwendungsfalls. In Fällen, in denen der Kunde nicht aufgefordert werden muss, seine Zustimmung zu geben, sollte der Wert dieses Feldes die Grundlage angeben, auf der die Personalisierung erfolgen sollte. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

### xdm:marketing {#marketing}

`xdm:marketing` erfasst Kundenpräferenzen hinsichtlich der Marketingzwecke, für die ihre Daten verwendet werden können. Kunden können bestimmte Anwendungsfälle Opt-out oder ganz Opt-out Direktmarketing.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:preferred` | Gibt den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an. Zulässige Werte finden Sie im [Anhang](#preferred-values) . |
| `xdm:any` | Stellt die Präferenzen des Kunden für Direktmarketing als Ganzes dar. Die in diesem Feld angegebene Voreinstellung für die Zustimmung gilt als &quot;Standardeinstellung&quot;für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder im `xdm:marketing`Abschnitt &quot;Überschrieben&quot;außer Kraft gesetzt. Wenn Sie planen, detailliertere Optionen für die Zustimmung zu verwenden, sollten Sie dieses Feld ausschließen.<br><br>Wenn der Wert auf `n`festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y`festgelegt ist, sollten alle feinkörnigen Personalisierungsoptionen ebenfalls wie `y`folgt behandelt werden, es sei denn, explizit auf `n`. Wenn der Wert nicht festgelegt ist, sollten die Werte für die einzelnen Personalisierungsoptionen wie angegeben berücksichtigt werden. |
| `xdm:email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. |
| `xdm:push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen genehmigt. |
| `xdm:sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. |
| `xdm:val` | Die vom Kunden angegebene Voreinstellung für den angegebenen Verwendungsfall. In Fällen, in denen der Kunde nicht zur Erteilung der Zustimmung aufgefordert werden muss, sollte der Wert dieses Feldes die Grundlage angeben, auf der der Verwendungsfall für das Inverkehrbringen erfolgen sollte. Zulässige Werte und Definitionen finden Sie im [Anhang](#choice-values) . |
| `xdm:time` | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Marketing-Voreinstellung geändert hat (falls zutreffend). Beachten Sie, dass, wenn der Zeitstempel für eine individuelle Voreinstellung mit dem unter angegebenen Zeitstempel identisch ist `xdm:metadata`, dieses Feld nicht für diese Voreinstellung festgelegt werden kann. |
| `xdm:reason` | Wenn ein Kunde sich aus einer Marketing-Verwendungsszenario ausschließt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |

### xdm:idBestimmte

`xdm:idSpecific` kann verwendet werden, wenn eine bestimmte Zustimmung oder Präferenz nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde E-Mails an eine Adresse Opt-out und gleichzeitig E-Mails an eine andere Adresse senden.

>[!IMPORTANT]
>
>Einwilligungen und Voreinstellungen auf Kanal-Ebene (d. h. die `xdm:consents` `xdm:idSpecific`außerhalb von bereitgestellten) gelten für IDs in diesem Kanal. Daher wirken sich alle Zustimmung und Voreinstellungen auf Kanal-Ebene direkt darauf aus, ob entsprechende ID- oder gerätespezifische Einstellungen berücksichtigt werden:
>
>* Wenn der Kunde sich auf Kanal-Ebene abgewählt hat, werden alle entsprechenden Zustimmungen oder Voreinstellungen in ignoriert `xdm:idSpecific` .
>* Wenn die Zustimmung oder Präferenz des Kanal nicht festgelegt ist oder der Kunde sich dafür entschieden hat, werden die entsprechenden Zustimmungen oder Präferenzen in `xdm:idSpecific` der Kundenliste berücksichtigt.


Jeder Schlüssel im `xdm:idSpecific` Objekt stellt einen bestimmten Identitäts-Namensraum dar, der vom Adobe Experience Platform Identity Service erkannt wird. Sie können zwar eigene benutzerdefinierte Namensraum definieren, um verschiedene Bezeichner zu kategorisieren, es wird jedoch empfohlen, einen der vom Identitätsdienst bereitgestellten Standard-Namensraum zu verwenden, um die Datenspeicherung für das Echtzeit-Kundendienstprogramm zu reduzieren. Weitere Informationen zu Identitäts-Namensräumen finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/namespaces.md) in der Dokumentation zum Identitätsdienst.

Die Schlüssel für jedes Namensraum-Objekt stellen die eindeutigen Identitätswerte dar, für die der Kunde Voreinstellungen festgelegt hat. Jeder Identitätswert kann einen vollständigen Satz von Inhalten und Voreinstellungen enthalten, die auf dieselbe Weise formatiert werden wie `xdm:consents`.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metadata

`xdm:metadata` erfasst allgemeine Metadaten über die Zustimmung und Voreinstellungen des Kunden, wann immer sie zuletzt aktualisiert wurden.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm:time` | Ein Zeitstempel zum letzten Mal, wenn die Zustimmung und Voreinstellungen des Kunden aktualisiert wurden. Dieses Feld kann anstelle von Zeitstempeln für einzelne Voreinstellungen verwendet werden, um die Belastung und Komplexität zu reduzieren. Wenn Sie einen `xdm:time` Wert unter einer individuellen Voreinstellung angeben, wird der `xdm:metadata` Zeitstempel für diese bestimmte Voreinstellung außer Kraft gesetzt. |

## Daten mithilfe des Datentyps aufnehmen {#ingest}

Um den [!DNL Consents & Preferences] Datentyp zum Erfassen von Daten zur Einwilligung Ihrer Kunden verwenden zu können, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diesen Datentyp enthält.

Anweisungen zum Zuweisen von Datentypen zu Feldern finden Sie im Lernprogramm zum [Erstellen eines Schemas in der Benutzeroberfläche](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . Nachdem Sie ein Schema erstellt haben, das ein Feld mit dem [!DNL Consents & Preferences] Datentyp enthält, lesen Sie den Abschnitt zum [Erstellen eines Datensatzes](../../catalog/datasets/user-guide.md#create) im DataSet-Benutzerhandbuch. Befolgen Sie dabei die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema.

>[!IMPORTANT]
>
>Wenn Sie Genehmigungsdaten an senden möchten, müssen Sie ein [!DNL Real-time Customer Profile]aktiviertes Schema erstellen, das auf der [!DNL Profile]Klasse basiert, die den [!DNL XDM Individual Profile] [!DNL Consents & Preferences] Datentyp enthält. Der Datensatz, den Sie auf der Grundlage dieses Schemas erstellen, muss ebenfalls aktiviert werden [!DNL Profile]. Spezifische Schritte zu den [!DNL Real-time Customer Profile] Anforderungen für Schema und Datensätze finden Sie in den oben verlinkten Lernprogrammen.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass die Datasets, die die neuesten Einwilligungs- und Voreinstellungsdaten enthalten, priorisiert werden, damit die Profil der Kunden ordnungsgemäß aktualisiert werden. Weitere Informationen finden Sie in der Übersicht zu [Zusammenführungsrichtlinien](../../rtcdp/profile/merge-policies.md) .

## Bearbeitung von Änderungen der Zustimmung und der Präferenz

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen mit dem [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md)erfasst und sofort erzwungen werden. Wenn sich ein Kunde aus der Datenerfassung ausschließt, muss die Datenerfassung sofort eingestellt werden. Wenn sich ein Kunde aus der Personalisierung ausschließt, sollte auf der nächsten Seite, die er besucht, keine Personalisierung vorhanden sein.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zum [!DNL Consents & Preferences] Datentyp.

### Akzeptierte Werte für xdm:val {#choice-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:val`die

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Zustimmung oder den Vorzug entschieden. Mit anderen Worten, sie **stimmen** der Verwendung ihrer Daten gemäß der jeweiligen Zustimmung oder Präferenz zu. |
| `n` | Nein | Der Kunde hat sich von der Zustimmung oder Präferenz abgemeldet. Mit anderen Worten, sie stimmen **nicht** der Verwendung ihrer Daten zu, wie sie in der betreffenden Einwilligung oder Präferenz angegeben ist. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungs- oder Präferenzwert erhalten. Dies wird meistens im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Empfang von E-Mails entscheidet, wird diese Zustimmung auf `p` so lange eingestellt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung aktualisiert `y`.<br><br>Wenn diese Zustimmung oder Präferenz kein zweistufiges Überprüfungsverfahren verwendet, kann die `p` Auswahl stattdessen dazu verwendet werden, anzugeben, dass der Kunde noch nicht auf die Aufforderung zur Einwilligung reagiert hat. Sie können beispielsweise den Wert automatisch auf `p` der ersten Seite einer Website einstellen, bevor der Kunde auf die Aufforderung zur Einwilligung reagiert hat. In Gerichtsbarkeiten, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde sich nicht explizit abgemeldet hat (d. h. die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Zustimmung oder Präferenz des Kunden ist unbekannt. |
| `LI` | Rechtliches Interesse | Das legitime Geschäftsinteresse, diese Daten für den angegebenen Zweck zu erheben und zu verarbeiten, überwiegt den potenziellen Schaden, den sie dem Einzelnen verursachen. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertraglichen Verpflichtungen mit der Einzelperson nachzukommen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wesentliches Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist zum Schutz der vitalen Interessen des Einzelnen erforderlich. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten zu dem festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt durchzuführen. |

### Akzeptierte Werte für xdm:prefer {#preferred-values}

In der folgenden Tabelle sind die zulässigen Werte für `xdm:preferred`die

| Wert | Beschreibung |
| --- | --- |
| `email` | E-Mail-Nachrichten. |
| `push` | Push-Benachrichtigungen. |
| `inApp` | In-App-Nachrichten. |
| `sms` | SMS-Nachrichten. |
| `phone` | Telefonanrufinteraktionen. |
| `phyMail` | Physikalische Post. |
| `inVehicle` | Fahrzeuginterne Meldungen. |
| `inHome` | In-Home-Nachrichten. |
| `iot` | Internet der Dinge (IoT) Nachrichten. |
| `social` | Social-Media-Inhalte |
| `other` | Ein Kanal, der nicht in eine Standard-Kategorie passt. |
| `none` | Kein bevorzugter Kanal. |
| `unknown` | Der bevorzugte Kanal ist unbekannt. |

### Vollständiges [!DNL Consents & Preferences] Schema {#full-schema}

Um das vollständige Schema für den [!DNL Consents & Preferences] Datentyp Ansicht, rufen Sie das [offizielle XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consentpreferences.schema.json)auf.