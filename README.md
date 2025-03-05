# createPDFA
How to create a PDFA with fpdf2

[TOC]

## Tutorial - Creating PDF/A Documents ##

### PDF/A Standards ###

<b>PDF/A-1</b> uses PDF-Version 1.4. All resources (pictures, graphics, fonts) must be embedded in the document. The color management must be precise and platform independently specified with ICC-Profiles and the document metadata must be given with XMP-Metadata.

<b>PDF/A-2</b> uses PDF-Version 1.7. It allows compression with JPEG2000, transparent elements, open type fonts and digital signatures.

The only extension for <b>PDF/A-3</b> is the possibility to embed any possible file.

### Conformance Classes ###

Level A (accessible) encompasses all the requirements of the standard, including mapping the content structure and the correct reading order of the document content. Text content must be extractable, and the structure must reflect the natural reading sequence.

Level B (Basic) guarantees a clear visual reproducibility of the content. Level B is generally easier to generate than Level A, but it does not ensure 100 percent text extraction or searchability. The hassle-free reuse of the content is not necessarily given.

To achieve this, here a little example:

```python
{% include "./tuto7.py" %}
```

[Resulting PDF](https://github.com/lka/createPDF/raw/master/tuto7.pdf) -
[fpdf2-logo](https://raw.githubusercontent.com/py-pdf/fpdf2/master/docs/fpdf2-logo.png)


```python
pdf = PDF()
```

The class PDF adds the needed embedded fonts using the
[add_font()](https://py-pdf.github.io/fpdf2/fpdf/fpdf.html#fpdf.fpdf.FPDF.add_font)
method for each style.

Then it adds the ICC profile object to the output intents array using the
[add_output_intent()](https://py-pdf.github.io/fpdf2/fpdf/fpdf.html#fpdf.fpdf.FPDF.output_intent)
method.

After adding first page, using the embedded font, writing some text, we create the pdf:
```python
pdf.create_pdf_with_metadata(
    filename="tuto7.pdf",
    language="en-US",
    title="Tutorial7",
    subject="Example for PDFA",
    creator=["John Dow", "Jane Dow"],
    description="this is my description of this file",
    keywords="Example Tutorial7"
    )
```

Here we use pikepdf to create the needed metadata and set the type to PDF/A-3B.

In the function `create_pdf_with_metadata` we need to set 'language' and 'subject' outside the metadata before we use pikepdf to achieve conformance.

Please use something like verapdf to check conformance of resulting PDF.