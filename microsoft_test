---
layout: Conceptual
title: TLS version supported by Azure Resource Manager - Azure Resource Manager | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tls-support
breadcrumb_path: /azure/bread/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/133/azure
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/9a0ece70-ff24-ec11-b6e6-000d3a4f07b8
feedback_system: Standard
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
author: Xelu86
learn_banner_products:
- azure
ms.author: jgao
ms.update-cycle: 365-days
ms.service: azure-resource-manager
ms.subservice: management
description: Describes the deprecation of TLS versions prior to 1.2 in Azure Resource Manager
ms.topic: article
ms.custom: devx-track-arm-template
ms.date: 2025-09-15T00:00:00.0000000Z
locale: en-us
document_id: 3aa65838-922f-ab99-9604-1c8d592f875d
document_version_independent_id: 3a6032ca-8315-c04f-168d-bfc4cd09ddb7
updated_at: 2025-12-08T23:11:00.0000000Z
original_content_git_url: https://github.com/MicrosoftDocs/azure-docs-pr/blob/live/articles/azure-resource-manager/management/tls-support.md
gitcommit: https://github.com/MicrosoftDocs/azure-docs-pr/blob/9c4dbd21839b2c6c7fe76655efc0608af6135fe8/articles/azure-resource-manager/management/tls-support.md
git_commit_id: 9c4dbd21839b2c6c7fe76655efc0608af6135fe8
site_name: Docs
depot_name: Azure.azure-documents
page_type: conceptual
toc_rel: toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/Azure.azure-documents/{branchName}{pdfName}
word_count: 609
asset_id: azure-resource-manager/management/tls-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: articles/azure-resource-manager/management/tls-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c5681ea0-e06d-d2e6-337a-e9fdcddf43a1
---

# TLS version supported by Azure Resource Manager - Azure Resource Manager | Microsoft Learn

Transport Layer Security (TLS) is a security protocol that establishes encryption channels over computer networks. TLS 1.2 is the current industry standard and is supported by Azure Resource Manager. For backwards compatibility, Azure Resource Manager also supports earlier versions, such as TLS 1.0 and 1.1, but that support is ending.

To ensure that Azure is compliant with regulatory requirements, and provide improved security for our customers, **Azure Resource Manager will stop supporting protocols older than TLS 1.2 on March 1, 2025.**

This article provides guidance for removing dependencies on older security protocols.

## Why migrate to TLS 1.2

TLS encrypts data sent over the internet to prevent malicious users from accessing private, sensitive information. The client and server perform a TLS handshake to verify each other's identity and determine how they'll communicate. During the handshake, each party identifies which TLS versions they use. The client and server can communicate if they both support a common version.

TLS 1.2 is more secure and faster than its predecessors.

Azure Resource Manager is the deployment and management service for Azure. You use Azure Resource Manager to create, update, and delete resources in your Azure account. To strengthen security and mitigate against any future protocol downgrade attacks, Azure Resource Manager will no longer support TLS 1.1 or earlier. To continue using Azure Resource Manager, make sure all of your clients that call Azure use TLS 1.2 or later.

## Prepare for migration to TLS 1.2

We recommend the following steps as you prepare to migrate your clients to TLS 1.2:

- Update your operating system to the latest version.
- Update your development libraries and frameworks to their latest versions. For example, Python 3.8 supports TLS 1.2.
- Fix hardcoded instances of security protocols older than TLS 1.2.
- Notify your customers and partners of your product or service's migration to TLS 1.2.

For a more detailed guidance, see the [checklist to deprecate older TLS versions](/en-us/security/engineering/solving-tls1-problem#figure-1-security-protocol-support-by-os-version) in your environment.

## Quick tips

- Windows 8+ has TLS 1.2 enabled by default.
- Windows Server 2016+ has TLS 1.2 enabled by default.
- When possible, avoid hardcoding the protocol version. Instead, configure your applications to always defer to your operating system's default TLS version.

    For example, you can enable the `SystemDefaultTLSVersion` flag in .NET Framework applications to defer to your operating system's default version. This approach lets your applications take advantage of future TLS versions.

    If you can't avoid hardcoding, specify TLS 1.2.
- Upgrade applications that target .NET Framework 4.5 or earlier. Instead, use .NET Framework 4.7 or later because these versions support TLS 1.2.

    For example, Visual Studio 2013 doesn't support TLS 1.2. Instead, use at least the latest release of Visual Studio 2017.
- You can use [Qualys SSL Labs](https://www.ssllabs.com/) to identify which TLS version is requested by clients connecting to your application.
- You can use [Fiddler](https://www.telerik.com/fiddler) to identify which TLS version your client uses when you send out HTTPS requests.
