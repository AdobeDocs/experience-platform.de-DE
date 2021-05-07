---
solution: Experience Platform
title: Schema-Feldgruppe "Datenschutz/Personalisierung/Marketing-Voreinstellungen"(Zusätze)
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die Feldgruppe "Datenschutz/Personalisierung/Marketing-Voreinstellungen"(Schema).
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2280'
ht-degree: 1%

---

# [!UICONTROL Feldgruppe &quot;Datenschutz/Personalisierung/Marketing-Voreinstellungen&quot;(Zustimmung)] 

[!UICONTROL Datenschutz/Personalisierung/Marketing-Voreinstellungen (Zustimmungen)]  (im Folgenden &quot; [!DNL Privacy & Consents] Feldgruppe&quot;genannt) ist eine Standardfeldgruppe für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md), die zur Erfassung von Informationen zur Kundenzustimmung und zu den Kundenpräferenzen verwendet wird.

>[!NOTE]
>
>Da diese Feldgruppe nur mit [!DNL XDM Individual Profile] kompatibel ist, kann sie nicht für [!DNL XDM ExperienceEvent]-Schema verwendet werden. Wenn Sie Daten zur Einwilligung und Voreinstellung in Ihr Experience Ereignis-Schema einbeziehen möchten, fügen Sie den Datentyp [[!UICONTROL Einwilligung zum Datenschutz, zur Personalisierung und zu Marketingeinstellungen]](../../data-types/consents.md) mithilfe einer [benutzerspezifischen Feldgruppe](../../ui/resources/field-groups.md#create) dem Schema hinzu.

## Feldgruppenstruktur {#structure}

>[!IMPORTANT]
>
>Die Feldgruppe [!DNL Consents & Preferences] deckt eine Reihe von Anwendungsfällen im Zusammenhang mit der Zustimmung und der Präferenzverwaltung ab. In diesem Dokument wird daher die Verwendung der Felder der Feldgruppe allgemein beschrieben und es werden nur Vorschläge zur Interpretation der Verwendung dieser Felder gemacht. Bitte wenden Sie sich an Ihr Datenschutzrechtsteam, um die Struktur der Feldgruppe mit der Interpretation und Präsentation dieser Einwilligung und Präferenz für Ihre Kunden abzustimmen.

Die Feldgruppe [!DNL Consents & Preferences] enthält mehrere Felder, die zum Erfassen von **Einwilligung**- und **Voreinstellungen**-Informationen verwendet werden.

Eine Einwilligung ist eine Option, mit der ein Kunde angeben kann, wie seine Daten verwendet werden können. Die meisten Zustimmungen haben einen rechtlichen Aspekt, da in einigen Rechtsordnungen eine Erlaubnis erforderlich ist, bevor Daten auf eine bestimmte Weise verwendet werden können, oder dass der Kunde die Möglichkeit hat, diese Verwendung zu beenden (Opt-out), wenn keine ausdrückliche Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde festlegen kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke behandelt werden sollen. Diese fallen in zwei Kategorien:

* **Voreinstellungen** für Personalisierung: Voreinstellungen für die Personalisierung der Erlebnisse, die ein Kunde von der Marke erhält.
* **Marketingvoreinstellungen**: Voreinstellungen, ob eine Marke über verschiedene Kanal mit einem Kunden in Kontakt treten darf.

Der folgende Screenshot zeigt, wie die Struktur der Feldgruppe in der Plattform-Benutzeroberfläche dargestellt wird:

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Anweisungen zum Suchen von XDM-Ressourcen](../../ui/explore.md) und zum Überprüfen ihrer Struktur in der Plattform-Benutzeroberfläche finden Sie im Handbuch [XDM-Ressourcen .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den die Feldgruppe [!DNL Consents & Preferences] verarbeiten kann. Informationen zur spezifischen Verwendung der einzelnen Felder finden Sie in den folgenden Abschnitten.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
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
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in der Experience Platform definieren, um zu veranschaulichen, wie Ihre Daten zur Kundeneinwilligung und zu den Kundenpräferenzen zugeordnet werden sollen. Weitere Informationen finden Sie in der folgenden Dokumentation:
>
>* [Musterdaten in der Benutzeroberfläche generieren](../../ui/sample.md)
>* [Musterdaten in der API generieren](../../api/sample-data.md)


## Anwendungsfälle vor Ort

Die Verwendungsfälle für jedes dieser Felder sind in den folgenden Abschnitten aufgeführt.

### `collect`

`collect` die Einwilligung des Kunden zur Erfassung seiner Daten.

```json
"collect" : {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Akzeptierte Werte und Definitionen finden Sie im Anhang [a1/>.](#choice-values) |

### `share`

`share` stellt die Zustimmung des Kunden dar, ob seine Daten an Dritte oder Zweitanbieter weitergegeben (oder an Dritte verkauft) werden können.

```json
"share" : {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden angegebene Auswahl der Zustimmung für diesen Verwendungsfall. Akzeptierte Werte und Definitionen finden Sie im Anhang [a1/>.](#choice-values) |

### `personalize` {#personalize}

`personalize` erfasst Kundenvoreinstellungen darüber, auf welche Weise ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Personalisierungs-Anwendungsfälle Opt-out oder ganz Opt-out Personalisierung.

>[!IMPORTANT]
>
>`personalize` umfasst nicht Anwendungsfälle für das Inverkehrbringen. Wenn ein Kunde beispielsweise die Personalisierung für alle Kanal ablehnt, sollte er nicht aufhören, über diese Kanal Nachrichten zu empfangen. Vielmehr sollten die Nachrichten, die sie erhalten, generisch sein und nicht auf ihrem Profil basieren.
>
>Wenn sich ein Kunde beispielsweise für alle Kanal (über `marketing`, wie im [nächsten Abschnitt](#marketing) erklärt) vom Direktmarketing abmeldet, sollte dieser Kunde keine Nachrichten erhalten, auch wenn eine Personalisierung zulässig ist.

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
| `val` | Die vom Kunden bereitgestellte Voreinstellung für die Personalisierung des angegebenen Anwendungsfalls. In Fällen, in denen der Kunde nicht aufgefordert werden muss, seine Zustimmung zu geben, sollte der Wert dieses Feldes die Grundlage angeben, auf der die Personalisierung erfolgen sollte. Akzeptierte Werte und Definitionen finden Sie im Anhang [a1/>.](#choice-values) |

### `marketing` {#marketing}

`marketing` erfasst Kundenpräferenzen hinsichtlich der Marketingzwecke, für die ihre Daten verwendet werden können. Kunden können bestimmte Anwendungsfälle Opt-out oder ganz Opt-out Direktmarketing.

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
| `preferred` | Gibt den bevorzugten Kanal des Kunden für den Empfang von Nachrichten an. Die zulässigen Werte finden Sie im Anhang [a1/>.](#preferred-values) |
| `any` | Stellt die Präferenzen des Kunden für Direktmarketing als Ganzes dar. Die in diesem Feld angegebene Voreinstellung für die Zustimmung gilt als &quot;Standard&quot; für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder unter `marketing` überschrieben. Wenn Sie planen, detailliertere Optionen für die Zustimmung zu verwenden, sollten Sie dieses Feld ausschließen.<br><br>Wenn der Wert auf  `n`festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y` festgelegt ist, sollten alle feiner abgestuften Personalisierungsoptionen ebenfalls als `y` behandelt werden, es sei denn, es wurde explizit auf `n` eingestellt. Wenn der Wert nicht festgelegt ist, sollten die Werte für die einzelnen Personalisierungsoptionen wie angegeben berücksichtigt werden. |
| `email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. Der Kunde kann in diesem Kanal auch individuelle Abonnement vorziehen. Weitere Informationen finden Sie im folgenden Abschnitt zu [Abonnements](#subscriptions). |
| `push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen genehmigt. Der Kunde kann in diesem Kanal auch individuelle Abonnement vorziehen. Weitere Informationen finden Sie im folgenden Abschnitt zu [Abonnements](#subscriptions). |
| `sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. Der Kunde kann in diesem Kanal auch individuelle Abonnement vorziehen. Weitere Informationen finden Sie im folgenden Abschnitt zu [Abonnements](#subscriptions). |
| `val` | Die vom Kunden angegebene Voreinstellung für den angegebenen Verwendungsfall. In Fällen, in denen der Kunde nicht zur Erteilung der Zustimmung aufgefordert werden muss, sollte der Wert dieses Feldes die Grundlage angeben, auf der der Verwendungsfall für das Inverkehrbringen erfolgen sollte. Akzeptierte Werte und Definitionen finden Sie im Anhang [a1/>.](#choice-values) |
| `time` | Ein Zeitstempel nach ISO 8601, der angibt, wann sich die Marketing-Voreinstellung geändert hat (falls zutreffend). Beachten Sie, dass, wenn der Zeitstempel für eine individuelle Voreinstellung mit dem unter `metadata` angegebenen Zeitstempel übereinstimmt, dieses Feld nicht für diese Voreinstellung festgelegt werden muss. |
| `reason` | Wenn ein Kunde sich aus einer Marketing-Verwendungsszenario ausschließt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |

#### `subscriptions` {#subscriptions}

Die `email`-, `push`- und `sms`-Eigenschaften des `marketing`-Objekts können Kundendaten für diese Kanal darstellen. Dies wird erreicht, indem dem betreffenden Marketing-Kanal eine `subscriptions`-Eigenschaft hinzugefügt wird.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Der Abonnement-Typ. Hierbei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, vorausgesetzt, diese darf nicht länger als 15 Zeichen sein. |
| `subscribers` | Ein optionales Kartenfeld, das einen Satz von Bezeichnern (wie E-Mail-Adressen oder Telefonnummern) darstellt, die ein bestimmtes Abonnement abonniert haben. Jeder Schlüssel in diesem Objekt stellt den betreffenden Bezeichner dar und enthält zwei Untereigenschaften: <ul><li>`time`: Ein ISO 8601-Zeitstempel zum Zeitpunkt des Abonnements der Identität, falls zutreffend.</li><li>`source`: Die Quelle, von der der Abonnent stammt. Hierbei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, vorausgesetzt, diese darf nicht länger als 15 Zeichen sein.</li></ul> |


### `metadata`

`metadata` erfasst allgemeine Metadaten über die Zustimmung und Voreinstellungen des Kunden, wann immer sie zuletzt aktualisiert wurden.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `time` | Ein ISO 8601-Zeitstempel zum letzten Mal, wenn die Zustimmung und Voreinstellungen des Kunden aktualisiert wurden. Dieses Feld kann anstelle von Zeitstempeln für einzelne Voreinstellungen verwendet werden, um die Belastung und Komplexität zu reduzieren. Wenn Sie einen `time`-Wert unter einer individuellen Voreinstellung angeben, wird der `metadata`-Zeitstempel für diese bestimmte Voreinstellung außer Kraft gesetzt. |

### `idSpecific`

`idSpecific` kann verwendet werden, wenn eine bestimmte Zustimmung oder Präferenz nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde E-Mails an eine Adresse Opt-out und gleichzeitig E-Mails an eine andere Adresse senden.

>[!IMPORTANT]
>
>Einwilligungen und Voreinstellungen auf Kanal-Ebene (d. h. die unter `consents` außerhalb von `idSpecific` bereitgestellten) gelten für IDs in diesem Kanal. Daher wirken sich alle Zustimmung und Voreinstellungen auf Kanal-Ebene direkt darauf aus, ob entsprechende ID- oder gerätespezifische Einstellungen berücksichtigt werden:
>
>* Wenn der Kunde sich auf Kanal-Ebene abgemeldet hat, werden alle entsprechenden Zustimmungen oder Voreinstellungen in `idSpecific` ignoriert.
>* Wenn die Einwilligung oder Präferenz des Kanals nicht festgelegt ist oder der Kunde sich dafür entschieden hat, werden die entsprechenden Einwilligungen oder Präferenzen in `idSpecific` berücksichtigt.


Jeder Schlüssel im `idSpecific`-Objekt stellt einen bestimmten, vom Adobe Experience Platform-Identitätsdienst erkannten Namensraum dar. Sie können zwar eigene benutzerdefinierte Namensraum definieren, um verschiedene Bezeichner zu kategorisieren, es wird jedoch empfohlen, einen der vom Identitätsdienst bereitgestellten Standard-Namensraum zu verwenden, um die Datenspeicherung für das Echtzeit-Kundendienstprogramm zu reduzieren. Weitere Informationen zu Identitäts-Namensräumen finden Sie unter [Übersicht über Identitäts-Namensraum](../../../identity-service/namespaces.md) in der Dokumentation zum Identitätsdienst.

Die Schlüssel für jedes Namensraum-Objekt stellen die eindeutigen Identitätswerte dar, für die der Kunde Voreinstellungen festgelegt hat. Jeder Identitätswert kann einen vollständigen Satz von Inhalten und Voreinstellungen enthalten, die auf dieselbe Weise wie `consents` formatiert sind.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Innerhalb der im Abschnitt `idSpecific` bereitgestellten Objekte werden die Felder `any` und `preferred` nicht unterstützt. `marketing` Diese Felder können nur auf Benutzerebene konfiguriert werden. Darüber hinaus unterstützen die Marketing-Voreinstellungen für `email`, `sms` und `push` die Felder `subscriptions` nicht.`idSpecific`

Es gibt auch eine Einwilligung, die nur im Abschnitt `idSpecific` bereitgestellt werden kann: `adID`. Dieses Feld wird im Unterabschnitt unten behandelt.

#### `adID`

Die `adID`-Einwilligung stellt die Einwilligung des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen. Dieser Wert kann nur unter dem Identitätskennzeichen `ECID` im Namensraum `idSpecific` konfiguriert werden und kann nicht für andere Namensraum oder auf Benutzerebene für diese Feldgruppe festgelegt werden.

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Es wird nicht erwartet, dass Sie diesen Wert direkt festlegen, da das Adobe Experience Platform Mobile SDK ihn bei Bedarf automatisch einstellt.

## Daten mit der Feldgruppe {#ingest} eingehen

Um die [!DNL Consents & Preferences]-Feldgruppe zum Erfassen von Genehmigungsdaten von Ihren Kunden zu verwenden, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diese Feldgruppe enthält.

Anweisungen zum Zuweisen von Feldgruppen zu Feldern finden Sie im Lernprogramm unter [Erstellen eines Schemas in der Benutzeroberfläche](http://www.adobe.com/go/xdm-schema-editor-tutorial-en). Nachdem Sie ein Schema erstellt haben, das ein Feld mit der Feldgruppe [!DNL Consents & Preferences] enthält, lesen Sie den Abschnitt [Erstellen eines Datensatzes](../../../catalog/datasets/user-guide.md#create) im DataSet-Benutzerhandbuch, wie Sie einen Datensatz mit einem vorhandenen Schema erstellen.

>[!IMPORTANT]
>
>Wenn Sie Genehmigungsdaten an [!DNL Real-time Customer Profile] senden möchten, müssen Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile]-Klasse basiert, die die [!DNL Consents & Preferences]-Feldgruppe enthält. Der Datensatz, den Sie anhand dieses Schemas erstellen, muss auch für [!DNL Profile] aktiviert werden. In den oben verlinkten Lernprogrammen finden Sie spezifische Schritte zu [!DNL Real-time Customer Profile]-Anforderungen für Schema und Datensätze.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass die Datasets, die die neuesten Einwilligungs- und Voreinstellungsdaten enthalten, priorisiert werden, damit die Profil der Kunden ordnungsgemäß aktualisiert werden. Weitere Informationen finden Sie in der Übersicht zu [Mergepolicies](../../../rtcdp/profile/merge-policies.md).

## Bearbeitung von Änderungen der Zustimmung und der Präferenz

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen mit dem [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md) erfasst und sofort erzwungen werden. Wenn sich ein Kunde aus der Datenerfassung ausschließt, muss die Datenerfassung sofort eingestellt werden. Wenn sich ein Kunde aus der Personalisierung ausschließt, sollte auf der nächsten Seite, die er besucht, keine Personalisierung vorhanden sein.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zur Feldgruppe [!DNL Consents & Preferences].

### Akzeptierte Werte für `val` {#choice-values}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Zustimmung oder den Vorzug entschieden. Mit anderen Worten, sie stimmen der Verwendung ihrer Daten gemäß der jeweiligen Zustimmung oder Präferenz zu.**** |
| `n` | Nein | Der Kunde hat sich von der Zustimmung oder Präferenz abgemeldet. Mit anderen Worten, sie **stimmen der Verwendung ihrer Daten nicht** zu, wie in der betreffenden Einwilligung oder Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungs- oder Präferenzwert erhalten. Dies wird meistens im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Empfang von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um sicherzustellen, dass er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Wenn diese Zustimmung oder Präferenz kein zweistufiges Überprüfungsverfahren verwendet, kann die  `p` Auswahl stattdessen dazu verwendet werden, anzugeben, dass der Kunde noch nicht auf die Aufforderung zur Einwilligung reagiert hat. Beispielsweise können Sie den Wert auf der ersten Seite einer Website automatisch auf `p` einstellen, bevor der Kunde auf die Aufforderung zur Einwilligung reagiert hat. In Gerichtsbarkeiten, die keine ausdrückliche Zustimmung erfordern, können Sie diese auch verwenden, um anzugeben, dass der Kunde sich nicht explizit abgemeldet hat (d. h. die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Zustimmung oder Präferenz des Kunden ist unbekannt. |
| `LI` | Rechtliches Interesse | Das legitime Geschäftsinteresse, diese Daten für den angegebenen Zweck zu erheben und zu verarbeiten, überwiegt den potenziellen Schaden, den sie dem Einzelnen verursachen. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertraglichen Verpflichtungen mit der Einzelperson nachzukommen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wesentliches Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist zum Schutz der vitalen Interessen des Einzelnen erforderlich. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten zu dem festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt durchzuführen. |

### Akzeptierte Werte für `preferred` {#preferred-values}

In der folgenden Tabelle sind die für `preferred` zulässigen Werte aufgeführt:

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

Informationen zur Ansicht des vollständigen Schemas für die Feldgruppe [!DNL Consents & Preferences] finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
