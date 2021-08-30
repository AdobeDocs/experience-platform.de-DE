---
audience: user
user-guide-title: Hilfe zum Experience-Datenmodell (XDM)-System
breadcrumb-title: Handbuch zum Experience-Datenmodell (XDM)
user-guide-description: Verwenden Sie Experience-Datenmodell (XDM)-Klassen und Schemafeldgruppen, um Erlebnisdaten zu standardisieren.
feature: Schemas
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 41%

---


# Experience-Datenmodell (XDM)-System {#xdm}

* [XDM-System – Übersicht](home.md)
* Schemas {#schema}
   * [Grundlagen der Schema-Komposition](schema/composition.md)
   * [Best Practices für die Datenmodellierung](schema/best-practices.md)
   * [XDM-Feldtypbegrenzungen](schema/field-constraints.md)
   * [Namespacing in XDM](./schema/namespaces.md)
   * [Wörterbuch der XDM-Felder](schema/field-dictionary.md)
   * Datenmodelle für die Branche {#industries}
      * [Übersicht](./schema/industries/overview.md)
      * [Einzelhandel](./schema/industries/retail.md)
      * [Finanzdienstleistungen](./schema/industries/financial.md)
      * [Telekommunikation](./schema/industries/telecom.md)
      * [Reise und Gastfreundschaft](./schema/industries/travel-hospitality.md)
* Klassen {#classes}
   * [XDM Individual Profile](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Segmentdefinition](./classes/segment-definition.md)
* Schemafeldgruppen {#field-groups}
   * Profilfeldgruppen {#profile}
      * [Demografische Details](./field-groups/profile/demographic-details.md)
      * [IAB TCF 2.0-Zustimmung](./field-groups/profile/iab.md)
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Treuedetails](./field-groups/profile/loyalty-details.md)
      * [Persönliche Kontaktangaben](./field-groups/profile/personal-contact-details.md)
      * [Einverständnis und Voreinstellungen](./field-groups/profile/consents.md)
      * [Details zur Segmentzugehörigkeit](./field-groups/profile/segmentation.md)
      * [Telekom-Abonnement](./field-groups/profile/telecom-subscription.md)
      * [Kontaktangaben für Arbeitskontakte](./field-groups/profile/work-contact-details.md)
   * Ereignisfeldgruppen {#event}
      * [Kampagnen-Marketingdetails](./field-groups/event/campaign-marketing-details.md)
      * [Kanaldetails](./field-groups/event/channel-details.md)
      * [Commerce-Details](./field-groups/event/commerce-details.md)
      * [Details zum Gerätehandel](./field-groups/event/device-trade-in-details.md)
      * [Details zur Endbenutzer-ID](./field-groups/event/enduserids.md)
      * [Umgebungsdetails](./field-groups/event/environment-details.md)
      * [IAB TCF 2.0-Zustimmung](./field-groups/event/iab.md)
      * [Webdetails](./field-groups/event/web-details.md)
   * [Namensänderungen der Feldergruppe](./field-groups/name-updates.md)
* Datentypen {#data-types}
   * [Anwendung](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Handel](./data-types/commerce.md)
   * [Zustimmungszeichenfolge](./data-types/consent-string.md)
   * [Einverständnisse und Voreinstellungen](./data-types/consents.md)
   * [Währung](./data-types/currency.md)
   * [Gerät](./data-types/device.md)
   * [E-Mail Adresse](./data-types/email-address.md)
   * [Umgebung](./data-types/environment.md)
   * [Experience-Kanal](./data-types/experience-channel.md)
   * [Generisches Einverständnisfeld](./data-types/consent-field.md)
   * [Feld für allgemeine Marketing-Voreinstellungen](./data-types/marketing-field.md)
   * [Allgemeines Marketing-Präferenzfeld mit Abonnements](./data-types/marketing-field-subscriptions.md)
   * [Feld für allgemeine Personalisierungseinstellungen](./data-types/personalization-field.md)
   * [Geo](./data-types/geo.md)
   * [Geo-Kreis](./data-types/geo-circle.md)
   * [Geo-Koordinaten](./data-types/geo-coordinates.md)
   * [Details zur Geo-Interaktion](./data-types/geo-interaction-details.md)
   * [Geo-Form](./data-types/geo-shape.md)
   * [Identität](./data-types/identity.md)
   * [Marketing](./data-types/marketing.md)
   * [Maßnahme](./data-types/measure.md)
   * [Bestellung](./data-types/order.md)
   * [Zahlungselement](./data-types/payment-item.md)
   * [Person](./data-types/person.md)
   * [Personenname](./data-types/person-name.md)
   * [Telefonnummer](./data-types/phone-number.md)
   * [Ortskontext](./data-types/place-context.md)
   * [POI-Details](./data-types/poi-details.md)
   * [POI-Interaktion](./data-types/poi-interaction.md)
   * [Postadresse](./data-types/postal-address.md)
   * [Produktlistenelement](./data-types/product-list-item.md)
   * [Durchsuchen](./data-types/search.md)
   * [Abonnement](./data-types/subscription.md)
   * [Telekom-Abonnement](./data-types/telecom-subscription.md)
   * [Webinformationen](./data-types/web-information.md)
   * [Webinteraktion](./data-types/web-interaction.md)
   * [Webseitendetails](./data-types/webpage-details.md)
*  SchemasUI  {#ui}
   * [Übersicht](./ui/overview.md)
   * [XDM-Ressourcen](./ui/explore.md)
   * Erstellen und Bearbeiten von Ressourcen {#resources}
      * [Schemas](./ui/resources/schemas.md)
      * [Klassen](./ui/resources/classes.md)
      * [Feldergruppen](./ui/resources/field-groups.md)
      * [Datentypen](./ui/resources/data-types.md)
   * Felder {#fields} definieren
      * [Übersicht](./ui/fields/overview.md)
      * [Erforderliche Felder](./ui/fields/required.md)
      * [Objektfelder](./ui/fields/object.md)
      * [Array-Felder](./ui/fields/array.md)
      * [Aufzählungsfelder](./ui/fields/enum.md)
      * [Identitätsfelder](./ui/fields/identity.md)
      * [Beziehungsfelder](./ui/fields/relationship.md)
   * [Beispiel-XDM-Daten generieren](./ui/sample.md)
   * [Exportieren von XDM-Schemata](./ui/export.md)
* Schema Registry-API {#api}
   * [Übersicht](api/overview.md)
   * [Erste Schritte](api/getting-started.md)
   * [Schemas](api/schemas.md)
   * [Verhalten](api/behaviors.md)
   * [Klassen](api/classes.md)
   * [Schemafeldgruppen](api/field-groups.md)
   * [Datentypen](api/data-types.md)
   * [Deskriptoren](api/descriptors.md)
   * [Vereinigungen](api/unions.md)
   * [Export/Import](api/export-import.md)
   * [Sample data](api/sample-data.md)
   * [Auditprotokoll](api/audit-log.md)
   * [Ad-hoc-Schemata](api/ad-hoc.md)
   * [Mixins (überholt)](api/mixins.md)
   * [Anhang](api/appendix.md)
* Tutorials {#tutorials}
   * [Erstellen eines Schemas (Benutzeroberfläche)](tutorials/create-schema-ui.md)
   * [Erstellen eines Schemas (API)](tutorials/create-schema-api.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (Benutzeroberfläche)](tutorials/relationship-ui.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (API)](tutorials/relationship-api.md)
   * [Erstellen eines Ad-hoc-Schemas (API)](tutorials/ad-hoc.md)
* [Handbuch zur Fehlerbehebung](troubleshooting-guide.md)
* [API-Referenz](https://www.adobe.io/experience-platform-apis/references/schema-registry/)
* [Platform – Versionshinweise](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)