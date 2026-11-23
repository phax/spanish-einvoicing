# Spain - Mandatory B2B e-invoicing (SEFE / SPFE)

Spanish eInvoicing and Tax Reporting details.

Local copy of the primary sources for the Spanish mandatory B2B e-invoicing system, collected for
GitHub issue [#1](https://github.com/phax/spanish-einvoicing/issues/1) (originally phase4 issue #398).
The material was moved here from `docs/spain/` of the [phase4](https://github.com/phax/phase4)
repository, including its history.

Everything below is derived from the documents stored in this repository, not from secondary sources.

Status: 2026-11-23.

## Why this is relevant for phase4

The Spanish system is a two-tier model:

| Tier | Who | Transport |
|---|---|---|
| Public hub - **SPFE** (*Solucion Publica de Facturacion Electronica*), run by AEAT | anybody; mandatory recipient of "faithful copies" of all invoices | synchronous **web services** (SOAP 1.2, WSDLs published for the PRE environment) + web form, authenticated with electronic certificates. Not AS4, but the envelope is genuine **ebMS 3.0** with eBCore party IDs and CID-referenced MIME payloads, presented by AEAT as "compatible AS4 / Peppol" and carrying no WS-Security at all. |
| **Private platforms** (*plataformas privadas de intercambio de facturas electronicas*) | commercial e-invoicing service providers | RD 238/2026 Art. 13.1.b): must use secure transmission protocols "complying with the **AS2 or AS4** specifications" |

The AS4 *obligation* applies only to private-platform to private-platform interconnection.
The SPFE leg is a separate, ebMS-shaped protocol of AEAT's own design.
See [AS4-relevance.md](AS4-relevance.md) for the detailed analysis and the list of open questions.

## Timeline

* 2026-03-31 - RD 238/2026 published in the BOE
* 2026-04-17 - draft Ministerial Order (SPFE) opened for public consultation
* 2026-04-20 - RD 238/2026 in force (20 days after publication, DF cuarta.1)
* 2026-05-08 - public consultation (audiencia e informacion publica) on the draft Order closed
* 2026-05-19 - AEAT developer seminar on the SPFE
* 2026-08-06 - EU notification procedure under Directive (EU) 2015/1535 closed
* 2026-09-10 - AEAT seminar "Actualizacion sobre la SPFE"; decks published afterwards
* 2026-10-05 - Orden HAC/1028/2026 (the SPFE Ministerial Order) published in the BOE
* 2026-10-06 - Orden HAC/1028/2026 in force (day after publication, DF única); starts all deadlines
* 2026-10-16 - first SPFE developer documentation incl. WSDLs on the AEAT developer portal
* 2026-10-29 - revised WSDLs (SOAP 1.2)
* 2026-11-10 - request/response examples for all SPFE services
* 2026-11-19 - business rules for Anexo I and Anexo II (v0.1, draft, PDF only); WSDL package and
  service catalogue re-uploaded with minor corrections
* 2026-11-23 - error code lists (`errores_*.properties`) and the BG/BT to UBL 2.5 XPath lists on
  the portal (date of the HTTP `Last-Modified` header; the first publication may be earlier)
* ~2027-08-06 - latest date for the SPFE to be available (Order DA segunda: at least two months
  before the first effective application)
* ~2027-10-06 - e-invoicing and payment reporting for turnover > EUR 8 m; obligations for private
  platforms (RD Arts. 6, 8, 9 and 13) take effect (RD: +12 months, DF cuarta.1.a and .2)
* ~2028-10-06 - e-invoicing for the rest; payment reporting for incorporated SMEs (RD: +24 months)
* 2029-10 - payment reporting for the remaining small taxpayers (AEAT slides)

The dates marked `~` are calculated as "twelve / twenty-four months" after the entry into force of
the Order; they are not written in the Order itself. The AEAT slides of 2026-09-10 still assumed
an entry into force on 2026-10-01.

## Contents

| Folder | Contents |
|---|---|
| [legal/](legal/) | RD 238/2026 (BOE), the draft and the final Ministerial Order on the SPFE, PDF plus extracted plain text |
| [aeat/2026-05-19-seminario-spfe/](aeat/2026-05-19-seminario-spfe/) | The four documents of the AEAT developer seminar of 2026-05-19 |
| [aeat/2026-09-10-actualizacion-spfe/](aeat/2026-09-10-actualizacion-spfe/) | The three decks of the AEAT seminar of 2026-09-10 - technical SPFE services incl. the ebXML message examples, updated draft Order, Anexo I changes |
| [aeat/2026-10-16-documentacion-spfe/](aeat/2026-10-16-documentacion-spfe/) | First SPFE developer documentation: Anexo I, WSDL package (SOAP 1.1 bindings), service catalogue, input/output formats, validation description, SendInvoice example |
| [aeat/2026-10-29-documentacion-spfe/](aeat/2026-10-29-documentacion-spfe/) | Revised documentation: Anexo I and II, WSDL package with SOAP 1.2 bindings, service catalogue v0.1.3, input/output formats v0.1.2, SendInvoice example. Unchanged files are not repeated |
| [aeat/2026-11-13-documentacion-spfe/](aeat/2026-11-13-documentacion-spfe/) | Service catalogue v0.1.5 and the request/response examples 02-09 for all other services. Unchanged files are not repeated |
| [aeat/2026-11-23-documentacion-spfe/](aeat/2026-11-23-documentacion-spfe/) | Business rules for Anexo I (BR-ES-1 to BR-ES-31 plus rules per regime and VAT category) and Anexo II, both v0.1 of 2026-11-19 and still drafts; error code lists (business `RULE_*` and technical 4xxx/5xxx/8xxx); BG/BT to UBL 2.5 XPath lists incl. BG-ES/BT-ES; WSDL package (only `LEEME.txt` changed); service catalogue v0.1.5 (revision table and one endpoint corrected). Unchanged files are not repeated. No Schematron or other machine-readable rules |

In each `documentacion-spfe` folder, `soap/` and `wsdl/` hold the extracted contents of the ZIP
files next to them.

`*.txt` files are `pdftotext -layout` extractions of the PDF next to them, kept for searching.

`*.properties` files are stored byte-for-byte as downloaded: CRLF line endings, the `errores_*`
files in ISO-8859-1.

## Source pages

* AEAT developer portal - https://www.agenciatributaria.es/AEAT.desarrolladores/Desarrolladores/Desarrolladores.html
* SPFE developer documentation - https://www.agenciatributaria.es/AEAT.desarrolladores/Desarrolladores/_menu_/Documentacion/Solucion_Publica_de_Facturacion_Electronica__SPFE_/Solucion_Publica_de_Facturacion_Electronica__SPFE_.html
* Seminar 2026-05-19 - https://www.agenciatributaria.es/AEAT.desarrolladores/Desarrolladores/_menu_/Reuniones/Ejercicio_2026/Seminario_SPFE/Seminario_SPFE.html
* Seminar 2026-09-10, documents - https://www.agenciatributaria.es/AEAT.desarrolladores/Desarrolladores/_menu_/Reuniones/Ejercicio_2026/Seminarios_sobre_obligacion_de_facturacion_electronica_y_la_Solucion_Publica_de_Facturacion_Electronica__SPFE_/Seminario_actualizacion_sobre_la_Solucion_Publica_de_Facturacion_Electronica__SPFE__10_09_2026/Seminario_actualizacion_sobre_la_Solucion_Publica_de_Facturacion_Electronica__SPFE__10_09_2026.html
* Seminar 2026-09-10, announcement/registration only - https://www.agenciatributaria.es/AEAT.desarrolladores/Desarrolladores/_menu_/Reuniones/Ejercicio_2026/Actualizacion_sobre_la_Solucion_Publica_de_Facturacion_Electronica__SPFE_/Actualizacion_sobre_la_Solucion_Publica_de_Facturacion_Electronica__SPFE_.html
* Technical questions to AEAT: facturaelectronica@correo.aeat.es
