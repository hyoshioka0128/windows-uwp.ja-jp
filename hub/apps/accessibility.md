---
title: Windows 10 のユーザー補助機能
description: このページは、アクセス可能な Windows アプリの開発を開始するための情報を提供します。
ms.topic: article
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.author: kbridge
author: Karl-Bridge-Microsoft
keywords: Windows 10、アクセシビリティ、アクセシビリティを備えた WinForms アプリを構築、アクセスの WPF アプリの構築、アクセスの UWP アプリの構築、アクセス可能な win32 アプリの構築のユーザー補助機能
ms.openlocfilehash: b818b99ebf896b2d2de219d2eedbfd101f3a5caa
ms.sourcegitcommit: d1c3e13de3da3f7dce878b3735ee53765d0df240
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66214993"
---
# <a name="accessibility-in-windows-10"></a>Windows 10 のユーザー補助機能

![hero-accessibility-bar-smaller.png](images/hero-accessibility-bar-smaller.png)

多くの人の (運転料理、まぶしく、やなどの) 状況、または可能であれば、障害、個人的な好み、特定の作業スタイルでは、これらの制約として使いやすさを向上し、包括的には、アクセシビリティ対応アプリが設計されています。

このページは、さまざまな Windows 開発フレームワークが、スクリーン リーダーと情報を読み上げたり、ソフトウェア テストなどのツールを構築する開発者を支援技術である Windows アプリケーションを構築する開発者のユーザー補助をサポートする方法の情報を提供しますエンジニアはアプリケーションのテストの自動化されたスクリプトを作成します。

## <a name="platform-specific-documentation"></a>プラットフォーム固有ドキュメント

:::row:::
    :::column:::
        ![Universal Windows Platform (UWP)](images/platform-uwp.png)

        ### Universal Windows Platform (UWP)

        Develop accessible apps and tools on the modern platform for Windows 10 applications and games on any Windows device (including PCs, phones, Xbox One, HoloLens, and more), and publish them to the Microsoft Store.

        [Designing inclusive software](https://docs.microsoft.com/windows/uwp/accessibility/designing-inclusive-software)

        [Developing inclusive Windows apps](https://docs.microsoft.com/windows/uwp/accessibility/developing-inclusive-windows-apps)

        [Accessibility testing](https://docs.microsoft.com/windows/uwp/accessibility/accessibility-testing)

        [Accessibility in the Store](https://docs.microsoft.com/windows/uwp/accessibility/accessibility-in-the-store)
    :::column-end:::
    :::column:::
        ![Win32 platform apps](images/platform-win32.png)

        ### Win32 platform

        Develop accessible apps and tools on the original platform for C/C++ Windows applications.

        [What's new in Windows accessibility and automation](https://docs.microsoft.com/windows/desktop/accessibility-whatsnew)

        [Developing accessible applications for Windows](https://docs.microsoft.com/windows/desktop/accessibility-appdev)

        [Developing accessible UI frameworks for Windows](https://docs.microsoft.com/windows/desktop/accessibility-uiframeworkdev)

        [Developing assistive technology for Windows](https://docs.microsoft.com/windows/desktop/accessibility-atdev)

        [Testing for accessibility](https://docs.microsoft.com/windows/desktop/accessibility-testwithuia)

        [Legacy accessibility and automation technology - MSAA to UI Automation](https://docs.microsoft.com/windows/desktop/accessibility-legacy)

        [Windows Accessibility features](https://docs.microsoft.com/windows/desktop/winauto/about-windows-accessibility-features)

        [Guidelines for designing accessible apps](https://docs.microsoft.com/windows/desktop/uxguide/inter-accessibility)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ![WPF platform](images/platform-wpf.png)

        ### Windows Presentation Foundation (WPF)

        Develop accessible apps and tools on the established platform for managed Windows applications with a XAML UI model and the .NET Framework.

        [Accessibility Best Practices](https://docs.microsoft.com/dotnet/framework/ui-automation/accessibility-best-practices)

        [UI Automation Fundamentals](https://docs.microsoft.com/dotnet/framework/ui-automation/index)

        [UI Automation Providers for Managed Code](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-providers-for-managed-code)

        [UI Automation Clients for Managed Code](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-clients-for-managed-code)

        [UI Automation Control Patterns](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-control-patterns)

        [UI Automation Text Pattern](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-text-pattern)

        [UI Automation Control Types](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-control-types)

        [UI Automation Specification and Community Promise](https://docs.microsoft.com/dotnet/framework/ui-automation/ui-automation-specification-and-community-promise)
        :::column-end:::
    :::column:::
        ![Windows Forms platform apps](images/platform-winforms.png)

        ### Windows Forms (WinForms)

        Develop accessible apps and tools for managed Windows applications with a XAML UI model and the .NET Framework.

        [Windows Forms Accessibility](https://docs.microsoft.com/dotnet/framework/winforms/advanced/windows-forms-accessibility)

        [Creating an Accessible Windows Application](https://docs.microsoft.com/dotnet/framework/winforms/advanced/walkthrough-creating-an-accessible-windows-based-application)

        [Properties on Windows Forms Controls That Support Accessibility Guidelines](https://docs.microsoft.com/dotnet/framework/winforms/advanced/properties-on-windows-forms-controls-that-support-accessibility-guidelines)

        [Providing Accessibility Information for Controls on a Windows Form](https://docs.microsoft.com/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)
    :::column-end:::
<!--         
    :::column:::
![.NET platform](images/platform-dotnet.png)

        ### .NET

        Develop accessible apps and tools for managed Windows applications with the .NET Framework.
    :::column-end:::
    :::column:::

    :::column-end:::
 -->    
:::row-end:::