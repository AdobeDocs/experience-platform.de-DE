---
description: Erfahren Sie, wie Sie die unterstützten Zielidentitäten für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Konfiguration von Identity-Namespaces
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 60%

---

# Konfiguration von Identity-Namespaces

Experience Platform verwendet Identity-Namespaces, um den Typ bestimmter Identitäten zu beschreiben. Beispiel: ein Identity-Namespace namens `Email` identifiziert einen Wert wie `name@email.com` als E-Mail-Adresse.

Beachten Sie je nach dem von Ihnen erstellten Zieltyp (Streaming oder dateibasiert) die folgenden Anforderungen an Identity-Namespaces:

* Beim Erstellen von Echtzeit-Zielen (Streaming) über Destination SDK müssen Sie zusätzlich zum [Konfigurieren eines Partnerschemas](schema-configuration.md) dem Benutzerinnen und Benutzer Profilattribute und Identitäten zuordnen können, auch *mindestens einen* Identity-Namespaces definieren, die von Ihrer Zielplattform unterstützt werden. Wenn Ihre Zielplattform beispielsweise Hash-E-Mails und [!DNL IDFA] akzeptiert, müssen Sie diese beiden Identitäten definieren, wie [weiter unten in diesem Dokument beschrieben](#supported-parameters).

  >[!IMPORTANT]
  >
  >Beim Aktivieren von Zielgruppen für Streaming-Ziele müssen Benutzerinnen und Benutzer _Zielgruppenattributen auch mindestens_ Zielidentität zuordnen. Andernfalls werden die Zielgruppen nicht für die Zielplattform aktiviert.

* Beim Erstellen dateibasierter Ziele über Destination SDK ist die Konfiguration von Identity-Namespaces _optional_.

Weitere Informationen zu Identity-Namespaces in Experience Platform finden Sie in der [Dokumentation zu Identity-Namespaces](../../../../identity-service/features/namespaces.md).

Beim Konfigurieren von Identity-Namespaces für Ihr Ziel können Sie die von Ihrem Ziel unterstützte Zielidentitätszuordnung anpassen, z. B.:

* Benutzerinnen und Benutzern ermöglichen, XDM-Attribute Identity-Namespaces zuzuordnen.
* Benutzerinnen und Benutzern ermöglichen, [Standard-Identity-Namespaces](../../../../identity-service/features/namespaces.md#standard) Ihren eigenen Identity-Namespaces zuzuordnen.
* Benutzerinnen und Benutzern ermöglichen, [benutzerdefinierte Identity-Namespaces](../../../../identity-service/features/namespaces.md#manage-namespaces) Ihren eigenen Identity-Namespaces zuzuordnen.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch [Verwenden von Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Sie können Ihre unterstützten Identity-Namespaces über den `/authoring/destinations`-Endpunkt konfigurieren. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Konfigurationsoptionen für Identity-Namespaces beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kundinnen und Kunden in der Experience Platform-Benutzeroberfläche sehen werden.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja (erforderlich) |
| Dateibasierte (Batch-)Integrationen | Ja (optional) |

## Unterstützte Parameter {#supported-parameters}

Bei der Definition der Zielidentitäten, die Ihr Ziel unterstützt, können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um ihr Verhalten zu konfigurieren.

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---------|----------|---|------|
| `acceptsAttributes` | Boolesch | Optional | Gibt an, ob Kundinnen und Kunden der Identität, die Sie konfigurieren, standardmäßige Profilattribute zuordnen können. |
| `acceptsCustomNamespaces` | Boolesch | Optional | Gibt an, ob Kundinnen und Kunden dem Identity-Namespace, den Sie konfigurieren, benutzerdefinierte Identity-Namespaces zuordnen können. |
| `acceptedGlobalNamespaces` | – | Optional | Gibt an, welche [Standard-Identity-Namespaces](../../../../identity-service/features/namespaces.md#standard) (z. B. [!UICONTROL IDFA]) Kundinnen und Kunden der Identität zuordnen können, die Sie konfigurieren. |
| `transformation` | Zeichenfolge | Optional | Zeigt das Kontrollkästchen [[!UICONTROL Umwandlung anwenden]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) in der Experience Platform-Benutzeroberfläche an, wenn das Quellfeld entweder ein XDM-Attribut oder ein benutzerdefinierter Identity-Namespace ist. Verwenden Sie diese Option, um Benutzerinnen und Benutzern die Möglichkeit zu geben, Quellattribute beim Export zu hashen. Um diese Option zu aktivieren, setzen Sie den Wert auf `sha256(lower($))`. |
| `requiredTransformation` | Zeichenfolge | Optional | Wenn Kundinnen und Kunden diesen Quell-Identity-Namespace auswählen, wird das Kontrollkästchen [[!UICONTROL Umwandlung anwenden]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) automatisch auf die Zuordnung angewendet, und Kundinnen und Kunden können sie nicht deaktivieren. Um diese Option zu aktivieren, setzen Sie den Wert auf `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Sie müssen angeben, welche [!DNL Experience Platform]-Identitäten Kundinnen und Kunden in Ihr Ziel exportieren können. Einige Beispiele: [!DNL Experience Cloud ID], gehashte E-Mail, Geräte-ID ([!DNL IDFA], [!DNL GAID]). Diese Werte sind Identity-Namespaces von [!DNL Experience Platform], die Kundinnen und Kunden von Ihrem Ziel aus Identity-Namespaces zuordnen können.

Identity-Namespaces erfordern keine 1:1-Korrespondenz zwischen [!DNL Experience Platform] und Ihrem Ziel.
Kunden können beispielsweise einen [!DNL Experience Platform] [!DNL IDFA]-Namespace einem [!DNL IDFA]-Namespace Ihres Ziels zuordnen oder sie können denselben [!DNL Experience Platform] [!DNL IDFA]-Namespace einem [!DNL Customer ID]-Namespace in Ihrem Ziel zuordnen.

Mehr zu Identitäten erfahren Sie in der [Übersicht über Identity-Namespaces](../../../../identity-service/features/namespaces.md).

## Zuordnungsüberlegungen

Wenn Kundinnen und Kunden einen Quell-Identity-Namespace auswählen und keine Zielzuordnung auswählen, füllt Experience Platform die Zielzuordnung automatisch mit einem Attribut mit demselben Namen.

## Konfigurieren des optionalen Hashing für Quellfelder

Experience Platform-Kunden können Daten im Hash-Format oder im Klartext in Experience Platform aufnehmen. Wenn Ihre Zielplattform sowohl gehashte als auch ungehashte Daten akzeptiert, können Sie Kundinnen und Kunden die Möglichkeit geben, festzulegen, ob Experience Platform die Quellfeldwerte beim Export in Ihr Ziel hashen soll.

Die folgende Konfiguration aktiviert die optionale Option [Umwandlung anwenden](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) in der Experience Platform-Benutzeroberfläche im Schritt „Zuordnung“.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Aktivieren Sie diese Option, wenn Sie nicht gehashte Quellfelder verwenden, damit diese automatisch von Adobe Experience Platform bei der Aktivierung gehasht werden.

Wenn Sie ungehashte Quellattribute Zielattributen zuordnen, von denen das Ziel erwartet, dass sie gehasht werden (z. B.: `email_lc_sha256` oder `phone_sha256`), aktivieren Sie die Option **Umwandlung anwenden**, damit Adobe Experience Platform die Quellattribute bei Aktivierung automatisch hasst.

## Konfigurieren von obligatorischem Hashing für Quellfelder

Wenn Ihr Ziel nur Hash-Daten akzeptiert, können Sie die exportierten Attribute so konfigurieren, dass sie automatisch von Experience Platform gehasht werden. Die folgende Konfiguration aktiviert automatisch die Option **Umwandlung anwenden**, wenn die `Email`- und `Phone`-Identitäten zugeordnet werden.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Ihre Identity-Namespaces für Ziele konfigurieren, die mit Destination SDK erstellt wurden.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth2-Autorisierung](oauth2-authorization.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
