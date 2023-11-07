---
description: Erfahren Sie, wie Sie Ihr Ziel für die unterstützten Konfigurationen der Identitäts- und Attributzuordnung konfigurieren.
title: Unterstützte Zuordnungskonfigurationen
exl-id: a477a3f2-a229-4b22-8588-ee58bd5436c6
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---

# Unterstützte Zuordnungskonfigurationen

Ziele, die mit Destination SDK erstellt wurden, unterstützen spezifische Konfigurationen für Identity-Namespaces und Attributzuordnungen, die auf dem Zieltyp basieren.

In diesem Artikel werden alle unterstützten Zuordnungskonfigurationen beschrieben, die Sie beim Konfigurieren Ihres Ziels verwenden können.

>[!WARNING]
>
>Zuordnungskonfigurationen, die in diesem Artikel nicht beschrieben werden, werden von Destination SDK nicht unterstützt.

Konfigurieren Sie beim Erstellen Ihres Ziels Ihr Schema und die Identity-Namespaces gemäß einer der auf dieser Seite beschriebenen Zuordnungskonfigurationen.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Zuordnungen für Streaming-Ziele {#streaming-mappings}

Mit Destination SDK erstellte Echtzeit-(Streaming-)Ziele unterstützen die in der folgenden Tabelle beschriebenen Zuordnungskonfigurationen.

| Quellfeld | Zielfeld |
| --- | --- |
| XDM-Attribut | Benutzerdefiniertes Attribut |
| Identity-Namespace | Identity-Namespace |

Im folgenden Konfigurationsbeispiel können Kundinnen und Kunden beide Zuordnungen in der obigen Tabelle verwenden.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Zuordnen von XDM-Attributen zu benutzerdefinierten Attributen {#streaming-xdm-to-custom}

Benutzerinnen und Benutzer können Attribute aus ihrem Quell-XDM-Profil benutzerdefinierten Attributen auf der Seite Ihres Ziels zuordnen.

Benutzerinnen und Benutzer müssen bei der Auswahl der Zielfeldzuordnung manuell den Namen des benutzerdefinierten Zielattributs eingeben.

![Screenshot der Platform-Benutzeroberfläche mit Auswahl der benutzerdefinierten Attribute.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![Screenshot der Platform-Benutzeroberfläche mit der XDM-Attributzuordnung zu benutzerdefinierten Attributen für Streaming-Ziele.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Zuordnen von Identity-Namespaces zu Partner-Identity-Namespaces {#streaming-identity-to-identity}

Benutzerinnen und Benutzer können benutzerdefinierte oder globale Identity-Namespaces von Platform den von Ihnen definierten Identity-Namespaces zuordnen.

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![Screenshot der Platform-Benutzeroberfläche mit Identitätszuordnung zu Identitäten für Streaming-Ziele.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Unterstützte Zuordnungen für dateibasierte Ziele {#batch-mappings}

Dateibasierte Ziele, die mit Destination SDK erstellt wurden, unterstützen die in der folgenden Tabelle beschriebenen Zuordnungskonfigurationen. Detaillierte Zuordnungsbeispiele finden Sie in den nächsten Abschnitten.

| Quellfeld | Zielfeld |
| --- | --- |
| XDM-Attribut | Attribut/benutzerspezifisches Attribut |
| Identity-Namespace | Attribut/benutzerspezifisches Attribut |
| Identity-Namespace | Identity-Namespace |

Im folgenden Konfigurationsbeispiel können Kundinnen und Kunden alle Zuordnungen aus der obigen Tabelle verwenden.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Zuordnen von XDM-Attributen zu benutzerdefinierten Attributen {#batch-xdm-to-custom}

Benutzerinnen und Benutzer können Attribute aus ihrem Quell-XDM-Profil benutzerdefinierten Attributen auf der Seite Ihres Ziels zuordnen.

Bei dateibasierten Zielen wird das Zielfeld automatisch mit einem Standardattribut mit demselben Namen wie das Quellfeld ausgefüllt.

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![Screenshot der Platform-Benutzeroberfläche mit der XDM-Zuordnung zu benutzerdefinierten Attributen für dateibasierte Ziele.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Benutzerinnen und Benutzer können den Standardnamen beibehalten oder einen benutzerdefinierten Attributnamen im Bildschirm zur Zielfeldauswahl eingeben.

![Screenshot der Platform-Benutzeroberfläche mit einer benutzerdefinierten Zielattribut-Auswahl für dateibasierte Ziele.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Zuordnen von Identity-Namespaces zu benutzerdefinierten Attributen {#batch-identity-to-custom}

Benutzerinnen und Benutzer können benutzerdefinierte oder globale Identity-Namespaces von Platform benutzerdefinierten Attributen auf der Seite Ihres Ziels zuordnen.

Bei der Auswahl eines Identity-Namespace als Quellfeld wird das Zielfeld automatisch mit einem entsprechenden Identity-Namespace ausgefüllt. Um das Zielfeld durch ein benutzerdefiniertes Attribut zu ersetzen, müssen Benutzerinnen und Benutzer einen benutzerdefinierten Attributnamen in den Bildschirm zur Zielfeldauswahl eingeben.

![Screenshot der Platform-Benutzeroberfläche mit einer benutzerdefinierten Zielattribut-Auswahl für dateibasierte Ziele.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![Screenshot der Platform-Benutzeroberfläche, der die Identitätszuordnung zu benutzerdefinierten Attributen für dateibasierte Ziele zeigt.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Zuordnen von Identity-Namespaces zu Partner-Identity-Namespaces {#batch-identity-to-identity}

Benutzerinnen und Benutzer können benutzerdefinierte oder globale Identity-Namespaces von Platform äquivalenten Identity-Namespaces zuordnen.

Bei der Auswahl eines Identity-Namespace als Quellfeld wird das Zielfeld automatisch mit einem entsprechenden Identity-Namespace ausgefüllt.

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![Screenshot der Platform-Benutzeroberfläche, der die Identitätszuordnung zur Identität für dateibasierte Ziele zeigt.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, welche Zuordnungen von Zielen unterstützt werden, die mit Destination SDK erstellt wurden.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authorization.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
