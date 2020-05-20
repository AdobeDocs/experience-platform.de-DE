---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Echtzeit-Profil des Kunden
topic: overview
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Verarbeitung von Datenschutzanfragen im Echtzeit-Profil des Kunden

Der Adobe Experience Platform Privacy Service verarbeitet Anfragen von Kunden zum Zugriff auf ihre personenbezogenen Daten, zu Opt-out oder zu löschen, wie sie in Datenschutzbestimmungen wie der Allgemeinen Datenschutzverordnung (GDPR) und dem California Consumer Privacy Act (CCPA) definiert sind.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanforderungen für Echtzeit-Kundendaten-Profile behandelt.

## Erste Schritte

Es wird empfohlen, die folgenden Experience Platform-Dienste zu verstehen, bevor Sie dieses Handbuch lesen:

* [Datenschutzdienst](home.md): Verwaltet Kundenanforderungen für den Zugriff auf, die Einstellung des Verkaufs oder das Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [Identitätsdienst](../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Profil](../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Identitäts-Namensräume {#namespaces}

Der Identitätsdienst für Adobe Experience Platform verbindet Daten zur Kundenidentität über Systeme und Geräte hinweg. Der Identitätsdienst nutzt **Identitätskennungen** , um einen Kontext für Identitätswerte bereitzustellen, indem er sie mit ihrem System der Herkunft verknüpft. Ein Namensraum kann ein allgemeines Konzept wie eine E-Mail-Adresse (&quot;E-Mail&quot;) oder die Identität einer bestimmten Anwendung zuordnen, z. B. einer Adobe Advertising Cloud ID (&quot;AdCloud&quot;) oder einer Adobe-Zielgruppe-ID (&quot;TNTID&quot;).

Der Identitätsdienst verwaltet einen Store von global definierten (Standard-) und benutzerdefinierten (benutzerdefinierten) Identitäts-Namensräumen. Standardmäßige Namensraum stehen für alle Unternehmen zur Verfügung (z. B. &quot;E-Mail&quot;und &quot;ECID&quot;), während Ihr Unternehmen benutzerdefinierte Namensraum erstellen kann, die den jeweiligen Anforderungen entsprechen.

Weitere Informationen zu Identitäts-Namensräumen in Experience Platform finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md).

## Einreichen von Anträgen {#submit}

>[!NOTE] In diesem Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für den Profil-Datenspeicher erstellen. Es wird dringend empfohlen, die Dokumentation der [Datenschutzdienst-API](../privacy-service/api/getting-started.md) oder der Benutzeroberfläche [des](../privacy-service/ui/overview.md) Datenschutzdienstes zu lesen, um die vollständigen Schritte zum Senden eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anforderungs-Nutzdaten.

Im folgenden Abschnitt wird beschrieben, wie Sie mithilfe der Datenschutzdienst-API oder der Benutzeroberfläche Datenschutzanforderungen für Echtzeit-Kundendaten und den Data Lake erstellen.

### Verwenden der API

Beim Erstellen von Auftragsanforderungen in der API müssen alle `userIDs` bereitgestellten Aufträge einen bestimmten `namespace` und `type` je nach Datenspeicher verwenden, für den sie gelten. IDs für den Profil-Store müssen entweder &quot;Standard&quot;oder &quot;benutzerdefiniert&quot;für ihren `type` Wert verwenden und einen gültigen [Identitäts-Namensraum](#namespaces) , der vom Identitätsdienst für ihren `namespace` Wert erkannt wird.


Darüber hinaus muss das `include` Array der Anforderungs-Nutzlast die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anforderung gesendet wird. Bei Anforderungen an den Data Lake muss das Array den Wert &quot;ProfileService&quot;enthalten.

Mit der folgenden Anforderung wird ein neuer Datenschutzauftrag für Echtzeit-Kundendaten erstellt, wobei der standardmäßige Namensraum &quot;E-Mail&quot; verwendet wird. Er enthält außerdem den Produktwert für Profil im `include` Array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Verwenden der Benutzeroberfläche

Wählen Sie beim Erstellen von Auftragsanforderungen in der Benutzeroberfläche **AEP Data Lake** und/oder **Profil** unter _Products_ aus, um Aufträge für Daten zu verarbeiten, die im Data Lake bzw. im Real-Time Customer Profil gespeichert werden.

<img src="images/privacy/product-value.png" width="450"><br>

## Anforderungsverarbeitung löschen

Wenn Experience Platform eine Löschanforderung vom Datenschutzdienst erhält, sendet Platform eine Bestätigung an den Datenschutzdienst, dass die Anforderung empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann innerhalb von sieben Tagen aus dem Data Lake oder dem Data Profil Store entfernt. Während dieses siebentägigen Fensters werden die Daten weich gelöscht und stehen daher keinem Plattformdienst zur Verfügung.

In zukünftigen Versionen sendet Platform eine Bestätigung an den Datenschutzdienst, nachdem die Daten physisch gelöscht wurden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie mit den wichtigen Konzepten zur Verarbeitung von Datenschutzanforderungen in Experience Platform vertraut gemacht. Es wird empfohlen, die Dokumentation in diesem Handbuch weiter zu lesen, um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen.

Informationen zur Verarbeitung von Datenschutzanforderungen für Plattformressourcen, die nicht von Profil verwendet werden, finden Sie im Dokument zur Verarbeitung von [Datenschutzanfragen im Data Lake](../catalog/privacy.md).