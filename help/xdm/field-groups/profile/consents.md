---
solution: Experience Platform
title: Einverständnis und Voreinstellungsfeldgruppe
description: Erfahren Sie mehr über die Feldgruppe "Einverständnis und Voreinstellungen".
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen]

[!UICONTROL Einverständnisse und Voreinstellungen] ist eine Standardfeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md), die Einwilligungs- und Präferenzinformationen für einen einzelnen Kunden erfasst.

>[!NOTE]
>
>Da diese Feldergruppe nur mit [!DNL XDM Individual Profile] kompatibel ist, kann sie nicht für [!DNL XDM ExperienceEvent] -Schemas verwendet werden. Wenn Sie Einwilligungs- und Präferenzdaten in Ihr Erlebnisereignis-Schema aufnehmen möchten, fügen Sie den Datentyp [[!UICONTROL Einverständnis für Datenschutz, Personalization- und Marketingeinstellungen]](../../data-types/consents.md) stattdessen mithilfe einer [benutzerdefinierten Feldergruppe](../../ui/resources/field-groups.md#create) zum Schema hinzu.

## Feldgruppenstruktur {#structure}

Die Feldergruppe [!UICONTROL Einverständnis und Voreinstellungen] enthält ein einzelnes Objektfeld, `consents`, um Einwilligungs- und Präferenzinformationen zu erfassen. Dieses Feld erweitert den Datentyp [[!UICONTROL Einverständnis für Datenschutz, Personalization- und Marketing-Voreinstellungen]](../../data-types/consents.md), entfernt das Feld `adID` und fügt ein Zuordnungsfeld `idSpecific` hinzu.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Anweisungen zum Nachschlagen einer beliebigen XDM-Ressource und zum Überprüfen ihrer Struktur in der Platform-Benutzeroberfläche finden Sie im Handbuch zu [Erkunden von XDM-Ressourcen](../../ui/explore.md) zu .

Die folgende JSON-Datei zeigt ein Beispiel für den Datentyp, den die Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] verarbeiten kann. Informationen zur Verwendung der meisten von der Feldergruppe bereitgestellten Felder finden Sie im Handbuch zum Datentyp [Einverständnisse und Voreinstellungen](../../data-types/consents.md). Die folgenden Unterabschnitte konzentrieren sich auf die eindeutigen Attribute, die die Feldergruppe zum Datentyp hinzufügt.

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
>* [Generieren von Beispieldaten in der API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kann verwendet werden, wenn eine bestimmte Zustimmung oder Voreinstellung nicht allgemein für einen Kunden gilt, sondern auf ein einzelnes Gerät oder eine einzelne ID beschränkt ist. Beispielsweise kann ein Kunde den Erhalt von E-Mails an eine Adresse deaktivieren und gleichzeitig E-Mails an eine andere Adresse zulassen.

>[!IMPORTANT]
>
>Die Zustimmungen und Voreinstellungen auf Kanalebene (d. h. die unter `consents` außerhalb von `idSpecific` bereitgestellten Voreinstellungen) gelten für alle IDs in diesem Kanal. Daher wirken sich alle Zustimmung und Voreinstellungen auf Kanalebene direkt darauf aus, ob entsprechende ID- oder gerätespezifische Einstellungen berücksichtigt werden:
>
>* Wenn der Kunde sich auf Kanalebene abgemeldet hat, werden alle entsprechenden Zustimmungen oder Voreinstellungen in `idSpecific` ignoriert.
>* Wenn die Zustimmung oder Voreinstellung auf Kanalebene nicht festgelegt ist oder der Kunde sich angemeldet hat, werden die entsprechenden Zustimmungen oder Voreinstellungen in `idSpecific` berücksichtigt.

Jeder Schlüssel im Objekt `idSpecific` stellt einen bestimmten Identitäts-Namespace dar, der vom Adobe Experience Platform Identity Service erkannt wird. Sie können Ihre eigenen benutzerdefinierten Namespaces definieren, um verschiedene IDs zu kategorisieren. Es wird jedoch empfohlen, einen der Standard-Namespaces zu verwenden, die von Identity Service bereitgestellt werden, um die Speichergrößen für das Echtzeit-Kundenprofil zu reduzieren. Weitere Informationen zu Identitäts-Namespaces finden Sie unter [Übersicht über Identitäts-Namespaces](../../../identity-service/features/namespaces.md) in der Dokumentation zu Identity Service.

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
  "ECID": {
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

Innerhalb von `marketing` -Objekten, die im Abschnitt `idSpecific` bereitgestellt werden, werden die Felder `any` und `preferred` nicht unterstützt. Diese Felder können nur auf Benutzerebene konfiguriert werden. Darüber hinaus unterstützen die Marketing-Voreinstellungen für `email`, `sms` und `push` die Felder `subscriptions` nicht.`idSpecific`

Es gibt auch eine Einwilligung, die nur im Abschnitt `idSpecific` bereitgestellt werden kann: `adID`. Dieses Feld wird im folgenden Unterabschnitt behandelt.

#### `adID`

Das Einverständnis `adID` stellt die Einwilligung des Kunden dar, ob eine Advertiser-ID (IDFA oder GAID) verwendet werden kann, um den Kunden über Apps auf diesem Gerät hinweg zu verknüpfen. Dieser Wert kann nur unter dem Identitäts-Namespace `ECID` im Abschnitt `idSpecific` konfiguriert werden und nicht für andere Namespaces oder auf Benutzerebene für diese Feldergruppe festgelegt werden.

```json
"idSpecific": {
  "ECID": {
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
>Es wird nicht erwartet, dass Sie diesen Wert direkt festlegen, da das Adobe Experience Platform Mobile-SDK ihn gegebenenfalls automatisch festlegt.

## Erfassen von Daten mithilfe der Feldergruppe {#ingest}

Um die Feldergruppe [!UICONTROL Einverständnis und Voreinstellungen] zum Erfassen der Einwilligungsdaten Ihrer Kunden zu verwenden, müssen Sie einen Datensatz erstellen, der auf einem Schema basiert, das diese Feldergruppe enthält.

Anweisungen zum Zuweisen von Feldergruppen zu Feldern finden Sie im Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) . [ Nachdem Sie ein Schema erstellt haben, das ein Feld mit der Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] enthält, lesen Sie den Abschnitt zum Erstellen eines Datensatzes [3} im Benutzerhandbuch zu Datensätzen und befolgen Sie die Schritte zum Erstellen eines Datensatzes mit einem vorhandenen Schema.](../../../catalog/datasets/user-guide.md#create)

>[!IMPORTANT]
>
>Wenn Sie Einwilligungsdaten an [!DNL Real-Time Customer Profile] senden möchten, müssen Sie ein [!DNL Profile]-aktiviertes Schema erstellen, das auf der [!DNL XDM Individual Profile] -Klasse basiert, die die Feldergruppe [!UICONTROL Einverständnis und Voreinstellungen] enthält. Der Datensatz, den Sie auf Grundlage dieses Schemas erstellen, muss auch für [!DNL Profile] aktiviert sein. Spezifische Schritte bezüglich der [!DNL Real-Time Customer Profile]-Anforderungen für Schemas und Datensätze finden Sie in den oben genannten Tutorials.
>
>Darüber hinaus müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass sie die Datensätze priorisieren, die die neuesten Zustimmungs- und Voreinstellungsdaten enthalten, damit Kundenprofile korrekt aktualisiert werden. Weitere Informationen finden Sie in der Übersicht zu [Zusammenführungsrichtlinien](../../../rtcdp/profile/merge-policies.md) .

## Handhabung von Zustimmungs- und Vorgabenänderungen

Wenn ein Kunde seine Zustimmung oder Voreinstellungen auf Ihrer Website ändert, sollten diese Änderungen erfasst und sofort mit dem [Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md) erzwungen werden. Wenn ein Kunde die Datenerfassung ablehnt, muss die Datenerfassung sofort eingestellt werden. Wenn ein Kunde die Personalisierung ablehnt, sollte auf der nächsten besuchten Seite keine Personalisierung vorhanden sein.

## Nächste Schritte

In diesem Dokument wurden die Struktur und Verwendung der Feldergruppe [!UICONTROL Einverständnisse und Voreinstellungen] behandelt. Weitere Informationen zu den anderen Feldern, die von der Feldergruppe bereitgestellt werden, finden Sie im Dokument zum Datentyp [[!UICONTROL Einverständnis für Datenschutz-, Personalization- und Marketing-Voreinstellungen]](../../data-types/consents.md).
