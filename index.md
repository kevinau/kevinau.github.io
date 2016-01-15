---
layout: default
title: PennyLedger 
---
An open source, document based, accounting system.

<!--
{% include navbar.html here="home" %}
-->

What is this?
=============

PennyLedger is an accounting system for home used, clubs and societies and small business.  As far as possible, it uses source documents as the basis for all accounting entries.  The source documents can be PDF's or scanned images of paper documents.

PennyLedger is written in Java, using [OSGi](http://wiki.osgi.org/wiki/Main_Page).  It is a client-server application, with the clients being any modern web browser. 

PennyLedger is still under development.  It has not been finished yet, but work is proceeding at pace.

In more detail
==============

PennyLedger tries to do as much as possible to capture accounting information without configuration.  The steps are:

1. Source documents are imported.  Source documents can be PDF's, scanned images or text files.  Other document types could also be supported.  The "import" can be done by uploading a file using a web client, or dropping the document into a "hot" folder.  PennyLedger watches "hot" folders and imports any documents it finds there.  PennyLedger can also watch email folders and import attached documents from there.

2. All the text is extracted from the from the PDF's and OCR scanned images.  If a PDF contains a background image, or consists entirely of scanned images, these are also OCR'd and the text extracted.  The [Tesseract OCR](https://github.com/tesseract-ocr) engine is used by default, but other OCR engines can be substituted. 

3. Machine learning techniques are used to classify the imported document.  It uses the [Weka Bayesian Network](http://www.cs.waikato.ac.nz/~remco/weka_bn/) classifier to determine what type of document is being imported (invoice, statement, payment advice, etc), and what business entity produced the document (in Australia: Telstra, Optus, Commonwealth Bank, etc).  
   
   This works well, even when there OCR is not entirely accurate.  When the user reviews the imported document, if the classification is wrong, they have the opportunity to correct it.  The corrected classification is then fed back into the Weka classifier so that when another document is received it is more likely to be correctly classified.

4. Machine learning techniques are also used to identify significant fields of the imported document.  For example, the significant fields of an invoice are: invoice date, amount, reference number and a short description of what the invoice is for.

   The Hidden Markov Model (HMM) is used to identify these fields.  If the identification of the fields is wrong, the user can correct it.  The corrected identification is fed back into the HMM so that when another dividend statement is looked at, it is more likely that the fields will be correctly identified.

   This step works well for documents where the text is cleanly read.  That is, for PDFs or when the OCR of scanned documents is accurate.  It is possible to enter the information required, but the philosophy of this project is to minimise such data entry.

5. The significant fields are fed into a simple accounting system.  A document generates one or more accounting transactions, which flows onto different accounting sub-systems, such as debtors and creditors ledgers, and the final general ledger.  

   Across the world there are different rules for accounting systems.  For example, value added tax (VAT) in the UK is called a goods and service tax (GST) in Australia and New Zealand, and the rules are different in all countries.  This diversity is handled by using OSGi and having different code bundles, as necessary, to accommodate different accounting rules.  A single set of code bundles can be used when all the source documents originate from a single country, or they can be combined to support multi-country accounting.
While Java and OSGi supports internationalisation, PennyLedger have been developed using examples from UK, Australia and New Zealand.

Author
======

PennyLedger is being developed by Kevin Holloway.  He has spent 7½ years in England, and 18 months in New Zealand.  He now lives in his home town of Adelaide, Australia.

Kevin is now working on PennyLedger full time.  He previously worked as a Solutions Architect and Senior Developer on various customer facing, web based applications, that used the full suite of Java technologies.
