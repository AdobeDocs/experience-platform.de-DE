---
solution: Experience Platform
title: Einverständnis und Voreinstellungsfeldgruppe
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemafeldergruppe "Einwilligungen und Voreinstellungen".
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '2316'
ht-degree: 2%

---

# [!UICONTROL Feldergruppe &quot;Einwilligungen und ] Voreinstellungen&quot;

[!UICONTROL Zustimmung und ]Voreinstellung sind eine Standardfeldgruppe für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md), die zum Erfassen der Kundenzustimmung und der Präferenzinformationen verwendet wird.

>[!NOTE]
>
>Da diese Feldergruppe nur mit [!DNL XDM Individual Profile] kompatibel ist, kann sie nicht für [!DNL XDM ExperienceEvent] -Schemata verwendet werden. Wenn Sie Einwilligungs- und Präferenzdaten in Ihr Erlebnisereignis-Schema aufnehmen möchten, fügen Sie den Datentyp [[!UICONTROL Einverständnis für Datenschutz, Personalisierung und Marketing-Voreinstellungen]](../../data-types/consents.md) zum Schema hinzu, indem Sie stattdessen eine [benutzerdefinierte Feldergruppe](../../ui/resources/field-groups.md#create) verwenden.

## Feldgruppenstruktur {#structure}

>[!IMPORTANT]
>
>Die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] deckt eine Reihe von Nutzungsszenarien für die Einwilligungs- und Vorgabenverwaltung ab. In diesem Dokument wird daher die Verwendung der Felder der Feldergruppe im Allgemeinen beschrieben und es werden nur Vorschläge zur Interpretation der Verwendung dieser Felder gemacht. Wenden Sie sich an Ihr Datenschutzrechtsteam, um die Struktur der Feldergruppe an die Interpretation und Präsentation dieser Zustimmungs- und Präferenzoptionen durch Ihre Organisation zu richten.

Die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] enthält mehrere Felder, mit denen **Einverständnis** und **Voreinstellungen** erfasst werden.

Eine Einwilligung ist eine Option, mit der ein Kunde festlegen kann, wie seine Daten verwendet werden können. Die meisten Einverständniserklärungen haben einen rechtlichen Aspekt, da in einigen Rechtsordnungen eine Erlaubnis erforderlich ist, bevor Daten in einer bestimmten Weise verwendet werden können, oder der Kunde die Möglichkeit hat, diese Verwendung zu stoppen (Opt-out), wenn keine Zustimmung erforderlich ist.

Eine Präferenz ist eine Option, mit der der Kunde festlegen kann, wie verschiedene Aspekte seines Erlebnisses mit einer Marke behandelt werden sollen. Diese Kategorien fallen in zwei Kategorien:

* **Personalisierungsvoreinstellungen**: Voreinstellungen bezüglich der Personalisierung von Erlebnissen, die für einen Kunden bereitgestellt werden.
* **Marketing-Voreinstellungen**: Einstellungen, die angeben, ob eine Marke einen Kunden über verschiedene Kanäle kontaktieren darf.

Der folgende Screenshot zeigt, wie die Struktur der Feldergruppe in der Platform-Benutzeroberfläche dargestellt wird:

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Anweisungen zum Suchen nach einer beliebigen XDM-Ressource und zum Überprüfen ihrer Struktur in der Platform-Benutzeroberfläche finden Sie im Handbuch zu [XDM-Ressourcen](../../ui/explore.md) zu .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] verarbeiten kann. Informationen zur spezifischen Verwendung dieser Felder finden Sie in den folgenden Abschnitten.

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
>Sie können JSON-Beispieldaten für jedes XDM-Schema generieren, das Sie in Experience Platform definieren, um zu veranschaulichen, wie Ihre Kundenzustimmungs- und -bevorzugte Daten zugeordnet werden sollen. Weitere Informationen finden Sie in der folgenden Dokumentation:
>
>* [Generieren von Beispieldaten in der Benutzeroberfläche](../../ui/sample.md)
* [Beispieldaten in der API generieren](../../api/sample-data.md)


## Anwendungsfälle für Felder

Die vorgesehenen Anwendungsfälle für jedes dieser Felder finden Sie in den folgenden Abschnitten.

### `collect`

`collect` stellt die Einwilligung des Kunden zur Erfassung seiner Daten dar.

```json
"collect" : {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` stellt die Einwilligung des Kunden dar, ob seine Daten an Zweit- oder Dritte weitergegeben (oder an Dritte verkauft) werden können.

```json
"share" : {
  "val": "y"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `val` | Die vom Kunden bereitgestellte Entscheidung für die Zustimmung für diesen Anwendungsfall. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` erfasst Kundenpräferenzen darüber, auf welche Weise ihre Daten für die Personalisierung verwendet werden können. Kunden können bestimmte Anwendungsfälle der Personalisierung deaktivieren oder die Personalisierung vollständig deaktivieren.

>[!IMPORTANT]
`personalize` umfasst keine Marketing-Anwendungsfälle. Wenn beispielsweise ein Kunde die Personalisierung für alle Kanäle ablehnt, sollte er nicht aufhören, Nachrichten über diese Kanäle zu empfangen. Stattdessen sollten die Nachrichten, die sie empfangen, generisch sein und nicht auf ihrem Profil basieren.
Wenn ein Kunde beispielsweise das Direktmarketing für alle Kanäle ablehnt (über `marketing`, wie im [nächsten Abschnitt](#marketing) erläutert), sollte dieser Kunde keine Nachrichten erhalten, selbst wenn eine Personalisierung zulässig ist.

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
| `val` | Die vom Kunden bereitgestellte Personalisierungseinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht zur Einwilligung aufgefordert werden muss, sollte der Wert dieses Felds die Grundlage angeben, auf der die Personalisierung erfolgen soll. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

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
| `any` | Stellt die Voreinstellungen des Kunden für Direktmarketing als Ganzes dar. Die in diesem Feld angegebene Zustimmungsvoreinstellung gilt als &quot;Standardeinstellung&quot;für jeden Marketing-Kanal, es sei denn, sie wird durch zusätzliche Unterfelder überschrieben, die unter `marketing` bereitgestellt werden. Wenn Sie planen, detailliertere Zustimmungsoptionen zu verwenden, wird empfohlen, dieses Feld auszuschließen.<br><br>Wenn der Wert auf  `n` festgelegt ist, sollten alle spezifischeren Personalisierungseinstellungen ignoriert werden. Wenn der Wert auf `y` festgelegt ist, sollten alle feinkörnigen Personalisierungsoptionen ebenfalls als `y` behandelt werden, es sei denn, dies ist explizit auf `n` festgelegt. Wenn der Wert nicht festgelegt ist, sollten die Werte für jede Personalisierungsoption wie angegeben berücksichtigt werden. |
| `email` | Gibt an, ob der Kunde dem Empfang von E-Mail-Nachrichten zustimmt. Der Kunde kann auch Voreinstellungen für einzelne Abonnements innerhalb dieses Kanals festlegen. Weitere Informationen finden Sie im Abschnitt [Abonnements](#subscriptions) unten. |
| `push` | Gibt an, ob der Kunde den Empfang von Push-Benachrichtigungen gestattet. Der Kunde kann auch Voreinstellungen für einzelne Abonnements innerhalb dieses Kanals festlegen. Weitere Informationen finden Sie im Abschnitt [Abonnements](#subscriptions) unten. |
| `sms` | Gibt an, ob der Kunde dem Empfang von Textnachrichten zustimmt. Der Kunde kann auch Voreinstellungen für einzelne Abonnements innerhalb dieses Kanals festlegen. Weitere Informationen finden Sie im Abschnitt [Abonnements](#subscriptions) unten. |
| `val` | Die vom Kunden angegebene Voreinstellung für den angegebenen Anwendungsfall. In Fällen, in denen der Kunde nicht aufgefordert werden muss, seine Zustimmung zu erteilen, sollte der Wert dieses Felds die Grundlage angeben, auf der der Marketing-Anwendungsfall stattfinden soll. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#choice-values) . |
| `time` | Ein ISO 8601-Zeitstempel, mit dem die Marketing-Voreinstellung geändert wurde (falls zutreffend). Beachten Sie, dass, wenn der Zeitstempel für eine individuelle Voreinstellung mit dem unter `metadata` angegebenen Zeitstempel übereinstimmt, dieses Feld nicht für diese Voreinstellung festgelegt werden darf. |
| `reason` | Wenn ein Kunde einen Marketing-Anwendungsfall ablehnt, stellt dieses Zeichenfolgenfeld den Grund dar, warum der Kunde sich abgemeldet hat. |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

Die Eigenschaften `email`, `push` und `sms` des Objekts `marketing` können Kundenanmeldungen für diese einzelnen Kanäle darstellen. Dies wird erreicht, indem dem betreffenden Marketing-Kanal eine `subscriptions` -Eigenschaft hinzugefügt wird.

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
| `type` | Der Abonnementtyp. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern diese 15 Zeichen oder weniger umfasst. |
| `subscribers` | Ein optionales Feld vom Typ Zuordnung , das eine Reihe von Kennungen (wie E-Mail-Adressen oder Telefonnummern) darstellt, die ein bestimmtes Abonnement abonniert haben. Jeder Schlüssel in diesem Objekt stellt die betreffende Kennung dar und enthält zwei Untereigenschaften: <ul><li>`time`: Ein ISO 8601-Zeitstempel, der angibt, wann die Identität abonniert hat (falls zutreffend).</li><li>`source`: Die Quelle, aus der der Abonnent stammt. Dabei kann es sich um eine beliebige beschreibende Zeichenfolge handeln, sofern diese 15 Zeichen oder weniger umfasst.</li></ul> |

{style=&quot;table-layout:auto&quot;}


### `metadata`

`metadata` erfasst allgemeine Metadaten über die Zustimmung und Voreinstellungen des Kunden, wann immer sie zuletzt aktualisiert wurden.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `time` | Ein ISO 8601-Zeitstempel zum letzten Mal, wenn die Zustimmungen und Voreinstellungen des Kunden aktualisiert wurden. Dieses Feld kann verwendet werden, anstatt Zeitstempel auf individuelle Voreinstellungen anzuwenden, um Belastung und Komplexität zu reduzieren. Wenn Sie einen `time` -Wert unter einer individuellen Voreinstellung angeben, wird der `metadata`-Zeitstempel für diese Voreinstellung überschrieben. |

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` kann verwendet werden, wenn eine bestimmte Zustimmung oder Voreinstellung nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde den Erhalt von E-Mails an eine Adresse deaktivieren und gleichzeitig E-Mails an eine andere Adresse zulassen.

>[!IMPORTANT]
Die Zustimmung und Voreinstellungen auf Kanalebene (d. h. die unter `consents` außerhalb von `idSpecific` bereitgestellten Voreinstellungen) gelten für IDs innerhalb dieses Kanals. Daher wirken sich alle Zustimmung und Voreinstellungen auf Kanalebene direkt darauf aus, ob entsprechende ID- oder gerätespezifische Einstellungen berücksichtigt werden:
* Wenn der Kunde sich auf Kanalebene abgemeldet hat, werden alle entsprechenden Zustimmungen oder Voreinstellungen in `idSpecific` ignoriert.
* Wenn die Zustimmung oder Voreinstellung auf Kanalebene nicht festgelegt ist oder der Kunde sich angemeldet hat, werden die entsprechenden Zustimmungen oder Voreinstellungen in `idSpecific` berücksichtigt.


Jeder Schlüssel im `idSpecific`-Objekt stellt einen bestimmten Identitäts-Namespace dar, der vom Adobe Experience Platform Identity Service erkannt wird. Sie können Ihre eigenen benutzerdefinierten Namespaces definieren, um verschiedene IDs zu kategorisieren. Es wird jedoch empfohlen, einen der Standard-Namespaces zu verwenden, die von Identity Service bereitgestellt werden, um die Speichergrößen für das Echtzeit-Kundenprofil zu reduzieren. Weitere Informationen zu Identitäts-Namespaces finden Sie unter [Übersicht über Identitäts-Namespaces](../../../identity-service/namespaces.md) in der Dokumentation zu Identity Service.

Die Schlüssel für jedes Namespace-Objekt stellen die eindeutigen Identitätswerte dar, für die der Kunde Voreinstellungen festgelegt hat. Jeder Identitätswert kann einen vollständigen Satz von Einverständnissen und Voreinstellungen enthalten, der auf dieselbe Weise wie `consents` formatiert ist.

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

Innerhalb von `marketing` Objekten, die im Abschnitt `idSpecific` bereitgestellt werden, werden die Felder `any` und `preferred` nicht unterstützt. Diese Felder können nur auf Benutzerebene konfiguriert werden. Darüber hinaus unterstützen die `idSpecific` Marketing-Voreinstellungen für `email`, `sms` und `push` keine `subscriptions`-Felder.

Es gibt auch eine Zustimmung, die nur im Abschnitt `idSpecific` bereitgestellt werden kann: `adID`. Dieses Feld wird im folgenden Unterabschnitt behandelt.

#### `adID`

Das `adID`-Einverständnis stellt die Einwilligung des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen. Dieser Wert kann nur unter dem Identitäts-Namespace `ECID` im Abschnitt `idSpecific` konfiguriert werden und nicht für andere Namespaces oder auf Benutzerebene für diese Feldergruppe festgelegt werden.

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
Es wird nicht erwartet, dass Sie diesen Wert direkt festlegen, da das Adobe Experience Platform Mobile-SDK ihn gegebenenfalls automatisch festlegt.

## Erfassen von Daten mithilfe der Feldergruppe {#ingest}

Um die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] zum Erfassen von Einwilligungsdaten Ihrer Kunden zu verwenden, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diese Feldergruppe enthält.

Anweisungen zum Zuweisen von Feldergruppen zu Feldern finden Sie im Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . [ Nachdem Sie ein Schema mit einem Feld mit der Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] erstellt haben, lesen Sie den Abschnitt [Erstellen eines Datensatzes](../../../catalog/datasets/user-guide.md#create) im Benutzerhandbuch zum Datensatz und befolgen Sie die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema.

>[!IMPORTANT]
Wenn Sie Einwilligungsdaten an [!DNL Real-time Customer Profile] senden möchten, müssen Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile]-Klasse basiert, die die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] enthält. Der Datensatz, den Sie auf Grundlage dieses Schemas erstellen, muss auch für [!DNL Profile] aktiviert sein. Spezifische Schritte bezüglich der [!DNL Real-time Customer Profile]-Anforderungen für Schemas und Datensätze finden Sie in den oben genannten Tutorials.
Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass sie die Datensätze priorisieren, die die neuesten Zustimmungs- und Voreinstellungsdaten enthalten, damit Kundenprofile korrekt aktualisiert werden. Weitere Informationen finden Sie in der Übersicht zu [Zusammenführungsrichtlinien](../../../rtcdp/profile/merge-policies.md) .

## Handhabung von Zustimmungs- und Vorgabenänderungen

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort mit dem [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md) erzwungen werden. Wenn ein Kunde die Datenerfassung ablehnt, muss die Datenerfassung sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten besuchten Seite keine Personalisierung vorhanden sein.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Referenzinformationen zur Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen].

### Zulässige Werte für `val` {#choice-values}

In der folgenden Tabelle sind die für `val` zulässigen Werte aufgeführt:

| Wert | Titel | Beschreibung |
| --- | --- | --- |
| `y` | Ja | Der Kunde hat sich für die Zustimmung oder Präferenz entschieden. Mit anderen Worten, sie stimmen **do** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `n` | Nein | Der Kunde hat sich von der Zustimmung oder Präferenz abgemeldet. Mit anderen Worten, sie **stimmen nicht** der Verwendung ihrer Daten zu, wie durch die betreffende Einwilligung oder Präferenz angegeben. |
| `p` | Ausstehende Überprüfung | Das System hat noch keinen endgültigen Zustimmungs- oder Präferenzwert erhalten. Dies wird meist im Rahmen einer Zustimmung verwendet, die eine zweistufige Überprüfung erfordert. Wenn sich ein Kunde beispielsweise für den Erhalt von E-Mails entscheidet, wird diese Zustimmung auf `p` gesetzt, bis er einen Link in einer E-Mail auswählt, um zu überprüfen, ob er die richtige E-Mail-Adresse angegeben hat. Anschließend wird die Zustimmung auf `y` aktualisiert.<br><br>Wenn diese Zustimmung oder Voreinstellung keinen zweistufigen Überprüfungsprozess verwendet, kann die  `p` Auswahl stattdessen verwendet werden, um anzugeben, dass der Kunde noch nicht auf die Einwilligungsaufforderung reagiert hat. Sie können beispielsweise den Wert auf `p` automatisch auf der ersten Seite einer Website festlegen, bevor der Kunde auf die Einverständnisaufforderung reagiert hat. In Rechtsordnungen, die keine ausdrückliche Zustimmung erfordern, können Sie damit auch angeben, dass der Kunde sich nicht ausdrücklich abgemeldet hat (d. h., die Zustimmung wird angenommen). |
| `u` | „Unbekannt“ | Die Einwilligungs- oder Präferenzinformationen des Kunden sind unbekannt. |
| `LI` | Rechtliches Interesse | Das berechtigte geschäftliche Interesse, diese Daten für den angegebenen Zweck zu sammeln und zu verarbeiten, überwiegt den potenziellen Schaden, den sie für die Person darstellt. |
| `CT` | Vertrag | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um vertragliche Verpflichtungen mit der Person zu erfüllen. |
| `CP` | Erfüllung einer rechtlichen Verpflichtung | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die rechtlichen Verpflichtungen des Unternehmens zu erfüllen. |
| `VI` | Wichtiges Interesse des Einzelnen | Die Erhebung von Daten für den angegebenen Zweck ist erforderlich, um die lebenswichtigen Interessen des Einzelnen zu schützen. |
| `PI` | Öffentliches Interesse | Die Erhebung von Daten für den festgelegten Zweck ist erforderlich, um eine Aufgabe im öffentlichen Interesse oder in Ausübung öffentlicher Gewalt zu erfüllen. |

{style=&quot;table-layout:auto&quot;}

### Zulässige Werte für `preferred` {#preferred-values}

In der folgenden Tabelle sind die für `preferred` zulässigen Werte aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `email` | E-Mail  Nachrichten. |
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

{style=&quot;table-layout:auto&quot;}

### Vollständiges Schema [!UICONTROL Einverständnisse und Voreinstellungen] {#full-schema}

Das vollständige Schema für die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
