+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

![](vertopal_086167a40080407f987d15583582be65/media/image1.png){width="1.8333333333333333in"
height="1.8888888888888888in"}

**RAP Format Specification**

**Version 6.11**

**05 December 2013**

> *This is a Binding Permanent Reference Document of the GSMA*
>
> **Security Classification: Confidential - Full, Rapporteur, and
> Associate Members**
>
> Access to and distribution of this document is restricted to the
> persons permitted by the security classification. This document is
> confidential to the Association and is subject to copyright
> protection. This document is to be used only for the purposes for
> which it has been supplied and information contained in it must not be
> disclosed or in any other way made available, in whole or in part, to
> persons other than those permitted under the security classification
> without the prior written approval of the Association.
>
> **Copyright Notice**
>
> Copyright © 2013 GSM Association
>
> **Disclaimer**
>
> The GSM Association ("Association") makes no representation, warranty
> or undertaking (express or implied) with respect to and does not
> accept any responsibility for, and hereby disclaims liability for the
> accuracy or completeness or timeliness of the information contained in
> this document. The information contained in this document may be
> subject to change without prior notice.
>
> **Antitrust Notice**
>
> The information contain herein is in full compliance with the GSM
> Association's antitrust compliance policy.

+-----------------------------------+-----------------------------------+
| > V6.11                           | Page 1 of 46                      |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

**Table of Contents**

**1** **Introduction** **3**

> 1.1 Overview 3
>
> 1.2 Scope 3
>
> 1.3 Definitions 3
>
> 1.4 Abbreviations 3
>
> 1.5 References 4
>
> 1.6 Conventions 4

**2** **Rejects and Returns Process** **4**

> 2.1 Physical Format ASN.1 Considerations 4
>
> 2.1.1 Encoding of returned TAP data within RAP files 4
>
> 2.2 Creation of RAP Acknowledgement file 4
>
> 2.3 Private Interface Considerations 5
>
> 2.3.1 VPMN Sends TAP to VDCH; VDCH Sends RAP Back to VPMN 5
>
> 2.3.2 VDCH Receives RAP from HPMN, Forwards to VPMN 6
>
> 2.3.3 HPMN Sends RAP to HDCH; HDCH Adjusts RAP, Sends to VPMN 7
>
> 2.4 Considerations on where the VPMN and HPMN use the same DCH 8

**3** **Logical Structures** **10**

> 3.1 RAP File 10
>
> 3.1.1 Return Batch 10
>
> 3.1.2 RAP Batch Control Information 11
>
> 3.1.3 Fatal Return 12
>
> 3.1.4 Error Detail 13
>
> 3.1.5 RAP Audit Control Information 14
>
> 3.1.6 RAP Acknowledgement File 15

**4** **Data Dictionary** **15**

**5** **Physical Format** **28**

**6** **File Naming Conventions** **37**

> 6.1 Commercial RAP Data 37
>
> 6.2 Test RAP Data 37
>
> 6.3 Acknowledgement of Commercial RAP Data 37
>
> 6.4 Acknowledgement of Test RAP Data 38

**7** **Migration to a New Release** **38**

**Annex A** **IOT Related Errors** **39**

**Annex B** **Other Errors** **41**

**Annex C** **Minimum Content of RAP Disputes and Denials** **42**

**Document Management** **43**

> Document History 43
>
> Other Information 46

V6.11 Page 2 of 46

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **1 Introduction**
>
> **1.1** **Overview**
>
> This document defines the logical and physical data that must be
> transferred between PMNs under the Returned Account Procedure (RAP).
>
> The primary commercial requirement for data to be transferred is
> defined in BA.13 ‎\[3\].
>
> **1.2** **Scope**
>
> The version of RAP supported by this document is RAP Specification
> Version Number 1, RAP Release Version Number 5 (RAP1.5). The
> implementation timetable for this version of RAP is such that all RAP
> files created on or after 1 May 2011 (the Effective Date) must conform
> to this format specification.
>
> Section ‎7 contains information on migration to a new RAP release and
> TD.34 ‎\[5\] contains rules for release management and how to make
> changes to the RAP format).
>
> The transfer medium is beyond the scope.

+-----------------------------------+-----------------------------------+
| > **1.3**                         | > **Definitions**                 |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Term**                        | > **Description**                 |
+===================================+===================================+
| Appropriate TAP Standard          | > TAP3 as defined by TADIG        |
+-----------------------------------+-----------------------------------+
| > Private Interface               | > Any interface between the agent |
|                                   | > (DCH) and its client.           |
+-----------------------------------+-----------------------------------+
| > Public Interface                | > The interface between two PMNs. |
|                                   | >                                 |
|                                   | > This may occur within a single  |
|                                   | > agent (DCH).                    |
+-----------------------------------+-----------------------------------+
| > Validation                      | > Action taken by the HPMN to     |
|                                   | > ensure that TAP data being sent |
|                                   | > to it conforms to the           |
|                                   | > appropriate TAP standard.       |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **1.4**                         | > **Abbreviations**               |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Term**                        | > **Description**                 |
+===================================+===================================+
| > ASN.1                           | > Abstract Syntax Notation 1      |
+-----------------------------------+-----------------------------------+
| > BER                             | > Basic Encoding Rules            |
+-----------------------------------+-----------------------------------+
| > CAMEL                           | > Customised Application Mobile   |
|                                   | > Enhanced Logic                  |
+-----------------------------------+-----------------------------------+
| > DCH                             | > Data Clearing House             |
+-----------------------------------+-----------------------------------+
| > EC                              | > Executive Committee             |
+-----------------------------------+-----------------------------------+
| > EMC                             | > Executive Management Committee  |
+-----------------------------------+-----------------------------------+
| > GPRS                            | > General Packet Radio Service    |
+-----------------------------------+-----------------------------------+
| > HDCH                            | > Home DCH, agent of the HPMN     |
+-----------------------------------+-----------------------------------+
| > HPMN                            | > Home PMN                        |
+-----------------------------------+-----------------------------------+
| > IOT                             | > Inter Operator Tariff           |
+-----------------------------------+-----------------------------------+
| > ISDN                            | > Integrated Services Digital     |
|                                   | > Network                         |
+-----------------------------------+-----------------------------------+
| > MSC                             | > Mobile Switching Centre         |
+-----------------------------------+-----------------------------------+
| > PMN                             | > Public Mobile Network           |
+-----------------------------------+-----------------------------------+
| > PRD                             | > Permanent Reference Document    |
+-----------------------------------+-----------------------------------+

> V6.11 Page 3 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Term**                        | > **Description**                 |
+===================================+===================================+
| > RAP                             | > Returned Account Procedure      |
+-----------------------------------+-----------------------------------+
| > SDR                             | > Special Drawing Right           |
+-----------------------------------+-----------------------------------+
| > TADIG                           | > Transferred Account Data        |
|                                   | > Interchange Group               |
+-----------------------------------+-----------------------------------+
| > TAP                             | > Transferred Account Procedure   |
+-----------------------------------+-----------------------------------+
| > UTC                             | > Universal Time Co-ordinated     |
+-----------------------------------+-----------------------------------+
| > VAT                             | > Value Added Tax                 |
+-----------------------------------+-----------------------------------+
| > VDCH                            | > Visited DCH, agent of the VPMN  |
+-----------------------------------+-----------------------------------+
| > VPMN                            | > Visited PMN                     |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **1.5**                         | > **References**                  |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------+-----------------------+-----------------------+
| > **Ref**             | **Doc Number**        | > **Title**           |
+=======================+=======================+=======================+
| \[1\]                 | > PRD BA.08           | > Timescales for Data |
|                       |                       | > Transfer            |
+-----------------------+-----------------------+-----------------------+
| \[2\]                 | > PRD BA.11           | > Treatment of        |
|                       |                       | > Exchange Rates for  |
|                       |                       | > Billing and Payment |
+-----------------------+-----------------------+-----------------------+
| \[3\]                 | > PRD BA.13           | > Returned Account    |
|                       |                       | > Procedure           |
+-----------------------+-----------------------+-----------------------+
| \[4\]                 | > PRD TD.13           | > TADIG Code Naming   |
|                       |                       | > Conventions         |
+-----------------------+-----------------------+-----------------------+
| \[5\]                 | > PRD TD.34           | > Release Management  |
|                       |                       | > Processes           |
+-----------------------+-----------------------+-----------------------+
| \[6\]                 | > PRD TD.57           | > TAP3 Format         |
|                       |                       | > Specification       |
+-----------------------+-----------------------+-----------------------+
| \[7\]                 | > RFC 2119            | > "Key words for use  |
|                       |                       | > in RFCs to Indicate |
|                       |                       | > Requirement         |
|                       |                       | > Levels", S.         |
|                       |                       | > Bradner, March      |
|                       |                       | > 1997. Available at  |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------+-----------------------------------+
| > **1.6**                         | > **Conventions**                 |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> The key words "must", "must not", "required", "shall", "shall not",
> "should", "should not",
>
> "recommended", "may", and "optional" in this document are to be
> interpreted as described in
>
> RFC 2119 ‎\[7\].
>
> **2 Rejects and Returns Process**
>
> The Rejects and Returns Process flow is described in BA.13 ‎\[3\].
>
> **2.1** **Physical Format ASN.1 Considerations**
>
> **2.1.1** **Encoding of Returned TAP data within RAP files**
>
> The returned ASN.1 group must be the original received from the VPMN,
> and not re-encoded.
>
> **2.2** **Creation of RAP Acknowledgement File**
>
> A RAP Acknowledgement File is not in any way related to the decoding
> of and/or processing of the contents of the RAP file. The necessary
> information (Sender, Recipient, RAP File Sequence Number, File Type
> Indicator) needed to produce the RAP Acknowledgement File can be found
> in the RAP file name, so as long as those elements can be identified,
> the Recipient of the RAP file must send a RAP Acknowledgement File
> back to the Sender of the RAP file.
>
> V6.11 Page 4 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

**2.3** **Private Interface Considerations**

An operator may employ an agent, for example a Data Clearing House
(DCH), to perform services such as validation of TAP data. This section
describes how RAP files can be created and handled between the operator
and its agent, in the 'private interface' between these entities. This
is strictly voluntary and subject to agreement between the operator and
its agent, and does not have any impact on the 'public interface'.

To facilitate the creation and transfer of RAP data between the operator
and its agent, an optional element in the RAP Batch Control Information,
the Roaming Partner element, can be used.

**Note:** If this element is present on the 'public interface', the
whole RAP file may be rejected due to an ASN.1 syntax error.

The following sections describe three scenarios where an operator and
its agent interact in the Returned Account Procedure:\
1. The VPMN sends a TAP file to its agent (VDCH), and the agent finds
errors and sends a RAP file back to the VPMN.

> 2\. The agent (VDCH) receives a RAP file from its customer's roaming
> partner (or its agent), and the VDCH forwards the RAP file to its
> customer (VPMN).
>
> 3\. The HPMN creates a RAP file for a TAP file it receives from its
> roaming partner; the HPMN sends the RAP file to its agent (HDCH),
> which then adjusts the RAP file to meet Public Interface requirements,
> and sends it to the VPMN or its agent.

**Note:** In all cases, file naming of RAP files and RAP Acknowledgement
files follows the normal file naming conventions defined in Section ‎6.

**2.3.1** **VPMN Sends TAP to VDCH; VDCH Sends RAP Back to VPMN**

In this scenario:\
• The VPMN sends a TAP file to its agent (VDCH).

> • The agent validates the file, finds errors, and creates a RAP file
> to return the errors to the VPMN.
>
> • The agent forwards the rest of the TAP file to the HPMN roaming
> partner or its agent (unless the errors were Fatal or Missing).

The TAP file created by VPMN and forwarded to the VDCH will be as
normal: • Sender: VPMN

> • Recipient: HPMN
>
> • Sequence: 1

The RAP file created by the VDCH will contain the optional Roaming
Partner element: • Sender: VDCH

> • Recipient: VPMN
>
> • Sequence: 1 (the next RAP sequence for this VDCH/VPMN pair)
>
> • Roaming Partner: HPMN

File naming for the RAP file will follow the standards in Section ‎6
(Sender will be VDCH, Recipient will be VPMN).

The VDCH forwards the valid portion of the TAP file to the roaming
partner (or its agent) as normal (unless the errors were Fatal or
Missing):\
• Sender: VPMN

> • Recipient: HPMN

V6.11 Page 5 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

> • Sequence: 1

In this scenario, note the following:

> • The sequence numbering of the TAP file and RAP file are independent.
> In the
>
> example, it is coincidental that the sequence numbers are the same.
>
> • When creating RAP files, the VDCH must create a separate RAP file
> for each of the
>
> VPMN's roaming partners; that is, it cannot combine returned data for
> more than one
>
> HPMN into the same RAP file.

+-----------------------+-----------------------+-----------------------+
| > •\                  | > The VPMN will need  |                       |
| > •                   | > to adjust the value |                       |
|                       | > of the TAP file on  |                       |
|                       | > the invoice it      |                       |
|                       | > sends to its        |                       |
|                       | > roaming partner, to |                       |
|                       | > reflect the amount  |                       |
|                       | > that was actually   |                       |
|                       | > forwarded to the    |                       |
|                       | > partner. If the     |                       |
|                       | > VPMN desires to     |                       |
|                       | > send a RAP          |                       |
|                       | > Acknowledgement     |                       |
|                       | > File to its agent,  |                       |
|                       | > it would include    |                       |
|                       | > the following:      |                       |
+=======================+=======================+=======================+
|                       | •                     | > Sender: VPMN        |
+-----------------------+-----------------------+-----------------------+
|                       | •                     | > Recipient: VDCH     |
+-----------------------+-----------------------+-----------------------+
|                       | •                     | > Sequence: 1         |
+-----------------------+-----------------------+-----------------------+

**Note:** The Roaming Partner element is not contained in the RAP
Acknowledgement file. File

naming will follow the standards in Section ‎6 (Sender will be VPMN,
Recipient will be

VDCH).

**2.3.2** **VDCH Receives RAP from HPMN, Forwards to VPMN**

In this scenario:

> • The VPMN has created a TAP file and sent it to its agent (VDCH).
>
> • The agent forwarded the TAP file to the HPMN's agent or, if it
> doesn't use an agent,
>
> directly to the HPMN.

+-----------------------------------+-----------------------------------+
| > •\                              | > The HPMN/agent discovers errors |
| > •\                              | > and creates a RAP file. It      |
| > •                               | > processes the remainder of the  |
|                                   | > TAP file as normal (unless the  |
|                                   | > errors were Fatal or Missing).  |
|                                   | >                                 |
|                                   | > The HPMN/agent sends the RAP    |
|                                   | > file to the VDCH.               |
|                                   | >                                 |
|                                   | > The VDCH in turn sends the RAP  |
|                                   | > file to the VPMN. The VDCH      |
|                                   | > sends a RAP Acknowledgement     |
|                                   | > file to the HPMN/agent.         |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

In this case, the VDCH merely passes the RAP file to the VPMN. It makes
no changes to

the RAP file.

<table style="width:100%;">
<colgroup>
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="9">The TAP file created by the VPMN and forwarded to the
VDCH will be as normal: • Sender: VPMN</th>
<th rowspan="8"><blockquote>
<p>same</p>
</blockquote></th>
</tr>
<tr class="odd">
<th>•</th>
<th colspan="8"><blockquote>
<p>Recipient: HPMN</p>
</blockquote></th>
</tr>
<tr class="header">
<th>•</th>
<th colspan="8"><blockquote>
<p>Sequence: 2</p>
</blockquote></th>
</tr>
<tr class="odd">
<th colspan="2"><p>The VDCH forwards this file to</p>
<p>Sender/Recipient/Sequence Number.</p></th>
<th>the</th>
<th>HPMN</th>
<th>or</th>
<th>its</th>
<th>agent</th>
<th>with</th>
<th>the</th>
</tr>
<tr class="header">
<th colspan="9">The RAP file created by the HPMN/agent will be as
normal: • Sender: HPMN</th>
</tr>
<tr class="odd">
<th>•</th>
<th colspan="8"><blockquote>
<p>Recipient: VPMN</p>
</blockquote></th>
</tr>
<tr class="header">
<th>•</th>
<th colspan="8"><blockquote>
<p>Sequence: 1 (the next RAP sequence number for this HPMN/VPMN
pair)</p>
</blockquote></th>
</tr>
<tr class="odd">
<th>•</th>
<th colspan="8"><blockquote>
<p>Roaming Partner: Not present</p>
</blockquote></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

The HPMN/agent sends this RAP file to the VDCH. The remainder of the TAP
file will be

processed by the HPMN/agent as normal (unless the errors were Fatal or
Missing).

V6.11 Page 6 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

**Note:** In this scenario, if the HPMN creates the RAP file, it's
assumed that it doesn't use an

agent (HDCH). See Section ‎2.3.3 for the scenario where the HPMN uses an
agent (HDCH)

and creates a RAP file.

The VDCH forwards the RAP file to the VPMN as-is; it makes no changes
(the Roaming

Partner element is not used):

> • Sender: HPMN
>
> • Recipient: VPMN
>
> • Sequence: 1
>
> • Roaming Partner: Not present

The VDCH creates and sends a RAP Acknowledgement file to the HPMN/agent
as normal:

> • Sender: VPMN
>
> • Recipient: HPMN
>
> • Sequence: 1

File naming for the RAP Acknowledgement file will follow the standards
in Section ‎6 (Sender

will be VPMN, Recipient will be HPMN).

In this scenario, note the following:

> • The normal TD.32 rules are followed. The VDCH merely passes along to
> the VPMN
>
> the RAP file that was created by the HPMN or its agent.
>
> • Financial adjustments are handled according to normal Rejects and
> Returns
>
> procedures. The HPMN is not liable for the charges returned to the
> VPMN.
>
> • If the VPMN desires to send a RAP Acknowledgement file to its agent
> (not
>
> recommended), it would include the following:
>
> • Sender: VPMN
>
> • Recipient: HPMN
>
> • Sequence: 1

File naming for the RAP Acknowledgement file would follow the standards
in Section ‎6

(Sender will be VPMN, Recipient will be HPMN).

**2.3.3** **HPMN Sends RAP to HDCH; HDCH Adjusts RAP, Sends to VPMN**

In this scenario:

> • The HPMN has received a TAP file, via its agent, from its roaming
> partner (VPMN) or
>
> its agent.
>
> • The HPMN finds errors in the file and creates a RAP file. It
> forwards the RAP file to
>
> its agent (HDCH). It processes the remainder of the TAP file as normal
> (unless the
>
> errors were Fatal or Missing).
>
> • The HDCH makes adjustments to the RAP file to prepare it for the
> Public Interface,
>
> and forwards it to the VPMN or its agent.

The TAP file that was received by the HPMN was as follows:

> • Sender: VPMN
>
> • Recipient: HPMN
>
> • Sequence: 3

The RAP file created by the HPMN will use the Roaming Partner element.
The RAP file will

be as follows:

V6.11 Page 7 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

> • Sender: HPMN
>
> • Recipient: HDCH
>
> • Sequence: 1 (the next RAP sequence for this HPMN/HDCH pair)
>
> • Roaming Partner: VPMN

File naming for the RAP file will follow the standards in Section ‎6
(Sender will be HPMN,

Recipient will be HDCH). The HPMN forwards this RAP file to its agent
(HDCH). It

processes the remainder of the TAP file as normal (unless the errors
were Fatal or Missing).

The HDCH adjusts the RAP file to prepare it for the Public Interface,
changing the Recipient

to the VPMN, changing the Sequence to the next number for that HPMN/VPMN
pair, and

removing the Roaming Partner element:

> • Sender: HPMN
>
> • Recipient: VPMN
>
> • Sequence: 2 (the next RAP sequence for that HPMN/VPMN pair)
>
> • Roaming Partner: Not present

File naming for the RAP file will follow the standards in Section ‎6
(Sender will be HPMN,

Recipient will be VPMN). The HDCH forwards this RAP file to the VPMN or
its agent.

In this scenario, note the following:

> • When creating RAP files, the HPMN must create a separate RAP file
> for each of its
>
> roaming partners; that is, it cannot combine returned data for more
> than one VPMN
>
> into the same RAP file.
>
> • If the HDCH desires to send a RAP Acknowledgement File to the HPMN,
> it would
>
> include the following:
>
> • Sender: HDCH
>
> • Recipient: HPMN
>
> • Sequence: 1
>
> • The Roaming Partner element is not contained in the RAP
> Acknowledgement file.
>
> File naming will follow the standards in Section ‎6 (Sender will be
> HDCH, Recipient
>
> will be HPMN).
>
> • Financial adjustments will be handled according to normal Rejects
> and Returns
>
> procedures. The HPMN is not liable for the charges returned to the
> VPMN.

**2.4** **Considerations on where the VPMN and HPMN use the same DCH**

Where the VPMN and HPMN use the same DCH, a public interface exists
inside this DCH.

In this situation the involved DCH must support the generation and
handling of public RAP

files. All services applied to the TAP file on behalf of the VPMN are
carried out before the

TAP file is made available to the HPMN on the public interface. Such
services may include,

but are not limited to, TAP release conversion and validation.

The public TAP file is validated on behalf of the HPMN and any rejected
TAP records must

be included in a public RAP file made available to the VPMN. All
appropriate binding PRDs

apply to public interfaces TAP and RAP files.

Any additional services carried out on the TAP file on behalf of the
HPMN are within the

private interface between the DCH and the HPMN. Additional services may
include, but are

not limited to, TAP release conversion.

The following scenario applies:

V6.11 Page 8 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

> • The VPMN creates a TAP file and sents it to its DCH.
>
> • The DCH may validate the TAP file on behalf of the VPMN and
> potentially create a
>
> private RAP.
>
> • A TAP release conversion is done on behalf of VPMN if necessary.
>
> • Optionally, the DCH can validate on behalf of the VPMN and generate
> a private RAP
>
> file, if necessary.
>
> • The DCH validates on behalf of the HPMN, discovers errors and
> creates a public
>
> RAP file according to timescale defined in BA.08 ‎\[1\]. It processes
> the remainder of
>
> the TAP file as normal, and sends it to the HPMN (unless the errors
> were Fatal).
>
> • The RAP file must be loaded, acknowledged and sent to the VPMN.
>
> • Financial adjustments are handled according to normal Rejects and
> Returns
>
> procedures. The HPMN is not liable for charges in TAP records returned
> to the
>
> VPMN.

V6.11 Page 9 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image2.png){width="5.569444444444445in"
height="3.763888888888889in"}

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **3 Logical Structures**

+-----------------------------------+-----------------------------------+
| > **3.1**\                        | > **RAP File**\                   |
| > **3.1.1**                       | > **Return Batch**                |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------------------------------------------+
| > Return\                                                             |
| > Batch                                                               |
|                                                                       |
| <table style="width:100%;">                                           |
| <colgroup>                                                            |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| <col style="width: 6%" />                                             |
| </colgroup>                                                           |
| <thead>                                                               |
| <tr class="header">                                                   |
| <th colspan="2" rowspan="2"><blockquote>                              |
| <p>RAP Batch Control<br />                                            |
| Information M</p>                                                     |
| </blockquote></th>                                                    |
| <th colspan="7"><blockquote>                                          |
| <p>Return<br />                                                       |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>Severe Return</p>                                                  |
| </blockquote></th>                                                    |
| <th rowspan="3">o</th>                                                |
| <th rowspan="3"><blockquote>                                          |
| <p>RAP Audit Control<br />                                            |
| Information M</p>                                                     |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="5"><blockquote>                              |
| <p>Error<br />                                                        |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| <th rowspan="8"><blockquote>                                          |
| <p>Operator<br />                                                     |
| Specific<br />                                                        |
| Information O R</p>                                                   |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="5">M</th>                                                |
| <th colspan="2">R</th>                                                |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th><blockquote>                                                      |
| <p>Stop<br />                                                         |
| Return</p>                                                            |
| </blockquote></th>                                                    |
| <th><blockquote>                                                      |
| <p>o</p>                                                              |
| </blockquote></th>                                                    |
| <th><blockquote>                                                      |
| <p>Missing Return</p>                                                 |
| </blockquote></th>                                                    |
| <th colspan="2"><blockquote>                                          |
| <p>o</p>                                                              |
| </blockquote></th>                                                    |
| <th colspan="3">Fatal<br />                                           |
| Return</th>                                                           |
| <th><blockquote>                                                      |
| <p>o</p>                                                              |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2" rowspan="2">M</th>                                    |
| <th>M</th>                                                            |
| <th colspan="6">M</th>                                                |
| <th colspan="2">M</th>                                                |
| <th rowspan="5"><blockquote>                                          |
| <p>Call<br />                                                         |
| Event<br />                                                           |
| Details<br />                                                         |
| M</p>                                                                 |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th colspan="2">Start Missing<br />                                   |
| Sequence<br />                                                        |
| Number Range</th>                                                     |
| <th colspan="2">End Missing<br />                                     |
| Sequence<br />                                                        |
| Number Range</th>                                                     |
| <th colspan="3" rowspan="2"><blockquote>                              |
| <p>Operator<br />                                                     |
| Specific<br />                                                        |
| Information O</p>                                                     |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="4"><blockquote>                              |
| <p>File<br />                                                         |
| Sequence Number M</p>                                                 |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2" rowspan="2">Last<br />                                |
| Sequence<br />                                                        |
| Number</th>                                                           |
| <th colspan="2">M</th>                                                |
| <th colspan="2"><blockquote>                                          |
| <p>C</p>                                                              |
| </blockquote></th>                                                    |
| <th rowspan="3">M</th>                                                |
| <th rowspan="3">R</th>                                                |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th colspan="7" rowspan="2"><blockquote>                              |
| <p>Operator<br />                                                     |
| Specific<br />                                                        |
| Information<br />                                                     |
| O</p>                                                                 |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| </thead>                                                              |
| <tbody>                                                               |
| </tbody>                                                              |
| </table>                                                              |
+=======================================================================+
+-----------------------------------------------------------------------+

**Figure 1: Return Batch Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > Return Batch        |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > RAP Batch Control   |                       | > ‎Figure 2:           |
| > Information         |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Return Detail       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Stop Return         |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Missing Return      |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Fatal Return        |                       | > ‎Figure 3:           |
+-----------------------+-----------------------+-----------------------+
| > Severe Return       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Call Event Details  |                       | > Appropriate TAP     |
|                       |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Error Detail        | > ‎Figure 3:           | > ‎Figure 4:           |
+-----------------------+-----------------------+-----------------------+
| > RAP Audit Control   |                       | > ‎Figure 5:           |
| > Information         |                       |                       |
+-----------------------+-----------------------+-----------------------+

**Table 1: Return Batch Group Elements**

> V6.11 Page 10 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image3.png){width="5.763888888888889in"
height="2.138888888888889in"}

+-----------------------+-----------------------+-----------------------+
| > GSM Association     |                       | > Confidential -      |
|                       |                       | > Full, Rapporteur,   |
|                       |                       | > and Associate       |
|                       |                       | > Members             |
+=======================+=======================+=======================+
| > Official Document   |                       |                       |
| > TD.32 - RAP Format  |                       |                       |
| > Specification       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > **3.1.2**           | > **RAP Batch Control |                       |
|                       | > Information**       |                       |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------------------------------------------+
| > RAP Batch\                                                          |
| > Control\                                                            |
| > Information                                                         |
|                                                                       |
| <table>                                                               |
| <colgroup>                                                            |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| <col style="width: 8%" />                                             |
| </colgroup>                                                           |
| <thead>                                                               |
| <tr class="header">                                                   |
| <th rowspan="2">Sender</th>                                           |
| <th rowspan="2"><blockquote>                                          |
| <p>RAP File Sequence</p>                                              |
| </blockquote></th>                                                    |
| <th rowspan="2"><blockquote>                                          |
| <p>RAP File Creation</p>                                              |
| </blockquote></th>                                                    |
| <th rowspan="2">RAP File Available</th>                               |
| <th rowspan="2">Specification Version</th>                            |
| <th colspan="2"><blockquote>                                          |
| <p>RAP Specif.</p>                                                    |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="2"><blockquote>                              |
| <p>File<br />                                                         |
| Type</p>                                                              |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="2"><blockquote>                              |
| <p>Operator Specific</p>                                              |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>TAP<br />                                                          |
| Currency</p>                                                          |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2"><blockquote>                                          |
| <p>Version</p>                                                        |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th colspan="2">Number</th>                                           |
| <th>Timestamp</th>                                                    |
| <th>Timestamp</th>                                                    |
| <th>Number</th>                                                       |
| <th colspan="2"><blockquote>                                          |
| <p>Number</p>                                                         |
| </blockquote></th>                                                    |
| <th colspan="2">Indicator</th>                                        |
| <th colspan="2">Information</th>                                      |
| </tr>                                                                 |
| </thead>                                                              |
| <tbody>                                                               |
| <tr class="odd">                                                      |
| <td><blockquote>                                                      |
| <p>M</p>                                                              |
| </blockquote></td>                                                    |
| <td>M</td>                                                            |
| <td><blockquote>                                                      |
| <p>M</p>                                                              |
| </blockquote></td>                                                    |
| <td><blockquote>                                                      |
| <p>M</p>                                                              |
| </blockquote></td>                                                    |
| <td><blockquote>                                                      |
| <p>C</p>                                                              |
| </blockquote></td>                                                    |
| <td colspan="2"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></td>                                                    |
| <td colspan="2">C</td>                                                |
| <td>O</td>                                                            |
| <td>R</td>                                                            |
| <td><blockquote>                                                      |
| <p>C</p>                                                              |
| </blockquote></td>                                                    |
| </tr>                                                                 |
| <tr class="even">                                                     |
| <td colspan="2" rowspan="2">Recipient</td>                            |
| <td rowspan="2">UTC<br />                                             |
| Time Offset</td>                                                      |
| <td rowspan="2">UTC<br />                                             |
| Time Offset</td>                                                      |
| <td colspan="2"><blockquote>                                          |
| <p>Release<br />                                                      |
| Version</p>                                                           |
| </blockquote></td>                                                    |
| <td colspan="2" rowspan="2">RAP Release Version</td>                  |
| <td colspan="2" rowspan="2"><blockquote>                              |
| <p>Roaming Partner</p>                                                |
| </blockquote></td>                                                    |
| <td colspan="2" rowspan="2"><blockquote>                              |
| <p>TAP<br />                                                          |
| Decimal<br />                                                         |
| Places</p>                                                            |
| </blockquote></td>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <td colspan="2">Number</td>                                           |
| </tr>                                                                 |
| <tr class="even">                                                     |
| <td colspan="2">M</td>                                                |
| <td>M</td>                                                            |
| <td><blockquote>                                                      |
| <p>M</p>                                                              |
| </blockquote></td>                                                    |
| <td>C</td>                                                            |
| <td colspan="2">M</td>                                                |
| <td colspan="3">O</td>                                                |
| <td colspan="2"><blockquote>                                          |
| <p>C</p>                                                              |
| </blockquote></td>                                                    |
| </tr>                                                                 |
| </tbody>                                                              |
| </table>                                                              |
+=======================================================================+
+-----------------------------------------------------------------------+

**Figure 2: RAP Batch Control Information Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > RAP Batch Control   | > ‎Figure 1:           |                       |
| > Information         |                       |                       |
+-----------------------+-----------------------+-----------------------+

**Table 2: RAP Batch Control Information Group Elements**

> V6.11 Page 11 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image4.png){width="5.902777777777778in"
height="2.888888888888889in"}

+-----------------------+-----------------------+-----------------------+
| > GSM Association     |                       | > Confidential -      |
|                       |                       | > Full, Rapporteur,   |
|                       |                       | > and Associate       |
|                       |                       | > Members             |
+=======================+=======================+=======================+
| > Official Document   |                       |                       |
| > TD.32 - RAP Format  |                       |                       |
| > Specification       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > **3.1.3**           | > **Fatal Return**    |                       |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------------------------------------------+
| > Fatal\                                                              |
| > Return                                                              |
|                                                                       |
| <table>                                                               |
| <colgroup>                                                            |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| <col style="width: 9%" />                                             |
| </colgroup>                                                           |
| <thead>                                                               |
| <tr class="header">                                                   |
| <th rowspan="3">File<br />                                            |
| Sequence</th>                                                         |
| <th colspan="2" rowspan="2"><blockquote>                              |
| <p>Notification</p>                                                   |
| </blockquote></th>                                                    |
| <th>Batch</th>                                                        |
| <th rowspan="4">Accounting Information Error</th>                     |
| <th rowspan="4"><blockquote>                                          |
| <p>Network Information Error</p>                                      |
| </blockquote></th>                                                    |
| <th>VAS</th>                                                          |
| <th rowspan="4"><blockquote>                                          |
| <p>Message<br />                                                      |
| Description Error</p>                                                 |
| </blockquote></th>                                                    |
| <th colspan="2">Audit Control</th>                                    |
| <th>Operator</th>                                                     |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th rowspan="3"><blockquote>                                          |
| <p>Control<br />                                                      |
| Error</p>                                                             |
| </blockquote></th>                                                    |
| <th rowspan="3">Information Error</th>                                |
| <th rowspan="4"><blockquote>                                          |
| <p>Information Error<br />                                            |
| C</p>                                                                 |
| </blockquote></th>                                                    |
| <th rowspan="4">R</th>                                                |
| <th rowspan="14"><blockquote>                                         |
| <p>Specific<br />                                                     |
| Information O R</p>                                                   |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th colspan="2" rowspan="2">Error</th>                                |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th>Number</th>                                                       |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th><blockquote>                                                      |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| <th colspan="2">C</th>                                                |
| <th><blockquote>                                                      |
| <p>C</p>                                                              |
| </blockquote></th>                                                    |
| <th><blockquote>                                                      |
| <p>C</p>                                                              |
| </blockquote></th>                                                    |
| <th><blockquote>                                                      |
| <p>C</p>                                                              |
| </blockquote></th>                                                    |
| <th>C</th>                                                            |
| <th>C</th>                                                            |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th rowspan="5"><blockquote>                                          |
| <p>Transfer Batch Error<br />                                         |
| C</p>                                                                 |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="2"><blockquote>                              |
| <p>Notification</p>                                                   |
| </blockquote></th>                                                    |
| <th rowspan="2">Batch Control Information</th>                        |
| <th>Accounting</th>                                                   |
| <th>Network</th>                                                      |
| <th>VAS</th>                                                          |
| <th>Message Desc</th>                                                 |
| <th colspan="2" rowspan="5"><blockquote>                              |
| <p>Audit Control Information 3</p>                                    |
| <p>M 4 :</p>                                                          |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th>Information</th>                                                  |
| <th>Information</th>                                                  |
| <th rowspan="2">Information</th>                                      |
| <th rowspan="2">Information</th>                                      |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2" rowspan="2">M</th>                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th rowspan="2"><blockquote>                                          |
| <p>M</p>                                                              |
| </blockquote></th>                                                    |
| <th rowspan="2">M</th>                                                |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th colspan="2"><blockquote>                                          |
| <p>R</p>                                                              |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th rowspan="2">Error</th>                                            |
| <th colspan="2">Error</th>                                            |
| <th>Error</th>                                                        |
| <th>Error</th>                                                        |
| <th rowspan="3"><blockquote>                                          |
| <p>Error<br />                                                        |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>Error<br />                                                        |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| <th rowspan="3"><blockquote>                                          |
| <p>Error<br />                                                        |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| <th colspan="2" rowspan="3"><blockquote>                              |
| <p>CError<br />                                                       |
| Detail</p>                                                            |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th rowspan="4"><blockquote>                                          |
| <p>3<br />                                                            |
| 4<br />                                                               |
| :</p>                                                                 |
| </blockquote></th>                                                    |
| <th rowspan="4">Detail<br />                                          |
| M R</th>                                                              |
| <th rowspan="2">Detail</th>                                           |
| <th rowspan="2">Detail</th>                                           |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th rowspan="2">Detail</th>                                           |
| </tr>                                                                 |
| <tr class="odd">                                                      |
| <th rowspan="2">M R</th>                                              |
| <th rowspan="2">M R</th>                                              |
| <th rowspan="2">M R</th>                                              |
| <th rowspan="2">M R</th>                                              |
| <th rowspan="2">M R</th>                                              |
| <th colspan="2" rowspan="2">M R</th>                                  |
| </tr>                                                                 |
| <tr class="header">                                                   |
| <th><blockquote>                                                      |
| <p>M R</p>                                                            |
| </blockquote></th>                                                    |
| </tr>                                                                 |
| </thead>                                                              |
| <tbody>                                                               |
| </tbody>                                                              |
| </table>                                                              |
+=======================================================================+
+-----------------------------------------------------------------------+

**Figure 3: Fatal Return Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > Fatal Return        | > ‎Figure 1:           |                       |
+-----------------------+-----------------------+-----------------------+
| > Transfer Batch      |                       |                       |
| > Error               |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Notification Error  |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Batch Control Error |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Accounting          |                       |                       |
| > Information Error   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Network Information |                       |                       |
| > Error               |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > VAS Information     |                       |                       |
| > Error               |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Message Description |                       |                       |
| > Error               |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Audit Control       |                       |                       |
| > Information Error   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > Notification        |                       | > Appropriate TAP     |
|                       |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Batch Control       |                       | > Appropriate TAP     |
| > Information         |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Accounting          |                       | > Appropriate TAP     |
| > Information         |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Network Information |                       | > Appropriate TAP     |
|                       |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > VAS Information     |                       | > Appropriate TAP     |
|                       |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Message Description |                       | > Appropriate TAP     |
| > Information         |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Audit Control       |                       | > Appropriate TAP     |
| > Information         |                       | > Standard            |
+-----------------------+-----------------------+-----------------------+
| > Error Detail        | > ‎Figure 1:           | > ‎Figure 4:           |
+-----------------------+-----------------------+-----------------------+

**Table 3: Fatal Return Group Elements**

> V6.11 Page 12 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image5.png){width="0.2361111111111111in"
height="0.1527777777777778in"}![](vertopal_086167a40080407f987d15583582be65/media/image6.png){width="0.3194444444444444in"
height="0.1527777777777778in"}![](vertopal_086167a40080407f987d15583582be65/media/image7.png){width="2.9027777777777777in"
height="1.375in"}![](vertopal_086167a40080407f987d15583582be65/media/image8.png){width="2.0416666666666665in"
height="0.7638888888888888in"}

+-----------------------+-----------------------+-----------------------+
| > GSM Association     |                       | > Confidential -      |
|                       |                       | > Full, Rapporteur,   |
|                       |                       | > and Associate       |
|                       |                       | > Members             |
+=======================+=======================+=======================+
| > Official Document   |                       |                       |
| > TD.32 - RAP Format  |                       |                       |
| > Specification       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > **3.1.4**           | > **Error Detail**    |                       |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------------------------------------------+
| > Error\                                                              |
| > Detail                                                              |
|                                                                       |
| +----------+----------+----------+----------+----------+----------+   |
| | > Path\  | Error    |          | > Item\  | > Item   | > Error\ |   |
| | > Item   |          |          | > Level  | > OffSet | > Code   |   |
| | > Id     |          |          |          |          |          |   |
| +==========+==========+==========+==========+==========+==========+   |
| |          | Context  |          |          |          |          |   |
| +----------+----------+----------+----------+----------+----------+   |
| |          | C        | R        |          | C        | > M      |   |
| +----------+----------+----------+----------+----------+----------+   |
| |          | Item     |          |          |          |          |   |
| +----------+----------+----------+----------+----------+----------+   |
| |          | Oc       |          |          |          |          |   |
| |          | currence |          |          |          |          |   |
| +----------+----------+----------+----------+----------+----------+   |
| | M        |          |          |          |          |          |   |
| +----------+----------+----------+----------+----------+----------+   |
| |          | > rC     |          | M        |          |          |   |
| +----------+----------+----------+----------+----------+----------+   |
+=======================================================================+
+-----------------------------------------------------------------------+

**Figure 4: Error Detail Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > Error Detail        | > ‎Figure 1:\          |                       |
|                       | > ‎Figure 3:           |                       |
+-----------------------+-----------------------+-----------------------+
| > Error Context       |                       |                       |
+-----------------------+-----------------------+-----------------------+

**Table 4: Error Detail Group Elements**

> V6.11 Page 13 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image9.png){width="2.7222222222222223in"
height="1.375in"}

+-----------------------+-----------------------+-----------------------+
| > GSM Association     |                       | > Confidential -      |
|                       |                       | > Full, Rapporteur,   |
|                       |                       | > and Associate       |
|                       |                       | > Members             |
+=======================+=======================+=======================+
| > Official Document   |                       |                       |
| > TD.32 - RAP Format  |                       |                       |
| > Specification       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| **3.1.5**             | > **RAP Audit Control |                       |
|                       | > Information**       |                       |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------------------------------------------+
| > RAP Audit\                                                          |
| > Control\                                                            |
| > Information                                                         |
|                                                                       |
| +---------------+---------------+---------------+---------------+     |
| | > Total       | > Return      | > Operator\   | > Total       |     |
| | > Severe\     | > Details     | > Specific\   | > Severe\     |     |
| | > Return\     | > Count       | > Information | > Return\     |     |
| | > Value       |               | > O R         | > Tax         |     |
| +===============+===============+===============+===============+     |
| | M             | > M           |               | > O           |     |
| +---------------+---------------+---------------+---------------+     |
+=======================================================================+
+-----------------------------------------------------------------------+

> **Figure 5: RAP Audit Control Information Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > RAP Audit Control   | > ‎Figure 1:           |                       |
| > Information         |                       |                       |
+-----------------------+-----------------------+-----------------------+

> **Table 5: RAP Audit Control Information Group Elements**
>
> V6.11 Page 14 of 46

![](vertopal_086167a40080407f987d15583582be65/media/image10.png){width="4.819444444444445in"
height="2.25in"}

+-----------------------+-----------------------+-----------------------+
| > GSM Association     |                       | > Confidential -      |
|                       |                       | > Full, Rapporteur,   |
|                       |                       | > and Associate       |
|                       |                       | > Members             |
+=======================+=======================+=======================+
| > Official Document   |                       |                       |
| > TD.32 - RAP Format  |                       |                       |
| > Specification       |                       |                       |
+-----------------------+-----------------------+-----------------------+
| > **3.1.6**           | > **RAP               |                       |
|                       | > Acknowledgement     |                       |
|                       | > File**              |                       |
+-----------------------+-----------------------+-----------------------+

+-----------------------------------------------------------------------+
| > Acknowledgement\                                                    |
| > File                                                                |
|                                                                       |
| +--------+--------+--------+--------+--------+--------+--------+      |
| | Sender | Rec    | RAP    | > Ack  | > Ack. | >      | > Ope  |      |
| |        | ipient | File   | >      | >      |  File\ | rator\ |      |
| |        |        | Se     |  File\ |  File\ | >      | > Spe  |      |
| |        |        | quence | > Cre  | > Avai |  Type\ | cific\ |      |
| |        |        | Number | ation\ | lable\ | > Ind  | >      |      |
| |        |        |        | > Tim  | > Tim  | icator |  Infor |      |
| |        |        |        | estamp | estamp |        | mation |      |
| |        |        |        |        |        |        | > O R  |      |
| +========+========+========+========+========+========+========+      |
| |        | > M    |        |        |        |        |        |      |
| +--------+--------+--------+--------+--------+--------+--------+      |
| | M      |        | > M    | > M    | M      | C      |        |      |
| +--------+--------+--------+--------+--------+--------+--------+      |
| |        |        |        | UTC\   | > UTC\ |        |        |      |
| |        |        |        | Time   | > Time |        |        |      |
| |        |        |        | Offset | >      |        |        |      |
| |        |        |        |        | Offset |        |        |      |
| +--------+--------+--------+--------+--------+--------+--------+      |
| |        |        |        | > M    | M      |        |        |      |
| +--------+--------+--------+--------+--------+--------+--------+      |
+=======================================================================+
+-----------------------------------------------------------------------+

**Figure 6: Acknowledgement File Logical Structure**

+-----------------------+-----------------------+-----------------------+
| > **Group element     | > **Also occurs in**  | > **Detail shown in** |
| > name**              |                       |                       |
+=======================+=======================+=======================+
| > Acknowledgement     |                       |                       |
| > File                |                       |                       |
+-----------------------+-----------------------+-----------------------+

**Table 6: Acknowledgement File Group Elements**

> **4 Data Dictionary**\
> This data dictionary gives a listing of all data items unique to the
> Returned Account Procedure (RAP). As well as providing values for the
> items, it describes conditionality in greater detail.
>
> The data dictionary also contains entries and cross-references for all
> other data items and groups referenced.
>
> Finally, the data dictionary contains the appropriate validation rules
> that must be used to report errors within a RAP File or
> Acknowledgement File.

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
| **Accounting Information**        | > The specific TAP file           |
|                                   | > accounting information that     |
|                                   | > caused the fatal error.         |
+-----------------------------------+-----------------------------------+

> V6.11 Page 15 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the Accounting     |
|                                   | > Information Error group.        |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Accounting Information        | > The group identifies Accounting |
| > Error**                         | > Information related fatal       |
|                                   | > errors.                         |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Accounting Information    |
|                                   | > level.                          |
+-----------------------------------+-----------------------------------+
| > **Ack File Available            | > The date and time the           |
| > Timestamp**                     | > Acknowledgement file was made   |
|                                   | > available to the Recipient PMN. |
|                                   | > The time is given in the local  |
|                                   | > time of the Sending PMN. There  |
|                                   | > must be a UTC Time OffSet       |
|                                   | > associated with this field.     |
|                                   | >                                 |
|                                   | > Physically this will normally   |
|                                   | > be the timestamp when the file  |
|                                   | > was transferred to the          |
|                                   | > Recipient PMN (start of push),  |
|                                   | > however on some systems this    |
|                                   | > will be the timestamp when the  |
|                                   | > file was made available to be   |
|                                   | > pulled.                         |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory in the group          |
|                                   | > Acknowledgement File.           |
+-----------------------------------+-----------------------------------+
| > **Ack File Creation Timestamp** | > The timestamp at which the      |
|                                   | > Acknowledgement File was        |
|                                   | > created.                        |
|                                   | >                                 |
|                                   | > The time is given in the local  |
|                                   | > time of the Sending PMN. There  |
|                                   | > must be a UTC Time OffSet       |
|                                   | > associated with this field.     |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the group          |
|                                   | > Acknowledgement File.           |
+-----------------------------------+-----------------------------------+
| > **Acknowledgement File**        | > In the case of a RAP file       |
|                                   | > transmission, an                |
|                                   | > Acknowledgement file is sent by |
|                                   | > the VPMN to the HPMN to         |
|                                   | > acknowledge the receipt of a    |
|                                   | > RAP file.                       |
+-----------------------------------+-----------------------------------+
| > **Audit Control Information**   | > The specific TAP file audit     |
|                                   | > control information that caused |
|                                   | > the fatal error.                |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the Audit Control  |
|                                   | > Information Error group. See    |
|                                   | > appropriate TAP standard for    |
|                                   | > full definition and content.    |
+-----------------------------------+-----------------------------------+
| > **Audit Control**\              | > The group identifies Audit      |
| > **Information Error**           | > Control Information related     |
|                                   | > fatal errors.                   |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Audit Control Information |
|                                   | > level.                          |
+-----------------------------------+-----------------------------------+
| > **Batch Control Error**         | > The group identifies Batch      |
|                                   | > Control Information related     |
|                                   | > fatal errors.                   |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Batch Control Information |
|                                   | > level.                          |
+-----------------------------------+-----------------------------------+
| > **Batch Control**               | > The specific TAP file batch     |
|                                   | > control information that caused |
|                                   | > the fatal error.                |
+-----------------------------------+-----------------------------------+

> V6.11 Page 16 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
| > **Information**                 | > Conditionality:\                |
|                                   | > Mandatory in the Batch Control  |
|                                   | > Information Error group.        |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Call Event Details**          | > The group contains details of   |
|                                   | > the call/event that contains    |
|                                   | > the reported error (see Error   |
|                                   | > Detail).                        |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within group Severe   |
|                                   | > Return.                         |
|                                   | >                                 |
|                                   | > When a Call Event Detail is     |
|                                   | > returned with more than one     |
|                                   | > severe error it must only be    |
|                                   | > returned once. This means that  |
|                                   | > it must not be present more     |
|                                   | > than once within a given RAP    |
|                                   | > file or present in more than    |
|                                   | > one RAP file.                   |
|                                   | >                                 |
|                                   | > **Note:** A resubmitted         |
|                                   | > (corrected) Call Event Detail   |
|                                   | > is deemed to be a new           |
|                                   | > call/event. If more than one    |
|                                   | > error is found in the Call      |
|                                   | > Event Detail it is reported by  |
|                                   | > the repeating group Error       |
|                                   | > Detail.                         |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **End Missing Sequence Number   | > Part of the Return Detail in    |
| > Range**                         | > the RAP file when sequence      |
|                                   | > numbers are missing. This will  |
|                                   | > be the last sequence number     |
|                                   | > missing from the series.        |
|                                   | >                                 |
|                                   | > This is a conditional field     |
|                                   | > used when multiple TAP files    |
|                                   | > are missing.                    |
|                                   | >                                 |
|                                   | > *Range of valid values:*        |
|                                   | >                                 |
|                                   | > 00001 -- 99999                  |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Present if there is a range of  |
|                                   | > missing sequence numbers in the |
|                                   | > Missing Return information.     |
+-----------------------------------+-----------------------------------+
| > **Error Code**                  | > Code associated to the error    |
|                                   | > found for a particular field.   |
|                                   | > Error codes and validation      |
|                                   | > processes are defined in the    |
|                                   | > appropriate TAP standard.       |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within the repeating  |
|                                   | > group Error Detail.             |
+-----------------------------------+-----------------------------------+
| > **Error Context**               | > Group with information about    |
|                                   | > the full context of the item in |
|                                   | > error.                          |
|                                   | >                                 |
|                                   | > There will be one occurrence of |
|                                   | > this group for each level       |
|                                   | > within the TAP file starting at |
|                                   | > the 'TransferBatch' or          |
|                                   | > 'Notification' (at level 1) and |
|                                   | > ending with information of the  |
|                                   | > item in error (at level n).     |
|                                   | >                                 |
|                                   | > The repeating set of records    |
|                                   | > may represent either the        |
|                                   | > "logical" or "physical"         |
|                                   | > structure of the file. When a   |
|                                   | > "physical" path is specified    |
|                                   | > ALL tags present will be        |
|                                   | > included from Tag 1 (Data       |
|                                   | > Interchange) down to (and       |
|                                   | > including) the item in error. A |
|                                   | > "logical" path will include     |
|                                   | > only Tag numbers, which have    |
|                                   | > corresponding logical entities  |
|                                   | > within the Logical Structure    |
|                                   | > (diagrams).                     |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory for all errors with   |
|                                   | > the exception of ASN.1 errors   |
+-----------------------------------+-----------------------------------+

> V6.11 Page 17 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > (error codes 50-59 as specified |
|                                   | > in TD.57 ‎\[6\]).                |
|                                   | >                                 |
|                                   | > **Note:** Error codes 142, 250  |
|                                   | > through 257, 260 and 261        |
|                                   | > (duplicate call events, Call    |
|                                   | > age) can be represented using   |
|                                   | > the call event detail (for      |
|                                   | > example                         |
|                                   | > TransferBatch.Call              |
|                                   | EventDetailList.CallEventDetail). |
+-----------------------------------+-----------------------------------+
| > **Error Detail**                | > Error Detail is a repeating     |
|                                   | > group identifying the errored   |
|                                   | > item and offset, where          |
|                                   | > applicable, together with the   |
|                                   | > Error Code.                     |
|                                   | >                                 |
|                                   | > Optionally, the group will also |
|                                   | > contain a repeated occurrence   |
|                                   | > of Error Context.               |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within groups\        |
|                                   | > Severe Return\                  |
|                                   | > Transfer Batch Error\           |
|                                   | > Notification Error\             |
|                                   | > Batch Control Error\            |
|                                   | > Accounting Information Error\   |
|                                   | > Network Information Error\      |
|                                   | > VAS Information Error\          |
|                                   | > Message Description Error\      |
|                                   | > Audit Control Information       |
|                                   | > Error\                          |
|                                   | > where one occurrence must be    |
|                                   | > present for each error          |
|                                   | > reported.                       |
+-----------------------------------+-----------------------------------+
| > **Fatal Return**                | > Constitutes a TAP file rejected |
|                                   | > in its entirety and a subset of |
|                                   | > information describing the      |
|                                   | > fatal error is returned to the  |
|                                   | > VPMN.                           |
|                                   | >                                 |
|                                   | > For a fatal return only         |
|                                   | > specific information pertaining |
|                                   | > to the fatal error is returned  |
|                                   | > to the VPMN and not the entire  |
|                                   | > file.                           |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Present within the group Return |
|                                   | > Detail if the return resulted   |
|                                   | > from a fatal error.             |
|                                   | >                                 |
|                                   | > If a fatal error is being       |
|                                   | > returned, Fatal Return is       |
|                                   | > Mandatory.                      |
+-----------------------------------+-----------------------------------+
| > **File Sequence Number**        | > A unique reference which        |
|                                   | > identifies the erroneous TAP    |
|                                   | > file.                           |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within groups\        |
|                                   | > Fatal Return\                   |
|                                   | > Severe Return                   |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **File Type Indicator**         | > Indicates the type of data      |
|                                   | > contained within the erroneous  |
|                                   | > TAP file. The type of data      |
|                                   | > could be either test or         |
|                                   | > chargeable data.                |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Present within groups           |
|                                   | >                                 |
|                                   | > RAP Batch Control Information   |
+-----------------------------------+-----------------------------------+

> V6.11 Page 18 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > Acknowledgement File\           |
|                                   | > where the file represents test  |
|                                   | > data only.                      |
|                                   | >                                 |
|                                   | > Not present where the data is   |
|                                   | > 'live' chargeable data.         |
|                                   | >                                 |
|                                   | > Values:\                        |
|                                   | > T Test Data\                    |
|                                   | > V (Reserved for proprietary     |
|                                   | > use) H (Reserved for            |
|                                   | > proprietary use) S\             |
|                                   | > (Reserved for proprietary use)  |
|                                   | > B (Reserved for proprietary     |
|                                   | > use)                            |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Item Level**                  | > Indicates the ASN.1 level of    |
|                                   | > the respective item that        |
|                                   | > specifies the context of the    |
|                                   | > error. The level starts with 1  |
|                                   | > for 'TransferBatch' or          |
|                                   | > 'Notification' and              |
|                                   | >                                 |
|                                   | > increases by 1 at each          |
|                                   | > group/item that follows in the  |
|                                   | > context. All levels must be in  |
|                                   | > consecutive order; no level may |
|                                   | > be omitted.                     |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Must be present within the      |
|                                   | > Error Context Group.            |
|                                   |                                   |
|                                   | *Values:*\                        |
|                                   | \> 0                              |
+-----------------------------------+-----------------------------------+
| > **Item Occurrence**             | > The occurrence of the path item |
|                                   | > at the specified level. Starts  |
|                                   | > with one. For example the 4th   |
|                                   | > call event detail within a      |
|                                   | > batch would be specified with   |
|                                   | >                                 |
|                                   | > occurrence of 4.                |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Must be present when the item   |
|                                   | > is repeated (SEQUENCE OF).      |
+-----------------------------------+-----------------------------------+
| > **Item OffSet**                 | > The OffSet in bytes from the    |
|                                   | > beginning of the file to the    |
|                                   | > start of the item in error,     |
|                                   | > beginning with an offset of     |
|                                   | > zero.                           |
|                                   | >                                 |
|                                   | > The Item OffSet must always     |
|                                   | > refer to the original byte      |
|                                   | > stream from the original TAP    |
|                                   | > file.                           |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Present when available.         |
+-----------------------------------+-----------------------------------+
| > **Last Sequence Number**        | > Part of the Return Detail in    |
|                                   | > the RAP file when the TAP file  |
|                                   | > stream has stopped. This will   |
|                                   | > be the last sequence number     |
|                                   | > received for this roaming       |
|                                   | > relation.                       |
|                                   | >                                 |
|                                   | > *Range of valid values:*        |
|                                   | >                                 |
|                                   | > 00001 -- 99999                  |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within group Stop     |
|                                   | > Return.                         |
+-----------------------------------+-----------------------------------+

> V6.11 Page 19 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > **Note:** The term "last        |
|                                   | > sequence number received"       |
|                                   | > refers to the last sequence     |
|                                   | > number from a sequence          |
|                                   | > perspective rather than from a  |
|                                   | > receipt time\                   |
|                                   | > perspective. This will be equal |
|                                   | > to the next expected sequence   |
|                                   | > number reduced by one when the  |
|                                   | > next expected sequence number   |
|                                   | > is greater than 00001. When the |
|                                   | > next expected sequence number   |
|                                   | > is 00001 then the Last Sequence |
|                                   | > Number is 99999.                |
+-----------------------------------+-----------------------------------+
| > **Message Description Error**   | > The group identifies Message    |
|                                   | > Description Information related |
|                                   | > fatal errors.                   |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Message Description       |
|                                   | > Information level.              |
+-----------------------------------+-----------------------------------+
| > **Message Description           | > The specific TAP file Message   |
| > Information**                   | > Description Information that    |
|                                   | > caused the fatal error.         |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the Message        |
|                                   | > Description Error group.        |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Missing Return**              | > Attributes used to describe     |
|                                   | > missing TAP file sequence       |
|                                   | > numbers.                        |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within the group Return |
|                                   | > Detail if the return resulted   |
|                                   | > from a missing file error.      |
+-----------------------------------+-----------------------------------+
| > **Network Information**         | > The specific TAP file network   |
|                                   | > information that caused the     |
|                                   | > fatal error.                    |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the Network        |
|                                   | > Information Error group.        |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Network Information Error**   | > The group identifies Network    |
|                                   | > Information related fatal       |
|                                   | > errors.                         |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Network Information       |
|                                   | > level.                          |
+-----------------------------------+-----------------------------------+
| > **Notification**                | > The specific TAP file           |
|                                   | > Notification that caused the    |
|                                   | > fatal error.                    |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory in the Notification   |
|                                   | > Error group.                    |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Notification Error**          | > The group identifies            |
|                                   | > Notification related fatal      |
|                                   | > errors. This could include for  |
|                                   | > example error codes 50-54 that  |
|                                   | > must be returned with either a  |
|                                   | > Notification Error or a         |
|                                   | > Transfer Batch Error.           |
+-----------------------------------+-----------------------------------+

> V6.11 Page 20 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Notification level.       |
+-----------------------------------+-----------------------------------+
| > **Operator Specific             | > This repeating item contains    |
| > Information**                   | > additional information that     |
|                                   | > must be populated when          |
|                                   | > rejecting for an IOT error.     |
|                                   | > This additional information     |
|                                   | > will assist with the            |
|                                   | > investigation and correction of |
|                                   | > the reported IOT error.         |
|                                   | >                                 |
|                                   | > The item can also be repeated   |
|                                   | > and contain information at the  |
|                                   | > discretion of the Sender or     |
|                                   | > where it has been bilaterally   |
|                                   | > agreed.                         |
|                                   | >                                 |
|                                   | > The content of the item could   |
|                                   | > be defined by the Sender or     |
|                                   | > defined by bilateral agreement  |
|                                   | > and may vary according to the   |
|                                   | > context.                        |
|                                   | >                                 |
|                                   | > For further information, see    |
|                                   | > ‎Annex A and ‎Annex B.            |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Three occurrences within group  |
|                                   | > Severe Return are Mandatory     |
|                                   | > when rejecting for error code   |
|                                   | > 200 in any of the following     |
|                                   | > elements:\                      |
|                                   | > Charge\                         |
|                                   | > Tax Value\                      |
|                                   | > CAMEL Invocation Fee            |
|                                   | >                                 |
|                                   | > Is also present when agreed     |
|                                   | > bilaterally within groups       |
|                                   | >                                 |
|                                   | > Missing Return                  |
|                                   | >                                 |
|                                   | > Fatal Return                    |
|                                   | >                                 |
|                                   | > Severe Return (other than IOT   |
|                                   | > error)                          |
|                                   | >                                 |
|                                   | > Stop Return                     |
|                                   | >                                 |
|                                   | > RAP Batch Control Information   |
|                                   | >                                 |
|                                   | > RAP Audit Control Information   |
|                                   | >                                 |
|                                   | > Acknowledgement File            |
|                                   | >                                 |
|                                   | > *Optionality:*                  |
|                                   | >                                 |
|                                   | > The Sender can also choose to   |
|                                   | > populate this item at its       |
|                                   | > discretion.                     |
+-----------------------------------+-----------------------------------+
| > **Path Item Id**                | > Tag Id of the item building the |
|                                   | > path to the item in error. The  |
|                                   | > Tag Id refers to Application    |
|                                   | > Tag Number as defined in the    |
|                                   | > ASN.1 definition in TD.57 ‎\[6\] |
|                                   | > and not to the physical tag in  |
|                                   | > the encoded file.               |
|                                   | >                                 |
|                                   | > Example: For                    |
|                                   | > "MobileOriginatedCall" the      |
|                                   | > value is "9".                   |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Must be present within the      |
|                                   | > Error Context Group.            |
+-----------------------------------+-----------------------------------+
| > **RAP Audit Control             | > The group identifies the end of |
| > Information**                   | > the Transfer batch.             |
|                                   | >                                 |
|                                   | > All items are mandatory except  |
|                                   | > Operator Specific Information   |
|                                   | > and Total Severe Return Tax,    |
|                                   | > which are optional.             |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within group Return   |
|                                   | > Batch.                          |
+-----------------------------------+-----------------------------------+
| > **RAP Batch Control**           | > All items are mandatory except  |
|                                   | > the following:                  |
+-----------------------------------+-----------------------------------+

> V6.11 Page 21 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
| > **Information**                 | > File Type Indicator which is    |
|                                   | > conditional (indicating test    |
|                                   | > data)\                          |
|                                   | > Roaming Partner which is        |
|                                   | > optional (can only be present   |
|                                   | > when bilaterally agreed)\       |
|                                   | > Operator Specific Information   |
|                                   | > which is optional\              |
|                                   | > TAP Currency which is           |
|                                   | > conditional\                    |
|                                   | > TAP Decimal Places which is     |
|                                   | > conditional                     |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within group Return   |
|                                   | > Batch.                          |
+-----------------------------------+-----------------------------------+
| > **RAP File Available            | > The date and time the RAP file  |
| > Timestamp**                     | > was made available to the       |
|                                   | > Recipient PMN. The time is      |
|                                   | > given in the local time of the  |
|                                   | > sender PMN. There must be a UTC |
|                                   | > Time OffSet associated with the |
|                                   | > item.                           |
|                                   | >                                 |
|                                   | > Physically this will normally   |
|                                   | > be the timestamp when the file  |
|                                   | > was transferred to the          |
|                                   | > Recipient PMN (start of push),  |
|                                   | > however on some systems this    |
|                                   | > will be the timestamp when the  |
|                                   | > file was made available to be   |
|                                   | > pulled.                         |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within the group RAP  |
|                                   | > Batch Control Information.      |
+-----------------------------------+-----------------------------------+
| > **RAP File Creation Timestamp** | > The timestamp at which the RAP  |
|                                   | > file was created. The time is   |
|                                   | > given in the local time of the  |
|                                   | > sender PMN. There must be a UTC |
|                                   | > Time OffSet\                    |
|                                   | > associated with the item.       |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within group RAP      |
|                                   | > Batch Control Information.      |
+-----------------------------------+-----------------------------------+
| > **RAP File Sequence Number**    | > A unique reference that         |
|                                   | > identifies each RAP data        |
|                                   | > interchange sent by one PMN to  |
|                                   | > another, specific, PMN.         |
|                                   | >                                 |
|                                   | > The sequence number starts at 1 |
|                                   | > and is incremented by one for   |
|                                   | > each subsequent Return Batch    |
|                                   | > sent by the Sender PMN to a     |
|                                   | > particular Recipient PMN.       |
|                                   | >                                 |
|                                   | > **Note:** In case of            |
|                                   | > retransmission for any reason   |
|                                   | > this number is not incremented. |
|                                   | >                                 |
|                                   | > RAP file sequence numbers are   |
|                                   | > independent from TAP file       |
|                                   | > sequence numbers.               |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within groups         |
|                                   | >                                 |
|                                   | > RAP Batch Control Information   |
|                                   | >                                 |
|                                   | > Acknowledgement File            |
|                                   | >                                 |
|                                   | > *Range:*                        |
|                                   | >                                 |
|                                   | > 00001 -- 99999                  |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **RAP Release Version Number**  | > Indicates the RAP release       |
|                                   | > version associated with the RAP |
|                                   | > Specification Version Number.   |
+-----------------------------------+-----------------------------------+

> V6.11 Page 22 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within group RAP      |
|                                   | > Batch Control Information.      |
|                                   | >                                 |
|                                   | > *Values:*\                      |
|                                   | > 5 for RAP1.5                    |
+-----------------------------------+-----------------------------------+
| > **RAP Specification Version     | > To enable a PMN to encode       |
| > Number**                        | > and/or read a RAP file it is    |
|                                   | > necessary to uniquely identify  |
|                                   | > the format. This is achieved    |
|                                   | > through the RAP Specification   |
|                                   | > Version Number.                 |
|                                   | >                                 |
|                                   | > There must be a RAP Release     |
|                                   | > Version Number present          |
|                                   | > associated with this item.      |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within group RAP      |
|                                   | > Batch Control Information.      |
|                                   | >                                 |
|                                   | > Values:                         |
|                                   | >                                 |
|                                   | > 1 for RAP version 1             |
+-----------------------------------+-----------------------------------+
| > **Recipient**                   | > A unique identifier used to     |
|                                   | > determine to whom (normally a   |
|                                   | > PMN) the data is being sent,    |
|                                   | > that is the Recipient.          |
|                                   | >                                 |
|                                   | > This can also represent a third |
|                                   | > party such as a data clearing   |
|                                   | > house, but only if bilaterally  |
|                                   | > agreed.                         |
|                                   | >                                 |
|                                   | > *Derivation:*\                  |
|                                   | > TD.13 ‎\[4\]: TADIG Code Naming  |
|                                   | > Conventions.                    |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within groups\        |
|                                   | > RAP Batch Control Information\  |
|                                   | > Acknowledgement File            |
|                                   | >                                 |
|                                   | > *Example content:*\             |
|                                   | > GBRCN\                          |
|                                   | > GBRVF\                          |
|                                   | > DEUD1\                          |
|                                   | > DEUD2                           |
+-----------------------------------+-----------------------------------+
| > **Release Version Number**      | > Indicates the release version   |
|                                   | > associated with the             |
|                                   | > Specification Version Number of |
|                                   | > the TAP file being returned.    |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Must be present within group    |
|                                   | > RAP Batch Control Information   |
|                                   | > where the Return Detail         |
|                                   | > contains Severe Return or a     |
|                                   | > Fatal Return with errors other  |
|                                   | > than Transfer Batch Error.      |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+

> V6.11 Page 23 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
| > **Return Batch**                | > Consists of RAP Batch Control   |
|                                   | > Information, Return Detail, and |
|                                   | > RAP Audit Control Information.  |
|                                   | > All information for these       |
|                                   | > attributes is obtained from the |
|                                   | > original TAP file submitted and |
|                                   | > the validation process.         |
+-----------------------------------+-----------------------------------+
| > **Return Detail**               | > Must consist of a Missing       |
|                                   | > Return, Stop Return, Fatal      |
|                                   | > Return, or Severe Return        |
|                                   | > depending on the type of error  |
|                                   | > found in the TAP file. One and  |
|                                   | > only one of these return types  |
|                                   | > must be found in the Return     |
|                                   | > detail.                         |
|                                   | >                                 |
|                                   | > **Note:** There can be only one |
|                                   | > Missing Return per RAP file,    |
|                                   | > only one Stop Return per RAP    |
|                                   | > file, and only one Fatal Return |
|                                   | > per RAP file, so for these      |
|                                   | > return types the Return Detail  |
|                                   | > cannot be repeated. The Return  |
|                                   | > Detail can only be repeated for |
|                                   | > Severe Returns.                 |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within the group      |
|                                   | > Return Batch.                   |
+-----------------------------------+-----------------------------------+
| > **Return Details Count**        | > Number of returned details in   |
|                                   | > the RAP file.                   |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within the group RAP  |
|                                   | > Audit Control Information.      |
|                                   | >                                 |
|                                   | > **Note:** For RAP files         |
|                                   | > containing a Missing Return,    |
|                                   | > Stop Return or Fatal Return,    |
|                                   | > this field must be 1.           |
+-----------------------------------+-----------------------------------+
| > **Roaming Partner**             | > A unique identifier used to     |
|                                   | > determine the roaming partner   |
|                                   | > in a RAP file, when the Sender  |
|                                   | > or Recipient element is         |
|                                   | > populated with a TADIG Code     |
|                                   | > that does not belong to an      |
|                                   | > operator (for example the       |
|                                   | > Sender or Recipient is          |
|                                   | > populated with the TADIG Code   |
|                                   | > of a third party such as a      |
|                                   | > clearinghouse).                 |
|                                   | >                                 |
|                                   | > This element can be present     |
|                                   | > only if explicitly agreed to by |
|                                   | > the receiving operator.         |
|                                   | >                                 |
|                                   | > *Derivation:*\                  |
|                                   | > TD.13 ‎\[4\]: TADIG Code Naming  |
|                                   | > Conventions.                    |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Optional within group RAP Batch |
|                                   | > Control Information.            |
|                                   | >                                 |
|                                   | > *Example content:*\             |
|                                   | > GBRCN\                          |
|                                   | > GBRVF\                          |
|                                   | > DEUD1\                          |
|                                   | > DEUD2                           |
+-----------------------------------+-----------------------------------+
| > **Sender**                      | > A unique identifier used to     |
|                                   | > determine the Sender (normally  |
|                                   | > a PMN) of the data.             |
|                                   | >                                 |
|                                   | > This can also represent a third |
|                                   | > party such as a data clearing   |
|                                   | > house, but only if bilaterally  |
|                                   | > agreed.                         |
|                                   | >                                 |
|                                   | > *Derivation:*                   |
|                                   | >                                 |
|                                   | > TD.13 ‎\[4\]: TADIG Code Naming  |
|                                   | > Conventions.                    |
+-----------------------------------+-----------------------------------+

> V6.11 Page 24 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within groups\        |
|                                   | > RAP Batch Control Information   |
|                                   | > Acknowledgement File.           |
|                                   | >                                 |
|                                   | > *Example content:*\             |
|                                   | > GBRCN\                          |
|                                   | > GBRVF\                          |
|                                   | > DEUD1\                          |
|                                   | > DEUD2                           |
+-----------------------------------+-----------------------------------+
| > **Severe Return**               | > Call event details Severe       |
|                                   | > Return allows the ability to    |
|                                   | > return specific call event      |
|                                   | > details that fail the           |
|                                   | > validation process from the TAP |
|                                   | > file without rejecting the      |
|                                   | > entire file.                    |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory only when returning   |
|                                   | > call event details.             |
+-----------------------------------+-----------------------------------+
| > **Specification Version         | > The specification version       |
| > Number**                        | > number of the TAP file          |
|                                   | > exchanged between the VPMN and  |
|                                   | > HPMN.                           |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Must be present within group    |
|                                   | > RAP Batch Control Information   |
|                                   | > where the Return Detail         |
|                                   | > contains Severe Return or a     |
|                                   | > Fatal Return with errors other  |
|                                   | > than Transfer Batch Error.      |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **Start Missing Sequence Number | > Part of the Return Detail in    |
| > Range**                         | > the RAP file when (a) TAP file  |
|                                   | > sequence number(s) is/are       |
|                                   | > missing. This is a mandatory    |
|                                   | > field containing the missing    |
|                                   | > sequence number, or when        |
|                                   | > multiple TAP files are missing, |
|                                   | > the first sequence number of    |
|                                   | > the series of missing TAP       |
|                                   | > files.                          |
|                                   | >                                 |
|                                   | > *Range of valid values:*        |
|                                   | >                                 |
|                                   | > 00001 -- 99999                  |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within the group      |
|                                   | > Missing Return.                 |
+-----------------------------------+-----------------------------------+
| > **Stop Return**                 | > Attributes used to describe a   |
|                                   | > situation where the TAP file    |
|                                   | > stream has stopped for a given  |
|                                   | > roaming relation (VPMN/HPMN     |
|                                   | > combination).                   |
|                                   | >                                 |
|                                   | > If the HPMN has not received    |
|                                   | > any TAP files from the VPMN for |
|                                   | > 7 calendar days, a Stop Return  |
|                                   | > must be produced reporting the  |
|                                   | > TAP file stream as stopped.     |
|                                   | >                                 |
|                                   | > A new RAP file containing a     |
|                                   | > Stop Return reporting this      |
|                                   | > error must be produced every 7  |
|                                   | > calendar days, until such time  |
|                                   | > a TAP file has been received    |
|                                   | > from the VPMN.                  |
|                                   |                                   |
|                                   | This error must only be raised    |
|                                   | where at least one commercial     |
|                                   | (CD) TAP file                     |
+-----------------------------------+-----------------------------------+

> V6.11 Page 25 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
|                                   | > has been received for that      |
|                                   | > roaming relation.               |
|                                   | >                                 |
|                                   | > **Note:** One operator can have |
|                                   | > more than one TADIG code, and   |
|                                   | > this error must be reported on  |
|                                   | > each TADIG code combination     |
|                                   | > independently. So if files from |
|                                   | > TADIG code A are received, but  |
|                                   | > no files from TADIG code B are  |
|                                   | > received, then the Stop Return  |
|                                   | > must be raised for the TADIG    |
|                                   | > code B relation.                |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Present within the group Return |
|                                   | > Detail if the return resulted   |
|                                   | > from a TAP file stream stopped  |
|                                   | > error.                          |
+-----------------------------------+-----------------------------------+
| > **TAP Currency**                | > TAP Currency contains the       |
|                                   | > Currency Code which identifies  |
|                                   | > the currency used for charges   |
|                                   | > within the TAP file for which   |
|                                   | > the call records are being      |
|                                   | > returned with RAP, where that   |
|                                   | > currency is not the standard    |
|                                   | > SDR.                            |
|                                   | >                                 |
|                                   | > *Derivation:*                   |
|                                   | >                                 |
|                                   | > ISO 4217 Currency Codes         |
|                                   | > standard.                       |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within RAP Batch      |
|                                   | > Control Information where       |
|                                   | > Severe Returns are present in   |
|                                   | > the RAP file and currency other |
|                                   | > than SDR is used as specified   |
|                                   | > in the roaming agreement.       |
|                                   | >                                 |
|                                   | > *Example*:                      |
|                                   | >                                 |
|                                   | > *Currency Code* *Currency name* |
|                                   | >                                 |
|                                   | > EUR Euro                        |
|                                   | >                                 |
|                                   | > INR Indian Rupee                |
|                                   | >                                 |
|                                   | > USD US Dollar                   |
+-----------------------------------+-----------------------------------+
| > **TAP Decimal Places**          | > Identifies the number of        |
|                                   | > decimal places used within all  |
|                                   | > absolute monetary values within |
|                                   | > the TAP file for which the call |
|                                   | > records are being returned with |
|                                   | > RAP.                            |
|                                   | >                                 |
|                                   | > The same number of decimal      |
|                                   | > places is applicable for all    |
|                                   | > tax, discount, charge and audit |
|                                   | > values throughout the whole TAP |
|                                   | > file.                           |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within RAP Batch      |
|                                   | > Control Information where       |
|                                   | > Severe Returns are present in   |
|                                   | > the RAP file.                   |
+-----------------------------------+-----------------------------------+
| **Total Severe Return Tax**       | > Total tax value of the Call     |
|                                   | > Event Details being rejected    |
|                                   | > with severe errors. If the tax  |
|                                   | > value of the Call Event Details |
|                                   | > cannot be determined, for       |
|                                   | > example due to syntax errors in |
|                                   | > the charges, that Call Event    |
|                                   | > Detail will be counted as zero  |
|                                   | > in calculating the Total Severe |
|                                   | > Return Tax.                     |
|                                   | >                                 |
|                                   | > If the RAP file contains a      |
|                                   | > Missing Return, Stop Return, or |
|                                   | > Fatal Return, the Total Severe  |
|                                   | > Return Tax will (when present)  |
|                                   | > have the value zero.            |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > The population of the field is  |
|                                   | > optional and up to the RAP      |
|                                   | > sender.                         |
+-----------------------------------+-----------------------------------+
| > **Total Severe Return**         | > Total value without tax of the  |
|                                   | > Call Event Details being        |
|                                   | > rejected with severe            |
+-----------------------------------+-----------------------------------+

> V6.11 Page 26 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Element**                     | > **Description**                 |
+===================================+===================================+
| > **Value**                       | > errors.                         |
|                                   | >                                 |
|                                   | > If the value without tax of the |
|                                   | > Call Event Details cannot be    |
|                                   | > determined, for example due to  |
|                                   | > syntax errors in the charges,   |
|                                   | > that Call Event Detail will be  |
|                                   | > counted as zero in calculating  |
|                                   | > the Total Severe Return Value.  |
|                                   | >                                 |
|                                   | > If the RAP file contains a      |
|                                   | > Missing Return, Stop Return, or |
|                                   | > Fatal Return, the Total Severe  |
|                                   | > Return Value will have the      |
|                                   | > value zero.                     |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within the group RAP  |
|                                   | > Audit Control Information.      |
+-----------------------------------+-----------------------------------+
| > **Transfer Batch Error**        | > The group identifies Transfer   |
|                                   | > Batch related fatal errors.     |
|                                   | > This could include for example  |
|                                   | > error codes 50-54 that must be  |
|                                   | > returned with either a\         |
|                                   | > Notification Error or a         |
|                                   | > Transfer Batch Error.           |
|                                   | >                                 |
|                                   | > *Conditionality:*               |
|                                   | >                                 |
|                                   | > Mandatory within group Fatal    |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group Transfer Batch level.     |
+-----------------------------------+-----------------------------------+
| > **UTC Time Offset**             | > All timestamps are in the local |
|                                   | > time of the Sender PMN. So that |
|                                   | > the time can be equated to time |
|                                   | > in the Recipient PMN, the       |
|                                   | > difference between local time   |
|                                   | > and UTC time must be supplied.  |
|                                   | >                                 |
|                                   | > *Derivation:*\                  |
|                                   | > UTC Time Offset = Local Time    |
|                                   | > minus UTC Time                  |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Mandatory within items\         |
|                                   | > RAP File Available Timestamp    |
|                                   | > Ack File Available Timestamp    |
|                                   | > RAP File Creation Timestamp Ack |
|                                   | > File Creation Timestamp.        |
|                                   | >                                 |
|                                   | > *Format:*\                      |
|                                   | > ±HHMM                           |
|                                   | >                                 |
|                                   | > See appropriate TAP standard    |
|                                   | > for full definition and         |
|                                   | > content.                        |
+-----------------------------------+-----------------------------------+
| > **VAS Information Error**       | > The group identifies VAS        |
|                                   | > Information related fatal       |
|                                   | > errors.                         |
|                                   | >                                 |
|                                   | > *Conditionality:*\              |
|                                   | > Present within group Fatal      |
|                                   | > Return where the Error Detail   |
|                                   | > relates to a fatal error at TAP |
|                                   | > group VAS Information level.    |
+-----------------------------------+-----------------------------------+

**Table 7: Data Dictionary**

> The following validation rule must be used to report ASN.1 syntax
> errors within a RAP File and Acknowledgement File:
>
> V6.11 Page 27 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------+-----------------+-----------------+-----------------+
| > **Error       | > **Context**   | > **Severity    | > **Validation  |
| > Code**        |                 | > level**       | > description** |
+=================+=================+=================+=================+
| > 50            | > Return Batch  | > Fatal         | > RAP Encoding  |
|                 | > AcknowFile    |                 | > Error.        |
|                 |                 |                 | >               |
|                 |                 |                 | > This could be |
|                 |                 |                 | > one of the    |
|                 |                 |                 | > following     |
|                 |                 |                 | > type of       |
|                 |                 |                 | > errors:\      |
|                 |                 |                 | > • Unknown     |
|                 |                 |                 | > tag, meaning  |
|                 |                 |                 | > that the tag  |
|                 |                 |                 | > is not        |
|                 |                 |                 | > recognised as |
|                 |                 |                 | > a valid tag   |
|                 |                 |                 | > within RAP;\  |
|                 |                 |                 | > •             |
|                 |                 |                 | > Non-repeating |
|                 |                 |                 | > element       |
|                 |                 |                 | > occurs more   |
|                 |                 |                 | > than once     |
|                 |                 |                 | > within the    |
|                 |                 |                 | > group;\       |
|                 |                 |                 | > • Tag invalid |
|                 |                 |                 | > within        |
|                 |                 |                 | > context;\     |
|                 |                 |                 | > • File not    |
|                 |                 |                 | > encoded       |
|                 |                 |                 | > according to  |
|                 |                 |                 | > ASN.1 BER.    |
+-----------------+-----------------+-----------------+-----------------+

**Table 8: ASN.1 Syntax Error Validation Rule**

> **Note:** This does NOT mean that a physical file is sent back
> reporting the error. This is only a manual process.
>
> **5 Physical Format**
>
> This section defines the physical format for the Return Batch and the
> Acknowledgement File. In accordance with the definitions for the
> appropriate TAP standard, the physical format uses ASN.1. The
> specification is complimentary to the definition of the physical TAP
> format in that data types and groups defined by TAP are referenced
> within this specification and that the ASN.1 tags for the data types
> added for the RAP are distinct from the tags used for TAP, so that by
> merging both ASN.1 specifications, a new ASN.1 specification which
> covers both RAP and TAP is obtained.
>
> **Note:** All elements in the TAP specification should be made
> "OPTIONAL" during the creation of the RAP file. This will make it
> possible to return structure errors in the TAP file.
>
> The returned ASN.1 group must be the original received from the VPMN,
> and not re-encoded.
>
> **Note:** According to the principles laid in TAP specifications, the
> following must apply for the return batch:
>
> • The size of encoded Integers in the return batch must not exceed 4
> bytes except for
>
> the data items representing Severe Return Value and Total Severe
> Return Value.
>
> • The maximum size of the encoded return batch is determined by the
> maximum size
>
> of a TAP file. Please note that the size of a RAP file may be slightly
> larger than the
>
> size of the related TAP file.
>
> The following ranges for tags are currently used:

+-----------------------------------+-----------------------------------+
| **Tag range**                     | > **Description**                 |
+===================================+===================================+
| > 0-6                             | > Reserved for TAP                |
+-----------------------------------+-----------------------------------+
| > 7-8                             | > In Use for both TAP and RAP     |
+-----------------------------------+-----------------------------------+
| > 9-142                           | > Reserved for TAP                |
+-----------------------------------+-----------------------------------+
| > 143                             | > In Use for both TAP and RAP     |
+-----------------------------------+-----------------------------------+
| > 144-237                         | > Reserved for TAP                |
+-----------------------------------+-----------------------------------+
| > 238                             | > In Use for both TAP and RAP     |
+-----------------------------------+-----------------------------------+
| > 239-511                         | > Reserved for TAP                |
+-----------------------------------+-----------------------------------+

> V6.11 Page 28 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| **Tag range**                     | > **Description**                 |
+===================================+===================================+
| > 512-513                         | > In Use for RAP                  |
+-----------------------------------+-----------------------------------+
| > 514                             | > Reserved for RAP                |
+-----------------------------------+-----------------------------------+
| > 515-528                         | > In Use for RAP                  |
+-----------------------------------+-----------------------------------+
| > 529-531                         | > Reserved for RAP                |
+-----------------------------------+-----------------------------------+
| > 532-555                         | > In Use for RAP                  |
+-----------------------------------+-----------------------------------+
| > 556-1023                        | > Reserved for RAP                |
+-----------------------------------+-----------------------------------+

**Table 9: Tag Ranges**

> V6.11 Page 29 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

\--\
\-- The following ASN.1 specification defines the abstract\
\-- syntax for the Rejects and Returns Returned Accounts Procedure.

\--\
\-- The specification is structured as follows: \-- (1) Structure of a
RAP batch\
\-- (2) Structure of the individual RAP records \-- (3) RAP data items
and groups of data items \--

RAP-0105 DEFINITIONS IMPLICIT TAGS ::=

BEGIN\
\--\
\-- NOTE: As the RAP can be used to report rejections of any \-- valid
TAP release this specification does not indicate \-- explicitly the TAP
release to be included.

\--\
\-- Please replace XX in 'FROM TAP-03XX' with the appropriate \-- TAP
release version: for example 02, 04, 10, 11, \...

\-- making all TAP fields OPTIONAL\
\--\
IMPORTS AbsoluteAmount, AccountingInfo, AuditControlInfo,\
BatchControlInfo, CallEventDetail, DateTimeLong,\
FileSequenceNumber, FileTypeIndicator,\
MessageDescription, MessageDescriptionCode, NetworkInfo, Notification,
NumberString, OperatorSpecInformation,\
PlmnId, RapFileSequenceNumber, Recipient, ReleaseVersionNumber, Sender,
SpecificationVersionNumber,\
TapDecimalPlaces, TapCurrency\
\-- For TAP releases earlier than TAP3.11\
\-- uncomment the following line\
\-- ,VasCode, VasDescription, VasShortDescription\
FROM TAP-03XX;

\--\
\-- Structure of a RAP batch\
\--

RapDataInterChange ::= CHOICE

V6.11 Page 30 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

{\
returnBatch ReturnBatch,\
acknowledgement Acknowledgement, \...

}

ReturnBatch ::= \[APPLICATION 534\] SEQUENCE\
{\
rapBatchControlInfoRap RapBatchControlInfo, returnDetails
ReturnDetailList, rapAuditControlInfo RapAuditControlInfo, \...

}

Acknowledgement ::= \[APPLICATION 535\] SEQUENCE {\
sender Sender,\
recipient Recipient,

> rapFileSequenceNumber\
> ackFileCreationTimeStamp
>
> RapFileSequenceNumber,\
> AckFileCreationTimeStamp,
>
> ackFileAvailableTimeStamp AckFileAvailableTimeStamp,

+-----------------------+-----------------------+-----------------------+
| > fileTypeIndicator   | > FileTypeIndicator   | OPTIONAL,             |
+=======================+=======================+=======================+
| > operatorSpecList    | > OperatorSpecList    | OPTIONAL,             |
+-----------------------+-----------------------+-----------------------+

\...\
}

ReturnDetailList ::= \[APPLICATION 536\] SEQUENCE OF ReturnDetail

ReturnDetail ::= CHOICE\
{\
stopReturn StopReturn,\
missingReturn MissingReturn,\
fatalReturn FatalReturn,\
SevereReturn,\
severeReturn \...

}

\--\
\-- Structure of the individual RAP records \--

V6.11 Page 31 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

RapBatchControlInfo ::= \[APPLICATION 537\] SEQUENCE

{

> sender Sender,
>
> recipient Recipient,
>
> rapFileSequenceNumber\
> rapFileCreationTimeStamp
>
> RapFileSequenceNumber,\
> RapFileCreationTimeStamp,
>
> rapFileAvailableTimeStamp RapFileAvailableTimeStamp,
>
> specificationVersionNumber SpecificationVersionNumber OPTIONAL,

+-----------------------+-----------------------+-----------------------+
| >                     | ReleaseVersionNumber  | OPTIONAL,             |
|  releaseVersionNumber |                       |                       |
+=======================+=======================+=======================+
+-----------------------+-----------------------+-----------------------+

> rapSpecificationVersionNumber RapSpecificationVersionNumber,

+-----------------------+-----------------------+-----------------------+
| > ra                  | Rap                   | > OPTIONAL,           |
| pReleaseVersionNumber | ReleaseVersionNumber, |                       |
+=======================+=======================+=======================+
| > fileTypeIndicator   | > FileTypeIndicator   |                       |
+-----------------------+-----------------------+-----------------------+
| > roamingPartner      | > RoamingPartner      | > OPTIONAL,           |
+-----------------------+-----------------------+-----------------------+
| > operatorSpecList    | > OperatorSpecList    | > OPTIONAL,           |
+-----------------------+-----------------------+-----------------------+
| > tapDecimalPlaces    | > TapDecimalPlaces    | > OPTIONAL,           |
+-----------------------+-----------------------+-----------------------+
| > tapCurrency         | > TapCurrency         | > OPTIONAL,           |
+-----------------------+-----------------------+-----------------------+

\...

}

StopReturn ::= \[APPLICATION 554\] SEQUENCE

{

+-----------------------+-----------------------+-----------------------+
| > lastSeqNumber       | > LastSeqNumber,      | > OPTIONAL,           |
+=======================+=======================+=======================+
| > operatorSpecList    | > OperatorSpecList    |                       |
+-----------------------+-----------------------+-----------------------+

\...

}

MissingReturn ::= \[APPLICATION 538\] SEQUENCE

{

+-----------------------+-----------------------+-----------------------+
| >                     | > S                   | > OPTIONAL,           |
| startMissingSeqNumber | tartMissingSeqNumber, |                       |
+=======================+=======================+=======================+
| > endMissingSeqNumber | > EndMissingSeqNumber |                       |
+-----------------------+-----------------------+-----------------------+
| > operatorSpecList    | > OperatorSpecList    | > OPTIONAL,           |
+-----------------------+-----------------------+-----------------------+

\...

}

FatalReturn ::= \[APPLICATION 539\] SEQUENCE

{

+-----------------+-----------------+-----------------+-----------------+
| > fil           | > File          | > OPTIONAL,     | Page 32 of 46   |
| eSequenceNumber | SequenceNumber, |                 |                 |
+=================+=================+=================+=================+
| > tra           | > Tra           |                 |                 |
| nsferBatchError | nsferBatchError |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| > no            | No              | > OPTIONAL,     |                 |
| tificationError | tificationError |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| V6.11           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

batchControlError BatchControlError OPTIONAL, accountingInfoError
AccountingInfoError OPTIONAL, OPTIONAL, networkInfoError\
NetworkInfoError \-- For TAP releases earlier than TAP3.11\
\-- uncomment the following line\
\-- vASInformationError VASInformationError OPTIONAL,
messageDescriptionError MessageDescriptionError OPTIONAL,
auditControlInfoError AuditControlInfoError OPTIONAL, operatorSpecList
OperatorSpecList OPTIONAL, \...

}

SevereReturn ::= \[APPLICATION 540\] SEQUENCE\
{\
fileSequenceNumber FileSequenceNumber,\
callEventDetail CallEventDetail,\
errorDetail ErrorDetailList,\
operatorSpecList OperatorSpecList OPTIONAL, \...

}

RapAuditControlInfo ::= \[APPLICATION 541\] SEQUENCE {

> totalSevereReturnValue returnDetailsCount
>
> TotalSevereReturnValue, ReturnDetailsCount,

+-----------------------+-----------------------+-----------------------+
| > operatorSpecList    | > OperatorSpecList    | > OPTIONAL,           |
+=======================+=======================+=======================+
| >                     | >                     | > OPTIONAL,           |
|  totalSevereReturnTax |  TotalSevereReturnTax |                       |
+-----------------------+-----------------------+-----------------------+

\...\
}

\--\
\-- RAP data items and groups of data items \--

AccountingInfoError ::= \[APPLICATION 512\] SEQUENCE {\
accountingInfo AccountingInfo,\
errorDetail ErrorDetailList,\
\...

}

V6.11 Page 33 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

AuditControlInfoError ::= \[APPLICATION 513\] SEQUENCE {\
auditControlInfo AuditControlInfo,\
errorDetail ErrorDetailList,\
\...

}

AckFileAvailableTimeStamp ::= \[APPLICATION 515\] DateTimeLong

AckFileCreationTimeStamp ::= \[APPLICATION 516\] DateTimeLong

BatchControlError ::= \[APPLICATION 517\] SEQUENCE {\
batchControlInfo BatchControlInfo,\
errorDetail ErrorDetailList,\
\...

}

EndMissingSeqNumber ::= \[APPLICATION 518\] FileSequenceNumber

ErrorCode ::= \[APPLICATION 519\] INTEGER

ErrorContext ::= \[APPLICATION 545\] SEQUENCE {

+-----------------------+-----------------------+-----------------------+
| > pathItemId          | > PathItemId*,*       | > OPTIONAL,           |
+=======================+=======================+=======================+
| > itemOccurrence      | > ItemOccurrence      |                       |
+-----------------------+-----------------------+-----------------------+
| > itemLevel           | > ItemLevel,          |                       |
+-----------------------+-----------------------+-----------------------+

\...\
}

ErrorContextList ::= \[APPLICATION 549\] SEQUENCE OF ErrorContext

ErrorDetail ::= \[APPLICATION 521\] SEQUENCE {\
errorContext ErrorContextList OPTIONAL, itemOffset ItemOffset OPTIONAL,
ErrorCode,\
errorCode \...

}

V6.11 Page 34 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

ErrorDetailList ::= \[APPLICATION 520\] SEQUENCE OF ErrorDetail

ItemLevel ::= \[APPLICATION 548\] INTEGER

ItemOccurrence ::= \[APPLICATION 547\] INTEGER

ItemOffset ::= \[APPLICATION 524\] INTEGER

LastSeqNumber ::= \[APPLICATION 555\] FileSequenceNumber

MessageDescriptionError ::= \[APPLICATION 522\] SEQUENCE

{

> messageDescriptionInfo MessageDescriptionInfoList,
>
> errorDetail ErrorDetailList,

\...

}

  ---------------------------------------------------------------------------------------------------------
  MessageDescriptionInfoList                ::=         \[APPLICATION   8\]         SEQUENCE    OF
  ----------------------------------------- ----------- --------------- ----------- ----------- -----------
  MessageDescriptionInformationDefinition                                                       

  ---------------------------------------------------------------------------------------------------------

MessageDescriptionInformationDefinition ::= \[APPLICATION 143\] SEQUENCE

{

> messageDescriptionCode MessageDescriptionCode OPTIONAL,
>
> messageDescription MessageDescription OPTIONAL,

\...

}

NetworkInfoError ::= \[APPLICATION 523\] SEQUENCE

{

> networkInfo NetworkInfo,
>
> errorDetail ErrorDetailList,

\...

}

NotificationError ::= \[APPLICATION 552\] SEQUENCE

{

> notification Notification,
>
> errorDetail ErrorDetailList,

\...

V6.11 Page 35 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

}

OperatorSpecList ::= \[APPLICATION 551\] SEQUENCE OF
OperatorSpecInformation

PathItemId ::= \[APPLICATION 546\] INTEGER

RapFileAvailableTimeStamp ::= \[APPLICATION 525\] DateTimeLong

RapFileCreationTimeStamp ::= \[APPLICATION 526\] DateTimeLong

RapReleaseVersionNumber ::= \[APPLICATION 543\] INTEGER

RapSpecificationVersionNumber ::= \[APPLICATION 544\] INTEGER

ReturnDetailsCount ::= \[APPLICATION 528\] INTEGER

RoamingPartner ::= \[APPLICATION 550\] PlmnId

StartMissingSeqNumber ::= \[APPLICATION 532\] FileSequenceNumber

TotalSevereReturnTax ::= \[APPLICATION 553\] AbsoluteAmount

TotalSevereReturnValue ::= \[APPLICATION 533\] AbsoluteAmount

TransferBatchError ::= \[APPLICATION 542\] SEQUENCE

{

> errorDetail ErrorDetailList,

\...

}

\-- For TAP releases earlier than TAP3.11

\-- uncomment the following 12 lines

\--VasInfoList ::= \[APPLICATION 7\] SEQUENCE OF
VasInformationDefinition

\--VasInformationDefinition ::= \[APPLICATION 238\] SEQUENCE

\--{

+-------------+-------------+-------------+-------------+-------------+
| \--         | > vasCode   | > VasCode   | > OPTIONAL, | > Page 36   |
|             |             |             |             | > of 46     |
+=============+=============+=============+=============+=============+
| \--         | > v         | VasShort    | > OPTIONAL, |             |
|             | asShortDesc | Description |             |             |
+-------------+-------------+-------------+-------------+-------------+
| \--         | > vasDesc   | > Vas       | > OPTIONAL, |             |
|             |             | Description |             |             |
+-------------+-------------+-------------+-------------+-------------+
| V6.11       |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.32 - RAP Format Specification

\--\...

\--}

\--VASInformationError ::= \[APPLICATION 527\] SEQUENCE

\--{

+-----------------------+-----------------------+-----------------------+
| \--                   | > vasInfo             | > VasInfoList,        |
+=======================+=======================+=======================+
| \--                   | > errorDetail         | > ErrorDetailList,    |
+-----------------------+-----------------------+-----------------------+

\--\...

\--}

END

**6 File Naming Conventions**

**6.1** **Commercial RAP Data**

RAP Files containing rejected chargeable data that is being returned
must follow the naming convention below:

RCxxxxxyyyyySEQNO

Where:\
RC = "Returned Chargeable data"\
xxxxx = the returning entity (Sender)\
yyyyy = the originator of the TAP data (Recipient) SEQNO = sequence
number

**6.2** **Test RAP Data**

RAP Files containing rejected test data that is being returned must
follow the naming convention below:

RTxxxxxyyyyySEQNO

Where:\
RT = "Returned Test data"\
xxxxx = the rejecting entity (Sender)\
yyyyy = the originator of the TAP test data (Recipient) SEQNO = sequence
number

**6.3** **Acknowledgement of Commercial RAP Data**

Acknowledgements of RAP Files containing rejected chargeable data that
is being returned must follow the naming convention below:

ACxxxxxyyyyySEQNO

Where:\
AC = "Acknowledgement of returned Chargeable data" xxxxx = the
acknowledging entity (Sender)\
yyyyy = the returning entity (Recipient)

V6.11 Page 37 of 46

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.32 - RAP Format Specification

> SEQNO = sequence number of the RAP File being acknowledged

**6.4** **Acknowledgement of Test RAP Data**

Acknowledgements of RAP Files containing rejected test data that is
being returned must follow the naming convention below:

ATxxxxxyyyyySEQNO

Where:

> AT = "Acknowledgement of returned Test data"
>
> xxxxx = the acknowledging entity (Sender)
>
> yyyyy = the returning entity (Recipient)
>
> SEQNO = sequence number of the RAP File being acknowledged

**7 Migration to a New Release**

The rules in this section apply to RAP files exchanged over the public
interface. RAP files exchanged over the private interface, for example
between an operator and its Agent is out of scope of these migration
rules.

There is an Effective Date defined for each release. This is the date on
which companies must send and receive the release over the public
interface.

Companies must be ready before the Effective Date to send and receive
RAP test files in the new release on a bilateral basis.

Appropriate format testing must be completed before the Effective Date
for a migration to a release containing major changes.

Companies that have not migrated to the new release, when the Effective
Date has been reached, must (prior to the Effective Date) make other
provisions (for example using the services of a conversion agent) to
send/receive the new release when exchanging RAP files with companies
who have implemented the new release.

Where a RAP file created in an old release cannot be read by the RAP
recipient and need to be corrected and resubmitted, the RAP file may be
resubmitted in either the old or the new release, taking the timescales
defined in BA.08 ‎\[1\] into consideration.

Unless agreed by the recipient, the sender is not allowed to revert to
the old release, once the first files of the new release have been
exchanged in commercial operation (excluding resubmitted files which
have initially been issued before the release switch and test files).

V6.11 Page 38 of 46

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **Annex A** **IOT Related Errors**
>
> This annex is mandatory to implement.

The HPMN must provide additional information when rejecting for an IOT
related error. This

additional information will assist with the investigation and correction
of the reported IOT

related error. This is done for all errors listed in the table below by
populating the Operator

> Specific Information item with information as shown in the right hand
> column of the table:

+-----------------+-----------------+-----------------+-----------------+
| > **Element     | **Error code**  | > **Error       | > **Information |
| > name**        |                 | > description** | > in Operator   |
|                 |                 |                 | > Specific      |
|                 |                 |                 | > Information** |
+=================+=================+=================+=================+
| > CAMEL\        | > 200           | > CAMEL         | > List a        |
| > Invocation    | >               | > Invocation    | > minimum of 3  |
| > Fee           | > 200           | > Fee not in    | > occurrences   |
| >               | >               | > line with     | > of Operator   |
| > Charge        | > 200           | > roaming       | > Specific      |
|                 |                 | > agreement.    | > Information,  |
| Tax Value       |                 | >               | > each          |
|                 |                 | > Charge not in | > including a   |
|                 |                 | > line with     | > unique        |
|                 |                 | > roaming\      | > keyword       |
|                 |                 | > agreement.    | > followed by   |
|                 |                 | >               | > the           |
|                 |                 | > Tax Value is  | > information.  |
|                 |                 | > not in\       | >               |
|                 |                 | > line with the | > 1\)           |
|                 |                 | > roaming       | > Mandatory:    |
|                 |                 | > agreement at  | > Keyword       |
|                 |                 | > the\          | > "IOTDate:"    |
|                 |                 | > corresponding | > followed by   |
|                 |                 | > call\         | > the date      |
|                 |                 | > event date.   | > (which must   |
|                 |                 |                 | > be in format  |
|                 |                 |                 | > YYYYMMDD)     |
|                 |                 |                 | > from which    |
|                 |                 |                 | > the IOT (for  |
|                 |                 |                 | > the rejected  |
|                 |                 |                 | > call event)   |
|                 |                 |                 | > is\           |
|                 |                 |                 | > applicable.   |
|                 |                 |                 | >               |
|                 |                 |                 | > **Note:** The |
|                 |                 |                 | > IOT could     |
|                 |                 |                 | > have          |
|                 |                 |                 | > different     |
|                 |                 |                 | > dates for     |
|                 |                 |                 | > different     |
|                 |                 |                 | > call events,  |
|                 |                 |                 | > and for       |
|                 |                 |                 | > different     |
|                 |                 |                 | > types of call |
|                 |                 |                 | > events.       |
|                 |                 |                 | >               |
|                 |                 |                 | > Example:      |
|                 |                 |                 | > I             |
|                 |                 |                 | OTDate:20120701 |
|                 |                 |                 | >               |
|                 |                 |                 | > 2\)           |
|                 |                 |                 | > Mandatory:    |
|                 |                 |                 | > Keyword       |
|                 |                 |                 | > "ExpCharge:"  |
|                 |                 |                 | > followed by   |
|                 |                 |                 | > the expected  |
|                 |                 |                 | > charge (in    |
|                 |                 |                 | > the same TAP  |
|                 |                 |                 | > Currency, the |
|                 |                 |                 | > same format,  |
|                 |                 |                 | > and with the  |
|                 |                 |                 | > same number   |
|                 |                 |                 | > of decimal    |
|                 |                 |                 | > places as in  |
|                 |                 |                 | > the TAP       |
|                 |                 |                 | > file).        |
|                 |                 |                 |                 |
|                 |                 |                 | If the call     |
|                 |                 |                 | scenario is not |
|                 |                 |                 | listed in the   |
|                 |                 |                 | IOT, then       |
|                 |                 |                 | instead         |
|                 |                 |                 |                 |
|                 |                 |                 | > of the        |
|                 |                 |                 | > expected      |
|                 |                 |                 | > charge the    |
|                 |                 |                 | > keyword "Not  |
|                 |                 |                 | > in IOT" is    |
|                 |                 |                 | > present.      |
|                 |                 |                 | >               |
|                 |                 |                 | > Example 1:    |
|                 |                 |                 | >               |
|                 |                 |                 |  ExpCharge:1234 |
|                 |                 |                 | >               |
|                 |                 |                 | > Example 2:    |
|                 |                 |                 | > ExpCharge:Not |
|                 |                 |                 | > in IOT        |
|                 |                 |                 | >               |
|                 |                 |                 | > 3\)           |
|                 |                 |                 | > Mandatory:    |
|                 |                 |                 | > Keyword       |
|                 |                 |                 | >               |
|                 |                 |                 |  "Calculation:" |
|                 |                 |                 | > followed by a |
|                 |                 |                 | > free text     |
|                 |                 |                 | > describing    |
|                 |                 |                 | > what          |
|                 |                 |                 | > calculation   |
|                 |                 |                 | > has been\     |
|                 |                 |                 | > performed.    |
|                 |                 |                 | >               |
|                 |                 |                 | > If the call   |
|                 |                 |                 | > scenario is   |
|                 |                 |                 | > not listed in |
|                 |                 |                 | > the IOT, then |
|                 |                 |                 | > instead of    |
|                 |                 |                 | > the           |
|                 |                 |                 | > calculation   |
|                 |                 |                 | > the keyword   |
|                 |                 |                 | > "Not in IOT"  |
|                 |                 |                 | > is present.   |
|                 |                 |                 | >               |
|                 |                 |                 | > Example 1:    |
|                 |                 |                 | > Calcula       |
|                 |                 |                 | tion:1\*30=1.2, |
|                 |                 |                 | > X\*15\~2.5    |
|                 |                 |                 | >               |
|                 |                 |                 | > Example 2:    |
|                 |                 |                 | >               |
|                 |                 |                 | Calculation:Not |
|                 |                 |                 | > in IOT        |
|                 |                 |                 | >               |
|                 |                 |                 | > (see Table    |
|                 |                 |                 | > 11: for more  |
|                 |                 |                 | > examples).    |
|                 |                 |                 | >               |
|                 |                 |                 | > 4\)           |
|                 |                 |                 | > Conditional:  |
|                 |                 |                 | > Keyword       |
|                 |                 |                 | >               |
|                 |                 |                 |  "BilatTariff:" |
|                 |                 |                 | > followed by a |
|                 |                 |                 | > Y if there is |
|                 |                 |                 | > a special     |
|                 |                 |                 | > agreement     |
|                 |                 |                 | > that          |
|                 |                 |                 | > overrides     |
|                 |                 |                 | > the\          |
|                 |                 |                 | > standard IOT  |
|                 |                 |                 | > (for the      |
|                 |                 |                 | > rejected call |
|                 |                 |                 | > event).       |
|                 |                 |                 | >               |
|                 |                 |                 | > **Note:**     |
|                 |                 |                 | > Different     |
|                 |                 |                 | > call events,  |
|                 |                 |                 | > and different |
|                 |                 |                 | > types of call |
|                 |                 |                 | > events, could |
|                 |                 |                 | > have          |
|                 |                 |                 | > different     |
|                 |                 |                 | > IOTs, so the  |
|                 |                 |                 | > BilatTariff   |
|                 |                 |                 | > could be Y    |
|                 |                 |                 | > for one type  |
|                 |                 |                 | > of call       |
|                 |                 |                 | > event, and N  |
|                 |                 |                 | > for\          |
|                 |                 |                 | > another.      |
|                 |                 |                 | >               |
|                 |                 |                 | > Example:      |
|                 |                 |                 | > BilatTariff:Y |
+-----------------+-----------------+-----------------+-----------------+

**Table 10: Charge Related Errors**

> V6.11 Page 39 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > **Example**\                    | > **Explanation**                 |
| > **calculation rule**            |                                   |
+===================================+===================================+
| > X\*60\~1.6                      | > Each minute fully charged at    |
|                                   | > 1.6 / minute                    |
+-----------------------------------+-----------------------------------+
| > 1\*30\~1.6, X\*10               | > First 30 seconds with minute    |
|                                   | > price of 1.6 and afterwards     |
|                                   | > charged each 10 seconds with    |
|                                   | > the same minute price           |
+-----------------------------------+-----------------------------------+
| > X\*3=1.2                        | Each 3 seconds are charged 1.2    |
|                                   | (this will result in a minute     |
|                                   | price of 1.2\*60/3)               |
+-----------------------------------+-----------------------------------+
| > 1\*30=1.2, X\*15\~2.5           | > First 30 seconds cost 1.2 and   |
|                                   | > afterwards each 15 seconds at a |
|                                   | > minute price of 2.5             |
+-----------------------------------+-----------------------------------+
| 0.5+1\*60%3\~1.5, X\*1            | > Access fee 0.5, 1st minute      |
|                                   | > charged from the 3rd second at  |
|                                   | > a price of 1.5 per minute and   |
|                                   | > afterwards charge each second   |
|                                   | > at a price of 1.5 per minute    |
+-----------------------------------+-----------------------------------+
| > X\*1024 = 0.005                 | > **Note**: In case of            |
|                                   | > non-duration based services,    |
|                                   | > only the unit price ( = ) must  |
|                                   | > be used. This is the case in    |
|                                   | > GPRS volume charging, for       |
|                                   | > example X\*1024 = 0.005.        |
+-----------------------------------+-----------------------------------+

> **Table 11: Examples of different calculation rules**
>
> V6.11 Page 40 of 46
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **Annex B** **Other Errors**
>
> This annex is optional to implement.
>
> It is also advised that the HPMN provide additional information to
> support some other reported errors in RAP files. This information will
> assist the VPMN to investigate and repair the error and thus it will
> help in reaching a quick settlement between the two parties.
>
> Where the following errors are reported, the HPMN is recommended to
> populate the Operator Specific Information item with information as
> shown in the below table:

+-----------------+-----------------+-----------------+-----------------+
| > **Element     | **Error code**  | > **Error       | > **Information |
| > name**        |                 | > description** | > in Operator   |
|                 |                 |                 | > Specific      |
|                 |                 |                 | > Information** |
+=================+=================+=================+=================+
|                 | > 250 -253,     | > Call is       | > Keyword       |
|                 |                 | > duplicate.    | > "SeqNo:"      |
|                 | 255 -257        |                 | > followed by   |
|                 |                 |                 | > the TAP file  |
|                 |                 |                 | > sequence      |
|                 |                 |                 | > number for    |
|                 |                 |                 | > the           |
|                 |                 |                 | > previously    |
|                 |                 |                 | > received      |
|                 |                 |                 | > duplicate     |
|                 |                 |                 | > call record.  |
|                 |                 |                 | >               |
|                 |                 |                 | > Example:      |
|                 |                 |                 | > SeqNo:12345   |
+-----------------+-----------------+-----------------+-----------------+
|                 | > 261           | > Call older    | > Keyword       |
|                 |                 | > than\         | > "Age:"        |
|                 |                 | > allowed by    | > followed by   |
|                 |                 | > BARG in       | > the Age of    |
|                 |                 | >               | > the Call      |
|                 |                 | > 'Exceptional\ | > record in     |
|                 |                 | > Situations'   | > whole days.   |
|                 |                 | > in BA.08      | >               |
|                 |                 | > ‎\[1\].        | > Example:      |
|                 |                 |                 | > Age:31        |
+-----------------+-----------------+-----------------+-----------------+
| > Exchange Rate | > 200           | > Exchange Rate | > Keyword       |
|                 |                 | > less than     | > "ExpRate:"    |
|                 |                 | > expected (see | > followed by   |
|                 |                 | > BA.11 ‎\[2\])  | > the expected\ |
|                 |                 | > and\          | > Exchange rate |
|                 |                 | > referenced by | > (using same   |
|                 |                 | > one or more   | > number of     |
|                 |                 | > Call Event\   | > decimal       |
|                 |                 | > Details.      | > places as in  |
|                 |                 |                 | > the TAP       |
|                 |                 |                 | > file).        |
|                 |                 |                 | >               |
|                 |                 |                 | > Example:      |
|                 |                 |                 | >               |
|                 |                 |                 |  ExpRate:123456 |
+-----------------+-----------------+-----------------+-----------------+
| > Tax Rate Code | > 200           | > The           | > Keyword       |
|                 |                 | > referenced    | > "ExpRate:"    |
|                 |                 | > Tax Rate is   | > followed by   |
|                 |                 | > not in line   | > the expected  |
|                 |                 | > with the      | > Tax Rate.     |
|                 |                 | > roaming\      | >               |
|                 |                 | > agreement at  | > Example:      |
|                 |                 | > the\          | >               |
|                 |                 | > corresponding | ExpRate:1500000 |
|                 |                 | > call\         |                 |
|                 |                 | > date.         |                 |
+-----------------+-----------------+-----------------+-----------------+

**Table 12: Other Errors**

> V6.11 Page 41 of 46
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **Annex C** **Minimum Content of RAP Disputes and Denials**
>
> The following information must be provided together with all RAP
> disputes and RAP dispute denials:

+-----------------------------------+-----------------------------------+
| > **Information**                 | > **Comments**                    |
+===================================+===================================+
| > RAP File Names                  | > List of RAP file names covered  |
|                                   | > by the dispute or denial.       |
+-----------------------------------+-----------------------------------+
| > TAP File Names                  | > TAP file name listed for each   |
|                                   | > RAP file.                       |
+-----------------------------------+-----------------------------------+
| > RAP dispute\                    | > The time the dispute was        |
| > raised timestamp                | > raised, given in local date and |
|                                   | > time with UTC offset. The party |
|                                   | > raising the dispute may         |
|                                   | > optionally include its own      |
|                                   | > local date and time into the    |
|                                   | > e-mail body, although the       |
|                                   | > timestamp generated by the      |
|                                   | > e-mail application (delivery to |
|                                   | > the recipient's domain) must be |
|                                   | > used for calculation of related |
|                                   | > timescales.                     |
+-----------------------------------+-----------------------------------+
| > RAP dispute denial raised       | > The time the denial was raised, |
| > timestamp                       | > given in local date and time    |
|                                   | > with UTC offset. The party      |
|                                   | > denying the dispute may         |
|                                   | > optionally include its own      |
|                                   | > local date and time into the    |
|                                   | > e-mail body, although the       |
|                                   | > timestamp generated by the      |
|                                   | > e-mail application (delivery to |
|                                   | > the recipient's domain) must be |
|                                   | > used for calculation of related |
|                                   | > timescales.                     |
+-----------------------------------+-----------------------------------+
| > Reason                          | > Free text to explain the reason |
|                                   | > the RAP is disputed or the      |
|                                   | > dispute is denied.              |
+-----------------------------------+-----------------------------------+

> **Table 13: Minimum Content of RAP Disputes and Denials**
>
> The following additional information must also be provided together
> with all RAP IOT disputes and denials, where the RAP file has rejected
> calls due to error code 200 on the Charge, Tax Value or CAMEL
> Invocation Fee elements, or on error code 203 on the Charge element:

+-----------------------+-----------------------+-----------------------+
| > **Information**     | > **Comments**        |                       |
+=======================+=======================+=======================+
| > IOT Date            | > The date the IOT    |                       |
|                       | > became applicable   |                       |
|                       | > (as taken from the  |                       |
|                       | > IOT and not from    |                       |
|                       | > the RAP file).      |                       |
+-----------------------+-----------------------+-----------------------+
| > Calculation         | > Free text           |                       |
|                       | > describing what     |                       |
|                       | > calculation has     |                       |
|                       | > been performed.     |                       |
|                       | > Example: 1\*30=1.2, |                       |
|                       | > X\*15\~2.5.         |                       |
|                       | >                     |                       |
|                       | > Mandatory to        |                       |
|                       | > provide at least    |                       |
|                       | > one calculation     |                       |
|                       | > (except where noted |                       |
|                       | > below).             |                       |
|                       | >                     |                       |
|                       | > At maximum, only    |                       |
|                       | > need to provide     |                       |
|                       | > information         |                       |
|                       | > sufficient to cover |                       |
|                       | > all CDRs rejected.  |                       |
|                       | > Not one calculation |                       |
|                       | > for each rejected   |                       |
|                       | > CDR.                |                       |
|                       | >                     |                       |
|                       | > Optional to provide |                       |
|                       | > when IOT Date is    |                       |
|                       | > identified as       |                       |
|                       | > different between   |                       |
|                       | > disputing parties.  |                       |
+-----------------------+-----------------------+-----------------------+

> **Table 14: Minimum Content of IOT RAP Disputes and Denials**
>
> **Note:** It is possible that more than one IOT may cover a specific
> set of calls within the RAP file. In this case information on all IOTs
> applicable needs to be provided.
>
> V6.11 Page 42 of 46
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.32 - RAP Format Specification
>
> **Document Management**
>
> **Document History**

+-------------+-------------+-------------+-------------+-------------+
| **Version** | > **Date**  | > **Brief   | **Approval  | > **Editor  |
|             |             | >           | Authority** | > /**\      |
|             |             | Description |             | >           |
|             |             | > of        |             | **Company** |
|             |             | > Change**  |             |             |
+=============+=============+=============+=============+=============+
| > 3.0.0     | > 23 Apr    | > New PRD   | TADIG #46\  | > Christer\ |
|             | > 1999      | > (TADIG    | Plenary #41 | >           |
|             |             | > Doc       |             |  Gullstrand |
|             |             | > 016/99).  |             | > /         |
|             |             |             |             | > Syniverse |
+-------------+-------------+-------------+-------------+-------------+
| > 3.1.0     | > 22 Oct    | > CRs 1-5   | TADIG #47\  | > Christer\ |
|             | > 1999      | > (TADIG    | Plenary #42 | >           |
|             |             | > Docs      |             |  Gullstrand |
|             |             | > 39/99,    |             | > /         |
|             |             | >           |             | > Syniverse |
|             |             |  44/99rev1, |             |             |
|             |             | > and       |             |             |
|             |             | > 73        |             |             |
|             |             | /99-75/99). |             |             |
|             |             | >           |             |             |
|             |             | > Inclusion |             |             |
|             |             | > of        |             |             |
|             |             | > Transfer  |             |             |
|             |             | > Batch     |             |             |
|             |             | > level     |             |             |
|             |             | > Fatal     |             |             |
|             |             | > errors.   |             |             |
|             |             | > Rewrite   |             |             |
|             |             | > of        |             |             |
|             |             | > section   |             |             |
|             |             | > 7 -       |             |             |
|             |             | >           |             |             |
|             |             |  Scenarios. |             |             |
|             |             | >           |             |             |
|             |             | > Cl        |             |             |
|             |             | arification |             |             |
|             |             | > of Return |             |             |
|             |             | > Value.    |             |             |
|             |             | >           |             |             |
|             |             | > Addition  |             |             |
|             |             | > of fields |             |             |
|             |             | > to make   |             |             |
|             |             | > RAP       |             |             |
|             |             | > release   |             |             |
|             |             | >           |             |             |
|             |             |  management |             |             |
|             |             | > possible. |             |             |
|             |             | >           |             |             |
|             |             | > Removal   |             |             |
|             |             | > of        |             |             |
|             |             | >           |             |             |
|             |             | unnecessary |             |             |
|             |             | > items     |             |             |
|             |             | > from the  |             |             |
|             |             | > Ackn      |             |             |
|             |             | owledgement |             |             |
|             |             | > File.     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.2.0     | > 27 Apr    | > CRs 6-10  | TADIG #48\  | > Christer\ |
|             | > 2000      | > (TADIG    | Plenary #43 | >           |
|             |             | > Docs      |             |  Gullstrand |
|             |             | > 22/00,    |             | > /         |
|             |             | >           |             | > Syniverse |
|             |             |  24/00rev1, |             |             |
|             |             | >           |             |             |
|             |             |  23/00rev1, |             |             |
|             |             | > 32/00 and |             |             |
|             |             | > 39/00).   |             |             |
|             |             | >           |             |             |
|             |             | > Changes   |             |             |
|             |             | > to        |             |             |
|             |             | > physical  |             |             |
|             |             | > format\   |             |             |
|             |             | > Value of  |             |             |
|             |             | > a         |             |             |
|             |             | > rejected  |             |             |
|             |             | > TAP file  |             |             |
|             |             | > must not  |             |             |
|             |             | > be\       |             |             |
|             |             | > present   |             |             |
|             |             | > in the    |             |             |
|             |             | > RAP file\ |             |             |
|             |             | > New       |             |             |
|             |             | > optional  |             |             |
|             |             | > error     |             |             |
|             |             | > context   |             |             |
|             |             | > p         |             |             |
|             |             | resentation |             |             |
|             |             | > in the    |             |             |
|             |             | > RAP file\ |             |             |
|             |             | > The RAP   |             |             |
|             |             | > File      |             |             |
|             |             | > Sequence  |             |             |
|             |             | > Number    |             |             |
|             |             | > must not  |             |             |
|             |             | > be        |             |             |
|             |             | > included  |             |             |
|             |             | > when a    |             |             |
|             |             | > TAP file  |             |             |
|             |             | >           |             |             |
|             |             |  previously |             |             |
|             |             | > reported  |             |             |
|             |             | > missing   |             |             |
|             |             | > is sent\  |             |             |
|             |             | > Error     |             |             |
|             |             | >           |             |             |
|             |             | correction: |             |             |
|             |             | > RAP File  |             |             |
|             |             | > Sequence  |             |             |
|             |             | > Number is |             |             |
|             |             | > not       |             |             |
|             |             | > present   |             |             |
|             |             | > in Audit  |             |             |
|             |             | > Control   |             |             |
|             |             | >           |             |             |
|             |             | Information |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.3.0     | > 12 Oct    | > CRs       | TADIG #49\  | > Christer\ |
|             | > 2000      | > 11-13,    | Plenary #44 | >           |
|             |             | > 15-19     |             |  Gullstrand |
|             |             | > (TADIG    |             | > /         |
|             |             | > Docs      |             | > Syniverse |
|             |             | > 8         |             |             |
|             |             | 1/00-83/00, |             |             |
|             |             | >           |             |             |
|             |             | 85/00-88/00 |             |             |
|             |             | > and       |             |             |
|             |             | > 123/00).  |             |             |
|             |             | > CR14 was\ |             |             |
|             |             | > withdrawn |             |             |
|             |             | > as it was |             |             |
|             |             | > redundant |             |             |
|             |             | > after     |             |             |
|             |             | > the\      |             |             |
|             |             | > approval  |             |             |
|             |             | > of CR12.  |             |             |
+-------------+-------------+-------------+-------------+-------------+
|             | > 15 Dec    | Correction  | > TADIG     | > Christer\ |
|             | > 2000      | of          |             | >           |
|             |             | erroneous   |             |  Gullstrand |
|             |             | in          |             | > /         |
|             |             | corporation |             | > Syniverse |
|             |             | of CR13.    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.4.0     | 5 Mar 2001  | > CRs 20-23 | > TADIG #50 | > Christer\ |
|             |             | > (TADIG    | > E-mail    | >           |
|             |             | > Docs      | > vote      |  Gullstrand |
|             |             | > 09        |             | > /         |
|             |             | /01-12/01), |             | > Syniverse |
|             |             | > and CR 25 |             |             |
|             |             | > (approved |             |             |
|             |             | > by        |             |             |
|             |             | > e-mail).  |             |             |
|             |             | >           |             |             |
|             |             | > Note that |             |             |
|             |             | > CR 24 was |             |             |
|             |             | > not       |             |             |
|             |             | > approved, |             |             |
|             |             | > but       |             |             |
|             |             | > agreed to |             |             |
|             |             | > in        |             |             |
|             |             | > principle |             |             |
|             |             | > by TADIG  |             |             |
|             |             | > #50,      |             |             |
|             |             | > subject   |             |             |
|             |             | > to        |             |             |
|             |             | > further   |             |             |
|             |             | > detailed  |             |             |
|             |             | > sp        |             |             |
|             |             | ecification |             |             |
|             |             | > work by   |             |             |
|             |             | > the FSS.  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.5.0     | 6 Jul\      | > CRs       | > TADIG #51 | > Christer\ |
|             | 2001        | > 26-30\    |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Docs      |             | > /         |
|             |             | > 94        |             | > Syniverse |
|             |             | /01-98/01). |             |             |
|             |             |             |             |             |
|             |             | Note that   |             |             |
|             |             | CR 24 was   |             |             |
|             |             | withdrawn   |             |             |
|             |             | and         |             |             |
|             |             | reworked    |             |             |
|             |             | into CR 29  |             |             |
|             |             | that was    |             |             |
|             |             | approved by |             |             |
|             |             | TADIG #51.  |             |             |
+-------------+-------------+-------------+-------------+-------------+

> V6.11 Page 43 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-------------+-------------+-------------+-------------+-------------+
| **Version** | > **Date**  | > **Brief   | **Approval  | > **Editor  |
|             |             | >           | Authority** | > /**\      |
|             |             | Description |             | >           |
|             |             | > of        |             | **Company** |
|             |             | > Change**  |             |             |
+=============+=============+=============+=============+=============+
| > 3.5.1     | 9 Nov 2001  | > CRs 31    | > TADIG #52 | > Christer\ |
|             |             | > and 33    |             | >           |
|             |             | >           |             |  Gullstrand |
|             |             | > (TADIG    |             | > /         |
|             |             | > Docs      |             | > Syniverse |
|             |             | > 199/01    |             |             |
|             |             | > and       |             |             |
|             |             | > 201/01).  |             |             |
|             |             | >           |             |             |
|             |             | > Note that |             |             |
|             |             | > CR 32 is  |             |             |
|             |             | > a format  |             |             |
|             |             | > change    |             |             |
|             |             | > and will  |             |             |
|             |             | > therefore |             |             |
|             |             | > form part |             |             |
|             |             | > of RAP1.2 |             |             |
|             |             | > (TD.32    |             |             |
|             |             | > version   |             |             |
|             |             | > 3.6.0).   |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.6.0     | 6 Jun 2002  | > This      | > TADIG #52 | > Christer\ |
|             |             | > version   | > TADIG #53 | >           |
|             |             | > is the    | > EC #31    |  Gullstrand |
|             |             | > first     |             | > /         |
|             |             | > version   |             | > Syniverse |
|             |             | > to        |             |             |
|             |             | > specify   |             |             |
|             |             | > RAP1.2.   |             |             |
|             |             | >           |             |             |
|             |             | > CR 32 and |             |             |
|             |             | > 34-38\    |             |             |
|             |             | > (TADIG    |             |             |
|             |             | > Docs      |             |             |
|             |             | > 200/01    |             |             |
|             |             | > and       |             |             |
|             |             | > 48        |             |             |
|             |             | /02-52/02). |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.6.1     | > 20 Nov    | > NSCRs     | > TADIG #54 | > Christer\ |
|             | > 2002      | > 39-42\    |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Docs      |             | > /         |
|             |             | > 13        |             | > Syniverse |
|             |             | 8/02-140/02 |             |             |
|             |             | > and       |             |             |
|             |             | > 1         |             |             |
|             |             | 41/02rev1). |             |             |
|             |             | > Update of |             |             |
|             |             | > scenarios |             |             |
|             |             | > to        |             |             |
|             |             | > RAP1.2.   |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.6.2     | > 20 Dec    | > NSCR 43\  | > TADIG\    | > Christer\ |
|             | > 2002      | > (TADIG    | > E-mail    | >           |
|             |             | > Doc       | > vote      |  Gullstrand |
|             |             | > 004/03).  |             | > /         |
|             |             |             |             | > Syniverse |
+-------------+-------------+-------------+-------------+-------------+
| > 3.6.3     | 2 Jun 2003  | > NSCR45\   | > TADIG #55 | > Christer\ |
|             |             | > (TADIG    |             | >           |
|             |             | > Doc       |             |  Gullstrand |
|             |             | > 39_03).   |             | > /         |
|             |             | >           |             | > Syniverse |
|             |             | > Editorial |             |             |
|             |             | > cl        |             |             |
|             |             | arification |             |             |
|             |             | > to        |             |             |
|             |             | > RAP1.2.   |             |             |
|             |             | > Note: CR  |             |             |
|             |             | > 44 was    |             |             |
|             |             | > rejected. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.6.4     | > 18 Sep    | > NSCRs     | > TADIG\    | > Christer\ |
|             | > 2003      | > 46-48\    | > E-mail    | >           |
|             |             | > (TADIG    | > vote      |  Gullstrand |
|             |             | > Docs      |             | > /         |
|             |             | > 105/      |             | > Syniverse |
|             |             | 03-107/03). |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.7.0     | > Jun\      | > NSCRs     | > TADIG #57 | > Christer\ |
|             | > 2004      | > 049-051\  | > EMC #21   | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Docs      |             | > /         |
|             |             | > 57_055,   |             | > Syniverse |
|             |             | >           |             |             |
|             |             |  57_056rev1 |             |             |
|             |             | > and       |             |             |
|             |             | > 57_057).  |             |             |
|             |             | >           |             |             |
|             |             | > SCR 052\  |             |             |
|             |             | > (TADIG    |             |             |
|             |             | > Doc       |             |             |
|             |             | > 5         |             |             |
|             |             | 7_067rev3). |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.8       | May\        | > Minor CR  | > TADIG #59 | > Christer\ |
|             | 2005        | > 053\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 59_028).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Removal   |             |             |
|             |             | > of text   |             |             |
|             |             | > moved     |             |             |
|             |             | > into      |             |             |
|             |             | > BA.13     |             |             |
|             |             | > ‎\[3\].    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.9       | > 14 Oct    | > Minor CRs | > TADIG #60 | > Christer\ |
|             | > 2005      | > 054 and   |             | >           |
|             |             | > 055\      |             |  Gullstrand |
|             |             | > (TADIG    |             | > /         |
|             |             | > Docs      |             | > Syniverse |
|             |             | > 60_022    |             |             |
|             |             | > and       |             |             |
|             |             | > 6         |             |             |
|             |             | 0_023rev1). |             |             |
|             |             | > Reduce    |             |             |
|             |             | > maximum   |             |             |
|             |             | > size of   |             |             |
|             |             | > RAP file. |             |             |
|             |             | >           |             |             |
|             |             | > Add       |             |             |
|             |             | > scenario  |             |             |
|             |             | > for       |             |             |
|             |             | > missing   |             |             |
|             |             | > returns.  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.10      | 9 Nov 2006  | > Minor CR  | > TADIG #62 | > Christer\ |
|             |             | > 058\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 62_021).\ |             | > Syniverse |
|             |             | > Editorial |             |             |
|             |             | > c         |             |             |
|             |             | orrections. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 3.11      | 7 Jun 2007  | > Minor CR  | > TADIG #63 | > Christer\ |
|             |             | > 060\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 63_042).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Editorial |             |             |
|             |             | > Updates   |             |             |
|             |             | > to        |             |             |
|             |             | > Reference |             |             |
|             |             | > List.     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 4.0       | > 27 Jun    | > Major CR  | > TADIG #63 | > Christer\ |
|             | > 2007      | > 061\      | > EMC #55   | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 6         |             |             |
|             |             | 3_075rev1). |             |             |
+-------------+-------------+-------------+-------------+-------------+

> V6.11 Page 44 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-------------+-------------+-------------+-------------+-------------+
| **Version** | > **Date**  | > **Brief   | **Approval  | > **Editor  |
|             |             | >           | Authority** | > /**\      |
|             |             | Description |             | >           |
|             |             | > of        |             | **Company** |
|             |             | > Change**  |             |             |
+=============+=============+=============+=============+=============+
|             |             | > RAP1.4.   |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Adding    |             |             |
|             |             | > TAP       |             |             |
|             |             | > Decimal   |             |             |
|             |             | > Places    |             |             |
|             |             | > and TAP   |             |             |
|             |             | > Currency. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 4.1       | > 26 Dec    | > Major CR  | > TADIG #64 | > Christer\ |
|             | > 2007      | > 062\      | > EMC #60   | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 64_018).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Minor CR  |             |             |
|             |             | > 063\      |             |             |
|             |             | > (TADIG    |             |             |
|             |             | > Doc       |             |             |
|             |             | > 64_019).  |             |             |
|             |             | >           |             |             |
|             |             | >           |             |             |
|             |             |  Additional |             |             |
|             |             | > IOT       |             |             |
|             |             | > I         |             |             |
|             |             | nformation. |             |             |
|             |             | >           |             |             |
|             |             | > RAP       |             |             |
|             |             | > Release   |             |             |
|             |             | > Version   |             |             |
|             |             | > Number.   |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 4.2       | > 27 Mar    | > Major CR  | > TADIG     | > Christer\ |
|             | > 2008      | > 064\      | > eVote EMC | >           |
|             |             | > (TADIG    | > #62       |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 65_006).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Adding    |             |             |
|             |             | > Total     |             |             |
|             |             | > Severe    |             |             |
|             |             | > Return    |             |             |
|             |             | > Tax. New  |             |             |
|             |             | > GSMA      |             |             |
|             |             | > template  |             |             |
|             |             | > applied   |             |             |
|             |             | > (4        |             |             |
|             |             | > December  |             |             |
|             |             | > 2008).    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 5.0       | 2 Jul\      | > Major CR  | > TADIG #67 | > Christer\ |
|             | 2009        | > 065\      | > EMC #74   | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 67_044).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Changing  |             |             |
|             |             | > the       |             |             |
|             |             | > creation  |             |             |
|             |             | > rules for |             |             |
|             |             | > ACK       |             |             |
|             |             | > files,    |             |             |
|             |             | > imp       |             |             |
|             |             | lementation |             |             |
|             |             | > date 1    |             |             |
|             |             | > Dec 2009. |             |             |
|             |             | >           |             |             |
|             |             | > Editorial |             |             |
|             |             | >           |             |             |
|             |             | corrections |             |             |
|             |             | > to        |             |             |
|             |             | > sections  |             |             |
|             |             | > 7.4.3,    |             |             |
|             |             | > 7.5.3 and |             |             |
|             |             | > 7.6.2.    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 5.1       | > 26 Nov    | > Minor CR  | > TADIG #68 | > Christer\ |
|             | > 2009      | > 066\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 68_036).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Editorial |             |             |
|             |             | >           |             |             |
|             |             | corrections |             |             |
|             |             | > to the    |             |             |
|             |             | > Annex.    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.0       | > 24 Jun    | > Major CRs | > TADIG #69 | > Christer\ |
|             | > 2010      | > 067 and   | > EMC #84   | >           |
|             |             | > 068\      |             |  Gullstrand |
|             |             | > (TADIG    |             | > /         |
|             |             | > Docs      |             | > Syniverse |
|             |             | > 69_011    |             |             |
|             |             | > and       |             |             |
|             |             | > 69_012).  |             |             |
|             |             | > RAP1.5,   |             |             |
|             |             | > effective |             |             |
|             |             | > 1 May     |             |             |
|             |             | > 2011.     |             |             |
|             |             | >           |             |             |
|             |             | > Mandatory |             |             |
|             |             | > OSI for   |             |             |
|             |             | > IOT       |             |             |
|             |             | > Errors.   |             |             |
|             |             | >           |             |             |
|             |             | > TAP File  |             |             |
|             |             | > Stream    |             |             |
|             |             | > Stopped   |             |             |
|             |             | > Error.    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.1       | > 11 Jan    | > Editorial | > N/A       | > Christer\ |
|             | > 2011      | >           |             | >           |
|             |             |  Correction |             |  Gullstrand |
|             |             | > of name   |             | > /         |
|             |             | > of ASN.1  |             | > Syniverse |
|             |             | > syntax    |             |             |
|             |             | > from      |             |             |
|             |             | > RAP-0104  |             |             |
|             |             | > to        |             |             |
|             |             | > RAP-0105. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.2       | > 24 Feb    | > Minor CR  | TADIG eVote | > Christer\ |
|             | > 2011      | > 069\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 71_008).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Adding    |             |             |
|             |             | > Stop      |             |             |
|             |             | > Return to |             |             |
|             |             | > a few     |             |             |
|             |             | > data      |             |             |
|             |             | >           |             |             |
|             |             |  dictionary |             |             |
|             |             | > entries   |             |             |
|             |             | > where it  |             |             |
|             |             | > was       |             |             |
|             |             | >           |             |             |
|             |             |  previously |             |             |
|             |             | > missing.  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.3       | 2 Jun 2011  | > Minor CR  | > TADIG #71 | > Christer\ |
|             |             | > 070\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 71_047).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Cla       |             |             |
|             |             | rifications |             |             |
|             |             | > to OSI    |             |             |
|             |             | > (Annex    |             |             |
|             |             | > 1).       |             |             |
|             |             | >           |             |             |
|             |             | > Imp       |             |             |
|             |             | lementation |             |             |
|             |             | > of new    |             |             |
|             |             | > GSMA PRD  |             |             |
|             |             | > template. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.4       | 2 Sep 2011  | > Minor CR  | TADIG eVote | > Christer\ |
|             |             | > 071\      |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 72_011).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Cla       |             |             |
|             |             | rifications |             |             |
|             |             | > to OSI    |             |             |
|             |             | > date and  |             |             |
|             |             | > charge    |             |             |
|             |             | > format    |             |             |
|             |             | > (Annex    |             |             |
|             |             | > 1).       |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.5       | 26 Oct      | > Major CR  | TADIG eVote | > Christer  |
|             |             | > 072       |             |             |
+-------------+-------------+-------------+-------------+-------------+

> V6.11 Page 45 of 46

+-----------------------------------+-----------------------------------+
| > GSM Association                 | > Confidential - Full,            |
|                                   | > Rapporteur, and Associate       |
|                                   | > Members                         |
+===================================+===================================+
| > Official Document TD.32 - RAP   |                                   |
| > Format Specification            |                                   |
+-----------------------------------+-----------------------------------+

+-------------+-------------+-------------+-------------+-------------+
| **Version** | > **Date**  | > **Brief   | **Approval  | > **Editor  |
|             |             | >           | Authority** | > /**\      |
|             |             | Description |             | >           |
|             |             | > of        |             | **Company** |
|             |             | > Change**  |             |             |
+=============+=============+=============+=============+=============+
|             | > 2011      | > (TADIG    | > EMC #97   | >           |
|             |             | > Doc       |             |  Gullstrand |
|             |             | > 72_012).  |             | > /         |
|             |             | >           |             | > Syniverse |
|             |             | > Stop      |             |             |
|             |             | > returns   |             |             |
|             |             | > are only  |             |             |
|             |             | > raised    |             |             |
|             |             | > when at   |             |             |
|             |             | > least one |             |             |
|             |             | > CD file   |             |             |
|             |             | > has been  |             |             |
|             |             | > received  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.6       | > 15 Dec    | > Minor CRs | > TADIG #72 | > Christer\ |
|             | > 2011      | > 073 -     |             | >           |
|             |             | > 076\      |             |  Gullstrand |
|             |             | > (TADIG    |             | > /         |
|             |             | > Docs      |             | > Syniverse |
|             |             | > 72_023 -- |             |             |
|             |             | > 72_026).  |             |             |
|             |             | >           |             |             |
|             |             | > Cl        |             |             |
|             |             | arification |             |             |
|             |             | > on global |             |             |
|             |             | > errors    |             |             |
|             |             | > without   |             |             |
|             |             | > data      |             |             |
|             |             | > items and |             |             |
|             |             | > on Last   |             |             |
|             |             | > Sequence  |             |             |
|             |             | > Number in |             |             |
|             |             | > Stop      |             |             |
|             |             | > Return.   |             |             |
|             |             | >           |             |             |
|             |             | > OSI       |             |             |
|             |             | >           |             |             |
|             |             | Information |             |             |
|             |             | > for IOT   |             |             |
|             |             | > Related   |             |             |
|             |             | > V         |             |             |
|             |             | alidations. |             |             |
|             |             | >           |             |             |
|             |             | > Removal   |             |             |
|             |             | > of RAP    |             |             |
|             |             | >           |             |             |
|             |             |  scenarios. |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.7       | > 15 Mar    | > Minor CR  | TADIG eVote | > Christer\ |
|             | > 2012      | > 077       |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 73_010).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > Annex 1:  |             |             |
|             |             | > Removal   |             |             |
|             |             | > of        |             |             |
|             |             | >           |             |             |
|             |             |  validation |             |             |
|             |             | > rule in   |             |             |
|             |             | > line with |             |             |
|             |             | > TD.57     |             |             |
|             |             | > ‎\[6\].    |             |             |
|             |             | >           |             |             |
|             |             | > New Annex |             |             |
|             |             | > 3:        |             |             |
|             |             | > Minimum   |             |             |
|             |             | > content   |             |             |
|             |             | > of RAP    |             |             |
|             |             | > disputes  |             |             |
|             |             | > and       |             |             |
|             |             | > denials   |             |             |
|             |             | > moved     |             |             |
|             |             | > from      |             |             |
|             |             | > BA.13     |             |             |
|             |             | > ‎\[3\].    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.8       | > 30 Mar    | > Editorial | > N/A       | > Christer\ |
|             | > 2012      | > change:   |             | >           |
|             |             | > Added a   |             |  Gullstrand |
|             |             | > note to   |             | > /         |
|             |             | > the end   |             | > Syniverse |
|             |             | > of Annex  |             |             |
|             |             | > 3. The    |             |             |
|             |             | > note was  |             |             |
|             |             | > lost by   |             |             |
|             |             | > mistake   |             |             |
|             |             | > when      |             |             |
|             |             | > moving    |             |             |
|             |             | > the text  |             |             |
|             |             | > from      |             |             |
|             |             | > BA.13     |             |             |
|             |             | > ‎\[3\].    |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.8       | > 13 Nov    | > Editorial | > N/A       | > Christer\ |
|             | > 2012      | > change:   |             | >           |
|             |             | > New GSMA  |             |  Gullstrand |
|             |             | > template. |             | > /         |
|             |             |             |             | > Syniverse |
+-------------+-------------+-------------+-------------+-------------+
| > 6.9       | > 22 Nov    | > Minor CR  | > TADIG #74 | > Christer\ |
|             | > 2012      | > 078       |             | >           |
|             |             | > (TADIG    |             |  Gullstrand |
|             |             | > Doc       |             | > /         |
|             |             | > 74_011).  |             | > Syniverse |
|             |             | >           |             |             |
|             |             | > New       |             |             |
|             |             | > section   |             |             |
|             |             | > 2.4 on    |             |             |
|             |             | > Public    |             |             |
|             |             | > interface |             |             |
|             |             | > within    |             |             |
|             |             | > one DCH.  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.10      | > 23 May    | > Minor CR  | > TADIG #75 | > Christer\ |
|             | > 2013      | > 1001.     |             | >           |
|             |             | >           |             |  Gullstrand |
|             |             | > Error     |             | > /         |
|             |             | >           |             | > Syniverse |
|             |             | corrections |             |             |
|             |             | > and       |             |             |
|             |             | > cla       |             |             |
|             |             | rifications |             |             |
|             |             | > on Annex  |             |             |
|             |             | > A IOT     |             |             |
|             |             | > related   |             |             |
|             |             | > errors.   |             |             |
+-------------+-------------+-------------+-------------+-------------+
| > 6.11      | 5 Dec 2013  | > Major CR  | > TADIG #76 | > Christer\ |
|             |             | > 1002.     |             | >           |
|             |             | >           |             |  Gullstrand |
|             |             | > RAP       |             | > /         |
|             |             | > release   |             | > Syniverse |
|             |             | >           |             |             |
|             |             | management. |             |             |
+-------------+-------------+-------------+-------------+-------------+

> **Other Information**

+-----------------------------------+-----------------------------------+
| > **Type**                        | > **Description**                 |
+===================================+===================================+
| > Document Owner                  | > TADIG                           |
+-----------------------------------+-----------------------------------+
| > Editor / Company                | > Christer Gullstrand / Syniverse |
+-----------------------------------+-----------------------------------+

> It is our intention to provide a quality product for your use. If you
> find any errors or omissions, please contact us with your comments.
> You may notify us at
>
> Your comments or suggestions & questions are always welc
>
> V6.11 Page 46 of 46
