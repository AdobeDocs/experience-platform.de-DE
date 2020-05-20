---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Akzeptierte Identitäts-Namensraum und Qualifikatoren
topic: developer guide
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 8%

---


# Anhang

## Standard-Identitäts-Namensraum {#standard-namespaces}

Alle Identitäten, die an den Datenschutzdienst gesendet werden, müssen unter einem bestimmten Namensraum angegeben werden. Identity Namensraums sind eine Komponente des [Adobe Experience Platform Identity Service](../../identity-service/home.md) , die den Kontext angibt, auf den sich eine Identität bezieht.

In der folgenden Tabelle sind einige häufig verwendete, vordefinierte Identitätstypen, die von Experience Platform bereitgestellt werden, zusammen mit den zugehörigen `namespace` Werten aufgeführt:

| Identitätstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-Mail  | E-Mail  | 6 |
| Telefon | Telefon | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| UUID für Adobe Audience Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Zielgruppe ID | TNTID | 9 |
| Apple-ID für Werbetreibende | IDFA | 20915 |
| Google Ad ID | GAID | 20914 |
| Windows-BEIHILFE | WAID | 8 |

>[!NOTE] Jeder Identitätstyp verfügt auch über einen `namespaceId` ganzzahligen Wert, der anstelle der `namespace` Zeichenfolge verwendet werden kann, wenn die `type` Eigenschaft der Identität auf &quot;namespaceId&quot;gesetzt wird. Weitere Informationen finden Sie im Abschnitt zu [Namensraum-Qualifikatoren](#namespace-qualifiers) .

Sie können eine Liste von Identitäts-Namensräumen abrufen, die in Ihrem Unternehmen verwendet werden, indem Sie eine GET-Anforderung an den `idnamespace/identities` Endpunkt in der Identitätsdienst-API stellen. Weitere Informationen finden Sie im Entwicklerhandbuch für den [Identitätsdienst](../../identity-service/api/getting-started.md) .

## Namensraum-Qualifikatoren

Beim Festlegen eines `namespace` Werts in der Datenschutzdienst-API muss ein **Namensraum-Qualifikator** in einen entsprechenden `type` Parameter aufgenommen werden. In der folgenden Tabelle sind die verschiedenen zulässigen Namensraum-Qualifikatoren aufgeführt.

| Qualifizierer | Definition |
| --------- | ---------- |
| Standard | Einer der weltweit definierten Standard-Namensraum, der nicht an einen unternehmensspezifischen Datensatz gebunden ist (z. B. E-Mail, Telefonnummer usw.). Namensraum-ID angegeben. |
| custom | Ein eindeutiger Namensraum, der im Kontext einer Organisation erstellt und nicht in der Experience Cloud freigegeben wurde. Der Wert stellt den Anzeigenamen (&quot;Namensfeld&quot;) dar, nach dem gesucht werden soll. Namensraum-ID angegeben. |
| integrationCode | Integrationscode - ähnlich wie &quot;benutzerspezifisch&quot;, aber spezifisch definiert als Integrationscode einer zu durchsuchenden Datenquelle. Namensraum-ID angegeben. |
| namespaceId | Gibt die tatsächliche ID des Namensraums an, der über den Namensraum-Dienst erstellt oder zugeordnet wurde. |
| nicht registriert | Eine Freiformzeichenfolge, die nicht im Namensraum-Dienst definiert ist und als &quot;wie vorhanden&quot;gilt. Jede Anwendung, die mit solchen Namensräumen umgeht, überprüft diese und verarbeitet sie gegebenenfalls für den Kontext und den Datensatz der Firma. Es wird keine Namensraum-ID angegeben. |
| analytics | Ein benutzerdefinierter Namensraum, der intern in Analytics und nicht im Namensraum-Dienst zugeordnet wird. Dies wird direkt wie von der ursprünglichen Anforderung angegeben ohne Namensraum-ID weitergeleitet |
| target | Ein benutzerdefinierter Namensraum, der intern von der Zielgruppe verstanden wird, nicht im Namensraum-Dienst. Dies wird direkt wie von der ursprünglichen Anforderung angegeben ohne Namensraum-ID weitergeleitet |

## Akzeptierte Produktwerte

In der folgenden Tabelle sind die für die Angabe eines Adobe-Produkts im Attribut einer Anforderung zum Erstellen von `include` Aufträgen zulässigen Werte aufgeführt.

| Produkt | Wert für die Verwendung im `include` Attribut |
--- | ---
| Adobe Advertizing Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime-Authentifizierung | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Customer Record Service | &quot;CRS&quot; |
| Echtzeit-Kundenprofil | &quot;ProfileService&quot; |