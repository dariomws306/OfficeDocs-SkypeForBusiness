---
title: 'Lync Server 2013: Certificate summary - Scaled consolidated edge, DNS load balancing with private IP addresses using NAT'
description: "Lync Server 2013: Certificate summary - Scaled consolidated edge, DNS load balancing with private IP addresses using NAT."
ms.reviewer: 
ms.author: v-lanac
author: lanachin
f1.keywords:
- NOCSH
TOCTitle: Certificate summary - Scaled consolidated edge, DNS load balancing with private IP addresses using NAT
ms:assetid: 41677dbd-3d07-498a-8591-df255b606647
ms:mtpsurl: https://technet.microsoft.com/library/Gg425921(v=OCS.15)
ms:contentKeyID: 48183959
ms.date: 07/23/2014
manager: serdars
mtps_version: v=OCS.15
---

# Certificate summary - Scaled consolidated edge, DNS load balancing with private IP addresses using NAT in Lync Server 2013

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="https://msdn.microsoft.com/">

<div data-asp="https://msdn2.microsoft.com/asp">



</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2012-09-08_

Microsoft Lync Server 2013 uses certificates to mutually authenticate other servers and to encrypt data from server to server and server to client. Certificates require name matching of the domain name system (DNS) records associated with the servers and the subject name (SN) and subject alternative name (SAN) on the certificate. To successfully map servers, DNS records and certificate entries, you must carefully plan your intended server fully qualified domain names as registered in DNS and the SN and SAN entries on the certificate.

The certificate assigned to the external interfaces of the Edge Server is requested from a public certification authority (CA). Public CAs that have demonstrated success in supplying certificates for the purposes of Unified Communications are listed in the following article: [https://go.microsoft.com/fwlink/p/?linkid=3052\&kbid=929395](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=929395) When requesting the certificate, you can use the certificate request generated by the Lync Server Deployment Wizard or create the request manually or by a process provided by the public CA. When assigning the certificate, the certificate is assigned to the Access Edge service interface, the Web Conferencing Edge service interface, and the Audio/Video Authentication service. The Audio/Video Authentication service should not be confused with the A/V Edge service which does not use a certificate to encrypt the audio and video streams. The internal Edge Server interface can use a certificate from an internal (to your organization) CA or a certificate from a public CA. The internal interface certificate uses only the SN and does not need or use SAN entries.

<div>


> [!NOTE]  
> The following table shows a second SIP entry (sip.fabrikam.com) in the subject alternative name list for reference. For each SIP domain in your organization, you need to add a corresponding FQDN listed in the certificate subject alternative name list.



</div>

<div>

## Scaled Consolidated Edge, DNS Load Balancing with Private IP Addresses Using NAT


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>Subject name (SN)</th>
<th>Subject alternative names (SAN)/Order</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Scaled consolidated Edge (External Edge)</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Certificate must be from a Public CA, and must have the server EKU and client EKU if public IM connectivity with AOL is to be deployed. Additionally, for scaled Edge Servers, the certificate private key must be exportable and the certificate and private key copied to each Edge Server. The certificate is assigned to the external Edge interfaces for:</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
</ul>
<p>Note that SANs are automatically added to the certificate based on your definitions in Topology Builder. You add SAN entries as needed for additional SIP domains and other entries that you need to support. The subject name is replicated in the SAN and must be present for correct operation.</p></td>
</tr>
<tr class="even">
<td><p>Scaled consolidated Edge (Internal Edge)</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>No SAN required</p></td>
<td><p>Certificate can be issued by a public or private CA, and must contain the server EKU. The certificate is assigned to the internal Edge interface.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Certificate Summary – Public Instant Messaging Connectivity


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>Subject name</th>
<th>Subject alternative names (SAN)/Order</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>External/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Certificate must be from a Public CA, and must have the server EKU and client EKU if public IM connectivity with AOL is to be deployed. The certificate is assigned to the external Edge interfaces for:</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
</ul>
<p>Note that SANs are automatically added to the certificate based on your definitions in Topology Builder. You add SAN entries as needed for additional SIP domains and other entries that you need to support. The subject name is replicated in the SAN and must be present for correct operation.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Certificate Summary for Extensible Messaging and Presence Protocol


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>Subject name</th>
<th>Subject alternative names (SAN)/Order</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Assign to Access Edge service of Edge Server or Edge pool</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>xmpp.contoso.com</p>
<p><strong>*.contoso.com</strong></p></td>
<td><p>The first three SAN entries are the normal SAN entries for a full Edge Server. The contoso.com is the entry required for federation with the XMPP partner at the root domain level. This entry will allow XMPP for all domains with the suffix *.contoso.com.</p></td>
</tr>
</tbody>
</table>


</div>

</div>

<span> </span>

</div>

</div>

</div>
