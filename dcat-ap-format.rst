==========================
DCAT-AP Switzerland Format
==========================

The following page is the reference documentation of the DCAT-AP Switzerland Format. 

Have a look at the following example for a quick start:

- Full dataset RDF example: `ogdch_dcatap_import.rdf <https://github.com/ogdch/dcat-ap-docs/blob/master/ogdch_dcatap_import.rdf>`_

----------
Namespaces
----------

.. code:: xml

  <rdf:RDF
   xmlns:dct="http://purl.org/dc/terms/"
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:dcat="http://www.w3.org/ns/dcat#"
   xmlns:foaf="http://xmlns.com/foaf/0.1/"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
   xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:vcard="http://www.w3.org/2006/vcard/ns#"
   xmlns:odrs="http://schema.theodi.org/odrs#"
   xmlns:schema="http://schema.org/">

--------------------
Internationalization
--------------------

The DCAT-AP for Switzerland Standard expects that text elements of the data sets and their distributions be translated in the following four languages:

- French (fr)
- German (de)
- Italian (it)
- English (en)

The multi-lingual elements have to contain the :code:`xml:lang` attribute, as the following example show:

.. code:: xml

  <dct:title xml:lang="fr">FR Titre</dct:title>
  <dct:title xml:lang="de">DE Titel</dct:title>
  <dct:title xml:lang="it">IT Titolo</dct:title>
  <dct:title xml:lang="en">EN Title</dct:title>

===============================
DCAT-AP reference documentation
===============================

----------------------------------
Definition of :code:`dcat:Dataset`
----------------------------------

:code:`dct:identifier`
----------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   yes
Cardinality 1..1
Description Unique identifier of the dataset across all publishers. A good way to make sure this identifier is unique is to link the source system ID with the ID of the publisher: :code:`<Source-Dataset-ID>@<Source-Organisation-ID>`
Example     :code:`<dct:identifier>325@swisstopo</dct:identifier>`
Open point  Who gives out the publisher ID ?
=========== ===

:code:`dct:title`
-----------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`xml:lang`
            Content     :code:`en` :code:`de` :code:`fr` :code:`it`
            Description Language of the element
            =========== =============================================
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   yes
Cardinality 1..n (one for each language)
Description The title of the dataset in the language defined by the :code:`xml:lang` attribute
Example     :code:`<dct:title xml:lang="de">Eisenbahnlärm Nacht</dct:title>`
=========== ===

:code:`dct:description`
-----------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`xml:lang`
            Content     :code:`en` :code:`de` :code:`fr` :code:`it`
            Description Language of the element
            =========== =============================================
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   yes - in all the languages in which distributions are available 
            TODO link to distribution
Cardinality 1..n (one for each language)
Description Description of the dataset in the language defined by the :code:`xml:lang` attribute
Example     :code:`<dct:description xml:lang="de">Die Karte zeigt, welcher Lärmbelastung die Bevölkerung durch den Schienenverkehr ausgesetzt ist.</dct:description>`
=========== ===

:code:`dct:issued`
------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#dateTime
            Description Type of the field
            =========== =============================================
Type        Date and time in ISO-8601_ format
Mandatory   Can be left out if there is no distribution
            TODO link to distribution
Cardinality 0..1
Description Date of the first publication of this dataset. If this date is unknown, the date of the first publication in this catalog can be used. If that date is in the future, the dataset is not displayed.
Example     :code:`<dct:issued rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-04-26T01:00:00Z</dct:issued>`
=========== ===

:code:`dct:modified`
--------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#dateTime
            Description Type of the field
            =========== =============================================
Type        Date and time in ISO-8601_ format
Mandatory   Only when the dataset has changed since the first publication.
Cardinality 0..1
Description Date of the last change (since the first publication on the portal).
Example     :code:`<dct:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2014-06-26T00:00:00Z</dct:modified>`
=========== ===

:code:`dct:publisher`
---------------------

=========== ===
Elements    :code:`rdf:Description`
Type        Nested element
Mandatory   yes
Cardinality 1..n
Description The publishers of the dataset. The :code:`rdf:about` attribute in the description must reference a TERMDAT
Example     .. code:: xml

              <dct:publisher>
                <rdf:Description rdf:about="Verweis auf TERMDAT-Eintrag">
                  <rdfs:label>Bundesamt für Landestopografie swisstopo</rdfs:label>
                </rdf:Description>
              </dct:publisher>
=========== ===

:code:`dcat:contactPoint`
-------------------------

=========== ===
Elements    :code:`vcard:Organization` 
Type        :code:`vcard:Kind`
Mandatory   yes
Cardinality 1..n
Description One or more contact email addresses for this dataset
            :code:`vcard:fn` Description of the point of contact
            :code:`vcard:hasEmail` has an attribute :code:`rdf:resource` which contains the email of the point of contact (including mailto:)
Example     .. code:: xml

              <dcat:contactPoint>
                <vcard:Organization>
               <vcard:fn>Abteilung Lärm BAFU</vcard:fn>
                  <vcard:hasEmail rdf:resource="mailto:noise@bafu.admin.ch"/>
                </vcard:Organization>
              </dcat:contactPoint>

              <dcat:contactPoint>
                <vcard:Individual>
                  <vcard:fn>Sekretariat BAFU</vcard:fn>
                  <vcard:hasEmail rdf:resource="mailto:sekretariat@bafu.admin.ch"/>
                </vcard:Individual>
              </dcat:contactPoint>
=========== ===

:code:`dcat:theme`
------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:resource`
            Description URI to the category
            =========== =============================================
Type        :code:`skos:Concept` http://www.w3.org/2009/08/skos-reference/skos.html#Concept
Mandatory   yes
Cardinality 1..n
Description Categorisation of the data. In the :code:`rdf:resource` attribute, the unique URI of the category from SKOS-RDF must be given.
            The following values are accepted from Themes_:

            - http://opendata.swiss/themes/Arbeit
            - http://opendata.swiss/themes/Bauwesen
            - http://opendata.swiss/themes/Bevoelkerung
            - http://opendata.swiss/themes/Bildung
            - http://opendata.swiss/themes/Energie
            - http://opendata.swiss/themes/Finanzen
            - http://opendata.swiss/themes/Geographie
            - http://opendata.swiss/themes/Gesetzgebung
            - http://opendata.swiss/themes/Gesundheit
            - http://opendata.swiss/themes/Handel
            - http://opendata.swiss/themes/Industrie
            - http://opendata.swiss/themes/Kriminalitaet
            - http://opendata.swiss/themes/Kultur
            - http://opendata.swiss/themes/Landwirtschaft
            - http://opendata.swiss/themes/Mobilitaet
            - http://opendata.swiss/themes/Sicherheit
            - http://opendata.swiss/themes/Politik
            - http://opendata.swiss/themes/Preise
            - http://opendata.swiss/themes/Raum
            - http://opendata.swiss/themes/Soziale-Sicherheit
            - http://opendata.swiss/themes/Statistische-Grundlagen
            - http://opendata.swiss/themes/Tourismus
            - http://opendata.swiss/themes/Verwaltung
            - http://opendata.swiss/themes/Volkswirtschaft
Example     :code:`<dcat:theme rdf:resource="http://opendata.swiss/themes/Bevoelkerung"/>`
=========== ===

:code:`dct:language`
--------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` ISO 639-1 two-letter code
Content     :code:`en` :code:`de` :code:`fr` :code:`it`
Mandatory   no
Cardinality 0..n (for each language)
Description Should contain all languages for which a distribution is available. 
            This field is not validated and is used for display purposes.
            If all distributions are language-independant, this field can be left out.
Example     :code:`<dct:language>de</dct:language>`
=========== ===

:code:`dct:relation`
--------------------

=========== ===
Elements    :code:`rdf:Description`
Type        Nested element
Mandatory   no
Cardinality 0..n
Description A relation to a document. The :code:`rdf:about` must link to a related document
Example     .. code:: xml

              <dct:relation>
                <rdf:Description rdf:about="http://www.bafu.admin.ch/laerm/index.html?lang=de">
                  <rdfs:label>Webseite des BAFU</rdfs:label>
                </rdf:Description>
              </dct:relation>
=========== ===

:code:`dcat:keyword`
--------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`xml:lang`
            Content     :code:`en` :code:`de` :code:`fr` :code:`it`
            Description Language of the element
            =========== =============================================
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no
Cardinality 0..n
Description Keyword who describe that dataset. 
            TODO check if TERMDAT is there
Example     .. code:: xml

              <dcat:keyword xml:lang="de" rdf:about="#nacht">Nacht</dcat:keyword>
              <dcat:keyword xml:lang="fr" rdf:about="#nacht">Nuit</dcat:keyword>
              <dcat:keyword xml:lang="it" rdf:about="#nacht">Noche</dcat:keyword>
              <dcat:keyword xml:lang="en" rdf:about="#nacht">Night</dcat:keyword>
=========== ===

:code:`dcat:landingPage`
------------------------

=========== ===
Attributes  
Type        :code:`foaf:Document` http://xmlns.com/foaf/spec/#term_Document
Mandatory   no
Cardinality 0..1
Description Website of the dataset with related information
Example     :code:`<dcat:landingPage>http://www.bafu.admin.ch/laerm/index.html?lang=de</dcat:landingPage>`
=========== ===

:code:`dct:spatial`
-------------------

=========== ===
Attributes  
Type        :code:`dct:Location` http://dublincore.org/documents/2012/06/14/dcmi-terms/?v=terms#Location
Mandatory   no
Cardinality 0..n
Description Geographical classification of the dataset. Can be a description, coordinates or a bounding-box.
Example     :code:`<dct:spatial rdf:resource="http://publications.europa.eu/mdr/authority/country/ZWE"/>`
=========== ===

:code:`dct:temporal`
--------------------

=========== ===
Attributes  
Type        :code:`ct:PeriodOfTime` http://dublincore.org/documents/2012/06/14/dcmi-terms/?v=terms#terms-PeriodOfTime
Mandatory   no
Cardinality 0..n
Description One or more time period that cover the dataset
            :code:`<schema:startDate>` contains the start date 
            :code:`<schema:endDate>` contains the end date 
            Format for dates: http://www.w3.org/2001/XMLSchema#date
Example     .. code:: xml

              <dct:temporal>
                <dct:PeriodOfTime>
                  <schema:startDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1905-03-01</schema:startDate>
                  <schema:endDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">2013-01-05</schema:endDate>
                </dct:PeriodOfTime>
              </dct:temporal>
=========== ===

:code:`dct:accrualPeriodicity`
------------------------------

=========== ===
Attributes  ===== =============================================
            Name  :code:`rdf:resource`
            Type  :code:`dct:Frequency`
            ===== =============================================
Mandatory   no
Cardinality 0..1
Description The frequency in which this dataset is updated.

            Values for :code:`dct:Frequency`: http://dublincore.org/groups/collections/frequency/
Example     :code:`<dct:accrualPeriodicity rdf:resource="http://purl.org/cld/freq/daily"/>`
=========== ===

:code:`rdfs:seeAlso`
--------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no
Cardinality 0..n
Description Link to related datasets. Contains the identifier of the linked dataset.
Example     :code:`<rdfs:seeAlso>326@swisstopo</rdfs:seeAlso>`
=========== ===

:code:`dcat:distribution`
-------------------------

=========== ===
Attributes  
Type        Nested elements. See `Definition of Distribution`_.
Mandatory   no
Cardinality 0..n
Description Distribution of the datasets.
Example     
=========== ===

--------------------------
Definition of Distribution
--------------------------

:code:`dct:identifier`
----------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no
Cardinality 0..1
Description Identifier of the distribution in the source system.
Example     :code:`<dct:identifier>ch.bafu.laerm-bahnlaerm_nacht</dct:identifier>`
=========== ===

:code:`dct:title`
-----------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`xml:lang`
            Content     :code:`en` :code:`de` :code:`fr` :code:`it`
            Description Language of the element
            =========== =============================================
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no - except if the distribution does not contain all the content of the dataset
Cardinality 0..n (one for each language)
Description The title of the distribution in the language defined by the :code:`xml:lang` attribute. If this element is left out, the :code:`dct:title` of the dataset is used instead
Example     :code:`<dct:title xml:lang="de">WMS (ch.bafu.laerm-bahnlaerm_nacht)</dct:title>`
=========== ===

:code:`dct:description`
-----------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`xml:lang`
            Content     :code:`en` :code:`de` :code:`fr` :code:`it`
            Description Language of the element
            =========== =============================================
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no - except if the distribution does not contain all the content of the dataset
Cardinality 1..n (one for each language)
Description Description of the distribution in the language defined by the :code:`xml:lang` attribute
Example     :code:`<dct:description xml:lang="de">Die Angaben basieren auf flächendeckenden Modellberechnungen.</dct:description>`
=========== ===

:code:`dct:issued`
------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#dateTime
            Description Type of the field
            =========== =============================================
Type        Date and time in ISO-8601_ format
Mandatory   yes
Cardinality 1..1
Description Date of the publication of this distribution
Example     :code:`<dct:issued rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2013-05-11T00:00:00Z</dct:issued>`
=========== ===

:code:`dct:modified`
--------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#dateTime
            Description Type of the field
            =========== =============================================
Type        Date and time in ISO-8601_ format
Mandatory   Only when the distribution has changed since the first publication. If this distribution was changed several times, this corresponds to the date of the latest change.
Cardinality 0..1
Description Date of the last change of the distribution.
Example     :code:`<dct:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2015-04-26T00:00:00Z</dct:modified>`
=========== ===

:code:`dct:language`
--------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` ISO 639-1 two-letter code
Content     :code:`en` :code:`de` :code:`fr` :code:`it`
Mandatory   no
Cardinality 0..n (for each language)
Description Languages in which this distribution is available. If the distribution is langauge-independant, this can be left out.
Example     :code:`<dct:language>de</dct:language>`
Open points What is this for exactly? The languages are defined on the fields with xml:lang already
=========== ===

:code:`dcat:accessURL`
----------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#anyURI
            Description Type of the field
            =========== =============================================
Type        http://www.w3.org/2001/XMLSchema#anyURI
Mandatory   yes
Cardinality 1..n
Description URL where the distribution can be found. This could be either a download URL, 
            a API URL or a landing page URL. If the distribution is only available through 
            a landing page, this field must contain the URL of the landing page.
            If a downloadURL was given for this distribution, this field has to contain the same value.
Example     :code:`<dcat:accessURL rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://wms.geo.admin.ch/</dcat:accessURL>`
=========== ===

:code:`dct:downloadURL`
-----------------------

=========== ===
Attributes  =========== =============================================
            Name        :code:`rdf:datatype`
            Content     http://www.w3.org/2001/XMLSchema#anyURI
            Description Type of the field
            =========== =============================================
Type        http://www.w3.org/2001/XMLSchema#anyURI
Mandatory   no
Cardinality 0..n
Description URL of a data file, if the distribution can be downloaded. For each of these, a :code:`dcat:accessURL` has to exist.
Example     :code:`<dcat:downloadURL rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://data.geo.admin.ch.s3.amazonaws.com/ch.swisstopo.swissboundaries3d-land-flaeche.fill/data.zip</dcat:downloadURL>`
=========== ===

:code:`dct:rights`
------------------

=========== ===
Attributes   
Type        Open Data Rights Statement Vocabulary (https://theodi.org/guides/publishers-guide-to-the-open-data-rights-statement-vocabulary)
Mandatory   yes
Cardinality 1..1
Description Rights statement on this distribution. This is composed of 3 elements that can be summarized in a 
            string literal (same concept as for the Creative Commons licenses)
            - Source Code : Mandatory/not mandatory
            - Non-commercial use : Allowed/not allowed
            - Commercial use : Allowed/not allowed/only with authorization
            
            TODO give out exact strings
Example     .. code:: xml

              <dct:rights>
                <odrs:dataLicence>ReferenceNotRequired-NonCommercialAllowed-CommercialAllowed</odrs:dataLicence>
              </dct:rights>
=========== ===

:code:`dct:license`
-------------------

=========== ===
Attributes  
Type        :code:`dct:LicenseDocument`
Mandatory   no
Cardinality 0..1
Description Not used, see :code:`dct:rights`
Example     :code:`<dct:license />`
=========== ===

:code:`dcat:byteSize`
---------------------

=========== ===
Attributes  
Type        :code:`rdfs:Literal` http://www.w3.org/TR/rdf-schema/#ch_literal
Mandatory   no - except if the distribution is available as a data download (see :code:`downloadURL`).
Cardinality 0..1
Description Size of the data in bytes
Example     :code:`<dcat:byteSize>1024</dcat:byteSize>`
=========== ===

:code:`dcat:mediaType`
----------------------

=========== ===
Attributes  
Type        :code:`dct:MediaTypeOrExtent` http://www.iana.org/assignments/media-types/media-types.xhtml
Mandatory   no - except if the distribution is available as a data download (see :code:`downloadURL`).
Cardinality 0..1
Description Only values from the list of IANA MIME types
            http://www.iana.org/assignments/media-types/media-types.xhtml
Example     :code:`<dcat:mediaType>text/html</dcat:mediaType>`
=========== ===

:code:`dct:format`
------------------

=========== ===
Attributes  
Type        :code:`dct:MediaTypeOrExtent`
Mandatory   no
Cardinality 0..1
Description Available for compatibility reasons. Not used
Example     :code:`<dct:format/>`
=========== ===

:code:`dct:coverage`
--------------------

=========== ===
Attributes  
Type        :code:`dct:LocationPeriodOrJurisdiction` http://dublincore.org/documents/2012/06/14/dcmi-terms/?v=terms#LocationPeriodOrJurisdiction
Mandatory   no
Cardinality 0..n
Description Distributions can be classified by their location or time period (for example, one for each canton, one for each year, etc...)
Example     :code:`<dct:coverage/>`
=========== ===


Common fields
-------------

:code:`rdf:Description`
-----------------------

=========== ===
Elements    :code:`rdfs:label`
Attributes  =========== =============================================
            Name        :code:`rdf:about`
            Mandatory   No
            =========== =============================================
Type        Sub-element
Mandatory   yes
Cardinality 1..1
Description The description of the dataset/distribution
=========== ===


.. _Themes: https://github.com/ogdch/ckanext-switzerland/blob/master/opendataswiss-themes.rdf
.. _ISO-8601: https://en.wikipedia.org/wiki/ISO_8601