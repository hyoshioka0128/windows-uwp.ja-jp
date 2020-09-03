---
title: Windows 10 バージョン 1607 API の変更点
description: 開発者は、次の一覧を使用して、Windows 10 バージョン 1607 での新しいまたは変更された名前空間を確認することができます。
keywords: Windows 10, 1607, 14393, API
ms.date: 11/02/2017
ms.topic: article
ms.assetid: 40335c70-46cc-40fd-9fe0-3cc8e6200482
ms.localizationpriority: medium
ms.openlocfilehash: e22f3e8ecce80cc65837289fe2c3d29ff2fb5cb2
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167136"
---
# <a name="new-apis-in-windows-10-build-14393"></a>Windows 10 ビルド 14393 の新しい API

Windows 10 ビルド 14393 (Anniversary Update またはバージョン 1607 とも呼ばれます) には、新規および更新された API 名前空間が開発者用に用意されています。 次の表に、このリリースで追加または変更されている名前空間を示します。


**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedChildItem](/uwp/api/windows.applicationmodel.socialinfo.socialfeedchilditem)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedChildItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.#ctor <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.Author <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.PrimaryContent <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.SecondaryContent <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.SharedItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.Thumbnails <br /> Windows.ApplicationModel.SocialInfo.SocialFeedChildItem.Timestamp
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedContent](/uwp/api/windows.applicationmodel.socialinfo.socialfeedcontent)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedContent <br /> Windows.ApplicationModel.SocialInfo.SocialFeedContent.Message <br /> Windows.ApplicationModel.SocialInfo.SocialFeedContent.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialFeedContent.Title
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedItem](/uwp/api/windows.applicationmodel.socialinfo.socialfeeditem)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.#ctor <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.Author <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.BadgeCountValue <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.BadgeStyle <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.ChildItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.PrimaryContent <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.RemoteId <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.SecondaryContent <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.SharedItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.Style <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.Thumbnails <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItem.Timestamp
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedItemStyle](/uwp/api/windows.applicationmodel.socialinfo.socialfeeditemstyle)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedItemStyle <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItemStyle.Default <br /> Windows.ApplicationModel.SocialInfo.SocialFeedItemStyle.Photo
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedKind](/uwp/api/windows.applicationmodel.socialinfo.socialfeedkind)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedKind <br /> Windows.ApplicationModel.SocialInfo.SocialFeedKind.ContactFeed <br /> Windows.ApplicationModel.SocialInfo.SocialFeedKind.Dashboard <br /> Windows.ApplicationModel.SocialInfo.SocialFeedKind.HomeFeed
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem](/uwp/api/windows.applicationmodel.socialinfo.socialfeedshareditem)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.#ctor <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.Content <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.OriginalSource <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.Thumbnail <br /> Windows.ApplicationModel.SocialInfo.SocialFeedSharedItem.Timestamp
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialFeedUpdateMode](/uwp/api/windows.applicationmodel.socialinfo.socialfeedupdatemode)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialFeedUpdateMode <br /> Windows.ApplicationModel.SocialInfo.SocialFeedUpdateMode.Append <br /> Windows.ApplicationModel.SocialInfo.SocialFeedUpdateMode.Replace
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialItemBadgeStyle](/uwp/api/windows.applicationmodel.socialinfo.socialitembadgestyle)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialItemBadgeStyle <br /> Windows.ApplicationModel.SocialInfo.SocialItemBadgeStyle.Hidden <br /> Windows.ApplicationModel.SocialInfo.SocialItemBadgeStyle.Visible <br /> Windows.ApplicationModel.SocialInfo.SocialItemBadgeStyle.VisibleWithCount
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialItemThumbnail](/uwp/api/windows.applicationmodel.socialinfo.socialitemthumbnail)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialItemThumbnail <br /> Windows.ApplicationModel.SocialInfo.SocialItemThumbnail.#ctor <br /> Windows.ApplicationModel.SocialInfo.SocialItemThumbnail.BitmapSize <br /> Windows.ApplicationModel.SocialInfo.SocialItemThumbnail.ImageUri <br /> Windows.ApplicationModel.SocialInfo.SocialItemThumbnail.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialItemThumbnail.SetImageAsync(Windows.Storage.Streams.IInputStream)
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.SocialUserInfo](/uwp/api/windows.applicationmodel.socialinfo.socialuserinfo)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.SocialUserInfo <br /> Windows.ApplicationModel.SocialInfo.SocialUserInfo.DisplayName <br /> Windows.ApplicationModel.SocialInfo.SocialUserInfo.RemoteId <br /> Windows.ApplicationModel.SocialInfo.SocialUserInfo.TargetUri <br /> Windows.ApplicationModel.SocialInfo.SocialUserInfo.UserName
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater](/uwp/api/windows.applicationmodel.socialinfo.provider.socialdashboarditemupdater)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.Content <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.OwnerRemoteId <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.TargetUri <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.Thumbnail <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.Timestamp <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialDashboardItemUpdater.CommitAsync
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater](/uwp/api/windows.applicationmodel.socialinfo.provider.socialfeedupdater)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater.Items <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater.Kind <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater.OwnerRemoteId <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialFeedUpdater.CommitAsync
<hr>

**項目**

[Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager](/uwp/api/windows.applicationmodel.socialinfo.provider.socialinfoprovidermanager)

**[プロパティ]**


Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.CreateDashboardItemUpdaterAsync(System.String) <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.CreateSocialFeedUpdaterAsync(Windows.ApplicationModel.SocialInfo.SocialFeedKind,Windows.ApplicationModel.SocialInfo.SocialFeedUpdateMode,System.String) <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.DeprovisionAsync <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.ProvisionAsync <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.ReportNewContentAvailable(System.String,Windows.ApplicationModel.SocialInfo.SocialFeedKind) <br /> Windows.ApplicationModel.SocialInfo.Provider.SocialInfoProviderManager.UpdateBadgeCountValue(System.String,System.Int32)
<hr>

**項目**

[Windows.ApplicationModel.StartupTask](/uwp/api/windows.applicationmodel.startuptask)

**[プロパティ]**


Windows.ApplicationModel.StartupTask <br /> Windows.ApplicationModel.StartupTask.State <br /> Windows.ApplicationModel.StartupTask.TaskId <br /> Windows.ApplicationModel.StartupTask.Disable <br /> Windows.ApplicationModel.StartupTask.GetAsync(System.String) <br /> Windows.ApplicationModel.StartupTask.GetForCurrentPackageAsync <br /> Windows.ApplicationModel.StartupTask.RequestEnableAsync
<hr>

**項目**

[Windows.ApplicationModel.StartupTaskState](/uwp/api/windows.applicationmodel.startuptaskstate)

**[プロパティ]**


Windows.ApplicationModel.StartupTaskState <br /> Windows.ApplicationModel.StartupTaskState.Disabled <br /> Windows.ApplicationModel.StartupTaskState.DisabledByUser <br /> Windows.ApplicationModel.StartupTaskState.Enabled
<hr>

**項目**

[Windows.ApplicationModel.EnteredBackgroundEventArgs](/uwp/api/windows.applicationmodel.enteredbackgroundeventargs)

**[プロパティ]**


Windows.ApplicationModel.EnteredBackgroundEventArgs <br /> Windows.ApplicationModel.EnteredBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.IEnteredBackgroundEventArgs](/uwp/api/windows.applicationmodel.ienteredbackgroundeventargs)

**[プロパティ]**


Windows.ApplicationModel.IEnteredBackgroundEventArgs <br /> Windows.ApplicationModel.IEnteredBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.ILeavingBackgroundEventArgs](/uwp/api/windows.applicationmodel.ileavingbackgroundeventargs)

**[プロパティ]**


Windows.ApplicationModel.ILeavingBackgroundEventArgs <br /> Windows.ApplicationModel.ILeavingBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.LeavingBackgroundEventArgs](/uwp/api/windows.applicationmodel.leavingbackgroundeventargs)

**[プロパティ]**


Windows.ApplicationModel.LeavingBackgroundEventArgs <br /> Windows.ApplicationModel.LeavingBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.PackageCatalog](/uwp/api/windows.applicationmodel.packagecatalog)

**[プロパティ]**


Windows.ApplicationModel.PackageCatalog <br /> Windows.ApplicationModel.PackageCatalog.PackageInstalling <br /> Windows.ApplicationModel.PackageCatalog.PackageStaging <br /> Windows.ApplicationModel.PackageCatalog.PackageStatusChanged <br /> Windows.ApplicationModel.PackageCatalog.PackageUninstalling <br /> Windows.ApplicationModel.PackageCatalog.PackageUpdating <br /> Windows.ApplicationModel.PackageCatalog.OpenForCurrentPackage <br /> Windows.ApplicationModel.PackageCatalog.OpenForCurrentUser
<hr>

**項目**

[Windows.ApplicationModel.ackageInstallingEventArgs](/uwp/api/windows.applicationmodel.packageinstallingeventargs)

**[プロパティ]**


Windows.ApplicationModel.PackageInstallingEventArgs <br /> Windows.ApplicationModel.PackageInstallingEventArgs.ActivityId <br /> Windows.ApplicationModel.PackageInstallingEventArgs.ErrorCode <br /> Windows.ApplicationModel.PackageInstallingEventArgs.IsComplete <br /> Windows.ApplicationModel.PackageInstallingEventArgs.Package <br /> Windows.ApplicationModel.PackageInstallingEventArgs.Progress
<hr>

**項目**

[Windows.ApplicationModel.PackageSignatureKind](/uwp/api/windows.applicationmodel.packagesignaturekind)

**[プロパティ]**


Windows.ApplicationModel.PackageSignatureKind <br /> Windows.ApplicationModel.PackageSignatureKind.Developer <br /> Windows.ApplicationModel.PackageSignatureKind.Enterprise <br /> Windows.ApplicationModel.PackageSignatureKind.None <br /> Windows.ApplicationModel.PackageSignatureKind.Store <br /> Windows.ApplicationModel.PackageSignatureKind.System
<hr>

**項目**

[Windows.ApplicationModel.PackageStagingEventArgs](/uwp/api/windows.applicationmodel.packagestagingeventargs)

**[プロパティ]**


Windows.ApplicationModel.PackageStagingEventArgs <br /> Windows.ApplicationModel.PackageStagingEventArgs.ActivityId <br /> Windows.ApplicationModel.PackageStagingEventArgs.ErrorCode <br /> Windows.ApplicationModel.PackageStagingEventArgs.IsComplete <br /> Windows.ApplicationModel.PackageStagingEventArgs.Package <br /> Windows.ApplicationModel.PackageStagingEventArgs.Progress
<hr>

**項目**

[Windows.ApplicationModel.PackageStatusChangedEventArgs](/uwp/api/windows.applicationmodel.packagestatuschangedeventargs)

**[プロパティ]**


Windows.ApplicationModel.PackageStatusChangedEventArgs <br /> Windows.ApplicationModel.PackageStatusChangedEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.PackageUninstallingEventArgs](/uwp/api/windows.applicationmodel.packageuninstallingeventargs)

**[プロパティ]**


Windows.ApplicationModel.PackageUninstallingEventArgs <br /> Windows.ApplicationModel.PackageUninstallingEventArgs.ActivityId <br /> Windows.ApplicationModel.PackageUninstallingEventArgs.ErrorCode <br /> Windows.ApplicationModel.PackageUninstallingEventArgs.IsComplete <br /> Windows.ApplicationModel.PackageUninstallingEventArgs.Package <br /> Windows.ApplicationModel.PackageUninstallingEventArgs.Progress
<hr>

**項目**

[Windows.ApplicationModel.PackageUpdatingEventArgs](/uwp/api/windows.applicationmodel.packageupdatingeventargs)

**[プロパティ]**


Windows.ApplicationModel.PackageUpdatingEventArgs <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.ActivityId <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.ErrorCode <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.IsComplete <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.Progress <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.SourcePackage <br /> Windows.ApplicationModel.PackageUpdatingEventArgs.TargetPackage
<hr>

**項目**

[Windows.ApplicationModel.Activation.BackgroundActivatedEventArgs](/uwp/api/windows.applicationmodel.activation.backgroundactivatedeventargs)

**[プロパティ]**


Windows.ApplicationModel.Activation.BackgroundActivatedEventArgs <br /> Windows.ApplicationModel.Activation.BackgroundActivatedEventArgs.TaskInstance
<hr>

**項目**

[Windows.ApplicationModel.Activation.IActivatedEventArgsWithUser](/uwp/api/windows.applicationmodel.activation.iactivatedeventargswithuser)

**[プロパティ]**


Windows.ApplicationModel.Activation.IActivatedEventArgsWithUser <br /> Windows.ApplicationModel.Activation.IActivatedEventArgsWithUser.User
<hr>

**項目**

[Windows.ApplicationModel.Activation.IBackgroundActivatedEventArgs](/uwp/api/windows.applicationmodel.activation.ibackgroundactivatedeventargs)

**[プロパティ]**


Windows.ApplicationModel.Activation.IBackgroundActivatedEventArgs <br /> Windows.ApplicationModel.Activation.IBackgroundActivatedEventArgs.TaskInstance
<hr>

**項目**

[Windows.ApplicationModel.Activation.ILaunchActivatedEventArgs2](/uwp/api/windows.applicationmodel.activation.ilaunchactivatedeventargs2)

**[プロパティ]**


Windows.ApplicationModel.Activation.ILaunchActivatedEventArgs2 <br /> Windows.ApplicationModel.Activation.ILaunchActivatedEventArgs2.TileActivatedInfo
<hr>

**項目**

[Windows.ApplicationModel.Activation.IUserDataAccountProviderActivatedEventArgs](/uwp/api/windows.applicationmodel.activation.iuserdataaccountprovideractivatedeventargs)

**[プロパティ]**


Windows.ApplicationModel.Activation.IUserDataAccountProviderActivatedEventArgs <br /> Windows.ApplicationModel.Activation.IUserDataAccountProviderActivatedEventArgs.Operation
<hr>

**項目**

[Windows.ApplicationModel.Activation.TileActivatedInfo](/uwp/api/windows.applicationmodel.activation.tileactivatedinfo)

**[プロパティ]**


Windows.ApplicationModel.Activation.TileActivatedInfo <br /> Windows.ApplicationModel.Activation.TileActivatedInfo.RecentlyShownNotifications
<hr>

**項目**

[Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs](/uwp/api/windows.applicationmodel.activation.userdataaccountprovideractivatedeventargs)

**[プロパティ]**


Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs <br /> Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs.Kind <br /> Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs.Operation <br /> Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs.PreviousExecutionState <br /> Windows.ApplicationModel.Activation.UserDataAccountProviderActivatedEventArgs.SplashScreen
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtension](/uwp/api/windows.applicationmodel.appextensions.appextension)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtension <br /> Windows.ApplicationModel.AppExtensions.AppExtension.AppInfo <br /> Windows.ApplicationModel.AppExtensions.AppExtension.Description <br /> Windows.ApplicationModel.AppExtensions.AppExtension.DisplayName <br /> Windows.ApplicationModel.AppExtensions.AppExtension.Id <br /> Windows.ApplicationModel.AppExtensions.AppExtension.Package <br /> Windows.ApplicationModel.AppExtensions.AppExtension.GetExtensionPropertiesAsync <br /> Windows.ApplicationModel.AppExtensions.AppExtension.GetPublicFolderAsync
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionCatalog](/uwp/api/windows.applicationmodel.appextensions.appextensioncatalog)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionCatalog <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.PackageInstalled <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.PackageStatusChanged <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.PackageUninstalling <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.PackageUpdated <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.PackageUpdating <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.FindAllAsync <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.Open(System.String) <br /> Windows.ApplicationModel.AppExtensions.AppExtensionCatalog.RequestRemovePackageAsync(System.String)
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionPackageInstalledEventArgs](/uwp/api/windows.applicationmodel.appextensions.appextensionpackageinstalledeventargs)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionPackageInstalledEventArgs <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageInstalledEventArgs.AppExtensionName <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageInstalledEventArgs.Extensions <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageInstalledEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionPackageStatusChangedEventArgs](/uwp/api/windows.applicationmodel.appextensions.appextensionpackagestatuschangedeventargs)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionPackageStatusChangedEventArgs <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageStatusChangedEventArgs.AppExtensionName <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageStatusChangedEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionPackageUninstallingEventArgs](/uwp/api/windows.applicationmodel.appextensions.appextensionpackageuninstallingeventargs)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionPackageUninstallingEventArgs <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUninstallingEventArgs.AppExtensionName <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUninstallingEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatedEventArgs](/uwp/api/windows.applicationmodel.appextensions.appextensionpackageupdatedeventargs)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatedEventArgs <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatedEventArgs.AppExtensionName <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatedEventArgs.Extensions <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatedEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatingEventArgs](/uwp/api/windows.applicationmodel.appextensions.appextensionpackageupdatingeventargs)

**[プロパティ]**


Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatingEventArgs <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatingEventArgs.AppExtensionName <br /> Windows.ApplicationModel.AppExtensions.AppExtensionPackageUpdatingEventArgs.Package
<hr>

**項目**

[Windows.ApplicationModel.Appointments.AppointmentManagerForUser](/uwp/api/windows.applicationmodel.appointments.appointmentmanagerforuser)

**[プロパティ]**


Windows.ApplicationModel.Appointments.AppointmentManagerForUser <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.User <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.RequestStoreAsync(Windows.ApplicationModel.Appointments.AppointmentStoreAccessType) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowAddAppointmentAsync(Windows.ApplicationModel.Appointments.Appointment,Windows.Foundation.Rect) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowAddAppointmentAsync(Windows.ApplicationModel.Appointments.Appointment,Windows.Foundation.Rect,Windows.UI.Popups.Placement) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowAppointmentDetailsAsync(System.String) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowAppointmentDetailsAsync(System.String,Windows.Foundation.DateTime) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowEditNewAppointmentAsync(Windows.ApplicationModel.Appointments.Appointment) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowRemoveAppointmentAsync(System.String,Windows.Foundation.Rect) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowRemoveAppointmentAsync(System.String,Windows.Foundation.Rect,Windows.UI.Popups.Placement) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowRemoveAppointmentAsync(System.String,Windows.Foundation.Rect,Windows.UI.Popups.Placement,Windows.Foundation.DateTime) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowReplaceAppointmentAsync(System.String,Windows.ApplicationModel.Appointments.Appointment,Windows.Foundation.Rect) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowReplaceAppointmentAsync(System.String,Windows.ApplicationModel.Appointments.Appointment,Windows.Foundation.Rect,Windows.UI.Popups.Placement) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowReplaceAppointmentAsync(System.String,Windows.ApplicationModel.Appointments.Appointment,Windows.Foundation.Rect,Windows.UI.Popups.Placement,Windows.Foundation.DateTime) <br /> Windows.ApplicationModel.Appointments.AppointmentManagerForUser.ShowTimeFrameAsync(Windows.Foundation.DateTime,Windows.Foundation.TimeSpan)
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarcancelmeetingrequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.AppointmentLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.AppointmentOriginalStartTime <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.Comment <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.NotifyInvitees <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.Subject <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarcancelmeetingrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCancelMeetingRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarcreateorupdateappointmentrequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.Appointment <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.ChangedProperties <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.NotifyInvitees <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.ReportCompletedAsync(Windows.ApplicationModel.Appointments.Appointment) <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarcreateorupdateappointmentrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarCreateOrUpdateAppointmentRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarforwardmeetingrequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.AppointmentLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.AppointmentOriginalStartTime <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.Comment <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.ForwardHeader <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.Invitees <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.Subject <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarforwardmeetingrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarForwardMeetingRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarproposenewtimeformeetingrequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.AppointmentLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.AppointmentOriginalStartTime <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.Comment <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.NewDuration <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.NewStartTime <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.Subject <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarproposenewtimeformeetingrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarProposeNewTimeForMeetingRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarsyncmanagersyncrequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarsyncmanagersyncrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarSyncManagerSyncRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarupdatemeetingresponserequest)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.AppointmentCalendarLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.AppointmentLocalId <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.AppointmentOriginalStartTime <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.Comment <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.Response <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.SendUpdate <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.Subject <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.</br>AppointmentCalendarUpdateMeetingResponseRequestEventArgs](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentcalendarupdatemeetingresponserequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequestEventArgs <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequestEventArgs.Request <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentCalendarUpdateMeetingResponseRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentdataproviderconnection)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.CancelMeetingRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.CreateOrUpdateAppointmentRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.ForwardMeetingRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.ProposeNewTimeForMeetingRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.SyncRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.UpdateMeetingResponseRequested <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderConnection.Start
<hr>

**項目**

[Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderTriggerDetails](/uwp/api/windows.applicationmodel.appointments.dataprovider.appointmentdataprovidertriggerdetails)

**[プロパティ]**


Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderTriggerDetails <br /> Windows.ApplicationModel.Appointments.DataProvider.AppointmentDataProviderTriggerDetails.Connection
<hr>

**項目**

[Windows.ApplicationModel.Background.IBackgroundTaskInstance4](/uwp/api/windows.applicationmodel.background.ibackgroundtaskinstance4)

**[プロパティ]**


Windows.ApplicationModel.Background.IBackgroundTaskInstance4 <br /> Windows.ApplicationModel.Background.IBackgroundTaskInstance4.User
<hr>

**項目**

[Windows.ApplicationModel.Background.SecondaryAuthenticationFactorAuthenticationTrigger](/uwp/api/windows.applicationmodel.background.secondaryauthenticationfactorauthenticationtrigger)

**[プロパティ]**


Windows.ApplicationModel.Background.SecondaryAuthenticationFactorAuthenticationTrigger <br /> Windows.ApplicationModel.Background.SecondaryAuthenticationFactorAuthenticationTrigger.#ctor
<hr>

**項目**

[Windows.ApplicationModel.Background.UserNotificationChangedTrigger](/uwp/api/windows.applicationmodel.background.usernotificationchangedtrigger)

**[プロパティ]**


Windows.ApplicationModel.Background.UserNotificationChangedTrigger <br /> Windows.ApplicationModel.Background.UserNotificationChangedTrigger.#ctor(Windows.UI.Notifications.NotificationKinds)
<hr>

**項目**

[Windows.ApplicationModel.Calls.PhoneCallHistoryManagerForUser](/uwp/api/windows.applicationmodel.calls.phonecallhistorymanagerforuser)

**[プロパティ]**


Windows.ApplicationModel.Calls.PhoneCallHistoryManagerForUser <br /> Windows.ApplicationModel.Calls.PhoneCallHistoryManagerForUser.User <br /> Windows.ApplicationModel.Calls.PhoneCallHistoryManagerForUser.RequestStoreAsync(Windows.ApplicationModel.Calls.PhoneCallHistoryStoreAccessType)
<hr>

**項目**

[Windows.ApplicationModel.Chat.ChatRestoreHistorySpan](/uwp/api/windows.applicationmodel.chat.chatrestorehistoryspan)

**[プロパティ]**


Windows.ApplicationModel.Chat.ChatRestoreHistorySpan <br /> Windows.ApplicationModel.Chat.ChatRestoreHistorySpan.AnyTime <br /> Windows.ApplicationModel.Chat.ChatRestoreHistorySpan.LastMonth <br /> Windows.ApplicationModel.Chat.ChatRestoreHistorySpan.LastYear
<hr>

**項目**

[Windows.ApplicationModel.Chat.ChatSyncConfiguration](/uwp/api/windows.applicationmodel.chat.chatsyncconfiguration)

**[プロパティ]**


Windows.ApplicationModel.Chat.ChatSyncConfiguration <br /> Windows.ApplicationModel.Chat.ChatSyncConfiguration.IsSyncEnabled <br /> Windows.ApplicationModel.Chat.ChatSyncConfiguration.RestoreHistorySpan
<hr>

**項目**

[Windows.ApplicationModel.Chat.ChatSyncManager](/uwp/api/windows.applicationmodel.chat.chatsyncmanager)

**[プロパティ]**


Windows.ApplicationModel.Chat.ChatSyncManager <br /> Windows.ApplicationModel.Chat.ChatSyncManager.Configuration <br /> Windows.ApplicationModel.Chat.ChatSyncManager.AssociateAccountAsync(Windows.Security.Credentials.WebAccount) <br /> Windows.ApplicationModel.Chat.ChatSyncManager.IsAccountAssociated(Windows.Security.Credentials.WebAccount) <br /> Windows.ApplicationModel.Chat.ChatSyncManager.SetConfigurationAsync(Windows.ApplicationModel.Chat.ChatSyncConfiguration) <br /> Windows.ApplicationModel.Chat.ChatSyncManager.StartSync <br /> Windows.ApplicationModel.Chat.ChatSyncManager.UnassociateAccountAsync
<hr>

**項目**

[Windows.ApplicationModel.Contacts.ContactListSyncConstraints](/uwp/api/windows.applicationmodel.contacts.contactlistsyncconstraints)

**[プロパティ]**


Windows.ApplicationModel.Contacts.ContactListSyncConstraints <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.CanSyncDescriptions <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxAnniversaryDates <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxAssistantPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxBirthdayDates <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxBusinessFaxPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxChildRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxCompanyPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxHomeAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxHomeFaxPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxHomePhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxJobInfo <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxMobilePhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxOtherAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxOtherDates <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxOtherEmailAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxOtherPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxOtherRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxPagerPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxParentRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxPartnerRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxPersonalEmailAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxRadioPhoneNumbers <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxSiblingRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxSpouseRelationships <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxWebsites <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxWorkAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxWorkEmailAddresses <br /> Windows.ApplicationModel.Contacts.ContactListSyncConstraints.MaxWorkPhoneNumbers
<hr>

**項目**

[Windows.ApplicationModel.Contacts.ContactManagerForUser](/uwp/api/windows.applicationmodel.contacts.contactmanagerforuser)

**[プロパティ]**


Windows.ApplicationModel.Contacts.ContactManagerForUser <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.SystemDisplayNameOrder <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.SystemSortOrder <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.User <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.ConvertContactToVCardAsync(Windows.ApplicationModel.Contacts.Contact) <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.ConvertContactToVCardAsync(Windows.ApplicationModel.Contacts.Contact,System.UInt32) <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.ConvertVCardToContactAsync(Windows.Storage.Streams.IRandomAccessStreamReference) <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.RequestAnnotationStoreAsync(Windows.ApplicationModel.Contacts.ContactAnnotationStoreAccessType) <br /> Windows.ApplicationModel.Contacts.ContactManagerForUser.RequestStoreAsync(Windows.ApplicationModel.Contacts.ContactStoreAccessType)
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderConnection](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactdataproviderconnection)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderConnection <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderConnection.ServerSearchReadBatchRequested <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderConnection.SyncRequested <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderConnection.Start
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderTriggerDetails](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactdataprovidertriggerdetails)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderTriggerDetails <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactDataProviderTriggerDetails.Connection
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactlistserversearchreadbatchrequest)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.ContactListId <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.Options <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.SessionId <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.SuggestedBatchSize <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.ReportFailedAsync(Windows.ApplicationModel.Contacts.ContactBatchStatus) <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequest.SaveContactAsync(Windows.ApplicationModel.Contacts.Contact)
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequestEventArgs](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactlistserversearchreadbatchrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequestEventArgs <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequestEventArgs.Request <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListServerSearchReadBatchRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequest](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactlistsyncmanagersyncrequest)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequest <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequest.ContactListId <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequestEventArgs](/uwp/api/windows.applicationmodel.contacts.dataprovider.contactlistsyncmanagersyncrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequestEventArgs <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequestEventArgs.Request <br /> Windows.ApplicationModel.Contacts.DataProvider.ContactListSyncManagerSyncRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.EmailManagerForUser](/uwp/api/windows.applicationmodel.email.emailmanagerforuser)

**[プロパティ]**


Windows.ApplicationModel.Email.EmailManagerForUser <br /> Windows.ApplicationModel.Email.EmailManagerForUser.User <br /> Windows.ApplicationModel.Email.EmailManagerForUser.RequestStoreAsync(Windows.ApplicationModel.Email.EmailStoreAccessType) <br /> Windows.ApplicationModel.Email.EmailManagerForUser.ShowComposeNewEmailAsync(Windows.ApplicationModel.Email.EmailMessage)
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection](/uwp/api/windows.applicationmodel.email.dataprovider.emaildataproviderconnection)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.CreateFolderRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.DeleteFolderRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.DownloadAttachmentRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.DownloadMessageRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.EmptyFolderRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.ForwardMeetingRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.GetAutoReplySettingsRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.MailboxSyncRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.MoveFolderRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.ProposeNewTimeForMeetingRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.ResolveRecipientsRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.ServerSearchReadBatchRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.SetAutoReplySettingsRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.UpdateMeetingResponseRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.ValidateCertificatesRequested <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderConnection.Start
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailDataProviderTriggerDetails](/uwp/api/windows.applicationmodel.email.dataprovider.emaildataprovidertriggerdetails)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailDataProviderTriggerDetails <br /> Windows.ApplicationModel.Email.DataProvider.EmailDataProviderTriggerDetails.Connection
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxcreatefolderrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest.Name <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest.ParentFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest.ReportCompletedAsync(Windows.ApplicationModel.Email.EmailFolder) <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequest.ReportFailedAsync(Windows.ApplicationModel.Email.EmailMailboxCreateFolderStatus)
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxcreatefolderrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxCreateFolderRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdeletefolderrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest.EmailFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequest.ReportFailedAsync(Windows.ApplicationModel.Email.EmailMailboxDeleteFolderStatus)
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdeletefolderrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDeleteFolderRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdownloadattachmentrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest.EmailAttachmentId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest.EmailMessageId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdownloadattachmentrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadAttachmentRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdownloadmessagerequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest.EmailMessageId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxdownloadmessagerequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxDownloadMessageRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxemptyfolderrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest.EmailFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequest.ReportFailedAsync(Windows.ApplicationModel.Email.EmailMailboxEmptyFolderStatus)
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxemptyfolderrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxEmptyFolderRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxforwardmeetingrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.Comment <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.EmailMessageId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.ForwardHeader <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.ForwardHeaderType <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.Recipients <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.Subject <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxforwardmeetingrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxForwardMeetingRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxgetautoreplysettingsrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest.RequestedFormat <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest.ReportCompletedAsync(Windows.ApplicationModel.Email.EmailMailboxAutoReplySettings) <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxgetautoreplysettingsrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxGetAutoReplySettingsRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxmovefolderrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.EmailFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.NewFolderName <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.NewParentFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxmovefolderrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxMoveFolderRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxproposenewtimeformeetingrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.Comment <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.EmailMessageId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.NewDuration <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.NewStartTime <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.Subject <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxproposenewtimeformeetingrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxProposeNewTimeForMeetingRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxresolverecipientsrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest.Recipients <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest.ReportCompletedAsync(Windows.Foundation.Collections.IIterable{Windows.ApplicationModel.Email.EmailRecipientResolutionResult}) <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxresolverecipientsrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxResolveRecipientsRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxserversearchreadbatchrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.EmailFolderId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.Options <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.SessionId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.SuggestedBatchSize <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.ReportFailedAsync(Windows.ApplicationModel.Email.EmailBatchStatus) <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequest.SaveMessageAsync(Windows.ApplicationModel.Email.EmailMessage)
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxserversearchreadbatchrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxServerSearchReadBatchRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxsetautoreplysettingsrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest.AutoReplySettings <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxsetautoreplysettingsrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSetAutoReplySettingsRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxsyncmanagersyncrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxsyncmanagersyncrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxSyncManagerSyncRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxupdatemeetingresponserequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.Comment <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.EmailMessageId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.Response <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.SendUpdate <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.Subject <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.ReportCompletedAsync <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxupdatemeetingresponserequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxUpdateMeetingResponseRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxvalidatecertificatesrequest)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest.Certificates <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest.EmailMailboxId <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest.ReportCompletedAsync(Windows.Foundation.Collections.IIterable{Windows.ApplicationModel.Email.EmailCertificateValidationStatus}) <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequest.ReportFailedAsync
<hr>

**項目**

[Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequestEventArgs](/uwp/api/windows.applicationmodel.email.dataprovider.emailmailboxvalidatecertificatesrequesteventargs)

**[プロパティ]**


Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequestEventArgs <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequestEventArgs.Request <br /> Windows.ApplicationModel.Email.DataProvider.EmailMailboxValidateCertificatesRequestEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.Store.LicenseManagement.LicenseManager](/uwp/api/windows.applicationmodel.store.licensemanagement.licensemanager)

**[プロパティ]**


Windows.ApplicationModel.Store.LicenseManagement.LicenseManager <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseManager.AddLicenseAsync(Windows.Storage.Streams.IBuffer) <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseManager.GetSatisfactionInfosAsync(Windows.Foundation.Collections.IIterable{System.String},Windows.Foundation.Collections.IIterable{System.String})
<hr>

**項目**

[Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo](/uwp/api/windows.applicationmodel.store.licensemanagement.licensesatisfactioninfo)

**[プロパティ]**


Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.IsSatisfied <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedByDevice <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedByInstallMedia <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedByOpenLicense <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedByPass <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedBySignedInUser <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionInfo.SatisfiedByTrial
<hr>

**項目**

[Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionResult](/uwp/api/windows.applicationmodel.store.licensemanagement.licensesatisfactionresult)

**[プロパティ]**


Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionResult <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionResult.ExtendedError <br /> Windows.ApplicationModel.Store.LicenseManagement.LicenseSatisfactionResult.LicenseSatisfactionInfos
<hr>

**項目**

[Windows.ApplicationModel.Store.Preview.StoreLogOptions](/uwp/api/windows.applicationmodel.store.preview.storelogoptions)

**[プロパティ]**


Windows.ApplicationModel.Store.Preview.StoreLogOptions <br /> Windows.ApplicationModel.Store.Preview.StoreLogOptions.None <br /> Windows.ApplicationModel.Store.Preview.StoreLogOptions.TryElevate
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.UserDataAccountManagerForUser](/uwp/api/windows.applicationmodel.userdataaccounts.userdataaccountmanagerforuser)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.UserDataAccountManagerForUser <br /> Windows.ApplicationModel.UserDataAccounts.UserDataAccountManagerForUser.User <br /> Windows.ApplicationModel.UserDataAccounts.UserDataAccountManagerForUser.RequestStoreAsync(Windows.ApplicationModel.UserDataAccounts.UserDataAccountStoreAccessType)
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.UserDataAccountStoreChangedEventArgs](/uwp/api/windows.applicationmodel.userdataaccounts.userdataaccountstorechangedeventargs)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.UserDataAccountStoreChangedEventArgs <br /> Windows.ApplicationModel.UserDataAccounts.UserDataAccountStoreChangedEventArgs.GetDeferral
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.IUserDataAccountProviderOperation](/uwp/api/windows.applicationmodel.userdataaccounts.provider.iuserdataaccountprovideroperation)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.IUserDataAccountProviderOperation <br /> Windows.ApplicationModel.UserDataAccounts.Provider.IUserDataAccountProviderOperation.Kind
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountPartnerAccountInfo](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountpartneraccountinfo)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountPartnerAccountInfo <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountPartnerAccountInfo.AccountKind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountPartnerAccountInfo.DisplayName <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountPartnerAccountInfo.Priority
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountprovideraddaccountoperation)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation.ContentKinds <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation.Kind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation.PartnerAccountInfos <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderAddAccountOperation.ReportCompleted(System.String)
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderOperationKind](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountprovideroperationkind)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderOperationKind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderOperationKind.AddAccount <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderOperationKind.ResolveErrors <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderOperationKind.Settings
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderPartnerAccountKind](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountproviderpartneraccountkind)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderPartnerAccountKind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderPartnerAccountKind.Exchange <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderPartnerAccountKind.PopOrImap
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderResolveErrorsOperation](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountproviderresolveerrorsoperation)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderResolveErrorsOperation <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderResolveErrorsOperation.Kind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderResolveErrorsOperation.UserDataAccountId <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderResolveErrorsOperation.ReportCompleted
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderSettingsOperation](/uwp/api/windows.applicationmodel.userdataaccounts.provider.userdataaccountprovidersettingsoperation)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderSettingsOperation <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderSettingsOperation.Kind <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderSettingsOperation.UserDataAccountId <br /> Windows.ApplicationModel.UserDataAccounts.Provider.UserDataAccountProviderSettingsOperation.ReportCompleted
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountAuthenticationType](/uwp/api/windows.applicationmodel.userdataaccounts.systemaccess.deviceaccountauthenticationtype)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountAuthenticationType <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountAuthenticationType.Basic <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountAuthenticationType.OAuth <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountAuthenticationType.SingleSignOn
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId](/uwp/api/windows.applicationmodel.userdataaccounts.systemaccess.deviceaccounticonid)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId.Exchange <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId.Generic <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId.Msa <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountIconId.Outlook
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter](/uwp/api/windows.applicationmodel.userdataaccounts.systemaccess.deviceaccountmailagefilter)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.All <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last14Days <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last1Day <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last30Days <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last3Days <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last7Days <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountMailAgeFilter.Last90Days
<hr>

**項目**

[Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind](/uwp/api/windows.applicationmodel.userdataaccounts.systemaccess.deviceaccountsyncschedulekind)

**[プロパティ]**


Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.AsItemsArrive <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Daily <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Every15Minutes <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Every2Hours <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Every30Minutes <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Every60Minutes <br /> Windows.ApplicationModel.UserDataAccounts.SystemAccess.DeviceAccountSyncScheduleKind.Manual
<hr>

**項目**

[Windows.Data.Text.TextPhoneme](/uwp/api/windows.data.text.textphoneme)

**[プロパティ]**


Windows.Data.Text.TextPhoneme <br /> Windows.Data.Text.TextPhoneme.DisplayText <br /> Windows.Data.Text.TextPhoneme.ReadingText
<hr>

**項目**

[Windows.Devices.AllJoyn.AllJoynBusObject](/uwp/api/windows.devices.alljoyn.alljoynbusobject)

**[プロパティ]**


Windows.Devices.AllJoyn.AllJoynBusObject <br /> Windows.Devices.AllJoyn.AllJoynBusObject.#ctor <br /> Windows.Devices.AllJoyn.AllJoynBusObject.#ctor(System.String) <br /> Windows.Devices.AllJoyn.AllJoynBusObject.#ctor(System.String,Windows.Devices.AllJoyn.AllJoynBusAttachment) <br /> Windows.Devices.AllJoyn.AllJoynBusObject.BusAttachment <br /> Windows.Devices.AllJoyn.AllJoynBusObject.Session <br /> Windows.Devices.AllJoyn.AllJoynBusObject.Stopped <br /> Windows.Devices.AllJoyn.AllJoynBusObject.AddProducer(Windows.Devices.AllJoyn.IAllJoynProducer) <br /> Windows.Devices.AllJoyn.AllJoynBusObject.Start <br /> Windows.Devices.AllJoyn.AllJoynBusObject.Stop
<hr>

**項目**

[Windows.Devices.AllJoyn.AllJoynBusObjectStoppedEventArgs](/uwp/api/windows.devices.alljoyn.alljoynbusobjectstoppedeventargs)

**[プロパティ]**


Windows.Devices.AllJoyn.AllJoynBusObjectStoppedEventArgs <br /> Windows.Devices.AllJoyn.AllJoynBusObjectStoppedEventArgs.#ctor(System.Int32) <br /> Windows.Devices.AllJoyn.AllJoynBusObjectStoppedEventArgs.Status
<hr>

**項目**

[Windows.Devices.AllJoyn.AllJoynSession](/uwp/api/windows.devices.alljoyn.alljoynsession)

**[プロパティ]**


Windows.Devices.AllJoyn.AllJoynSession <br /> Windows.Devices.AllJoyn.AllJoynSession.Id <br /> Windows.Devices.AllJoyn.AllJoynSession.Status <br /> Windows.Devices.AllJoyn.AllJoynSession.Lost <br /> Windows.Devices.AllJoyn.AllJoynSession.MemberAdded <br /> Windows.Devices.AllJoyn.AllJoynSession.MemberRemoved <br /> Windows.Devices.AllJoyn.AllJoynSession.GetFromServiceInfoAsync(Windows.Devices.AllJoyn.AllJoynServiceInfo) <br /> Windows.Devices.AllJoyn.AllJoynSession.GetFromServiceInfoAsync(Windows.Devices.AllJoyn.AllJoynServiceInfo,Windows.Devices.AllJoyn.AllJoynBusAttachment) <br /> Windows.Devices.AllJoyn.AllJoynSession.RemoveMemberAsync(System.String)
<hr>

**項目**

[Windows.Devices.AllJoyn.AllJoynSessionJoinedEventArgs](/uwp/api/windows.devices.alljoyn.alljoynsessionjoinedeventargs)

**[プロパティ]**


Windows.Devices.AllJoyn.AllJoynSessionJoinedEventArgs <br /> Windows.Devices.AllJoyn.AllJoynSessionJoinedEventArgs.#ctor(Windows.Devices.AllJoyn.AllJoynSession) <br /> Windows.Devices.AllJoyn.AllJoynSessionJoinedEventArgs.Session
<hr>

**項目**

[Windows.Devices.AllJoyn.IAllJoynProducer](/uwp/api/windows.devices.alljoyn.ialljoynproducer)

**[プロパティ]**


Windows.Devices.AllJoyn.IAllJoynProducer <br /> Windows.Devices.AllJoyn.IAllJoynProducer.SetBusObject(Windows.Devices.AllJoyn.AllJoynBusObject)
<hr>

**項目**

[Windows.Devices.Bluetooth.Rfcomm.RfcommDeviceServicesResult](/uwp/api/windows.devices.bluetooth.rfcomm.rfcommdeviceservicesresult)

**[プロパティ]**


Windows.Devices.Bluetooth.Rfcomm.RfcommDeviceServicesResult <br /> Windows.Devices.Bluetooth.Rfcomm.RfcommDeviceServicesResult.Error <br /> Windows.Devices.Bluetooth.Rfcomm.RfcommDeviceServicesResult.Services
<hr>

**項目**

[Windows.Devices.Printers.Extensions.Print3DWorkflowPrinterChangedEventArgs](/uwp/api/windows.devices.printers.extensions.print3dworkflowprinterchangedeventargs)

**[プロパティ]**


Windows.Devices.Printers.Extensions.Print3DWorkflowPrinterChangedEventArgs <br /> Windows.Devices.Printers.Extensions.Print3DWorkflowPrinterChangedEventArgs.NewDeviceId
<hr>

**項目**

[Windows.Devices.Sensors.AccelerometerReadingType](/uwp/api/windows.devices.sensors.accelerometerreadingtype)

**[プロパティ]**


Windows.Devices.Sensors.AccelerometerReadingType <br /> Windows.Devices.Sensors.AccelerometerReadingType.Gravity <br /> Windows.Devices.Sensors.AccelerometerReadingType.Linear <br /> Windows.Devices.Sensors.AccelerometerReadingType.Standard
<hr>

**項目**

[Windows.Devices.Sensors.SensorOptimizationGoal](/uwp/api/windows.devices.sensors.sensoroptimizationgoal)

**[プロパティ]**


Windows.Devices.Sensors.SensorOptimizationGoal <br /> Windows.Devices.Sensors.SensorOptimizationGoal.PowerEfficiency <br /> Windows.Devices.Sensors.SensorOptimizationGoal.Precision
<hr>

**項目**

[Windows.Foundation.Metadata.CreateFromStringAttribute](/uwp/api/windows.foundation.metadata.createfromstringattribute)

**[プロパティ]**


Windows.Foundation.Metadata.CreateFromStringAttribute <br /> Windows.Foundation.Metadata.CreateFromStringAttribute.MethodName <br /> Windows.Foundation.Metadata.CreateFromStringAttribute.#ctor
<hr>

**項目**

[Windows.Gaming.Input.ArcadeStick](/uwp/api/windows.gaming.input.arcadestick)

**[プロパティ]**


Windows.Gaming.Input.ArcadeStick <br /> Windows.Gaming.Input.ArcadeStick.ArcadeSticks <br /> Windows.Gaming.Input.ArcadeStick.Headset <br /> Windows.Gaming.Input.ArcadeStick.IsWireless <br /> Windows.Gaming.Input.ArcadeStick.User <br /> Windows.Gaming.Input.ArcadeStick.ArcadeStickAdded <br /> Windows.Gaming.Input.ArcadeStick.ArcadeStickRemoved <br /> Windows.Gaming.Input.ArcadeStick.HeadsetConnected <br /> Windows.Gaming.Input.ArcadeStick.HeadsetDisconnected <br /> Windows.Gaming.Input.ArcadeStick.UserChanged <br /> Windows.Gaming.Input.ArcadeStick.GetButtonLabel(Windows.Gaming.Input.ArcadeStickButtons) <br /> Windows.Gaming.Input.ArcadeStick.GetCurrentReading
<hr>

**項目**

[Windows.Gaming.Input.ArcadeStickButtons](/uwp/api/windows.gaming.input.arcadestickbuttons)

**[プロパティ]**


Windows.Gaming.Input.ArcadeStickButtons <br /> Windows.Gaming.Input.ArcadeStickButtons.Action1 <br /> Windows.Gaming.Input.ArcadeStickButtons.Action2 <br /> Windows.Gaming.Input.ArcadeStickButtons.Action3 <br /> Windows.Gaming.Input.ArcadeStickButtons.Action4 <br /> Windows.Gaming.Input.ArcadeStickButtons.Action5 <br /> Windows.Gaming.Input.ArcadeStickButtons.Action6 <br /> Windows.Gaming.Input.ArcadeStickButtons.None <br /> Windows.Gaming.Input.ArcadeStickButtons.Special1 <br /> Windows.Gaming.Input.ArcadeStickButtons.Special2 <br /> Windows.Gaming.Input.ArcadeStickButtons.StickDown <br /> Windows.Gaming.Input.ArcadeStickButtons.StickLeft <br /> Windows.Gaming.Input.ArcadeStickButtons.StickRight <br /> Windows.Gaming.Input.ArcadeStickButtons.StickUp
<hr>

**項目**

[Windows.Gaming.Input.ArcadeStickReading](/uwp/api/windows.gaming.input.arcadestickreading)

**[プロパティ]**


Windows.Gaming.Input.ArcadeStickReading <br /> Windows.Gaming.Input.ArcadeStickReading.Buttons <br /> Windows.Gaming.Input.ArcadeStickReading.Timestamp
<hr>

**項目**

[Windows.Gaming.Input.GameControllerButtonLabel](/uwp/api/windows.gaming.input.gamecontrollerbuttonlabel)

**[プロパティ]**


Windows.Gaming.Input.GameControllerButtonLabel <br /> Windows.Gaming.Input.GameControllerButtonLabel.Back <br /> Windows.Gaming.Input.GameControllerButtonLabel.Circle <br /> Windows.Gaming.Input.GameControllerButtonLabel.Cross <br /> Windows.Gaming.Input.GameControllerButtonLabel.DialLeft <br /> Windows.Gaming.Input.GameControllerButtonLabel.DialRight <br /> Windows.Gaming.Input.GameControllerButtonLabel.Down <br /> Windows.Gaming.Input.GameControllerButtonLabel.DownLeftArrow <br /> Windows.Gaming.Input.GameControllerButtonLabel.Left <br /> Windows.Gaming.Input.GameControllerButtonLabel.Left1 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Left2 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Left3 <br /> Windows.Gaming.Input.GameControllerButtonLabel.LeftBumper <br /> Windows.Gaming.Input.GameControllerButtonLabel.LeftStickButton <br /> Windows.Gaming.Input.GameControllerButtonLabel.LeftTrigger <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterA <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterB <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterC <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterL <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterR <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterX <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterY <br /> Windows.Gaming.Input.GameControllerButtonLabel.LetterZ <br /> Windows.Gaming.Input.GameControllerButtonLabel.Menu <br /> Windows.Gaming.Input.GameControllerButtonLabel.Minus <br /> Windows.Gaming.Input.GameControllerButtonLabel.Mode <br /> Windows.Gaming.Input.GameControllerButtonLabel.None <br /> Windows.Gaming.Input.GameControllerButtonLabel.Options <br /> Windows.Gaming.Input.GameControllerButtonLabel.Paddle1 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Paddle2 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Paddle3 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Paddle4 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Plus <br /> Windows.Gaming.Input.GameControllerButtonLabel.Right <br /> Windows.Gaming.Input.GameControllerButtonLabel.Right1 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Right2 <br /> Windows.Gaming.Input.GameControllerButtonLabel.Right3 <br /> Windows.Gaming.Input.GameControllerButtonLabel.RightBumper <br /> Windows.Gaming.Input.GameControllerButtonLabel.RightStickButton <br /> Windows.Gaming.Input.GameControllerButtonLabel.RightTrigger <br /> Windows.Gaming.Input.GameControllerButtonLabel.Select <br /> Windows.Gaming.Input.GameControllerButtonLabel.Share <br /> Windows.Gaming.Input.GameControllerButtonLabel.Square <br /> Windows.Gaming.Input.GameControllerButtonLabel.Start <br /> Windows.Gaming.Input.GameControllerButtonLabel.Suspension <br /> Windows.Gaming.Input.GameControllerButtonLabel.Triangle <br /> Windows.Gaming.Input.GameControllerButtonLabel.Up <br /> Windows.Gaming.Input.GameControllerButtonLabel.View <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxA <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxB <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxBack <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxDown <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxLeft <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxLeftBumper <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxLeftStickButton <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxLeftTrigger <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxMenu <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxPaddle1 <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxPaddle2 <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxPaddle3 <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxPaddle4 <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxRight <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxRightBumper <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxRightStickButton <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxRightTrigger <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxStart <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxUp <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxView <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxX <br /> Windows.Gaming.Input.GameControllerButtonLabel.XboxY
<hr>

**項目**

[Windows.Gaming.Input.OptionalUINavigationButtons](/uwp/api/windows.gaming.input.optionaluinavigationbuttons)

**[プロパティ]**


Windows.Gaming.Input.OptionalUINavigationButtons <br /> Windows.Gaming.Input.OptionalUINavigationButtons.Context1 <br /> Windows.Gaming.Input.OptionalUINavigationButtons.Context2 <br /> Windows.Gaming.Input.OptionalUINavigationButtons.Context3 <br /> Windows.Gaming.Input.OptionalUINavigationButtons.Context4 <br /> Windows.Gaming.Input.OptionalUINavigationButtons.None <br /> Windows.Gaming.Input.OptionalUINavigationButtons.PageDown <br /> Windows.Gaming.Input.OptionalUINavigationButtons.PageLeft <br /> Windows.Gaming.Input.OptionalUINavigationButtons.PageRight <br /> Windows.Gaming.Input.OptionalUINavigationButtons.PageUp <br /> Windows.Gaming.Input.OptionalUINavigationButtons.ScrollDown <br /> Windows.Gaming.Input.OptionalUINavigationButtons.ScrollLeft <br /> Windows.Gaming.Input.OptionalUINavigationButtons.ScrollRight <br /> Windows.Gaming.Input.OptionalUINavigationButtons.ScrollUp
<hr>

**項目**

[Windows.Gaming.Input.RacingWheel](/uwp/api/windows.gaming.input.racingwheel)

**[プロパティ]**


Windows.Gaming.Input.RacingWheel <br /> Windows.Gaming.Input.RacingWheel.HasClutch <br /> Windows.Gaming.Input.RacingWheel.HasHandbrake <br /> Windows.Gaming.Input.RacingWheel.HasPatternShifter <br /> Windows.Gaming.Input.RacingWheel.Headset <br /> Windows.Gaming.Input.RacingWheel.IsWireless <br /> Windows.Gaming.Input.RacingWheel.MaxPatternShifterGear <br /> Windows.Gaming.Input.RacingWheel.MaxWheelAngle <br /> Windows.Gaming.Input.RacingWheel.RacingWheels <br /> Windows.Gaming.Input.RacingWheel.User <br /> Windows.Gaming.Input.RacingWheel.WheelMotor <br /> Windows.Gaming.Input.RacingWheel.HeadsetConnected <br /> Windows.Gaming.Input.RacingWheel.HeadsetDisconnected <br /> Windows.Gaming.Input.RacingWheel.RacingWheelAdded <br /> Windows.Gaming.Input.RacingWheel.RacingWheelRemoved <br /> Windows.Gaming.Input.RacingWheel.UserChanged <br /> Windows.Gaming.Input.RacingWheel.GetButtonLabel(Windows.Gaming.Input.RacingWheelButtons) <br /> Windows.Gaming.Input.RacingWheel.GetCurrentReading
<hr>

**項目**

[Windows.Gaming.Input.RacingWheelButtons](/uwp/api/windows.gaming.input.racingwheelbuttons)

**[プロパティ]**


Windows.Gaming.Input.RacingWheelButtons <br /> Windows.Gaming.Input.RacingWheelButtons.Button1 <br /> Windows.Gaming.Input.RacingWheelButtons.Button10 <br /> Windows.Gaming.Input.RacingWheelButtons.Button11 <br /> Windows.Gaming.Input.RacingWheelButtons.Button12 <br /> Windows.Gaming.Input.RacingWheelButtons.Button13 <br /> Windows.Gaming.Input.RacingWheelButtons.Button14 <br /> Windows.Gaming.Input.RacingWheelButtons.Button15 <br /> Windows.Gaming.Input.RacingWheelButtons.Button16 <br /> Windows.Gaming.Input.RacingWheelButtons.Button2 <br /> Windows.Gaming.Input.RacingWheelButtons.Button3 <br /> Windows.Gaming.Input.RacingWheelButtons.Button4 <br /> Windows.Gaming.Input.RacingWheelButtons.Button5 <br /> Windows.Gaming.Input.RacingWheelButtons.Button6 <br /> Windows.Gaming.Input.RacingWheelButtons.Button7 <br /> Windows.Gaming.Input.RacingWheelButtons.Button8 <br /> Windows.Gaming.Input.RacingWheelButtons.Button9 <br /> Windows.Gaming.Input.RacingWheelButtons.DPadDown <br /> Windows.Gaming.Input.RacingWheelButtons.DPadLeft <br /> Windows.Gaming.Input.RacingWheelButtons.DPadRight <br /> Windows.Gaming.Input.RacingWheelButtons.DPadUp <br /> Windows.Gaming.Input.RacingWheelButtons.NextGear <br /> Windows.Gaming.Input.RacingWheelButtons.None <br /> Windows.Gaming.Input.RacingWheelButtons.PreviousGear
<hr>

**項目**

[Windows.Gaming.Input.RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading)

**[プロパティ]**


Windows.Gaming.Input.RacingWheelReading <br /> Windows.Gaming.Input.RacingWheelReading.Brake <br /> Windows.Gaming.Input.RacingWheelReading.Buttons <br /> Windows.Gaming.Input.RacingWheelReading.Clutch <br /> Windows.Gaming.Input.RacingWheelReading.Handbrake <br /> Windows.Gaming.Input.RacingWheelReading.PatternShifterGear <br /> Windows.Gaming.Input.RacingWheelReading.Throttle <br /> Windows.Gaming.Input.RacingWheelReading.Timestamp <br /> Windows.Gaming.Input.RacingWheelReading.Wheel
<hr>

**項目**

[Windows.Gaming.Input.RequiredUINavigationButtons](/uwp/api/windows.gaming.input.requireduinavigationbuttons)

**[プロパティ]**


Windows.Gaming.Input.RequiredUINavigationButtons <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Accept <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Cancel <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Down <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Left <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Menu <br /> Windows.Gaming.Input.RequiredUINavigationButtons.None <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Right <br /> Windows.Gaming.Input.RequiredUINavigationButtons.Up <br /> Windows.Gaming.Input.RequiredUINavigationButtons.View
<hr>

**項目**

[Windows.Gaming.Input.UINavigationController](/uwp/api/windows.gaming.input.uinavigationcontroller)

**[プロパティ]**


Windows.Gaming.Input.UINavigationController <br /> Windows.Gaming.Input.UINavigationController.Headset <br /> Windows.Gaming.Input.UINavigationController.IsWireless <br /> Windows.Gaming.Input.UINavigationController.UINavigationControllers <br /> Windows.Gaming.Input.UINavigationController.User <br /> Windows.Gaming.Input.UINavigationController.HeadsetConnected <br /> Windows.Gaming.Input.UINavigationController.HeadsetDisconnected <br /> Windows.Gaming.Input.UINavigationController.UINavigationControllerAdded <br /> Windows.Gaming.Input.UINavigationController.UINavigationControllerRemoved <br /> Windows.Gaming.Input.UINavigationController.UserChanged <br /> Windows.Gaming.Input.UINavigationController.GetCurrentReading <br /> Windows.Gaming.Input.UINavigationController.GetOptionalButtonLabel(Windows.Gaming.Input.OptionalUINavigationButtons) <br /> Windows.Gaming.Input.UINavigationController.GetRequiredButtonLabel(Windows.Gaming.Input.RequiredUINavigationButtons)
<hr>

**項目**

[Windows.Gaming.Input.UINavigationReading](/uwp/api/windows.gaming.input.uinavigationreading)

**[プロパティ]**


Windows.Gaming.Input.UINavigationReading <br /> Windows.Gaming.Input.UINavigationReading.OptionalButtons <br /> Windows.Gaming.Input.UINavigationReading.RequiredButtons <br /> Windows.Gaming.Input.UINavigationReading.Timestamp
<hr>

**項目**

[Windows.Gaming.Input.Custom.GameControllerFactoryManager](/uwp/api/windows.gaming.input.custom.gamecontrollerfactorymanager)

**[プロパティ]**


Windows.Gaming.Input.Custom.GameControllerFactoryManager <br /> Windows.Gaming.Input.Custom.GameControllerFactoryManager.RegisterCustomFactoryForGipInterface(Windows.Gaming.Input.Custom.ICustomGameControllerFactory,System.Guid) <br /> Windows.Gaming.Input.Custom.GameControllerFactoryManager.RegisterCustomFactoryForHardwareId(Windows.Gaming.Input.Custom.ICustomGameControllerFactory,System.UInt16,System.UInt16) <br /> Windows.Gaming.Input.Custom.GameControllerFactoryManager.RegisterCustomFactoryForXusbType(Windows.Gaming.Input.Custom.ICustomGameControllerFactory,Windows.Gaming.Input.Custom.XusbDeviceType,Windows.Gaming.Input.Custom.XusbDeviceSubtype)
<hr>

**項目**

[Windows.Gaming.Input.Custom.GameControllerVersionInfo](/uwp/api/windows.gaming.input.custom.gamecontrollerversioninfo)

**[プロパティ]**


Windows.Gaming.Input.Custom.GameControllerVersionInfo <br /> Windows.Gaming.Input.Custom.GameControllerVersionInfo.Build <br /> Windows.Gaming.Input.Custom.GameControllerVersionInfo.Major <br /> Windows.Gaming.Input.Custom.GameControllerVersionInfo.Minor <br /> Windows.Gaming.Input.Custom.GameControllerVersionInfo.Revision
<hr>

**項目**

[Windows.Gaming.Input.Custom.GipFirmwareUpdateProgress](/uwp/api/windows.gaming.input.custom.gipfirmwareupdateprogress)

**[プロパティ]**


Windows.Gaming.Input.Custom.GipFirmwareUpdateProgress <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateProgress.CurrentComponentId <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateProgress.PercentCompleted
<hr>

**項目**

[Windows.Gaming.Input.Custom.GipFirmwareUpdateResult](/uwp/api/windows.gaming.input.custom.gipfirmwareupdateresult)

**[プロパティ]**


Windows.Gaming.Input.Custom.GipFirmwareUpdateResult <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateResult.ExtendedErrorCode <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateResult.FinalComponentId <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateResult.Status
<hr>

**項目**

[Windows.Gaming.Input.Custom.GipFirmwareUpdateStatus](/uwp/api/windows.gaming.input.custom.gipfirmwareupdatestatus)

**[プロパティ]**


Windows.Gaming.Input.Custom.GipFirmwareUpdateStatus <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateStatus.Completed <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateStatus.Failed <br /> Windows.Gaming.Input.Custom.GipFirmwareUpdateStatus.UpToDate
<hr>

**項目**

[Windows.Gaming.Input.Custom.GipGameControllerProvider](/uwp/api/windows.gaming.input.custom.gipgamecontrollerprovider)

**[プロパティ]**


Windows.Gaming.Input.Custom.GipGameControllerProvider <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.FirmwareVersionInfo <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.HardwareProductId <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.HardwareVendorId <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.HardwareVersionInfo <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.IsConnected <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.SendMessage(Windows.Gaming.Input.Custom.GipMessageClass,System.Byte,System.Byte[]) <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.SendReceiveMessage(Windows.Gaming.Input.Custom.GipMessageClass,System.Byte,System.Byte[],System.Byte[]) <br /> Windows.Gaming.Input.Custom.GipGameControllerProvider.UpdateFirmwareAsync(Windows.Storage.Streams.IInputStream)
<hr>

**項目**

[Windows.Gaming.Input.Custom.GipMessageClass](/uwp/api/windows.gaming.input.custom.gipmessageclass)

**[プロパティ]**


Windows.Gaming.Input.Custom.GipMessageClass <br /> Windows.Gaming.Input.Custom.GipMessageClass.Command <br /> Windows.Gaming.Input.Custom.GipMessageClass.LowLatency <br /> Windows.Gaming.Input.Custom.GipMessageClass.StandardLatency
<hr>

**項目**

[Windows.Gaming.Input.Custom.ICustomGameControllerFactory](/uwp/api/windows.gaming.input.custom.icustomgamecontrollerfactory)

**[プロパティ]**


Windows.Gaming.Input.Custom.ICustomGameControllerFactory <br /> Windows.Gaming.Input.Custom.ICustomGameControllerFactory.CreateGameController(Windows.Gaming.Input.Custom.IGameControllerProvider) <br /> Windows.Gaming.Input.Custom.ICustomGameControllerFactory.OnGameControllerAdded(Windows.Gaming.Input.IGameController) <br /> Windows.Gaming.Input.Custom.ICustomGameControllerFactory.OnGameControllerRemoved(Windows.Gaming.Input.IGameController)
<hr>

**項目**

[Windows.Gaming.Input.Custom.IGameControllerInputSink](/uwp/api/windows.gaming.input.custom.igamecontrollerinputsink)

**[プロパティ]**


Windows.Gaming.Input.Custom.IGameControllerInputSink <br /> Windows.Gaming.Input.Custom.IGameControllerInputSink.OnInputResumed(System.UInt64) <br /> Windows.Gaming.Input.Custom.IGameControllerInputSink.OnInputSuspended(System.UInt64)
<hr>

**項目**

[Windows.Gaming.Input.Custom.IGameControllerProvider](/uwp/api/windows.gaming.input.custom.igamecontrollerprovider)

**[プロパティ]**


Windows.Gaming.Input.Custom.IGameControllerProvider <br /> Windows.Gaming.Input.Custom.IGameControllerProvider.FirmwareVersionInfo <br /> Windows.Gaming.Input.Custom.IGameControllerProvider.HardwareProductId <br /> Windows.Gaming.Input.Custom.IGameControllerProvider.HardwareVendorId <br /> Windows.Gaming.Input.Custom.IGameControllerProvider.HardwareVersionInfo <br /> Windows.Gaming.Input.Custom.IGameControllerProvider.IsConnected
<hr>

**項目**

[Windows.Gaming.Input.Custom.IGipGameControllerInputSink](/uwp/api/windows.gaming.input.custom.igipgamecontrollerinputsink)

**[プロパティ]**


Windows.Gaming.Input.Custom.IGipGameControllerInputSink <br /> Windows.Gaming.Input.Custom.IGipGameControllerInputSink.OnKeyReceived(System.UInt64,System.Byte,System.Boolean) <br /> Windows.Gaming.Input.Custom.IGipGameControllerInputSink.OnMessageReceived(System.UInt64,Windows.Gaming.Input.Custom.GipMessageClass,System.Byte,System.Byte,System.Byte[])
<hr>

**項目**

[Windows.Gaming.Input.Custom.IXusbGameControllerInputSink](/uwp/api/windows.gaming.input.custom.ixusbgamecontrollerinputsink)

**[プロパティ]**


Windows.Gaming.Input.Custom.IXusbGameControllerInputSink <br /> Windows.Gaming.Input.Custom.IXusbGameControllerInputSink.OnInputReceived(System.UInt64,System.Byte,System.Byte[])
<hr>

**項目**

[Windows.Gaming.Input.Custom.XusbDeviceSubtype](/uwp/api/windows.gaming.input.custom.xusbdevicesubtype)

**[プロパティ]**


Windows.Gaming.Input.Custom.XusbDeviceSubtype <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.ArcadePad <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.ArcadeStick <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.DancePad <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.DrumKit <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.FlightStick <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.Gamepad <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.Guitar <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.GuitarAlternate <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.GuitarBass <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.Unknown <br /> Windows.Gaming.Input.Custom.XusbDeviceSubtype.Wheel
<hr>

**項目**

[Windows.Gaming.Input.Custom.XusbDeviceType](/uwp/api/windows.gaming.input.custom.xusbdevicetype)

**[プロパティ]**


Windows.Gaming.Input.Custom.XusbDeviceType <br /> Windows.Gaming.Input.Custom.XusbDeviceType.Gamepad <br /> Windows.Gaming.Input.Custom.XusbDeviceType.Unknown
<hr>

**項目**

[Windows.Gaming.Input.Custom.XusbGameControllerProvider](/uwp/api/windows.gaming.input.custom.xusbgamecontrollerprovider)

**[プロパティ]**


Windows.Gaming.Input.Custom.XusbGameControllerProvider <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.FirmwareVersionInfo <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.HardwareProductId <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.HardwareVendorId <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.HardwareVersionInfo <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.IsConnected <br /> Windows.Gaming.Input.Custom.XusbGameControllerProvider.SetVibration(System.Double,System.Double)
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ConditionForceEffect](/uwp/api/windows.gaming.input.forcefeedback.conditionforceeffect)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ConditionForceEffect <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.#ctor(Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind) <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.Gain <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.Kind <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.State <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.SetParameters(Windows.Foundation.Numerics.Vector3,System.Single,System.Single,System.Single,System.Single,System.Single,System.Single) <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.Start <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffect.Stop
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind](/uwp/api/windows.gaming.input.forcefeedback.conditionforceeffectkind)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind.Damper <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind.Friction <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind.Inertia <br /> Windows.Gaming.Input.ForceFeedback.ConditionForceEffectKind.Spring
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ConstantForceEffect](/uwp/api/windows.gaming.input.forcefeedback.constantforceeffect)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ConstantForceEffect <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.#ctor <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.Gain <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.State <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.SetParameters(Windows.Foundation.Numerics.Vector3,Windows.Foundation.TimeSpan) <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.SetParametersWithEnvelope(Windows.Foundation.Numerics.Vector3,System.Single,System.Single,System.Single,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,System.UInt32) <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.Start <br /> Windows.Gaming.Input.ForceFeedback.ConstantForceEffect.Stop
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes](/uwp/api/windows.gaming.input.forcefeedback.forcefeedbackeffectaxes)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes.None <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes.X <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes.Y <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectAxes.Z
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState](/uwp/api/windows.gaming.input.forcefeedback.forcefeedbackeffectstate)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState.Faulted <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState.Paused <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState.Running <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackEffectState.Stopped
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ForceFeedbackLoadEffectResult](/uwp/api/windows.gaming.input.forcefeedback.forcefeedbackloadeffectresult)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ForceFeedbackLoadEffectResult <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackLoadEffectResult.EffectNotSupported <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackLoadEffectResult.EffectStorageFull <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackLoadEffectResult.Succeeded
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor](/uwp/api/windows.gaming.input.forcefeedback.forcefeedbackmotor)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.AreEffectsPaused <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.IsEnabled <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.MasterGain <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.SupportedAxes <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.LoadEffectAsync(Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect) <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.PauseAllEffects <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.ResumeAllEffects <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.StopAllEffects <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.TryDisableAsync <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.TryEnableAsync <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.TryResetAsync <br /> Windows.Gaming.Input.ForceFeedback.ForceFeedbackMotor.TryUnloadEffectAsync(Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect)
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect](/uwp/api/windows.gaming.input.forcefeedback.iforcefeedbackeffect)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect <br /> Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect.Gain <br /> Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect.State <br /> Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect.Start <br /> Windows.Gaming.Input.ForceFeedback.IForceFeedbackEffect.Stop
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect](/uwp/api/windows.gaming.input.forcefeedback.periodicforceeffect)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.#ctor(Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind) <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.Gain <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.Kind <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.State <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.SetParameters(Windows.Foundation.Numerics.Vector3,System.Single,System.Single,System.Single,Windows.Foundation.TimeSpan) <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.SetParametersWithEnvelope(Windows.Foundation.Numerics.Vector3,System.Single,System.Single,System.Single,System.Single,System.Single,System.Single,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,System.UInt32) <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.Start <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffect.Stop
<hr>

**項目**

[Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind](/uwp/api/windows.gaming.input.forcefeedback.periodicforceeffectkind)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind.SawtoothWaveDown <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind.SawtoothWaveUp <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind.SineWave <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind.SquareWave <br /> Windows.Gaming.Input.ForceFeedback.PeriodicForceEffectKind.TriangleWave
<hr>

**項目**

[Windows.Gaming.Input<br />ForceFeedback.RampForceEffect](/uwp/api/windows.gaming.input.forcefeedback.rampforceeffect)

**[プロパティ]**


Windows.Gaming.Input.ForceFeedback.RampForceEffect <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.#ctor <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.Gain <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.State <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.SetParameters(Windows.Foundation.Numerics.Vector3,Windows.Foundation.Numerics.Vector3,Windows.Foundation.TimeSpan) <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.SetParametersWithEnvelope(Windows.Foundation.Numerics.Vector3,Windows.Foundation.Numerics.Vector3,System.Single,System.Single,System.Single,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,Windows.Foundation.TimeSpan,System.UInt32) <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.Start <br /> Windows.Gaming.Input.ForceFeedback.RampForceEffect.Stop
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat](/uwp/api/windows.globalization.phonenumberformatting.phonenumberformat)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat.E164 <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat.International <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat.National <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat.Rfc3966
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter](/uwp/api/windows.globalization.phonenumberformatting.phonenumberformatter)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.#ctor <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.Format(Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.Format(Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo,Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormat) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.FormatPartialString(System.String) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.FormatString(System.String) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.FormatStringWithLeftToRightMarkers(System.String) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.GetCountryCodeForRegion(System.String) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.GetNationalDirectDialingPrefixForRegion(System.String,System.Boolean) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.TryCreate(System.String,Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter@) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberFormatter.WrapWithLeftToRightMarkers(System.String)
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo](/uwp/api/windows.globalization.phonenumberformatting.phonenumberinfo)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.#ctor(System.String) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.CountryCode <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.PhoneNumber <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.CheckNumberMatch(Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.GetGeographicRegionCode <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.GetLengthOfGeographicalAreaCode <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.GetLengthOfNationalDestinationCode <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.GetNationalSignificantNumber <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.PredictNumberKind <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.ToString <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.TryParse(System.String,System.String,Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo@) <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo.TryParse(System.String,Windows.Globalization.PhoneNumberFormatting.PhoneNumberInfo@)
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult](/uwp/api/windows.globalization.phonenumberformatting.phonenumbermatchresult)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult.ExactMatch <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult.NationalSignificantNumberMatch <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult.NoMatch <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberMatchResult.ShortNationalSignificantNumberMatch
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult](/uwp/api/windows.globalization.phonenumberformatting.phonenumberparseresult)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult.InvalidCountryCode <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult.NotANumber <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult.TooLong <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult.TooShort <br /> Windows.Globalization.PhoneNumberFormatting.PhoneNumberParseResult.Valid
<hr>

**項目**

[Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind](/uwp/api/windows.globalization.phonenumberformatting.predictedphonenumberkind)

**[プロパティ]**


Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.FixedLine <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.FixedLineOrMobile <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.Mobile <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.Pager <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.PersonalNumber <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.PremiumRate <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.SharedCost <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.TollFree <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.UniversalAccountNumber <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.Unknown <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.Voicemail <br /> Windows.Globalization.PhoneNumberFormatting.PredictedPhoneNumberKind.Voip
<hr>

**項目**

[Windows.Graphics.Printing.PrintBordering](/uwp/api/windows.graphics.printing.printbordering)

**[プロパティ]**


Windows.Graphics.Printing.PrintBordering <br /> Windows.Graphics.Printing.PrintBordering.Bordered <br /> Windows.Graphics.Printing.PrintBordering.Borderless <br /> Windows.Graphics.Printing.PrintBordering.Default <br /> Windows.Graphics.Printing.PrintBordering.NotAvailable <br /> Windows.Graphics.Printing.PrintBordering.PrinterCustom
<hr>

**項目**

[Windows.Graphics.Printing.PrintPageInfo](/uwp/api/windows.graphics.printing.printpageinfo)

**[プロパティ]**


Windows.Graphics.Printing.PrintPageInfo <br /> Windows.Graphics.Printing.PrintPageInfo.#ctor <br /> Windows.Graphics.Printing.PrintPageInfo.DpiX <br /> Windows.Graphics.Printing.PrintPageInfo.DpiY <br /> Windows.Graphics.Printing.PrintPageInfo.MediaSize <br /> Windows.Graphics.Printing.PrintPageInfo.Orientation <br /> Windows.Graphics.Printing.PrintPageInfo.PageSize
<hr>

**項目**

[Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails](/uwp/api/windows.graphics.printing.optiondetails.printborderingoptiondetails)

**[プロパティ]**


Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.ErrorText <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.Items <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.OptionId <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.OptionType <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.State <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.Value <br /> Windows.Graphics.Printing.OptionDetails.PrintBorderingOptionDetails.TrySetValue(System.Object)
<hr>

**項目**

[Windows.Management.Workplace.MessagingSyncPolicy](/uwp/api/windows.management.workplace.messagingsyncpolicy)

**[プロパティ]**


Windows.Management.Workplace.MessagingSyncPolicy <br /> Windows.Management.Workplace.MessagingSyncPolicy.Allowed <br /> Windows.Management.Workplace.MessagingSyncPolicy.Disallowed <br /> Windows.Management.Workplace.MessagingSyncPolicy.Required
<hr>

**項目**

[Windows.Media.MediaTimelineController](/uwp/api/windows.media.mediatimelinecontroller)

**[プロパティ]**


Windows.Media.MediaTimelineController <br /> Windows.Media.MediaTimelineController.#ctor <br /> Windows.Media.MediaTimelineController.ClockRate <br /> Windows.Media.MediaTimelineController.Position <br /> Windows.Media.MediaTimelineController.State <br /> Windows.Media.MediaTimelineController.PositionChanged <br /> Windows.Media.MediaTimelineController.StateChanged <br /> Windows.Media.MediaTimelineController.Pause <br /> Windows.Media.MediaTimelineController.Resume <br /> Windows.Media.MediaTimelineController.Start
<hr>

**項目**

[Windows.Media.MediaTimelineControllerState](/uwp/api/windows.media.mediatimelinecontrollerstate)

**[プロパティ]**


Windows.Media.MediaTimelineControllerState <br /> Windows.Media.MediaTimelineControllerState.Paused <br /> Windows.Media.MediaTimelineControllerState.Running
<hr>

**項目**

[Windows.Media.Audio.AudioGraphBatchUpdater](/uwp/api/windows.media.audio.audiographbatchupdater)

**[プロパティ]**


Windows.Media.Audio.AudioGraphBatchUpdater <br /> Windows.Media.Audio.AudioGraphBatchUpdater.Close
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitter](/uwp/api/windows.media.audio.audionodeemitter)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitter <br /> Windows.Media.Audio.AudioNodeEmitter.#ctor <br /> Windows.Media.Audio.AudioNodeEmitter.#ctor(Windows.Media.Audio.AudioNodeEmitterShape,Windows.Media.Audio.AudioNodeEmitterDecayModel,Windows.Media.Audio.AudioNodeEmitterSettings) <br /> Windows.Media.Audio.AudioNodeEmitter.DecayModel <br /> Windows.Media.Audio.AudioNodeEmitter.Direction <br /> Windows.Media.Audio.AudioNodeEmitter.DistanceScale <br /> Windows.Media.Audio.AudioNodeEmitter.DopplerScale <br /> Windows.Media.Audio.AudioNodeEmitter.DopplerVelocity <br /> Windows.Media.Audio.AudioNodeEmitter.Gain <br /> Windows.Media.Audio.AudioNodeEmitter.IsDopplerDisabled <br /> Windows.Media.Audio.AudioNodeEmitter.Position <br /> Windows.Media.Audio.AudioNodeEmitter.Shape
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterConeProperties](/uwp/api/windows.media.audio.audionodeemitterconeproperties)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterConeProperties <br /> Windows.Media.Audio.AudioNodeEmitterConeProperties.InnerAngle <br /> Windows.Media.Audio.AudioNodeEmitterConeProperties.OuterAngle <br /> Windows.Media.Audio.AudioNodeEmitterConeProperties.OuterAngleGain
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterDecayKind](/uwp/api/windows.media.audio.audionodeemitterdecaykind)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterDecayKind <br /> Windows.Media.Audio.AudioNodeEmitterDecayKind.Custom <br /> Windows.Media.Audio.AudioNodeEmitterDecayKind.Natural
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterDecayModel](/uwp/api/windows.media.audio.audionodeemitterdecaymodel)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterDecayModel <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.Kind <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.MaxGain <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.MinGain <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.NaturalProperties <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.CreateCustom(System.Double,System.Double) <br /> Windows.Media.Audio.AudioNodeEmitterDecayModel.CreateNatural(System.Double,System.Double,System.Double,System.Double)
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterNaturalDecayModelProperties](/uwp/api/windows.media.audio.audionodeemitternaturaldecaymodelproperties)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterNaturalDecayModelProperties <br /> Windows.Media.Audio.AudioNodeEmitterNaturalDecayModelProperties.CutoffDistance <br /> Windows.Media.Audio.AudioNodeEmitterNaturalDecayModelProperties.UnityGainDistance
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterSettings](/uwp/api/windows.media.audio.audionodeemittersettings)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterSettings <br /> Windows.Media.Audio.AudioNodeEmitterSettings.DisableDoppler <br /> Windows.Media.Audio.AudioNodeEmitterSettings.None
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterShape](/uwp/api/windows.media.audio.audionodeemittershape)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterShape <br /> Windows.Media.Audio.AudioNodeEmitterShape.ConeProperties <br /> Windows.Media.Audio.AudioNodeEmitterShape.Kind <br /> Windows.Media.Audio.AudioNodeEmitterShape.CreateCone(System.Double,System.Double,System.Double) <br /> Windows.Media.Audio.AudioNodeEmitterShape.CreateOmnidirectional
<hr>

**項目**

[Windows.Media.Audio.AudioNodeEmitterShapeKind](/uwp/api/windows.media.audio.audionodeemittershapekind)

**[プロパティ]**


Windows.Media.Audio.AudioNodeEmitterShapeKind <br /> Windows.Media.Audio.AudioNodeEmitterShapeKind.Cone <br /> Windows.Media.Audio.AudioNodeEmitterShapeKind.Omnidirectional
<hr>

**項目**

[Windows.Media.Audio.AudioNodeListener](/uwp/api/windows.media.audio.audionodelistener)

**[プロパティ]**


Windows.Media.Audio.AudioNodeListener <br /> Windows.Media.Audio.AudioNodeListener.#ctor <br /> Windows.Media.Audio.AudioNodeListener.DopplerVelocity <br /> Windows.Media.Audio.AudioNodeListener.Orientation <br /> Windows.Media.Audio.AudioNodeListener.Position <br /> Windows.Media.Audio.AudioNodeListener.SpeedOfSound
<hr>

**項目**

[Windows.Media.Audio.IAudioInputNode2](/uwp/api/windows.media.audio.iaudioinputnode2)

**[プロパティ]**


Windows.Media.Audio.IAudioInputNode2 <br /> Windows.Media.Audio.IAudioInputNode2.Emitter
<hr>

**項目**

[Windows.Media.Audio.IAudioNodeWithListener](/uwp/api/windows.media.audio.iaudionodewithlistener)

**[プロパティ]**


Windows.Media.Audio.IAudioNodeWithListener <br /> Windows.Media.Audio.IAudioNodeWithListener.Listener
<hr>

**項目**

[Windows.Media.Capture.MediaCaptureMemoryPreference](/uwp/api/windows.media.capture.mediacapturememorypreference)

**[プロパティ]**


Windows.Media.Capture.MediaCaptureMemoryPreference <br /> Windows.Media.Capture.MediaCaptureMemoryPreference.Auto <br /> Windows.Media.Capture.MediaCaptureMemoryPreference.Cpu
<hr>

**項目**

[Windows.Media.Capture.MediaCapturePauseResult](/uwp/api/windows.media.capture.mediacapturepauseresult)

**[プロパティ]**


Windows.Media.Capture.MediaCapturePauseResult <br /> Windows.Media.Capture.MediaCapturePauseResult.LastFrame <br /> Windows.Media.Capture.MediaCapturePauseResult.RecordDuration <br /> Windows.Media.Capture.MediaCapturePauseResult.Close
<hr>

**項目**

[Windows.Media.Capture.MediaCaptureSharingMode](/uwp/api/windows.media.capture.mediacapturesharingmode)

**[プロパティ]**


Windows.Media.Capture.MediaCaptureSharingMode <br /> Windows.Media.Capture.MediaCaptureSharingMode.ExclusiveControl <br /> Windows.Media.Capture.MediaCaptureSharingMode.SharedReadOnly
<hr>

**項目**

[Windows.Media.Capture.MediaCaptureStopResult](/uwp/api/windows.media.capture.mediacapturestopresult)

**[プロパティ]**


Windows.Media.Capture.MediaCaptureStopResult <br /> Windows.Media.Capture.MediaCaptureStopResult.LastFrame <br /> Windows.Media.Capture.MediaCaptureStopResult.RecordDuration <br /> Windows.Media.Capture.MediaCaptureStopResult.Close
<hr>

**項目**

[Windows.Media.Capture.Frames.BufferMediaFrame](/uwp/api/windows.media.capture.frames.buffermediaframe)

**[プロパティ]**


Windows.Media.Capture.Frames.BufferMediaFrame <br /> Windows.Media.Capture.Frames.BufferMediaFrame.Buffer <br /> Windows.Media.Capture.Frames.BufferMediaFrame.FrameReference
<hr>

**項目**

[Windows.Media.Capture.Frames.DepthMediaFrame](/uwp/api/windows.media.capture.frames.depthmediaframe)

**[プロパティ]**


Windows.Media.Capture.Frames.DepthMediaFrame <br /> Windows.Media.Capture.Frames.DepthMediaFrame.DepthFormat <br /> Windows.Media.Capture.Frames.DepthMediaFrame.FrameReference <br /> Windows.Media.Capture.Frames.DepthMediaFrame.VideoMediaFrame <br /> Windows.Media.Capture.Frames.DepthMediaFrame.TryCreateCoordinateMapper(Windows.Media.Devices.Core.CameraIntrinsics,Windows.Perception.Spatial.SpatialCoordinateSystem)
<hr>

**項目**

[Windows.Media.Capture.Frames.DepthMediaFrameFormat](/uwp/api/windows.media.capture.frames.depthmediaframeformat)

**[プロパティ]**


Windows.Media.Capture.Frames.DepthMediaFrameFormat <br /> Windows.Media.Capture.Frames.DepthMediaFrameFormat.DepthScaleInMeters <br /> Windows.Media.Capture.Frames.DepthMediaFrameFormat.VideoFormat
<hr>

**項目**

[Windows.Media.Capture.Frames.InfraredMediaFrame](/uwp/api/windows.media.capture.frames.infraredmediaframe)

**[プロパティ]**


Windows.Media.Capture.Frames.InfraredMediaFrame <br /> Windows.Media.Capture.Frames.InfraredMediaFrame.FrameReference <br /> Windows.Media.Capture.Frames.InfraredMediaFrame.IsIlluminated <br /> Windows.Media.Capture.Frames.InfraredMediaFrame.VideoMediaFrame
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameArrivedEventArgs](/uwp/api/windows.media.capture.frames.mediaframearrivedeventargs)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameArrivedEventArgs
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameFormat](/uwp/api/windows.media.capture.frames.mediaframeformat)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameFormat <br /> Windows.Media.Capture.Frames.MediaFrameFormat.FrameRate <br /> Windows.Media.Capture.Frames.MediaFrameFormat.MajorType <br /> Windows.Media.Capture.Frames.MediaFrameFormat.Properties <br /> Windows.Media.Capture.Frames.MediaFrameFormat.Subtype <br /> Windows.Media.Capture.Frames.MediaFrameFormat.VideoFormat
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameReader](/uwp/api/windows.media.capture.frames.mediaframereader)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameReader <br /> Windows.Media.Capture.Frames.MediaFrameReader.FrameArrived <br /> Windows.Media.Capture.Frames.MediaFrameReader.Close <br /> Windows.Media.Capture.Frames.MediaFrameReader.StartAsync <br /> Windows.Media.Capture.Frames.MediaFrameReader.StopAsync <br /> Windows.Media.Capture.Frames.MediaFrameReader.TryAcquireLatestFrame
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameReaderStartStatus](/uwp/api/windows.media.capture.frames.mediaframereaderstartstatus)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameReaderStartStatus <br /> Windows.Media.Capture.Frames.MediaFrameReaderStartStatus.DeviceNotAvailable <br /> Windows.Media.Capture.Frames.MediaFrameReaderStartStatus.OutputFormatNotSupported <br /> Windows.Media.Capture.Frames.MediaFrameReaderStartStatus.Success <br /> Windows.Media.Capture.Frames.MediaFrameReaderStartStatus.UnknownFailure
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameReference](/uwp/api/windows.media.capture.frames.mediaframereference)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameReference <br /> Windows.Media.Capture.Frames.MediaFrameReference.BufferMediaFrame <br /> Windows.Media.Capture.Frames.MediaFrameReference.CoordinateSystem <br /> Windows.Media.Capture.Frames.MediaFrameReference.Duration <br /> Windows.Media.Capture.Frames.MediaFrameReference.Format <br /> Windows.Media.Capture.Frames.MediaFrameReference.Properties <br /> Windows.Media.Capture.Frames.MediaFrameReference.SourceKind <br /> Windows.Media.Capture.Frames.MediaFrameReference.SystemRelativeTime <br /> Windows.Media.Capture.Frames.MediaFrameReference.VideoMediaFrame <br /> Windows.Media.Capture.Frames.MediaFrameReference.Close
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSource](/uwp/api/windows.media.capture.frames.mediaframesource)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSource <br /> Windows.Media.Capture.Frames.MediaFrameSource.Controller <br /> Windows.Media.Capture.Frames.MediaFrameSource.CurrentFormat <br /> Windows.Media.Capture.Frames.MediaFrameSource.Info <br /> Windows.Media.Capture.Frames.MediaFrameSource.SupportedFormats <br /> Windows.Media.Capture.Frames.MediaFrameSource.FormatChanged <br /> Windows.Media.Capture.Frames.MediaFrameSource.SetFormatAsync(Windows.Media.Capture.Frames.MediaFrameFormat) <br /> Windows.Media.Capture.Frames.MediaFrameSource.TryGetCameraIntrinsics(Windows.Media.Capture.Frames.MediaFrameFormat)
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceController](/uwp/api/windows.media.capture.frames.mediaframesourcecontroller)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceController <br /> Windows.Media.Capture.Frames.MediaFrameSourceController.VideoDeviceController <br /> Windows.Media.Capture.Frames.MediaFrameSourceController.GetPropertyAsync(System.String) <br /> Windows.Media.Capture.Frames.MediaFrameSourceController.SetPropertyAsync(System.String,System.Object)
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyResult](/uwp/api/windows.media.capture.frames.mediaframesourcegetpropertyresult)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyResult <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyResult.Status <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyResult.Value
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus](/uwp/api/windows.media.capture.frames.mediaframesourcegetpropertystatus)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus.DeviceNotAvailable <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus.NotSupported <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus.Success <br /> Windows.Media.Capture.Frames.MediaFrameSourceGetPropertyStatus.UnknownFailure
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceGroup](/uwp/api/windows.media.capture.frames.mediaframesourcegroup)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceGroup <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.DisplayName <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.Id <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.SourceInfos <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.FindAllAsync <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.FromIdAsync(System.String) <br /> Windows.Media.Capture.Frames.MediaFrameSourceGroup.GetDeviceSelector
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceInfo](/uwp/api/windows.media.capture.frames.mediaframesourceinfo)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceInfo <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.CoordinateSystem <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.DeviceInformation <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.Id <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.MediaStreamType <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.Properties <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.SourceGroup <br /> Windows.Media.Capture.Frames.MediaFrameSourceInfo.SourceKind
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceKind](/uwp/api/windows.media.capture.frames.mediaframesourcekind)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceKind <br /> Windows.Media.Capture.Frames.MediaFrameSourceKind.Color <br /> Windows.Media.Capture.Frames.MediaFrameSourceKind.Custom <br /> Windows.Media.Capture.Frames.MediaFrameSourceKind.Depth <br /> Windows.Media.Capture.Frames.MediaFrameSourceKind.Infrared
<hr>

**項目**

[Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus](/uwp/api/windows.media.capture.frames.mediaframesourcesetpropertystatus)

**[プロパティ]**


Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.DeviceNotAvailable <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.InvalidValue <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.NotInControl <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.NotSupported <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.Success <br /> Windows.Media.Capture.Frames.MediaFrameSourceSetPropertyStatus.UnknownFailure
<hr>

**項目**

[Windows.Media.Capture.Frames.VideoMediaFrame](/uwp/api/windows.media.capture.frames.videomediaframe)

**[プロパティ]**


Windows.Media.Capture.Frames.VideoMediaFrame <br /> Windows.Media.Capture.Frames.VideoMediaFrame.CameraIntrinsics <br /> Windows.Media.Capture.Frames.VideoMediaFrame.DepthMediaFrame <br /> Windows.Media.Capture.Frames.VideoMediaFrame.Direct3DSurface <br /> Windows.Media.Capture.Frames.VideoMediaFrame.FrameReference <br /> Windows.Media.Capture.Frames.VideoMediaFrame.InfraredMediaFrame <br /> Windows.Media.Capture.Frames.VideoMediaFrame.SoftwareBitmap <br /> Windows.Media.Capture.Frames.VideoMediaFrame.VideoFormat <br /> Windows.Media.Capture.Frames.VideoMediaFrame.GetVideoFrame
<hr>

**項目**

[Windows.Media.Capture.Frames.VideoMediaFrameFormat](/uwp/api/windows.media.capture.frames.videomediaframeformat)

**[プロパティ]**


Windows.Media.Capture.Frames.VideoMediaFrameFormat <br /> Windows.Media.Capture.Frames.VideoMediaFrameFormat.DepthFormat <br /> Windows.Media.Capture.Frames.VideoMediaFrameFormat.Height <br /> Windows.Media.Capture.Frames.VideoMediaFrameFormat.MediaFrameFormat <br /> Windows.Media.Capture.Frames.VideoMediaFrameFormat.Width
<hr>

**項目**

[Windows.Media.Core.AudioDecoderDegradation](/uwp/api/windows.media.core.audiodecoderdegradation)

**[プロパティ]**


Windows.Media.Core.AudioDecoderDegradation <br /> Windows.Media.Core.AudioDecoderDegradation.DownmixTo2Channels <br /> Windows.Media.Core.AudioDecoderDegradation.DownmixTo6Channels <br /> Windows.Media.Core.AudioDecoderDegradation.DownmixTo8Channels <br /> Windows.Media.Core.AudioDecoderDegradation.None
<hr>

**項目**

[Windows.Media.Core.AudioDecoderDegradationReason](/uwp/api/windows.media.core.audiodecoderdegradationreason)

**[プロパティ]**


Windows.Media.Core.AudioDecoderDegradationReason <br /> Windows.Media.Core.AudioDecoderDegradationReason.LicensingRequirement <br /> Windows.Media.Core.AudioDecoderDegradationReason.None
<hr>

**項目**

[Windows.Media.Core.AudioTrackOpenFailedEventArgs](/uwp/api/windows.media.core.audiotrackopenfailedeventargs)

**[プロパティ]**


Windows.Media.Core.AudioTrackOpenFailedEventArgs <br /> Windows.Media.Core.AudioTrackOpenFailedEventArgs.ExtendedError
<hr>

**項目**

[Windows.Media.Core.AudioTrackSupportInfo](/uwp/api/windows.media.core.audiotracksupportinfo)

**[プロパティ]**


Windows.Media.Core.AudioTrackSupportInfo <br /> Windows.Media.Core.AudioTrackSupportInfo.DecoderStatus <br /> Windows.Media.Core.AudioTrackSupportInfo.Degradation <br /> Windows.Media.Core.AudioTrackSupportInfo.DegradationReason <br /> Windows.Media.Core.AudioTrackSupportInfo.MediaSourceStatus
<hr>

**項目**

[Windows.Media.Core.MediaDecoderStatus](/uwp/api/windows.media.core.mediadecoderstatus)

**[プロパティ]**


Windows.Media.Core.MediaDecoderStatus <br /> Windows.Media.Core.MediaDecoderStatus.Degraded <br /> Windows.Media.Core.MediaDecoderStatus.FullySupported <br /> Windows.Media.Core.MediaDecoderStatus.UnsupportedEncoderProperties <br /> Windows.Media.Core.MediaDecoderStatus.UnsupportedSubtype
<hr>

**項目**

[Windows.Media.Core.MediaSourceStatus](/uwp/api/windows.media.core.mediasourcestatus)

**[プロパティ]**


Windows.Media.Core.MediaSourceStatus <br /> Windows.Media.Core.MediaSourceStatus.FullySupported <br /> Windows.Media.Core.MediaSourceStatus.Unknown
<hr>

**項目**

[Windows.Media.Core.MediaStreamSourceSampleRenderedEventArgs](/uwp/api/windows.media.core.mediastreamsourcesamplerenderedeventargs)

**[プロパティ]**


Windows.Media.Core.MediaStreamSourceSampleRenderedEventArgs <br /> Windows.Media.Core.MediaStreamSourceSampleRenderedEventArgs.SampleLag
<hr>

**項目**

[Windows.Media.Core.VideoTrackOpenFailedEventArgs](/uwp/api/windows.media.core.videotrackopenfailedeventargs)

**[プロパティ]**


Windows.Media.Core.VideoTrackOpenFailedEventArgs <br /> Windows.Media.Core.VideoTrackOpenFailedEventArgs.ExtendedError
<hr>

**項目**

[Windows.Media.Core.VideoTrackSupportInfo](/uwp/api/windows.media.core.videotracksupportinfo)

**[プロパティ]**


Windows.Media.Core.VideoTrackSupportInfo <br /> Windows.Media.Core.VideoTrackSupportInfo.DecoderStatus <br /> Windows.Media.Core.VideoTrackSupportInfo.MediaSourceStatus
<hr>

**項目**

[Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper](/uwp/api/windows.media.devices.core.depthcorrelatedcoordinatemapper)

**[プロパティ]**


Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper <br /> Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper.Close <br /> Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper.MapPoint(Windows.Foundation.Point,Windows.Perception.Spatial.SpatialCoordinateSystem,Windows.Media.Devices.Core.CameraIntrinsics) <br /> Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper.MapPoints(Windows.Foundation.Point[],Windows.Perception.Spatial.SpatialCoordinateSystem,Windows.Media.Devices.Core.CameraIntrinsics,Windows.Foundation.Point[]) <br /> Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper.UnprojectPoint(Windows.Foundation.Point,Windows.Perception.Spatial.SpatialCoordinateSystem) <br /> Windows.Media.Devices.Core.DepthCorrelatedCoordinateMapper.UnprojectPoints(Windows.Foundation.Point[],Windows.Perception.Spatial.SpatialCoordinateSystem,Windows.Foundation.Numerics.Vector3[])
<hr>

**項目**

[Windows.Media.Import.PhotoImportSubfolderDateFormat](/uwp/api/windows.media.import.photoimportsubfolderdateformat)

**[プロパティ]**


Windows.Media.Import.PhotoImportSubfolderDateFormat <br /> Windows.Media.Import.PhotoImportSubfolderDateFormat.Year <br /> Windows.Media.Import.PhotoImportSubfolderDateFormat.YearMonth <br /> Windows.Media.Import.PhotoImportSubfolderDateFormat.YearMonthDay
<hr>

**項目**

[Windows.Media.MediaProperties.StereoscopicVideoPackingMode](/uwp/api/windows.media.mediaproperties.stereoscopicvideopackingmode)

**[プロパティ]**


Windows.Media.MediaProperties.StereoscopicVideoPackingMode <br /> Windows.Media.MediaProperties.StereoscopicVideoPackingMode.None <br /> Windows.Media.MediaProperties.StereoscopicVideoPackingMode.SideBySide <br /> Windows.Media.MediaProperties.StereoscopicVideoPackingMode.TopBottom
<hr>

**項目**

[Windows.Media.Playback.MediaBreak](/uwp/api/windows.media.playback.mediabreak)

**[プロパティ]**


Windows.Media.Playback.MediaBreak <br /> Windows.Media.Playback.MediaBreak.#ctor(Windows.Media.Playback.MediaBreakInsertionMethod) <br /> Windows.Media.Playback.MediaBreak.#ctor(Windows.Media.Playback.MediaBreakInsertionMethod,Windows.Foundation.TimeSpan) <br /> Windows.Media.Playback.MediaBreak.CanStart <br /> Windows.Media.Playback.MediaBreak.CustomProperties <br /> Windows.Media.Playback.MediaBreak.InsertionMethod <br /> Windows.Media.Playback.MediaBreak.PlaybackList <br /> Windows.Media.Playback.MediaBreak.PresentationPosition
<hr>

**項目**

[Windows.Media.Playback.MediaBreakEndedEventArgs](/uwp/api/windows.media.playback.mediabreakendedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaBreakEndedEventArgs <br /> Windows.Media.Playback.MediaBreakEndedEventArgs.MediaBreak
<hr>

**項目**

[Windows.Media.Playback.MediaBreakInsertionMethod](/uwp/api/windows.media.playback.mediabreakinsertionmethod)

**[プロパティ]**


Windows.Media.Playback.MediaBreakInsertionMethod <br /> Windows.Media.Playback.MediaBreakInsertionMethod.Interrupt <br /> Windows.Media.Playback.MediaBreakInsertionMethod.Replace
<hr>

**項目**

[Windows.Media.Playback.MediaBreakManager](/uwp/api/windows.media.playback.mediabreakmanager)

**[プロパティ]**


Windows.Media.Playback.MediaBreakManager <br /> Windows.Media.Playback.MediaBreakManager.CurrentBreak <br /> Windows.Media.Playback.MediaBreakManager.PlaybackSession <br /> Windows.Media.Playback.MediaBreakManager.BreakEnded <br /> Windows.Media.Playback.MediaBreakManager.BreakSkipped <br /> Windows.Media.Playback.MediaBreakManager.BreaksSeekedOver <br /> Windows.Media.Playback.MediaBreakManager.BreakStarted <br /> Windows.Media.Playback.MediaBreakManager.PlayBreak(Windows.Media.Playback.MediaBreak) <br /> Windows.Media.Playback.MediaBreakManager.SkipCurrentBreak
<hr>

**項目**

[Windows.Media.Playback.MediaBreakSchedule](/uwp/api/windows.media.playback.mediabreakschedule)

**[プロパティ]**


Windows.Media.Playback.MediaBreakSchedule <br /> Windows.Media.Playback.MediaBreakSchedule.MidrollBreaks <br /> Windows.Media.Playback.MediaBreakSchedule.PlaybackItem <br /> Windows.Media.Playback.MediaBreakSchedule.PostrollBreak <br /> Windows.Media.Playback.MediaBreakSchedule.PrerollBreak <br /> Windows.Media.Playback.MediaBreakSchedule.ScheduleChanged <br /> Windows.Media.Playback.MediaBreakSchedule.InsertMidrollBreak(Windows.Media.Playback.MediaBreak) <br /> Windows.Media.Playback.MediaBreakSchedule.RemoveMidrollBreak(Windows.Media.Playback.MediaBreak)
<hr>

**項目**

[Windows.Media.Playback.MediaBreakSeekedOverEventArgs](/uwp/api/windows.media.playback.mediabreakseekedovereventargs)

**[プロパティ]**


Windows.Media.Playback.MediaBreakSeekedOverEventArgs <br /> Windows.Media.Playback.MediaBreakSeekedOverEventArgs.NewPosition <br /> Windows.Media.Playback.MediaBreakSeekedOverEventArgs.OldPosition <br /> Windows.Media.Playback.MediaBreakSeekedOverEventArgs.SeekedOverBreaks
<hr>

**項目**

[Windows.Media.Playback.MediaBreakSkippedEventArgs](/uwp/api/windows.media.playback.mediabreakskippedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaBreakSkippedEventArgs <br /> Windows.Media.Playback.MediaBreakSkippedEventArgs.MediaBreak
<hr>

**項目**

[Windows.Media.Playback.MediaBreakStartedEventArgs](/uwp/api/windows.media.playback.mediabreakstartedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaBreakStartedEventArgs <br /> Windows.Media.Playback.MediaBreakStartedEventArgs.MediaBreak
<hr>

**項目**

[Windows.Media.Playback.MediaCommandEnablingRule](/uwp/api/windows.media.playback.mediacommandenablingrule)

**[プロパティ]**


Windows.Media.Playback.MediaCommandEnablingRule <br /> Windows.Media.Playback.MediaCommandEnablingRule.Always <br /> Windows.Media.Playback.MediaCommandEnablingRule.Auto <br /> Windows.Media.Playback.MediaCommandEnablingRule.Never
<hr>

**項目**

[Windows.Media.Playback.MediaItemDisplayProperties](/uwp/api/windows.media.playback.mediaitemdisplayproperties)

**[プロパティ]**


Windows.Media.Playback.MediaItemDisplayProperties <br /> Windows.Media.Playback.MediaItemDisplayProperties.MusicProperties <br /> Windows.Media.Playback.MediaItemDisplayProperties.Thumbnail <br /> Windows.Media.Playback.MediaItemDisplayProperties.Type <br /> Windows.Media.Playback.MediaItemDisplayProperties.VideoProperties <br /> Windows.Media.Playback.MediaItemDisplayProperties.ClearAll
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManager](/uwp/api/windows.media.playback.mediaplaybackcommandmanager)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManager <br /> Windows.Media.Playback.MediaPlaybackCommandManager.AutoRepeatModeBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.FastForwardBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.IsEnabled <br /> Windows.Media.Playback.MediaPlaybackCommandManager.MediaPlayer <br /> Windows.Media.Playback.MediaPlaybackCommandManager.NextBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PauseBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PlayBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PositionBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PreviousBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.RateBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.RewindBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.ShuffleBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManager.AutoRepeatModeReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.FastForwardReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.NextReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PauseReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PlayReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PositionReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.PreviousReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.RateReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.RewindReceived <br /> Windows.Media.Playback.MediaPlaybackCommandManager.ShuffleReceived
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerAutoRepeatModeReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerautorepeatmodereceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerAutoRepeatModeReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerAutoRepeatModeReceivedEventArgs.AutoRepeatMode <br /> Windows.Media.Playback.MediaPlaybackCommandManagerAutoRepeatModeReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerAutoRepeatModeReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior](/uwp/api/windows.media.playback.mediaplaybackcommandmanagercommandbehavior)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior <br /> Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior.CommandManager <br /> Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior.EnablingRule <br /> Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior.IsEnabled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerCommandBehavior.IsEnabledChanged
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerFastForwardReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerfastforwardreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerFastForwardReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerFastForwardReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerFastForwardReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerNextReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagernextreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerNextReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerNextReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerNextReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerPauseReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerpausereceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerPauseReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPauseReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPauseReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerPlayReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerplayreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerPlayReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPlayReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPlayReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerPositionReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerpositionreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerPositionReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPositionReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPositionReceivedEventArgs.Position <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPositionReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerPreviousReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerpreviousreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerPreviousReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPreviousReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerPreviousReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerRateReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerratereceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerRateReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerRateReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerRateReceivedEventArgs.PlaybackRate <br /> Windows.Media.Playback.MediaPlaybackCommandManagerRateReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerRewindReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagerrewindreceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerRewindReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerRewindReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerRewindReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackCommandManagerShuffleReceivedEventArgs](/uwp/api/windows.media.playback.mediaplaybackcommandmanagershufflereceivedeventargs)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackCommandManagerShuffleReceivedEventArgs <br /> Windows.Media.Playback.MediaPlaybackCommandManagerShuffleReceivedEventArgs.Handled <br /> Windows.Media.Playback.MediaPlaybackCommandManagerShuffleReceivedEventArgs.IsShuffleRequested <br /> Windows.Media.Playback.MediaPlaybackCommandManagerShuffleReceivedEventArgs.GetDeferral
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackSession](/uwp/api/windows.media.playback.mediaplaybacksession)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackSession <br /> Windows.Media.Playback.MediaPlaybackSession.BufferingProgress <br /> Windows.Media.Playback.MediaPlaybackSession.CanPause <br /> Windows.Media.Playback.MediaPlaybackSession.CanSeek <br /> Windows.Media.Playback.MediaPlaybackSession.DownloadProgress <br /> Windows.Media.Playback.MediaPlaybackSession.IsProtected <br /> Windows.Media.Playback.MediaPlaybackSession.MediaPlayer <br /> Windows.Media.Playback.MediaPlaybackSession.NaturalDuration <br /> Windows.Media.Playback.MediaPlaybackSession.NaturalVideoHeight <br /> Windows.Media.Playback.MediaPlaybackSession.NaturalVideoWidth <br /> Windows.Media.Playback.MediaPlaybackSession.NormalizedSourceRect <br /> Windows.Media.Playback.MediaPlaybackSession.PlaybackRate <br /> Windows.Media.Playback.MediaPlaybackSession.PlaybackState <br /> Windows.Media.Playback.MediaPlaybackSession.Position <br /> Windows.Media.Playback.MediaPlaybackSession.StereoscopicVideoPackingMode <br /> Windows.Media.Playback.MediaPlaybackSession.BufferingEnded <br /> Windows.Media.Playback.MediaPlaybackSession.BufferingProgressChanged <br /> Windows.Media.Playback.MediaPlaybackSession.BufferingStarted <br /> Windows.Media.Playback.MediaPlaybackSession.DownloadProgressChanged <br /> Windows.Media.Playback.MediaPlaybackSession.NaturalDurationChanged <br /> Windows.Media.Playback.MediaPlaybackSession.NaturalVideoSizeChanged <br /> Windows.Media.Playback.MediaPlaybackSession.PlaybackRateChanged <br /> Windows.Media.Playback.MediaPlaybackSession.PlaybackStateChanged <br /> Windows.Media.Playback.MediaPlaybackSession.PositionChanged <br /> Windows.Media.Playback.MediaPlaybackSession.SeekCompleted
<hr>

**項目**

[Windows.Media.Playback.MediaPlaybackState](/uwp/api/windows.media.playback.mediaplaybackstate)

**[プロパティ]**


Windows.Media.Playback.MediaPlaybackState <br /> Windows.Media.Playback.MediaPlaybackState.Buffering <br /> Windows.Media.Playback.MediaPlaybackState.None <br /> Windows.Media.Playback.MediaPlaybackState.Opening <br /> Windows.Media.Playback.MediaPlaybackState.Paused <br /> Windows.Media.Playback.MediaPlaybackState.Playing
<hr>

**項目**

[Windows.Media.Playback.MediaPlayerSurface](/uwp/api/windows.media.playback.mediaplayersurface)

**[プロパティ]**


Windows.Media.Playback.MediaPlayerSurface <br /> Windows.Media.Playback.MediaPlayerSurface.CompositionSurface <br /> Windows.Media.Playback.MediaPlayerSurface.Compositor <br /> Windows.Media.Playback.MediaPlayerSurface.MediaPlayer <br /> Windows.Media.Playback.MediaPlayerSurface.Close
<hr>

**項目**

[Windows.Media.Playback.StereoscopicVideoRenderMode](/uwp/api/windows.media.playback.stereoscopicvideorendermode)

**[プロパティ]**


Windows.Media.Playback.StereoscopicVideoRenderMode <br /> Windows.Media.Playback.StereoscopicVideoRenderMode.Mono <br /> Windows.Media.Playback.StereoscopicVideoRenderMode.Stereo
<hr>

**項目**

[Windows.Media.Protection.HdcpProtection](/uwp/api/windows.media.protection.hdcpprotection)

**[プロパティ]**


Windows.Media.Protection.HdcpProtection <br /> Windows.Media.Protection.HdcpProtection.Off <br /> Windows.Media.Protection.HdcpProtection.On <br /> Windows.Media.Protection.HdcpProtection.OnWithTypeEnforcement
<hr>

**項目**

[Windows.Media.Protection.HdcpSession](/uwp/api/windows.media.protection.hdcpsession)

**[プロパティ]**


Windows.Media.Protection.HdcpSession <br /> Windows.Media.Protection.HdcpSession.#ctor <br /> Windows.Media.Protection.HdcpSession.ProtectionChanged <br /> Windows.Media.Protection.HdcpSession.Close <br /> Windows.Media.Protection.HdcpSession.GetEffectiveProtection <br /> Windows.Media.Protection.HdcpSession.IsEffectiveProtectionAtLeast(Windows.Media.Protection.HdcpProtection) <br /> Windows.Media.Protection.HdcpSession.SetDesiredMinProtectionAsync(Windows.Media.Protection.HdcpProtection)
<hr>

**項目**

[Windows.Media.Protection.HdcpSetProtectionResult](/uwp/api/windows.media.protection.hdcpsetprotectionresult)

**[プロパティ]**


Windows.Media.Protection.HdcpSetProtectionResult <br /> Windows.Media.Protection.HdcpSetProtectionResult.NotSupported <br /> Windows.Media.Protection.HdcpSetProtectionResult.Success <br /> Windows.Media.Protection.HdcpSetProtectionResult.TimedOut <br /> Windows.Media.Protection.HdcpSetProtectionResult.UnknownFailure
<hr>

**項目**

[Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser](/uwp/api/windows.networking.pushnotifications.pushnotificationchannelmanagerforuser)

**[プロパティ]**


Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser <br /> Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser.User <br /> Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser.CreatePushNotificationChannelForApplicationAsync <br /> Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser.CreatePushNotificationChannelForApplicationAsync(System.String) <br /> Windows.Networking.PushNotifications.PushNotificationChannelManagerForUser.CreatePushNotificationChannelForSecondaryTileAsync(System.String)
<hr>

**項目**

[Windows.Networking.Sockets.IWebSocketControl2](/uwp/api/windows.networking.sockets.iwebsocketcontrol2)

**[プロパティ]**


Windows.Networking.Sockets.IWebSocketControl2 <br /> Windows.Networking.Sockets.IWebSocketControl2.IgnorableServerCertificateErrors
<hr>

**項目**

[Windows.Networking.Sockets.IWebSocketInformation2](/uwp/api/windows.networking.sockets.iwebsocketinformation2)

**[プロパティ]**


Windows.Networking.Sockets.IWebSocketInformation2 <br /> Windows.Networking.Sockets.IWebSocketInformation2.ServerCertificate <br /> Windows.Networking.Sockets.IWebSocketInformation2.ServerCertificateErrors <br /> Windows.Networking.Sockets.IWebSocketInformation2.ServerCertificateErrorSeverity <br /> Windows.Networking.Sockets.IWebSocketInformation2.ServerIntermediateCertificates
<hr>

**項目**

[Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs](/uwp/api/windows.networking.sockets.websocketservercustomvalidationrequestedeventargs)

**[プロパティ]**


Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.ServerCertificate <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.ServerCertificateErrors <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.ServerCertificateErrorSeverity <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.ServerIntermediateCertificates <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.GetDeferral <br /> Windows.Networking.Sockets.WebSocketServerCustomValidationRequestedEventArgs.Reject
<hr>

**項目**

[Windows.Networking.Vpn.VpnManagementConnectionStatus](/uwp/api/windows.networking.vpn.vpnmanagementconnectionstatus)

**[プロパティ]**


Windows.Networking.Vpn.VpnManagementConnectionStatus <br /> Windows.Networking.Vpn.VpnManagementConnectionStatus.Connected <br /> Windows.Networking.Vpn.VpnManagementConnectionStatus.Connecting <br /> Windows.Networking.Vpn.VpnManagementConnectionStatus.Disconnected <br /> Windows.Networking.Vpn.VpnManagementConnectionStatus.Disconnecting
<hr>

**項目**

[Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo](/uwp/api/windows.security.authentication.identity.enterprisekeycredentialregistrationinfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo.KeyId <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo.KeyName <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo.Subject <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo.TenantId <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationInfo.TenantName
<hr>

**項目**

[Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationManager](/uwp/api/windows.security.authentication.identity.enterprisekeycredentialregistrationmanager)

**[プロパティ]**


Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationManager <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationManager.Current <br /> Windows.Security.Authentication.Identity.EnterpriseKeyCredentialRegistrationManager.GetRegistrationsAsync
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorauthenticationmanager)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.Current <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.AddDeviceAsync(System.String,System.String,System.String) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.ApproveSessionAsync(Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus,System.String,System.String,Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.ApproveSessionAsync(Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus,Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.DenySessionAsync(System.String,System.String,Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.DenySessionAsync(Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.GetOneTimePassCodeAsync(System.String,System.UInt32) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.GetSessionsAndUnregisteredAccountsAsync(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.GetSessionsAsync(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.RemoveDeviceAsync(System.String) <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationManager.UpdateWnsChannelAsync(System.String,System.String)
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorauthenticationtype)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType.Device <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorAuthenticationType.User
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorGetSessionsResult](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorgetsessionsresult)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorGetSessionsResult <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorGetSessionsResult.ServiceResponse <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorGetSessionsResult.Sessions
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactoronetimecodedinfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo.Code <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo.ServiceResponse <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo.TimeInterval <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorOneTimeCodedInfo.TimeToLive
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorserviceresponse)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.DeviceIdChanged <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.DeviceNotFound <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.Error <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.FlowDisabled <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.InvalidOperation <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.InvalidSessionId <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.InvalidSessionType <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.InvalidStateTransition <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.NgcDisabledByServer <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.NgcKeyNotFoundOnServer <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.NgcNonceExpired <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.NgcNotSetup <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.NoNetworkConnection <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.OperationCanceledByUser <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.ServiceUnavailable <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.SessionAlreadyApproved <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.SessionAlreadyDenied <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.SessionExpired <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.SessionNotApproved <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.Success <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.TotpSetupDenied <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorServiceResponse.UIRequired
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionApprovalStatus](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorsessionapprovalstatus)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionApprovalStatus <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionApprovalStatus.Approved <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionApprovalStatus.Denied <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionApprovalStatus.Pending
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorsessionauthenticationstatus)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus.Authenticated <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionAuthenticationStatus.Unauthenticated
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorsessioninfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.ApprovalStatus <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.AuthenticationType <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.DisplaySessionId <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.ExpirationTime <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.RequestTime <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.SessionId <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorSessionInfo.UserAccountId
<hr>

**項目**

[Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorUnregisteredAccountsAndSessionInfo](/uwp/api/windows.security.authentication.identity.core.microsoftaccountmultifactorunregisteredaccountsandsessioninfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorUnregisteredAccountsAndSessionInfo <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorUnregisteredAccountsAndSessionInfo.ServiceResponse <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorUnregisteredAccountsAndSessionInfo.Sessions <br /> Windows.Security.Authentication.Identity.Core.MicrosoftAccountMultiFactorUnregisteredAccountsAndSessionInfo.UnregisteredAccounts
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthentication)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.DeviceConfigurationData <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.DeviceNonce <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.ServiceAuthenticationHmac <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.SessionNonce <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.AuthenticationStageChanged <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.AbortAuthenticationAsync(System.String) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.FinishAuthenticationAsync(Windows.Storage.Streams.IBuffer,Windows.Storage.Streams.IBuffer) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.GetAuthenticationStageInfoAsync <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.ShowNotificationMessageAsync(System.String,Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthentication.StartAuthenticationAsync(System.String,Windows.Storage.Streams.IBuffer)
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationmessage)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.BluetoothIsDisabled <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.DeviceNeedsAttention <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.DisabledByPolicy <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.ExtraTapIsRequired <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.HoldFinger <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.Invalid <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.LookingForDevice <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.LookingForDevicePluggedin <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.NfcIsDisabled <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.ReadyToSignIn <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.ReregisterRequired <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.SayPassphrase <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.ScanFinger <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.SwipeUpWelcome <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.TapOnDeviceRequired <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.TapWelcome <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.TryAgain <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.UnauthorizedUser <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.UseAnotherSignInOption <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationMessage.WiFiIsDisabled
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationResult](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationresult)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationResult <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationResult.Authentication <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationResult.Status
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationScenario](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationscenario)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationScenario <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationScenario.CredentialPrompt <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationScenario.SignIn
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationstage)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.CollectingCredential <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.CredentialAuthenticated <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.CredentialCollected <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.NotStarted <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.ReadyForLock <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.StoppingAuthentication <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.SuspendingAuthentication <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStage.WaitingForUserConfirmation
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageChangedEventArgs](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationstagechangedeventargs)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageChangedEventArgs <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageChangedEventArgs.StageInfo
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageInfo](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationstageinfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageInfo <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageInfo.DeviceId <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageInfo.Scenario <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStageInfo.Stage
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorauthenticationstatus)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus.DisabledByPolicy <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus.Failed <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus.InvalidAuthenticationStage <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus.Started <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorAuthenticationStatus.UnknownDevice
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactordevicecapabilities)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.ConfirmUserIntentToAuthenticate <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.HMacSha256 <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.None <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.SecureStorage <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.StoreKeys <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.SupportSecureUserPresenceCheck <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities.TransmittedDataIsEncrypted
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceFindScope](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactordevicefindscope)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceFindScope <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceFindScope.AllUsers <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceFindScope.User
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorFinishAuthenticationStatus](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorfinishauthenticationstatus)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorFinishAuthenticationStatus <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorFinishAuthenticationStatus.Completed <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorFinishAuthenticationStatus.Failed <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorFinishAuthenticationStatus.NonceExpired
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorinfo)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo.DeviceConfigurationData <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo.DeviceFriendlyName <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo.DeviceId <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorInfo.DeviceModelNumber
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorregistration)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.AbortRegisteringDeviceAsync(System.String) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.FindAllRegisteredDeviceInfoAsync(Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceFindScope) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.FinishRegisteringDeviceAsync(Windows.Storage.Streams.IBuffer) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.RequestStartRegisteringDeviceAsync(System.String,Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorDeviceCapabilities,System.String,System.String,Windows.Storage.Streams.IBuffer,Windows.Storage.Streams.IBuffer) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.UnregisterDeviceAsync(System.String) <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistration.UpdateDeviceConfigurationDataAsync(System.String,Windows.Storage.Streams.IBuffer)
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationResult](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorregistrationresult)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationResult <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationResult.Registration <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationResult.Status
<hr>

**項目**

[Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus](/uwp/api/windows.security.authentication.identity.provider.secondaryauthenticationfactorregistrationstatus)

**[プロパティ]**


Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus.CanceledByUser <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus.DisabledByPolicy <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus.Failed <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus.PinSetupRequired <br /> Windows.Security.Authentication.Identity.Provider.SecondaryAuthenticationFactorRegistrationStatus.Started
<hr>

**項目**

[Windows.Security.Authentication.Web.Core.WebAccountEventArgs](/uwp/api/windows.security.authentication.web.core.webaccounteventargs)

**[プロパティ]**


Windows.Security.Authentication.Web.Core.WebAccountEventArgs <br /> Windows.Security.Authentication.Web.Core.WebAccountEventArgs.Account
<hr>

**項目**

[Windows.Security.Authentication.Web.Core.WebAccountMonitor](/uwp/api/windows.security.authentication.web.core.webaccountmonitor)

**[プロパティ]**


Windows.Security.Authentication.Web.Core.WebAccountMonitor <br /> Windows.Security.Authentication.Web.Core.WebAccountMonitor.DefaultSignInAccountChanged <br /> Windows.Security.Authentication.Web.Core.WebAccountMonitor.Removed <br /> Windows.Security.Authentication.Web.Core.WebAccountMonitor.Updated
<hr>

**項目**

[Windows.Security.Cryptography.Certificates.StandardCertificateStoreNames](/uwp/api/windows.security.cryptography.certificates.standardcertificatestorenames)

**[プロパティ]**


Windows.Security.Cryptography.Certificates.StandardCertificateStoreNames <br /> Windows.Security.Cryptography.Certificates.StandardCertificateStoreNames.IntermediateCertificationAuthorities <br /> Windows.Security.Cryptography.Certificates.StandardCertificateStoreNames.Personal <br /> Windows.Security.Cryptography.Certificates.StandardCertificateStoreNames.TrustedRootCertificationAuthorities
<hr>

**項目**

[Windows.Security.Cryptography.Certificates.UserCertificateStore](/uwp/api/windows.security.cryptography.certificates.usercertificatestore)

**[プロパティ]**


Windows.Security.Cryptography.Certificates.UserCertificateStore <br /> Windows.Security.Cryptography.Certificates.UserCertificateStore.Name <br /> Windows.Security.Cryptography.Certificates.UserCertificateStore.RequestAddAsync(Windows.Security.Cryptography.Certificates.Certificate) <br /> Windows.Security.Cryptography.Certificates.UserCertificateStore.RequestDeleteAsync(Windows.Security.Cryptography.Certificates.Certificate)
<hr>

**項目**

[Windows.Services.Maps.MapLocationDesiredAccuracy](/uwp/api/windows.services.maps.maplocationdesiredaccuracy)

**[プロパティ]**


Windows.Services.Maps.MapLocationDesiredAccuracy <br /> Windows.Services.Maps.MapLocationDesiredAccuracy.High <br /> Windows.Services.Maps.MapLocationDesiredAccuracy.Low <br /> Windows.Services.Maps.MapLocationFinder.FindLocationsAtAsync(Windows.Devices.Geolocation.Geopoint,Windows.Services.Maps.MapLocationDesiredAccuracy)
<hr>

**項目**

[Windows.Storage.StorageLibraryChange](/uwp/api/windows.storage.storagelibrarychange)

**[プロパティ]**


Windows.Storage.StorageLibraryChange <br /> Windows.Storage.StorageLibraryChange.ChangeType <br /> Windows.Storage.StorageLibraryChange.Path <br /> Windows.Storage.StorageLibraryChange.PreviousPath <br /> Windows.Storage.StorageLibraryChange.GetStorageItemAsync <br /> Windows.Storage.StorageLibraryChange.IsOfType(Windows.Storage.StorageItemTypes)
<hr>

**項目**

[Windows.Storage.StorageLibraryChangeReader](/uwp/api/windows.storage.storagelibrarychangereader)

**[プロパティ]**


Windows.Storage.StorageLibraryChangeReader <br /> Windows.Storage.StorageLibraryChangeReader.AcceptChangesAsync <br /> Windows.Storage.StorageLibraryChangeReader.ReadBatchAsync
<hr>

**項目**

[Windows.Storage.StorageLibraryChangeTracker](/uwp/api/windows.storage.storagelibrarychangetracker)

**[プロパティ]**


Windows.Storage.StorageLibraryChangeTracker <br /> Windows.Storage.StorageLibraryChangeTracker.Enable <br /> Windows.Storage.StorageLibraryChangeTracker.GetChangeReader <br /> Windows.Storage.StorageLibraryChangeTracker.Reset
<hr>

**項目**

[Windows.Storage.StorageLibraryChangeType](/uwp/api/windows.storage.storagelibrarychangetype)

**[プロパティ]**


Windows.Storage.StorageLibraryChangeType <br /> Windows.Storage.StorageLibraryChangeType.ChangeTrackingLost <br /> Windows.Storage.StorageLibraryChangeType.ContentsChanged <br /> Windows.Storage.StorageLibraryChangeType.ContentsReplaced <br /> Windows.Storage.StorageLibraryChangeType.Created <br /> Windows.Storage.StorageLibraryChangeType.Deleted <br /> Windows.Storage.StorageLibraryChangeType.EncryptionChanged <br /> Windows.Storage.StorageLibraryChangeType.IndexingStatusChanged <br /> Windows.Storage.StorageLibraryChangeType.MovedIntoLibrary <br /> Windows.Storage.StorageLibraryChangeType.MovedOrRenamed <br /> Windows.Storage.StorageLibraryChangeType.MovedOutOfLibrary
<hr>

**項目**

[Windows.System.LaunchFileStatus](/uwp/api/windows.system.launchfilestatus)

**[プロパティ]**


Windows.System.LaunchFileStatus <br /> Windows.System.LaunchFileStatus.AppUnavailable <br /> Windows.System.LaunchFileStatus.DeniedByPolicy <br /> Windows.System.LaunchFileStatus.FileTypeNotSupported <br /> Windows.System.LaunchFileStatus.Success <br /> Windows.System.LaunchFileStatus.Unknown
<hr>

**項目**

[Windows.System.RemoteLauncher](/uwp/api/windows.system.remotelauncher)

**[プロパティ]**


Windows.System.RemoteLauncher <br /> Windows.System.RemoteLauncher.LaunchUriAsync(Windows.System.RemoteSystems.RemoteSystemConnectionRequest,Windows.Foundation.Uri) <br /> Windows.System.RemoteLauncher.LaunchUriAsync(Windows.System.RemoteSystems.RemoteSystemConnectionRequest,Windows.Foundation.Uri,Windows.System.RemoteLauncherOptions) <br /> Windows.System.RemoteLauncher.LaunchUriAsync(Windows.System.RemoteSystems.RemoteSystemConnectionRequest,Windows.Foundation.Uri,Windows.System.RemoteLauncherOptions,Windows.Foundation.Collections.ValueSet)
<hr>

**項目**

[Windows.System.RemoteLauncherOptions](/uwp/api/windows.system.remotelauncheroptions)

**[プロパティ]**


Windows.System.RemoteLauncherOptions <br /> Windows.System.RemoteLauncherOptions.#ctor <br /> Windows.System.RemoteLauncherOptions.FallbackUri <br /> Windows.System.RemoteLauncherOptions.PreferredAppIds
<hr>

**項目**

[Windows.System.RemoteLaunchUriStatus](/uwp/api/windows.system.remotelaunchuristatus)

**[プロパティ]**


Windows.System.RemoteLaunchUriStatus <br /> Windows.System.RemoteLaunchUriStatus.AppUnavailable <br /> Windows.System.RemoteLaunchUriStatus.DeniedByLocalSystem <br /> Windows.System.RemoteLaunchUriStatus.DeniedByRemoteSystem <br /> Windows.System.RemoteLaunchUriStatus.ProtocolUnavailable <br /> Windows.System.RemoteLaunchUriStatus.RemoteSystemUnavailable <br /> Windows.System.RemoteLaunchUriStatus.Success <br /> Windows.System.RemoteLaunchUriStatus.Unknown <br /> Windows.System.RemoteLaunchUriStatus.ValueSetTooLarge
<hr>

**項目**

[Windows.System.UserDeviceAssociation](/uwp/api/windows.system.userdeviceassociation)

**[プロパティ]**


Windows.System.UserDeviceAssociation <br /> Windows.System.UserDeviceAssociation.UserDeviceAssociationChanged <br /> Windows.System.UserDeviceAssociation.FindUserFromDeviceId(System.String)
<hr>

**項目**

[Windows.System.UserDeviceAssociationChangedEventArgs](/uwp/api/windows.system.userdeviceassociationchangedeventargs)

**[プロパティ]**


Windows.System.UserDeviceAssociationChangedEventArgs <br /> Windows.System.UserDeviceAssociationChangedEventArgs.DeviceId <br /> Windows.System.UserDeviceAssociationChangedEventArgs.NewUser <br /> Windows.System.UserDeviceAssociationChangedEventArgs.OldUser
<hr>

**項目**

[Windows.System.UserPicker](/uwp/api/windows.system.userpicker)

**[プロパティ]**


Windows.System.UserPicker <br /> Windows.System.UserPicker.#ctor <br /> Windows.System.UserPicker.AllowGuestAccounts <br /> Windows.System.UserPicker.SuggestedSelectedUser <br /> Windows.System.UserPicker.IsSupported <br /> Windows.System.UserPicker.PickSingleUserAsync
<hr>

**項目**

[Windows.System.Profile.SystemIdentification](/uwp/api/windows.system.profile.systemidentification)

**[プロパティ]**


Windows.System.Profile.SystemIdentification <br /> Windows.System.Profile.SystemIdentification.GetSystemIdForPublisher <br /> Windows.System.Profile.SystemIdentification.GetSystemIdForUser(Windows.System.User)
<hr>

**項目**

[Windows.System.Profile.SystemIdentificationInfo](/uwp/api/windows.system.profile.systemidentificationinfo)

**[プロパティ]**


Windows.System.Profile.SystemIdentificationInfo <br /> Windows.System.Profile.SystemIdentificationInfo.Id <br /> Windows.System.Profile.SystemIdentificationInfo.Source
<hr>

**項目**

[Windows.System.Profile.SystemIdentificationSource](/uwp/api/windows.system.profile.systemidentificationsource)

**[プロパティ]**


Windows.System.Profile.SystemIdentificationSource <br /> Windows.System.Profile.SystemIdentificationSource.None <br /> Windows.System.Profile.SystemIdentificationSource.Tpm <br /> Windows.System.Profile.SystemIdentificationSource.Uefi
<hr>

**項目**

[Windows.System.RemoteSystems.IRemoteSystemFilter](/uwp/api/windows.system.remotesystems.iremotesystemfilter)

**[プロパティ]**


Windows.System.RemoteSystems.IRemoteSystemFilter
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystem](/uwp/api/windows.system.remotesystems.remotesystem)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystem <br /> Windows.System.RemoteSystems.RemoteSystem.DisplayName <br /> Windows.System.RemoteSystems.RemoteSystem.Id <br /> Windows.System.RemoteSystems.RemoteSystem.IsAvailableByProximity <br /> Windows.System.RemoteSystems.RemoteSystem.Kind <br /> Windows.System.RemoteSystems.RemoteSystem.Status <br /> Windows.System.RemoteSystems.RemoteSystem.CreateWatcher <br /> Windows.System.RemoteSystems.RemoteSystem.CreateWatcher(Windows.Foundation.Collections.IIterable{Windows.System.RemoteSystems.IRemoteSystemFilter}) <br /> Windows.System.RemoteSystems.RemoteSystem.FindByHostNameAsync(Windows.Networking.HostName) <br /> Windows.System.RemoteSystems.RemoteSystem.RequestAccessAsync
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemAccessStatus](/uwp/api/windows.system.remotesystems.remotesystemaccessstatus)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemAccessStatus <br /> Windows.System.RemoteSystems.RemoteSystemAccessStatus.Allowed <br /> Windows.System.RemoteSystems.RemoteSystemAccessStatus.DeniedBySystem <br /> Windows.System.RemoteSystems.RemoteSystemAccessStatus.DeniedByUser <br /> Windows.System.RemoteSystems.RemoteSystemAccessStatus.Unspecified
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemAddedEventArgs](/uwp/api/windows.system.remotesystems.remotesystemaddedeventargs)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemAddedEventArgs <br /> Windows.System.RemoteSystems.RemoteSystemAddedEventArgs.RemoteSystem
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemConnectionRequest](/uwp/api/windows.system.remotesystems.remotesystemconnectionrequest)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemConnectionRequest <br /> Windows.System.RemoteSystems.RemoteSystemConnectionRequest.#ctor(Windows.System.RemoteSystems.RemoteSystem) <br /> Windows.System.RemoteSystems.RemoteSystemConnectionRequest.RemoteSystem
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemDiscoveryType](/uwp/api/windows.system.remotesystems.remotesystemdiscoverytype)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemDiscoveryType <br /> Windows.System.RemoteSystems.RemoteSystemDiscoveryType.Any <br /> Windows.System.RemoteSystems.RemoteSystemDiscoveryType.Cloud <br /> Windows.System.RemoteSystems.RemoteSystemDiscoveryType.Proximal
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemDiscoveryTypeFilter](/uwp/api/windows.system.remotesystems.remotesystemdiscoverytypefilter)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemDiscoveryTypeFilter <br /> Windows.System.RemoteSystems.RemoteSystemDiscoveryTypeFilter.#ctor(Windows.System.RemoteSystems.RemoteSystemDiscoveryType) <br /> Windows.System.RemoteSystems.RemoteSystemDiscoveryTypeFilter.RemoteSystemDiscoveryType
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemKindFilter](/uwp/api/windows.system.remotesystems.remotesystemkindfilter)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemKindFilter <br /> Windows.System.RemoteSystems.RemoteSystemKindFilter.#ctor(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.System.RemoteSystems.RemoteSystemKindFilter.RemoteSystemKinds
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemKinds](/uwp/api/windows.system.remotesystems.remotesystemkinds)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemKinds <br /> Windows.System.RemoteSystems.RemoteSystemKinds.Desktop <br /> Windows.System.RemoteSystems.RemoteSystemKinds.Holographic <br /> Windows.System.RemoteSystems.RemoteSystemKinds.Hub <br /> Windows.System.RemoteSystems.RemoteSystemKinds.Phone <br /> Windows.System.RemoteSystems.RemoteSystemKinds.Xbox
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemRemovedEventArgs](/uwp/api/windows.system.remotesystems.remotesystemremovedeventargs)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemRemovedEventArgs <br /> Windows.System.RemoteSystems.RemoteSystemRemovedEventArgs.RemoteSystemId
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemStatus](/uwp/api/windows.system.remotesystems.remotesystemstatus)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemStatus <br /> Windows.System.RemoteSystems.RemoteSystemStatus.Available <br /> Windows.System.RemoteSystems.RemoteSystemStatus.DiscoveringAvailability <br /> Windows.System.RemoteSystems.RemoteSystemStatus.Unavailable <br /> Windows.System.RemoteSystems.RemoteSystemStatus.Unknown
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemStatusType](/uwp/api/windows.system.remotesystems.remotesystemstatustype)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemStatusType <br /> Windows.System.RemoteSystems.RemoteSystemStatusType.Any <br /> Windows.System.RemoteSystems.RemoteSystemStatusType.Available
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemStatusTypeFilter](/uwp/api/windows.system.remotesystems.remotesystemstatustypefilter)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemStatusTypeFilter <br /> Windows.System.RemoteSystems.RemoteSystemStatusTypeFilter.#ctor(Windows.System.RemoteSystems.RemoteSystemStatusType) <br /> Windows.System.RemoteSystems.RemoteSystemStatusTypeFilter.RemoteSystemStatusType
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemUpdatedEventArgs](/uwp/api/windows.system.remotesystems.remotesystemupdatedeventargs)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemUpdatedEventArgs <br /> Windows.System.RemoteSystems.RemoteSystemUpdatedEventArgs.RemoteSystem
<hr>

**項目**

[Windows.System.RemoteSystems.RemoteSystemWatcher](/uwp/api/windows.system.remotesystems.remotesystemwatcher)

**[プロパティ]**


Windows.System.RemoteSystems.RemoteSystemWatcher <br /> Windows.System.RemoteSystems.RemoteSystemWatcher.RemoteSystemAdded <br /> Windows.System.RemoteSystems.RemoteSystemWatcher.RemoteSystemRemoved <br /> Windows.System.RemoteSystems.RemoteSystemWatcher.RemoteSystemUpdated <br /> Windows.System.RemoteSystems.RemoteSystemWatcher.Start <br /> Windows.System.RemoteSystems.RemoteSystemWatcher.Stop
<hr>

**項目**

[Windows.System.UserProfile.AdvertisingManagerForUser](/uwp/api/windows.system.userprofile.advertisingmanagerforuser)

**[プロパティ]**


Windows.System.UserProfile.AdvertisingManagerForUser <br /> Windows.System.UserProfile.AdvertisingManagerForUser.AdvertisingId <br /> Windows.System.UserProfile.AdvertisingManagerForUser.User
<hr>

**項目**

[Windows.UI.Composition.AmbientLight](/uwp/api/windows.ui.composition.ambientlight)

**[プロパティ]**


Windows.UI.Composition.AmbientLight <br /> Windows.UI.Composition.AmbientLight.Color
<hr>

**項目**

[Windows.UI.Composition.AnimationDirection](/uwp/api/windows.ui.composition.animationdirection)

**[プロパティ]**


Windows.UI.Composition.AnimationDirection <br /> Windows.UI.Composition.AnimationDirection.Alternate <br /> Windows.UI.Composition.AnimationDirection.AlternateReverse <br /> Windows.UI.Composition.AnimationDirection.Normal <br /> Windows.UI.Composition.AnimationDirection.Reverse
<hr>

**項目**

[Windows.UI.Composition.CompositionAnimationGroup](/uwp/api/windows.ui.composition.compositionanimationgroup)

**[プロパティ]**


Windows.UI.Composition.CompositionAnimationGroup <br /> Windows.UI.Composition.CompositionAnimationGroup.Count <br /> Windows.UI.Composition.CompositionAnimationGroup.Add(Windows.UI.Composition.CompositionAnimation) <br /> Windows.UI.Composition.CompositionAnimationGroup.First <br /> Windows.UI.Composition.CompositionAnimationGroup.Remove(Windows.UI.Composition.CompositionAnimation) <br /> Windows.UI.Composition.CompositionAnimationGroup.RemoveAll
<hr>

**項目**

[Windows.UI.Composition.CompositionBackdropBrush](/uwp/api/windows.ui.composition.compositionbackdropbrush)

**[プロパティ]**


Windows.UI.Composition.CompositionBackdropBrush
<hr>

**項目**

[Windows.UI.Composition.CompositionLight](/uwp/api/windows.ui.composition.compositionlight)

**[プロパティ]**


Windows.UI.Composition.CompositionLight <br /> Windows.UI.Composition.CompositionLight.Targets
<hr>

**項目**

[Windows.UI.Composition.CompositionMaskBrush](/uwp/api/windows.ui.composition.compositionmaskbrush)

**[プロパティ]**


Windows.UI.Composition.CompositionMaskBrush <br /> Windows.UI.Composition.CompositionMaskBrush.Mask <br /> Windows.UI.Composition.CompositionMaskBrush.Source
<hr>

**項目**

[Windows.UI.Composition.CompositionNineGridBrush](/uwp/api/windows.ui.composition.compositionninegridbrush)

**[プロパティ]**


Windows.UI.Composition.CompositionNineGridBrush <br /> Windows.UI.Composition.CompositionNineGridBrush.BottomInset <br /> Windows.UI.Composition.CompositionNineGridBrush.BottomInsetScale <br /> Windows.UI.Composition.CompositionNineGridBrush.IsCenterHollow <br /> Windows.UI.Composition.CompositionNineGridBrush.LeftInset <br /> Windows.UI.Composition.CompositionNineGridBrush.LeftInsetScale <br /> Windows.UI.Composition.CompositionNineGridBrush.RightInset <br /> Windows.UI.Composition.CompositionNineGridBrush.RightInsetScale <br /> Windows.UI.Composition.CompositionNineGridBrush.Source <br /> Windows.UI.Composition.CompositionNineGridBrush.TopInset <br /> Windows.UI.Composition.CompositionNineGridBrush.TopInsetScale <br /> Windows.UI.Composition.CompositionNineGridBrush.SetInsets(System.Single) <br /> Windows.UI.Composition.CompositionNineGridBrush.SetInsets(System.Single,System.Single,System.Single,System.Single) <br /> Windows.UI.Composition.CompositionNineGridBrush.SetInsetScales(System.Single) <br /> Windows.UI.Composition.CompositionNineGridBrush.SetInsetScales(System.Single,System.Single,System.Single,System.Single)
<hr>

**項目**

[Windows.UI.Composition.CompositionShadow](/uwp/api/windows.ui.composition.compositionshadow)

**[プロパティ]**


Windows.UI.Composition.CompositionShadow
<hr>

**項目**

[Windows.UI.Composition.DistantLight](/uwp/api/windows.ui.composition.distantlight)

**[プロパティ]**


Windows.UI.Composition.DistantLight <br /> Windows.UI.Composition.DistantLight.Color <br /> Windows.UI.Composition.DistantLight.CoordinateSpace <br /> Windows.UI.Composition.DistantLight.Direction
<hr>

**項目**

[Windows.UI.Composition.DropShadow](/uwp/api/windows.ui.composition.dropshadow)

**[プロパティ]**


Windows.UI.Composition.DropShadow <br /> Windows.UI.Composition.DropShadow.BlurRadius <br /> Windows.UI.Composition.DropShadow.Color <br /> Windows.UI.Composition.DropShadow.Mask <br /> Windows.UI.Composition.DropShadow.Offset <br /> Windows.UI.Composition.DropShadow.Opacity
<hr>

**項目**

[Windows.UI.Composition.ICompositionAnimationBase](/uwp/api/windows.ui.composition.icompositionanimationbase)

**[プロパティ]**


Windows.UI.Composition.ICompositionAnimationBase
<hr>

**項目**

[Windows.UI.Composition.ImplicitAnimationCollection](/uwp/api/windows.ui.composition.implicitanimationcollection)

**[プロパティ]**


Windows.UI.Composition.ImplicitAnimationCollection <br /> Windows.UI.Composition.ImplicitAnimationCollection.Size <br /> Windows.UI.Composition.ImplicitAnimationCollection.Clear <br /> Windows.UI.Composition.ImplicitAnimationCollection.First <br /> Windows.UI.Composition.ImplicitAnimationCollection.GetView <br /> Windows.UI.Composition.ImplicitAnimationCollection.HasKey(System.String) <br /> Windows.UI.Composition.ImplicitAnimationCollection.Insert(System.String,Windows.UI.Composition.ICompositionAnimationBase) <br /> Windows.UI.Composition.ImplicitAnimationCollection.Lookup(System.String) <br /> Windows.UI.Composition.ImplicitAnimationCollection.Remove(System.String)
<hr>

**項目**

[Windows.UI.Composition.LayerVisual](/uwp/api/windows.ui.composition.layervisual)

**[プロパティ]**


Windows.UI.Composition.LayerVisual <br /> Windows.UI.Composition.LayerVisual.Effect
<hr>

**項目**

[Windows.UI.Composition.PointLight](/uwp/api/windows.ui.composition.pointlight)

**[プロパティ]**


Windows.UI.Composition.PointLight <br /> Windows.UI.Composition.PointLight.Color <br /> Windows.UI.Composition.PointLight.ConstantAttenuation <br /> Windows.UI.Composition.PointLight.CoordinateSpace <br /> Windows.UI.Composition.PointLight.LinearAttenuation <br /> Windows.UI.Composition.PointLight.Offset <br /> Windows.UI.Composition.PointLight.QuadraticAttenuation
<hr>

**項目**

[Windows.UI.Composition.SpotLight](/uwp/api/windows.ui.composition.spotlight)

**[プロパティ]**


Windows.UI.Composition.SpotLight <br /> Windows.UI.Composition.SpotLight.ConstantAttenuation <br /> Windows.UI.Composition.SpotLight.CoordinateSpace <br /> Windows.UI.Composition.SpotLight.Direction <br /> Windows.UI.Composition.SpotLight.InnerConeAngle <br /> Windows.UI.Composition.SpotLight.InnerConeAngleInDegrees <br /> Windows.UI.Composition.SpotLight.InnerConeColor <br /> Windows.UI.Composition.SpotLight.LinearAttenuation <br /> Windows.UI.Composition.SpotLight.Offset <br /> Windows.UI.Composition.SpotLight.OuterConeAngle <br /> Windows.UI.Composition.SpotLight.OuterConeAngleInDegrees <br /> Windows.UI.Composition.SpotLight.OuterConeColor <br /> Windows.UI.Composition.SpotLight.QuadraticAttenuation
<hr>

**項目**

[Windows.UI.Composition.StepEasingFunction](/uwp/api/windows.ui.composition.stepeasingfunction)

**[プロパティ]**


Windows.UI.Composition.StepEasingFunction <br /> Windows.UI.Composition.StepEasingFunction.FinalStep <br /> Windows.UI.Composition.StepEasingFunction.InitialStep <br /> Windows.UI.Composition.StepEasingFunction.IsFinalStepSingleFrame <br /> Windows.UI.Composition.StepEasingFunction.IsInitialStepSingleFrame <br /> Windows.UI.Composition.StepEasingFunction.StepCount
<hr>

**項目**

[Windows.UI.Composition.VisualUnorderedCollection](/uwp/api/windows.ui.composition.visualunorderedcollection)

**[プロパティ]**


Windows.UI.Composition.VisualUnorderedCollection <br /> Windows.UI.Composition.VisualUnorderedCollection.Count <br /> Windows.UI.Composition.VisualUnorderedCollection.Add(Windows.UI.Composition.Visual) <br /> Windows.UI.Composition.VisualUnorderedCollection.First <br /> Windows.UI.Composition.VisualUnorderedCollection.Remove(Windows.UI.Composition.Visual) <br /> Windows.UI.Composition.VisualUnorderedCollection.RemoveAll
<hr>

**項目**

[Windows.UI.Composition.Effects.SceneLightingEffect](/uwp/api/windows.ui.composition.effects.scenelightingeffect)

**[プロパティ]**


Windows.UI.Composition.Effects.SceneLightingEffect <br /> Windows.UI.Composition.Effects.SceneLightingEffect.#ctor <br /> Windows.UI.Composition.Effects.SceneLightingEffect.AmbientAmount <br /> Windows.UI.Composition.Effects.SceneLightingEffect.DiffuseAmount <br /> Windows.UI.Composition.Effects.SceneLightingEffect.Name <br /> Windows.UI.Composition.Effects.SceneLightingEffect.NormalMapSource <br /> Windows.UI.Composition.Effects.SceneLightingEffect.SpecularAmount <br /> Windows.UI.Composition.Effects.SceneLightingEffect.SpecularShine
<hr>

**項目**

[Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection](/uwp/api/windows.ui.composition.interactions.compositioninteractionsourcecollection)

**[プロパティ]**


Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection <br /> Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection.Count <br /> Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection.Add(Windows.UI.Composition.Interactions.ICompositionInteractionSource) <br /> Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection.First <br /> Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection.Remove(Windows.UI.Composition.Interactions.ICompositionInteractionSource) <br /> Windows.UI.Composition.Interactions.CompositionInteractionSourceCollection.RemoveAll
<hr>

**項目**

[Windows.UI.Composition.Interactions.ICompositionInteractionSource](/uwp/api/windows.ui.composition.interactions.icompositioninteractionsource)

**[プロパティ]**


Windows.UI.Composition.Interactions.ICompositionInteractionSource
<hr>

**項目**

[Windows.UI.Composition.Interactions.IInteractionTrackerOwner](/uwp/api/windows.ui.composition.interactions.iinteractiontrackerowner)

**[プロパティ]**


Windows.UI.Composition.Interactions.IInteractionTrackerOwner <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.CustomAnimationStateEntered(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerCustomAnimationStateEnteredArgs) <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.IdleStateEntered(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerIdleStateEnteredArgs) <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.InertiaStateEntered(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs) <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.InteractingStateEntered(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerInteractingStateEnteredArgs) <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.RequestIgnored(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerRequestIgnoredArgs) <br /> Windows.UI.Composition.Interactions.IInteractionTrackerOwner.ValuesChanged(Windows.UI.Composition.Interactions.InteractionTracker,Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs)
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionChainingMode](/uwp/api/windows.ui.composition.interactions.interactionchainingmode)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionChainingMode <br /> Windows.UI.Composition.Interactions.InteractionChainingMode.Always <br /> Windows.UI.Composition.Interactions.InteractionChainingMode.Auto <br /> Windows.UI.Composition.Interactions.InteractionChainingMode.Never
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionSourceMode](/uwp/api/windows.ui.composition.interactions.interactionsourcemode)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionSourceMode <br /> Windows.UI.Composition.Interactions.InteractionSourceMode.Disabled <br /> Windows.UI.Composition.Interactions.InteractionSourceMode.EnabledWithInertia <br /> Windows.UI.Composition.Interactions.InteractionSourceMode.EnabledWithoutInertia
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTracker](/uwp/api/windows.ui.composition.interactions.interactiontracker)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTracker <br /> Windows.UI.Composition.Interactions.InteractionTracker.InteractionSources <br /> Windows.UI.Composition.Interactions.InteractionTracker.IsPositionRoundingSuggested <br /> Windows.UI.Composition.Interactions.InteractionTracker.MaxPosition <br /> Windows.UI.Composition.Interactions.InteractionTracker.MaxScale <br /> Windows.UI.Composition.Interactions.InteractionTracker.MinPosition <br /> Windows.UI.Composition.Interactions.InteractionTracker.MinScale <br /> Windows.UI.Composition.Interactions.InteractionTracker.NaturalRestingPosition <br /> Windows.UI.Composition.Interactions.InteractionTracker.NaturalRestingScale <br /> Windows.UI.Composition.Interactions.InteractionTracker.Owner <br /> Windows.UI.Composition.Interactions.InteractionTracker.Position <br /> Windows.UI.Composition.Interactions.InteractionTracker.PositionInertiaDecayRate <br /> Windows.UI.Composition.Interactions.InteractionTracker.PositionVelocityInPixelsPerSecond <br /> Windows.UI.Composition.Interactions.InteractionTracker.Scale <br /> Windows.UI.Composition.Interactions.InteractionTracker.ScaleInertiaDecayRate <br /> Windows.UI.Composition.Interactions.InteractionTracker.ScaleVelocityInPercentPerSecond <br /> Windows.UI.Composition.Interactions.InteractionTracker.AdjustPositionXIfGreaterThanThreshold(System.Single,System.Single) <br /> Windows.UI.Composition.Interactions.InteractionTracker.AdjustPositionYIfGreaterThanThreshold(System.Single,System.Single) <br /> Windows.UI.Composition.Interactions.InteractionTracker.ConfigurePositionXInertiaModifiers(Windows.Foundation.Collections.IIterable{Windows.UI.Composition.Interactions.InteractionTrackerInertiaModifier}) <br /> Windows.UI.Composition.Interactions.InteractionTracker.ConfigurePositionYInertiaModifiers(Windows.Foundation.Collections.IIterable{Windows.UI.Composition.Interactions.InteractionTrackerInertiaModifier}) <br /> Windows.UI.Composition.Interactions.InteractionTracker.ConfigureScaleInertiaModifiers(Windows.Foundation.Collections.IIterable{Windows.UI.Composition.Interactions.InteractionTrackerInertiaModifier}) <br /> Windows.UI.Composition.Interactions.InteractionTracker.Create(Windows.UI.Composition.Compositor) <br /> Windows.UI.Composition.Interactions.InteractionTracker.CreateWithOwner(Windows.UI.Composition.Compositor,Windows.UI.Composition.Interactions.IInteractionTrackerOwner) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdatePosition(Windows.Foundation.Numerics.Vector3) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdatePositionBy(Windows.Foundation.Numerics.Vector3) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdatePositionWithAdditionalVelocity(Windows.Foundation.Numerics.Vector3) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdatePositionWithAnimation(Windows.UI.Composition.CompositionAnimation) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdateScale(System.Single,Windows.Foundation.Numerics.Vector3) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdateScaleWithAdditionalVelocity(System.Single,Windows.Foundation.Numerics.Vector3) <br /> Windows.UI.Composition.Interactions.InteractionTracker.TryUpdateScaleWithAnimation(Windows.UI.Composition.CompositionAnimation,Windows.Foundation.Numerics.Vector3)
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerCustomAnimationStateEnteredArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackercustomanimationstateenteredargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerCustomAnimationStateEnteredArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerCustomAnimationStateEnteredArgs.RequestId
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerIdleStateEnteredArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackeridlestateenteredargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerIdleStateEnteredArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerIdleStateEnteredArgs.RequestId
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerInertiaModifier](/uwp/api/windows.ui.composition.interactions.interactiontrackerinertiamodifier)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerInertiaModifier
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerInertiaMotion](/uwp/api/windows.ui.composition.interactions.interactiontrackerinertiamotion)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerInertiaMotion <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaMotion.Condition <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaMotion.Motion <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaMotion.Create(Windows.UI.Composition.Compositor)
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerInertiaRestingValue](/uwp/api/windows.ui.composition.interactions.interactiontrackerinertiarestingvalue)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerInertiaRestingValue <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaRestingValue.Condition <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaRestingValue.RestingValue <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaRestingValue.Create(Windows.UI.Composition.Compositor)
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackerinertiastateenteredargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.ModifiedRestingPosition <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.ModifiedRestingScale <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.NaturalRestingPosition <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.NaturalRestingScale <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.PositionVelocityInPixelsPerSecond <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.RequestId <br /> Windows.UI.Composition.Interactions.InteractionTrackerInertiaStateEnteredArgs.ScaleVelocityInPercentPerSecond
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerInteractingStateEnteredArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackerinteractingstateenteredargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerInteractingStateEnteredArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerInteractingStateEnteredArgs.RequestId
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerRequestIgnoredArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackerrequestignoredargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerRequestIgnoredArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerRequestIgnoredArgs.RequestId
<hr>

**項目**

[Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs](/uwp/api/windows.ui.composition.interactions.interactiontrackervalueschangedargs)

**[プロパティ]**


Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs <br /> Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs.Position <br /> Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs.RequestId <br /> Windows.UI.Composition.Interactions.InteractionTrackerValuesChangedArgs.Scale
<hr>

**項目**

[Windows.UI.Composition.Interactions.VisualInteractionSource](/uwp/api/windows.ui.composition.interactions.visualinteractionsource)

**[プロパティ]**


Windows.UI.Composition.Interactions.VisualInteractionSource <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.IsPositionXRailsEnabled <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.IsPositionYRailsEnabled <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.ManipulationRedirectionMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.PositionXChainingMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.PositionXSourceMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.PositionYChainingMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.PositionYSourceMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.ScaleChainingMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.ScaleSourceMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.Source <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.Create(Windows.UI.Composition.Visual) <br /> Windows.UI.Composition.Interactions.VisualInteractionSource.TryRedirectForManipulation(Windows.UI.Input.PointerPoint)
<hr>

**項目**

[Windows.UI.Composition.Interactions.VisualInteractionSourceRedirectionMode](/uwp/api/windows.ui.composition.interactions.visualinteractionsourceredirectionmode)

**[プロパティ]**


Windows.UI.Composition.Interactions.VisualInteractionSourceRedirectionMode <br /> Windows.UI.Composition.Interactions.VisualInteractionSourceRedirectionMode.CapableTouchpadOnly <br /> Windows.UI.Composition.Interactions.VisualInteractionSourceRedirectionMode.Off
<hr>

**項目**

[Windows.UI.Core.ClosestInteractiveBoundsRequestedEventArgs](/uwp/api/windows.ui.core.closestinteractiveboundsrequestedeventargs)

**[プロパティ]**


Windows.UI.Core.ClosestInteractiveBoundsRequestedEventArgs <br /> Windows.UI.Core.ClosestInteractiveBoundsRequestedEventArgs.ClosestInteractiveBounds <br /> Windows.UI.Core.ClosestInteractiveBoundsRequestedEventArgs.PointerPosition <br /> Windows.UI.Core.ClosestInteractiveBoundsRequestedEventArgs.SearchBounds
<hr>

**項目**

[Windows.UI.Input.RadialController](/uwp/api/windows.ui.input.radialcontroller)

**[プロパティ]**


Windows.UI.Input.RadialController <br /> Windows.UI.Input.RadialController.Menu <br /> Windows.UI.Input.RadialController.RotationResolutionInDegrees <br /> Windows.UI.Input.RadialController.UseAutomaticHapticFeedback <br /> Windows.UI.Input.RadialController.ButtonClicked <br /> Windows.UI.Input.RadialController.ControlAcquired <br /> Windows.UI.Input.RadialController.ControlLost <br /> Windows.UI.Input.RadialController.RotationChanged <br /> Windows.UI.Input.RadialController.ScreenContactContinued <br /> Windows.UI.Input.RadialController.ScreenContactEnded <br /> Windows.UI.Input.RadialController.ScreenContactStarted <br /> Windows.UI.Input.RadialController.CreateForCurrentView <br /> Windows.UI.Input.RadialController.IsSupported
<hr>

**項目**

[Windows.UI.Input.RadialControllerButtonClickedEventArgs](/uwp/api/windows.ui.input.radialcontrollerbuttonclickedeventargs)

**[プロパティ]**


Windows.UI.Input.RadialControllerButtonClickedEventArgs <br /> Windows.UI.Input.RadialControllerButtonClickedEventArgs.Contact
<hr>

**項目**

[Windows.UI.Input.RadialControllerConfiguration](/uwp/api/windows.ui.input.radialcontrollerconfiguration)

**[プロパティ]**


Windows.UI.Input.RadialControllerConfiguration <br /> Windows.UI.Input.RadialControllerConfiguration.GetForCurrentView <br /> Windows.UI.Input.RadialControllerConfiguration.ResetToDefaultMenuItems <br /> Windows.UI.Input.RadialControllerConfiguration.SetDefaultMenuItems(Windows.Foundation.Collections.IIterable{Windows.UI.Input.RadialControllerSystemMenuItemKind}) <br /> Windows.UI.Input.RadialControllerConfiguration.TrySelectDefaultMenuItem(Windows.UI.Input.RadialControllerSystemMenuItemKind)
<hr>

**項目**

[Windows.UI.Input.RadialControllerControlAcquiredEventArgs](/uwp/api/windows.ui.input.radialcontrollercontrolacquiredeventargs)

**[プロパティ]**


Windows.UI.Input.RadialControllerControlAcquiredEventArgs <br /> Windows.UI.Input.RadialControllerControlAcquiredEventArgs.Contact
<hr>

**項目**

[Windows.UI.Input.RadialControllerMenu](/uwp/api/windows.ui.input.radialcontrollermenu)

**[プロパティ]**


Windows.UI.Input.RadialControllerMenu <br /> Windows.UI.Input.RadialControllerMenu.IsEnabled <br /> Windows.UI.Input.RadialControllerMenu.Items <br /> Windows.UI.Input.RadialControllerMenu.GetSelectedMenuItem <br /> Windows.UI.Input.RadialControllerMenu.SelectMenuItem(Windows.UI.Input.RadialControllerMenuItem) <br /> Windows.UI.Input.RadialControllerMenu.TrySelectPreviouslySelectedMenuItem
<hr>

**項目**

[Windows.UI.Input.RadialControllerMenuItem](/uwp/api/windows.ui.input.radialcontrollermenuitem)

**[プロパティ]**


Windows.UI.Input.RadialControllerMenuItem <br /> Windows.UI.Input.RadialControllerMenuItem.DisplayText <br /> Windows.UI.Input.RadialControllerMenuItem.Tag <br /> Windows.UI.Input.RadialControllerMenuItem.Invoked <br /> Windows.UI.Input.RadialControllerMenuItem.CreateFromIcon(System.String,Windows.Storage.Streams.RandomAccessStreamReference) <br /> Windows.UI.Input.RadialControllerMenuItem.CreateFromKnownIcon(System.String,Windows.UI.Input.RadialControllerMenuKnownIcon)
<hr>

**項目**

[Windows.UI.Input.RadialControllerMenuKnownIcon](/uwp/api/windows.ui.input.radialcontrollermenuknownicon)

**[プロパティ]**


Windows.UI.Input.RadialControllerMenuKnownIcon <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.InkColor <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.InkThickness <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.NextPreviousTrack <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.PenType <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.Ruler <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.Scroll <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.UndoRedo <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.Volume <br /> Windows.UI.Input.RadialControllerMenuKnownIcon.Zoom
<hr>

**項目**

[Windows.UI.Input.RadialControllerRotationChangedEventArgs](/uwp/api/windows.ui.input.radialcontrollerrotationchangedeventargs)

**[プロパティ]**


Windows.UI.Input.RadialControllerRotationChangedEventArgs <br /> Windows.UI.Input.RadialControllerRotationChangedEventArgs.Contact <br /> Windows.UI.Input.RadialControllerRotationChangedEventArgs.RotationDeltaInDegrees
<hr>

**項目**

[Windows.UI.Input.RadialControllerScreenContact](/uwp/api/windows.ui.input.radialcontrollerscreencontact)

**[プロパティ]**


Windows.UI.Input.RadialControllerScreenContact <br /> Windows.UI.Input.RadialControllerScreenContact.Bounds <br /> Windows.UI.Input.RadialControllerScreenContact.Position
<hr>

**項目**

[Windows.UI.Input.RadialControllerScreenContactContinuedEventArgs](/uwp/api/windows.ui.input.radialcontrollerscreencontactcontinuedeventargs)

**[プロパティ]**


Windows.UI.Input.RadialControllerScreenContactContinuedEventArgs <br /> Windows.UI.Input.RadialControllerScreenContactContinuedEventArgs.Contact
<hr>

**項目**

[Windows.UI.Input.RadialControllerScreenContactStartedEventArgs](/uwp/api/windows.ui.input.radialcontrollerscreencontactstartedeventargs)

**[プロパティ]**


Windows.UI.Input.RadialControllerScreenContactStartedEventArgs <br /> Windows.UI.Input.RadialControllerScreenContactStartedEventArgs.Contact
<hr>

**項目**

[Windows.UI.Input.RadialControllerSystemMenuItemKind](/uwp/api/windows.ui.input.radialcontrollersystemmenuitemkind)

**[プロパティ]**


Windows.UI.Input.RadialControllerSystemMenuItemKind <br /> Windows.UI.Input.RadialControllerSystemMenuItemKind.NextPreviousTrack <br /> Windows.UI.Input.RadialControllerSystemMenuItemKind.Scroll <br /> Windows.UI.Input.RadialControllerSystemMenuItemKind.UndoRedo <br /> Windows.UI.Input.RadialControllerSystemMenuItemKind.Volume <br /> Windows.UI.Input.RadialControllerSystemMenuItemKind.Zoom
<hr>

**項目**

[Windows.UI.Input.Inking.IInkPresenterRulerFactory](/uwp/api/windows.ui.input.inking.iinkpresenterrulerfactory)

**[プロパティ]**


Windows.UI.Input.Inking.IInkPresenterRulerFactory <br /> Windows.UI.Input.Inking.IInkPresenterRulerFactory.Create(Windows.UI.Input.Inking.InkPresenter)
<hr>

**項目**

[Windows.UI.Input.Inking.IInkPresenterStencil](/uwp/api/windows.ui.input.inking.iinkpresenterstencil)

**[プロパティ]**


Windows.UI.Input.Inking.IInkPresenterStencil <br /> Windows.UI.Input.Inking.IInkPresenterStencil.BackgroundColor <br /> Windows.UI.Input.Inking.IInkPresenterStencil.ForegroundColor <br /> Windows.UI.Input.Inking.IInkPresenterStencil.IsVisible <br /> Windows.UI.Input.Inking.IInkPresenterStencil.Kind <br /> Windows.UI.Input.Inking.IInkPresenterStencil.Transform
<hr>

**項目**

[Windows.UI.Input.Inking.InkDrawingAttributesKind](/uwp/api/windows.ui.input.inking.inkdrawingattributeskind)

**[プロパティ]**


Windows.UI.Input.Inking.InkDrawingAttributesKind <br /> Windows.UI.Input.Inking.InkDrawingAttributesKind.Default <br /> Windows.UI.Input.Inking.InkDrawingAttributesKind.Pencil
<hr>

**項目**

[Windows.UI.Input.Inking.InkDrawingAttributesPencilProperties](/uwp/api/windows.ui.input.inking.inkdrawingattributespencilproperties)

**[プロパティ]**


Windows.UI.Input.Inking.InkDrawingAttributesPencilProperties <br /> Windows.UI.Input.Inking.InkDrawingAttributesPencilProperties.Opacity
<hr>

**項目**

[Windows.UI.Input.Inking.InkPresenterRuler](/uwp/api/windows.ui.input.inking.inkpresenterruler)

**[プロパティ]**


Windows.UI.Input.Inking.InkPresenterRuler <br /> Windows.UI.Input.Inking.InkPresenterRuler.#ctor(Windows.UI.Input.Inking.InkPresenter) <br /> Windows.UI.Input.Inking.InkPresenterRuler.BackgroundColor <br /> Windows.UI.Input.Inking.InkPresenterRuler.ForegroundColor <br /> Windows.UI.Input.Inking.InkPresenterRuler.IsVisible <br /> Windows.UI.Input.Inking.InkPresenterRuler.Kind <br /> Windows.UI.Input.Inking.InkPresenterRuler.Length <br /> Windows.UI.Input.Inking.InkPresenterRuler.Transform <br /> Windows.UI.Input.Inking.InkPresenterRuler.Width
<hr>

**項目**

[Windows.UI.Input.Inking.InkPresenterStencilKind](/uwp/api/windows.ui.input.inking.inkpresenterstencilkind)

**[プロパティ]**


Windows.UI.Input.Inking.InkPresenterStencilKind <br /> Windows.UI.Input.Inking.InkPresenterStencilKind.Other <br /> Windows.UI.Input.Inking.InkPresenterStencilKind.Ruler
<hr>

**項目**

[Windows.UI.Input.Inking.Core.CoreWetStrokeDisposition](/uwp/api/windows.ui.input.inking.core.corewetstrokedisposition)

**[プロパティ]**


Windows.UI.Input.Inking.Core.CoreWetStrokeDisposition <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeDisposition.Canceled <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeDisposition.Completed <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeDisposition.Inking
<hr>

**項目**

[Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateEventArgs](/uwp/api/windows.ui.input.inking.core.corewetstrokeupdateeventargs)

**[プロパティ]**


Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateEventArgs <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateEventArgs.Disposition <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateEventArgs.NewInkPoints <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateEventArgs.PointerId
<hr>

**項目**

[Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource](/uwp/api/windows.ui.input.inking.core.corewetstrokeupdatesource)

**[プロパティ]**


Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.InkPresenter <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.WetStrokeCanceled <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.WetStrokeCompleted <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.WetStrokeContinuing <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.WetStrokeStarting <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.WetStrokeStopping <br /> Windows.UI.Input.Inking.Core.CoreWetStrokeUpdateSource.Create(Windows.UI.Input.Inking.InkPresenter)
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind](/uwp/api/windows.ui.input.preview.injection.injectedinputbuttonchangekind)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FifthButtonDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FifthButtonUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FirstButtonDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FirstButtonUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FourthButtonDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.FourthButtonUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.SecondButtonDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.SecondButtonUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.ThirdButtonDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputButtonChangeKind.ThirdButtonUp
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo](/uwp/api/windows.ui.input.preview.injection.injectedinputkeyboardinfo)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo.#ctor <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo.KeyOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo.ScanCode <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo.VirtualKey
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions](/uwp/api/windows.ui.input.preview.injection.injectedinputkeyoptions)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions.ExtendedKey <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions.KeyUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions.ScanCode <br /> Windows.UI.Input.Preview.Injection.InjectedInputKeyOptions.Unicode
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo](/uwp/api/windows.ui.input.preview.injection.injectedinputmouseinfo)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.#ctor <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.DeltaX <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.DeltaY <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.MouseData <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.MouseOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo.TimeOffsetInMilliseconds
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions](/uwp/api/windows.ui.input.preview.injection.injectedinputmouseoptions)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.Absolute <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.HWheel <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.LeftDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.LeftUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.MiddleDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.MiddleUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.Move <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.MoveNoCoalesce <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.RightDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.RightUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.VirtualDesk <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.Wheel <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.XDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputMouseOptions.XUp
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPenButtons](/uwp/api/windows.ui.input.preview.injection.injectedinputpenbuttons)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPenButtons <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenButtons.Barrel <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenButtons.Eraser <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenButtons.Inverted <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenButtons.None
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPenInfo](/uwp/api/windows.ui.input.preview.injection.injectedinputpeninfo)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPenInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.#ctor <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.PenButtons <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.PenParameters <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.PointerInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.Pressure <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.Rotation <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.TiltX <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenInfo.TiltY
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPenParameters](/uwp/api/windows.ui.input.preview.injection.injectedinputpenparameters)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPenParameters <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenParameters.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenParameters.Pressure <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenParameters.Rotation <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenParameters.TiltX <br /> Windows.UI.Input.Preview.Injection.InjectedInputPenParameters.TiltY
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPoint](/uwp/api/windows.ui.input.preview.injection.injectedinputpoint)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPoint <br /> Windows.UI.Input.Preview.Injection.InjectedInputPoint.PositionX <br /> Windows.UI.Input.Preview.Injection.InjectedInputPoint.PositionY
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo](/uwp/api/windows.ui.input.preview.injection.injectedinputpointerinfo)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo.PerformanceCount <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo.PixelLocation <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo.PointerId <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo.PointerOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerInfo.TimeOffsetInMilliseconds
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions](/uwp/api/windows.ui.input.preview.injection.injectedinputpointeroptions)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.Canceled <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.CaptureChanged <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.Confidence <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.FirstButton <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.InContact <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.InRange <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.New <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.PointerDown <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.PointerUp <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.Primary <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.SecondButton <br /> Windows.UI.Input.Preview.Injection.InjectedInputPointerOptions.Update
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputRectangle](/uwp/api/windows.ui.input.preview.injection.injectedinputrectangle)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputRectangle <br /> Windows.UI.Input.Preview.Injection.InjectedInputRectangle.Bottom <br /> Windows.UI.Input.Preview.Injection.InjectedInputRectangle.Left <br /> Windows.UI.Input.Preview.Injection.InjectedInputRectangle.Right <br /> Windows.UI.Input.Preview.Injection.InjectedInputRectangle.Top
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputShortcut](/uwp/api/windows.ui.input.preview.injection.injectedinputshortcut)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputShortcut <br /> Windows.UI.Input.Preview.Injection.InjectedInputShortcut.Back <br /> Windows.UI.Input.Preview.Injection.InjectedInputShortcut.Search <br /> Windows.UI.Input.Preview.Injection.InjectedInputShortcut.Start
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo](/uwp/api/windows.ui.input.preview.injection.injectedinputtouchinfo)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.#ctor <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.Contact <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.Orientation <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.PointerInfo <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.Pressure <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo.TouchParameters
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters](/uwp/api/windows.ui.input.preview.injection.injectedinputtouchparameters)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters.Contact <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters.None <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters.Orientation <br /> Windows.UI.Input.Preview.Injection.InjectedInputTouchParameters.Pressure
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode](/uwp/api/windows.ui.input.preview.injection.injectedinputvisualizationmode)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode <br /> Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode.Default <br /> Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode.Indirect <br /> Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode.None
<hr>

**項目**

[Windows.UI.Input.Preview.Injection.InputInjector](/uwp/api/windows.ui.input.preview.injection.inputinjector)

**[プロパティ]**


Windows.UI.Input.Preview.Injection.InputInjector <br /> Windows.UI.Input.Preview.Injection.InputInjector.InitializePenInjection(Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InitializeTouchInjection(Windows.UI.Input.Preview.Injection.InjectedInputVisualizationMode) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InjectKeyboardInput(Windows.Foundation.Collections.IIterable{Windows.UI.Input.Preview.Injection.InjectedInputKeyboardInfo}) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InjectMouseInput(Windows.Foundation.Collections.IIterable{Windows.UI.Input.Preview.Injection.InjectedInputMouseInfo}) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InjectPenInput(Windows.UI.Input.Preview.Injection.InjectedInputPenInfo) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InjectShortcut(Windows.UI.Input.Preview.Injection.InjectedInputShortcut) <br /> Windows.UI.Input.Preview.Injection.InputInjector.InjectTouchInput(Windows.Foundation.Collections.IIterable{Windows.UI.Input.Preview.Injection.InjectedInputTouchInfo}) <br /> Windows.UI.Input.Preview.Injection.InputInjector.TryCreate <br /> Windows.UI.Input.Preview.Injection.InputInjector.UninitializePenInjection <br /> Windows.UI.Input.Preview.Injection.InputInjector.UninitializeTouchInjection
<hr>

**項目**

[Windows.UI.Notifications.AdaptiveNotificationContentKind](/uwp/api/windows.ui.notifications.adaptivenotificationcontentkind)

**[プロパティ]**


Windows.UI.Notifications.AdaptiveNotificationContentKind <br /> Windows.UI.Notifications.AdaptiveNotificationContentKind.Text
<hr>

**項目**

[Windows.UI.Notifications.AdaptiveNotificationText](/uwp/api/windows.ui.notifications.adaptivenotificationtext)

**[プロパティ]**


Windows.UI.Notifications.AdaptiveNotificationText <br /> Windows.UI.Notifications.AdaptiveNotificationText.#ctor <br /> Windows.UI.Notifications.AdaptiveNotificationText.Hints <br /> Windows.UI.Notifications.AdaptiveNotificationText.Kind <br /> Windows.UI.Notifications.AdaptiveNotificationText.Language <br /> Windows.UI.Notifications.AdaptiveNotificationText.Text
<hr>

**項目**

[Windows.UI.Notifications.BadgeUpdateManagerForUser](/uwp/api/windows.ui.notifications.badgeupdatemanagerforuser)

**[プロパティ]**


Windows.UI.Notifications.BadgeUpdateManagerForUser <br /> Windows.UI.Notifications.BadgeUpdateManagerForUser.User <br /> Windows.UI.Notifications.BadgeUpdateManagerForUser.CreateBadgeUpdaterForApplication <br /> Windows.UI.Notifications.BadgeUpdateManagerForUser.CreateBadgeUpdaterForApplication(System.String) <br /> Windows.UI.Notifications.BadgeUpdateManagerForUser.CreateBadgeUpdaterForSecondaryTile(System.String)
<hr>

**項目**

[Windows.UI.Notifications.IAdaptiveNotificationContent](/uwp/api/windows.ui.notifications.iadaptivenotificationcontent)

**[プロパティ]**


Windows.UI.Notifications.IAdaptiveNotificationContent <br /> Windows.UI.Notifications.IAdaptiveNotificationContent.Hints <br /> Windows.UI.Notifications.IAdaptiveNotificationContent.Kind
<hr>

**項目**

[Windows.UI.Notifications.KnownAdaptiveNotificationHints](/uwp/api/windows.ui.notifications.knownadaptivenotificationhints)

**[プロパティ]**


Windows.UI.Notifications.KnownAdaptiveNotificationHints <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.Align <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.MaxLines <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.MinLines <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.Style <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.TextStacking <br /> Windows.UI.Notifications.KnownAdaptiveNotificationHints.Wrap
<hr>

**項目**

[Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles](/uwp/api/windows.ui.notifications.knownadaptivenotificationtextstyles)

**[プロパティ]**


Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Base <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.BaseSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Body <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.BodySubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Caption <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.CaptionSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Header <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.HeaderNumeral <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.HeaderNumeralSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.HeaderSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Subheader <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.SubheaderNumeral <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.SubheaderNumeralSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.SubheaderSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Subtitle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.SubtitleSubtle <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.Title <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.TitleNumeral <br /> Windows.UI.Notifications.KnownAdaptiveNotificationTextStyles.TitleSubtle
<hr>

**項目**

[Windows.UI.Notifications.KnownNotificationBindings](/uwp/api/windows.ui.notifications.knownnotificationbindings)

**[プロパティ]**


Windows.UI.Notifications.KnownNotificationBindings <br /> Windows.UI.Notifications.KnownNotificationBindings.ToastGeneric
<hr>

**項目**

[Windows.UI.Notifications.Notification](/uwp/api/windows.ui.notifications.notification)

**[プロパティ]**


Windows.UI.Notifications.Notification <br /> Windows.UI.Notifications.Notification.#ctor <br /> Windows.UI.Notifications.Notification.ExpirationTime <br /> Windows.UI.Notifications.Notification.Visual
<hr>

**項目**

[Windows.UI.Notifications.NotificationBinding](/uwp/api/windows.ui.notifications.notificationbinding)

**[プロパティ]**


Windows.UI.Notifications.NotificationBinding <br /> Windows.UI.Notifications.NotificationBinding.Hints <br /> Windows.UI.Notifications.NotificationBinding.Language <br /> Windows.UI.Notifications.NotificationBinding.Template <br /> Windows.UI.Notifications.NotificationBinding.GetTextElements
<hr>

**項目**

[Windows.UI.Notifications.NotificationKinds](/uwp/api/windows.ui.notifications.notificationkinds)

**[プロパティ]**


Windows.UI.Notifications.NotificationKinds <br /> Windows.UI.Notifications.NotificationKinds.Toast <br /> Windows.UI.Notifications.NotificationKinds.Unknown
<hr>

**項目**

[Windows.UI.Notifications.NotificationMirroring](/uwp/api/windows.ui.notifications.notificationmirroring)

**[プロパティ]**


Windows.UI.Notifications.NotificationMirroring <br /> Windows.UI.Notifications.NotificationMirroring.Allowed <br /> Windows.UI.Notifications.NotificationMirroring.Disabled
<hr>

**項目**

[Windows.UI.Notifications.NotificationVisual](/uwp/api/windows.ui.notifications.notificationvisual)

**[プロパティ]**


Windows.UI.Notifications.NotificationVisual <br /> Windows.UI.Notifications.NotificationVisual.Bindings <br /> Windows.UI.Notifications.NotificationVisual.Language <br /> Windows.UI.Notifications.NotificationVisual.GetBinding(System.String)
<hr>

**項目**

[Windows.UI.Notifications.ShownTileNotification](/uwp/api/windows.ui.notifications.showntilenotification)

**[プロパティ]**


Windows.UI.Notifications.ShownTileNotification <br /> Windows.UI.Notifications.ShownTileNotification.Arguments
<hr>

**項目**

[Windows.UI.Notifications.TileUpdateManagerForUser](/uwp/api/windows.ui.notifications.tileupdatemanagerforuser)

**[プロパティ]**


Windows.UI.Notifications.TileUpdateManagerForUser <br /> Windows.UI.Notifications.TileUpdateManagerForUser.User <br /> Windows.UI.Notifications.TileUpdateManagerForUser.CreateTileUpdaterForApplication(System.String) <br /> Windows.UI.Notifications.TileUpdateManagerForUser.CreateTileUpdaterForApplicationForUser <br /> Windows.UI.Notifications.TileUpdateManagerForUser.CreateTileUpdaterForSecondaryTile(System.String)
<hr>

**項目**

[Windows.UI.Notifications.ToastNotificationManagerForUser](/uwp/api/windows.ui.notifications.toastnotificationmanagerforuser)

**[プロパティ]**


Windows.UI.Notifications.ToastNotificationManagerForUser <br /> Windows.UI.Notifications.ToastNotificationManagerForUser.History <br /> Windows.UI.Notifications.ToastNotificationManagerForUser.User <br /> Windows.UI.Notifications.ToastNotificationManagerForUser.CreateToastNotifier <br /> Windows.UI.Notifications.ToastNotificationManagerForUser.CreateToastNotifier(System.String)
<hr>

**項目**

[Windows.UI.Notifications.UserNotification](/uwp/api/windows.ui.notifications.usernotification)

**[プロパティ]**


Windows.UI.Notifications.UserNotification <br /> Windows.UI.Notifications.UserNotification.AppInfo <br /> Windows.UI.Notifications.UserNotification.CreationTime <br /> Windows.UI.Notifications.UserNotification.Id <br /> Windows.UI.Notifications.UserNotification.Notification
<hr>

**項目**

[Windows.UI.Notifications.UserNotificationChangedEventArgs](/uwp/api/windows.ui.notifications.usernotificationchangedeventargs)

**[プロパティ]**


Windows.UI.Notifications.UserNotificationChangedEventArgs <br /> Windows.UI.Notifications.UserNotificationChangedEventArgs.ChangeKind <br /> Windows.UI.Notifications.UserNotificationChangedEventArgs.UserNotificationId
<hr>

**項目**

[Windows.UI.Notifications.UserNotificationChangedKind](/uwp/api/windows.ui.notifications.usernotificationchangedkind)

**[プロパティ]**


Windows.UI.Notifications.UserNotificationChangedKind <br /> Windows.UI.Notifications.UserNotificationChangedKind.Added <br /> Windows.UI.Notifications.UserNotificationChangedKind.Removed
<hr>

**項目**

[Windows.UI.Notifications.Management.UserNotificationListener](/uwp/api/windows.ui.notifications.management.usernotificationlistener)

**[プロパティ]**


Windows.UI.Notifications.Management.UserNotificationListener <br /> Windows.UI.Notifications.Management.UserNotificationListener.Current <br /> Windows.UI.Notifications.Management.UserNotificationListener.NotificationChanged <br /> Windows.UI.Notifications.Management.UserNotificationListener.ClearNotifications <br /> Windows.UI.Notifications.Management.UserNotificationListener.GetAccessStatus <br /> Windows.UI.Notifications.Management.UserNotificationListener.GetNotification(System.UInt32) <br /> Windows.UI.Notifications.Management.UserNotificationListener.GetNotificationsAsync(Windows.UI.Notifications.NotificationKinds) <br /> Windows.UI.Notifications.Management.UserNotificationListener.RemoveNotification(System.UInt32) <br /> Windows.UI.Notifications.Management.UserNotificationListener.RequestAccessAsync
<hr>

**項目**

[Windows.UI.Notifications.Management.UserNotificationListenerAccessStatus](/uwp/api/windows.ui.notifications.management.usernotificationlisteneraccessstatus)

**[プロパティ]**


Windows.UI.Notifications.Management.UserNotificationListenerAccessStatus <br /> Windows.UI.Notifications.Management.UserNotificationListenerAccessStatus.Allowed <br /> Windows.UI.Notifications.Management.UserNotificationListenerAccessStatus.Denied <br /> Windows.UI.Notifications.Management.UserNotificationListenerAccessStatus.Unspecified
<hr>

**項目**

[Windows.UI.WebUI.EnteredBackgroundEventArgs](/uwp/api/windows.ui.webui.enteredbackgroundeventargs)

**[プロパティ]**


Windows.UI.WebUI.EnteredBackgroundEventArgs <br /> Windows.UI.WebUI.EnteredBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.UI.WebUI.EnteredBackgroundEventHandler](/uwp/api/windows.ui.webui.enteredbackgroundeventhandler)

**[プロパティ]**


Windows.UI.WebUI.EnteredBackgroundEventHandler <br /> Windows.UI.WebUI.EnteredBackgroundEventHandler.Invoke(System.Object,Windows.ApplicationModel.IEnteredBackgroundEventArgs)
<hr>

**項目**

[Windows.UI.WebUI.LeavingBackgroundEventArgs](/uwp/api/windows.ui.webui.leavingbackgroundeventargs)

**[プロパティ]**


Windows.UI.WebUI.LeavingBackgroundEventArgs <br /> Windows.UI.WebUI.LeavingBackgroundEventArgs.GetDeferral
<hr>

**項目**

[Windows.UI.WebUI.LeavingBackgroundEventHandler](/uwp/api/windows.ui.webui.leavingbackgroundeventhandler)

**[プロパティ]**


Windows.UI.WebUI.LeavingBackgroundEventHandler <br /> Windows.UI.WebUI.LeavingBackgroundEventHandler.Invoke(System.Object,Windows.ApplicationModel.ILeavingBackgroundEventArgs)
<hr>

**項目**

[Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs](/uwp/api/windows.ui.webui.webuiuserdataaccountprovideractivatedeventargs)

**[プロパティ]**


Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs <br /> Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs.ActivatedOperation <br /> Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs.Kind <br /> Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs.Operation <br /> Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs.PreviousExecutionState <br /> Windows.UI.WebUI.WebUIUserDataAccountProviderActivatedEventArgs.SplashScreen
<hr>

**項目**

[Windows.UI.Xaml.ApplicationRequiresPointerMode](/uwp/api/windows.ui.xaml.applicationrequirespointermode)

**[プロパティ]**


Windows.UI.Xaml.ApplicationRequiresPointerMode <br /> Windows.UI.Xaml.ApplicationRequiresPointerMode.Auto <br /> Windows.UI.Xaml.ApplicationRequiresPointerMode.WhenRequested
<hr>

**項目**

[Windows.UI.Xaml.ElementSoundKind](/uwp/api/windows.ui.xaml.elementsoundkind)

**[プロパティ]**


Windows.UI.Xaml.ElementSoundKind <br /> Windows.UI.Xaml.ElementSoundKind.Focus <br /> Windows.UI.Xaml.ElementSoundKind.GoBack <br /> Windows.UI.Xaml.ElementSoundKind.Hide <br /> Windows.UI.Xaml.ElementSoundKind.Invoke <br /> Windows.UI.Xaml.ElementSoundKind.MoveNext <br /> Windows.UI.Xaml.ElementSoundKind.MovePrevious <br /> Windows.UI.Xaml.ElementSoundKind.Show
<hr>

**項目**

[Windows.UI.Xaml.ElementSoundMode](/uwp/api/windows.ui.xaml.elementsoundmode)

**[プロパティ]**


Windows.UI.Xaml.ElementSoundMode <br /> Windows.UI.Xaml.ElementSoundMode.Default <br /> Windows.UI.Xaml.ElementSoundMode.FocusOnly <br /> Windows.UI.Xaml.ElementSoundMode.Off
<hr>

**項目**

[Windows.UI.Xaml.ElementSoundPlayer](/uwp/api/windows.ui.xaml.elementsoundplayer)

**[プロパティ]**


Windows.UI.Xaml.ElementSoundPlayer <br /> Windows.UI.Xaml.ElementSoundPlayer.State <br /> Windows.UI.Xaml.ElementSoundPlayer.Volume <br /> Windows.UI.Xaml.ElementSoundPlayer.Play(Windows.UI.Xaml.ElementSoundKind)
<hr>

**項目**

[Windows.UI.Xaml.ElementSoundPlayerState](/uwp/api/windows.ui.xaml.elementsoundplayerstate)

**[プロパティ]**


Windows.UI.Xaml.ElementSoundPlayerState <br /> Windows.UI.Xaml.ElementSoundPlayerState.Auto <br /> Windows.UI.Xaml.ElementSoundPlayerState.Off <br /> Windows.UI.Xaml.ElementSoundPlayerState.On
<hr>

**項目**

[Windows.UI.Xaml.EnteredBackgroundEventHandler](/uwp/api/windows.ui.xaml.enteredbackgroundeventhandler)

**[プロパティ]**


Windows.UI.Xaml.EnteredBackgroundEventHandler <br /> Windows.UI.Xaml.EnteredBackgroundEventHandler.Invoke(System.Object,Windows.ApplicationModel.EnteredBackgroundEventArgs)
<hr>

**項目**

[Windows.UI.Xaml.FocusVisualKind](/uwp/api/windows.ui.xaml.focusvisualkind)

**[プロパティ]**


Windows.UI.Xaml.FocusVisualKind <br /> Windows.UI.Xaml.FocusVisualKind.DottedLine <br /> Windows.UI.Xaml.FocusVisualKind.HighVisibility
<hr>

**項目**

[Windows.UI.Xaml.LeavingBackgroundEventHandler](/uwp/api/windows.ui.xaml.leavingbackgroundeventhandler)

**[プロパティ]**


Windows.UI.Xaml.LeavingBackgroundEventHandler <br /> Windows.UI.Xaml.LeavingBackgroundEventHandler.Invoke(System.Object,Windows.ApplicationModel.LeavingBackgroundEventArgs)
<hr>

**項目**

[Windows.UI.Xaml.Automation.Peers.InkToolbarAutomationPeer](/uwp/api/windows.ui.xaml.automation.peers.inktoolbarautomationpeer)

**[プロパティ]**


Windows.UI.Xaml.Automation.Peers.InkToolbarAutomationPeer
<hr>

**項目**

[Windows.UI.Xaml.Automation.Peers.MediaPlayerElementAutomationPeer](/uwp/api/windows.ui.xaml.automation.peers.mediaplayerelementautomationpeer)

**[プロパティ]**


Windows.UI.Xaml.Automation.Peers.MediaPlayerElementAutomationPeer <br /> Windows.UI.Xaml.Automation.Peers.MediaPlayerElementAutomationPeer.#ctor(Windows.UI.Xaml.Controls.MediaPlayerElement)
<hr>

**項目**

[Windows.UI.Xaml.Controls.CommandBarDefaultLabelPosition](/uwp/api/windows.ui.xaml.controls.commandbardefaultlabelposition)

**[プロパティ]**


Windows.UI.Xaml.Controls.CommandBarDefaultLabelPosition <br /> Windows.UI.Xaml.Controls.CommandBarDefaultLabelPosition.Bottom <br /> Windows.UI.Xaml.Controls.CommandBarDefaultLabelPosition.Collapsed <br /> Windows.UI.Xaml.Controls.CommandBarDefaultLabelPosition.Right
<hr>

**項目**

[Windows.UI.Xaml.Controls.CommandBarDynamicOverflowAction](/uwp/api/windows.ui.xaml.controls.commandbardynamicoverflowaction)

**[プロパティ]**


Windows.UI.Xaml.Controls.CommandBarDynamicOverflowAction <br /> Windows.UI.Xaml.Controls.CommandBarDynamicOverflowAction.AddingToOverflow <br /> Windows.UI.Xaml.Controls.CommandBarDynamicOverflowAction.RemovingFromOverflow
<hr>

**項目**

[Windows.UI.Xaml.Controls.CommandBarLabelPosition](/uwp/api/windows.ui.xaml.controls.commandbarlabelposition)

**[プロパティ]**


Windows.UI.Xaml.Controls.CommandBarLabelPosition <br /> Windows.UI.Xaml.Controls.CommandBarLabelPosition.Collapsed <br /> Windows.UI.Xaml.Controls.CommandBarLabelPosition.Default
<hr>

**項目**

[Windows.UI.Xaml.Controls.CommandBarOverflowButtonVisibility](/uwp/api/windows.ui.xaml.controls.commandbaroverflowbuttonvisibility)

**[プロパティ]**


Windows.UI.Xaml.Controls.CommandBarOverflowButtonVisibility <br /> Windows.UI.Xaml.Controls.CommandBarOverflowButtonVisibility.Auto <br /> Windows.UI.Xaml.Controls.CommandBarOverflowButtonVisibility.Collapsed <br /> Windows.UI.Xaml.Controls.CommandBarOverflowButtonVisibility.Visible
<hr>

**項目**

[Windows.UI.Xaml.Controls.DynamicOverflowItemsChangingEventArgs](/uwp/api/windows.ui.xaml.controls.dynamicoverflowitemschangingeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.DynamicOverflowItemsChangingEventArgs <br /> Windows.UI.Xaml.Controls.DynamicOverflowItemsChangingEventArgs.#ctor <br /> Windows.UI.Xaml.Controls.DynamicOverflowItemsChangingEventArgs.Action
<hr>

**項目**

[Windows.UI.Xaml.Controls.FocusDisengagedEventArgs](/uwp/api/windows.ui.xaml.controls.focusdisengagedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.FocusDisengagedEventArgs
<hr>

**項目**

[Windows.UI.Xaml.Controls.FocusEngagedEventArgs](/uwp/api/windows.ui.xaml.controls.focusengagedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.FocusEngagedEventArgs
<hr>

**項目**

[Windows.UI.Xaml.Controls.ICommandBarElement2](/uwp/api/windows.ui.xaml.controls.icommandbarelement2)

**[プロパティ]**


Windows.UI.Xaml.Controls.ICommandBarElement2 <br /> Windows.UI.Xaml.Controls.ICommandBarElement2.DynamicOverflowOrder <br /> Windows.UI.Xaml.Controls.ICommandBarElement2.IsInOverflow
<hr>

**項目**

[Windows.UI.Xaml.Controls.IInsertionPanel](/uwp/api/windows.ui.xaml.controls.iinsertionpanel)

**[プロパティ]**


Windows.UI.Xaml.Controls.IInsertionPanel <br /> Windows.UI.Xaml.Controls.IInsertionPanel.GetInsertionIndexes(Windows.Foundation.Point,System.Int32@,System.Int32@)
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbar](/uwp/api/windows.ui.xaml.controls.inktoolbar)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbar <br /> Windows.UI.Xaml.Controls.InkToolbar.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbar.ActiveTool <br /> Windows.UI.Xaml.Controls.InkToolbar.ActiveToolProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.Children <br /> Windows.UI.Xaml.Controls.InkToolbar.ChildrenProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.InitialControls <br /> Windows.UI.Xaml.Controls.InkToolbar.InitialControlsProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.InkDrawingAttributes <br /> Windows.UI.Xaml.Controls.InkToolbar.InkDrawingAttributesProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.IsRulerButtonChecked <br /> Windows.UI.Xaml.Controls.InkToolbar.IsRulerButtonCheckedProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.TargetInkCanvas <br /> Windows.UI.Xaml.Controls.InkToolbar.TargetInkCanvasProperty <br /> Windows.UI.Xaml.Controls.InkToolbar.ActiveToolChanged <br /> Windows.UI.Xaml.Controls.InkToolbar.EraseAllClicked <br /> Windows.UI.Xaml.Controls.InkToolbar.InkDrawingAttributesChanged <br /> Windows.UI.Xaml.Controls.InkToolbar.IsRulerButtonCheckedChanged <br /> Windows.UI.Xaml.Controls.InkToolbar.GetToggleButton(Windows.UI.Xaml.Controls.InkToolbarToggle) <br /> Windows.UI.Xaml.Controls.InkToolbar.GetToolButton(Windows.UI.Xaml.Controls.InkToolbarTool)
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarBallpointPenButton](/uwp/api/windows.ui.xaml.controls.inktoolbarballpointpenbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarBallpointPenButton <br /> Windows.UI.Xaml.Controls.InkToolbarBallpointPenButton.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarCustomPen](/uwp/api/windows.ui.xaml.controls.inktoolbarcustompen)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarCustomPen <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPen.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPen.CreateInkDrawingAttributes(Windows.UI.Xaml.Media.Brush,System.Double) <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPen.CreateInkDrawingAttributesCore(Windows.UI.Xaml.Media.Brush,System.Double)
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarCustomPenButton](/uwp/api/windows.ui.xaml.controls.inktoolbarcustompenbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarCustomPenButton <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPenButton.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPenButton.ConfigurationContent <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPenButton.ConfigurationContentProperty <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPenButton.CustomPen <br /> Windows.UI.Xaml.Controls.InkToolbarCustomPenButton.CustomPenProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton](/uwp/api/windows.ui.xaml.controls.inktoolbarcustomtogglebutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton <br /> Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarCustomToolButton](/uwp/api/windows.ui.xaml.controls.inktoolbarcustomtoolbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarCustomToolButton <br /> Windows.UI.Xaml.Controls.InkToolbarCustomToolButton.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbarCustomToolButton.ConfigurationContent <br /> Windows.UI.Xaml.Controls.InkToolbarCustomToolButton.ConfigurationContentProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarEraserButton](/uwp/api/windows.ui.xaml.controls.inktoolbareraserbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarEraserButton <br /> Windows.UI.Xaml.Controls.InkToolbarEraserButton.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarHighlighterButton](/uwp/api/windows.ui.xaml.controls.inktoolbarhighlighterbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarHighlighterButton <br /> Windows.UI.Xaml.Controls.InkToolbarHighlighterButton.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarInitialControls](/uwp/api/windows.ui.xaml.controls.inktoolbarinitialcontrols)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarInitialControls <br /> Windows.UI.Xaml.Controls.InkToolbarInitialControls.All <br /> Windows.UI.Xaml.Controls.InkToolbarInitialControls.AllExceptPens <br /> Windows.UI.Xaml.Controls.InkToolbarInitialControls.None <br /> Windows.UI.Xaml.Controls.InkToolbarInitialControls.PensOnly
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarPenButton](/uwp/api/windows.ui.xaml.controls.inktoolbarpenbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarPenButton <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.MaxStrokeWidth <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.MaxStrokeWidthProperty <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.MinStrokeWidth <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.MinStrokeWidthProperty <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.Palette <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.PaletteProperty <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedBrush <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedBrushIndex <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedBrushIndexProperty <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedBrushProperty <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedStrokeWidth <br /> Windows.UI.Xaml.Controls.InkToolbarPenButton.SelectedStrokeWidthProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarPencilButton](/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarPencilButton <br /> Windows.UI.Xaml.Controls.InkToolbarPencilButton.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarPenConfigurationControl](/uwp/api/windows.ui.xaml.controls.inktoolbarpenconfigurationcontrol)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarPenConfigurationControl <br /> Windows.UI.Xaml.Controls.InkToolbarPenConfigurationControl.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbarPenConfigurationControl.PenButton <br /> Windows.UI.Xaml.Controls.InkToolbarPenConfigurationControl.PenButtonProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarRulerButton](/uwp/api/windows.ui.xaml.controls.inktoolbarrulerbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarRulerButton <br /> Windows.UI.Xaml.Controls.InkToolbarRulerButton.#ctor <br /> Windows.UI.Xaml.Controls.InkToolbarRulerButton.Ruler <br /> Windows.UI.Xaml.Controls.InkToolbarRulerButton.RulerProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarToggle](/uwp/api/windows.ui.xaml.controls.inktoolbartoggle)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarToggle <br /> Windows.UI.Xaml.Controls.InkToolbarToggle.Custom <br /> Windows.UI.Xaml.Controls.InkToolbarToggle.Ruler
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarToggleButton](/uwp/api/windows.ui.xaml.controls.inktoolbartogglebutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarToggleButton <br /> Windows.UI.Xaml.Controls.InkToolbarToggleButton.ToggleKind
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarTool](/uwp/api/windows.ui.xaml.controls.inktoolbartool)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarTool <br /> Windows.UI.Xaml.Controls.InkToolbarTool.BallpointPen <br /> Windows.UI.Xaml.Controls.InkToolbarTool.CustomPen <br /> Windows.UI.Xaml.Controls.InkToolbarTool.CustomTool <br /> Windows.UI.Xaml.Controls.InkToolbarTool.Eraser <br /> Windows.UI.Xaml.Controls.InkToolbarTool.Highlighter <br /> Windows.UI.Xaml.Controls.InkToolbarTool.Pencil
<hr>

**項目**

[Windows.UI.Xaml.Controls.InkToolbarToolButton](/uwp/api/windows.ui.xaml.controls.inktoolbartoolbutton)

**[プロパティ]**


Windows.UI.Xaml.Controls.InkToolbarToolButton <br /> Windows.UI.Xaml.Controls.InkToolbarToolButton.IsExtensionGlyphShown <br /> Windows.UI.Xaml.Controls.InkToolbarToolButton.IsExtensionGlyphShownProperty <br /> Windows.UI.Xaml.Controls.InkToolbarToolButton.ToolKind
<hr>

**項目**

[Windows.UI.Xaml.Controls.LightDismissOverlayMode](/uwp/api/windows.ui.xaml.controls.lightdismissoverlaymode)

**[プロパティ]**


Windows.UI.Xaml.Controls.LightDismissOverlayMode <br /> Windows.UI.Xaml.Controls.LightDismissOverlayMode.Auto <br /> Windows.UI.Xaml.Controls.LightDismissOverlayMode.Off <br /> Windows.UI.Xaml.Controls.LightDismissOverlayMode.On
<hr>

**項目**

[Windows.UI.Xaml.Controls.MediaPlayerElement](/uwp/api/windows.ui.xaml.controls.mediaplayerelement)

**[プロパティ]**


Windows.UI.Xaml.Controls.MediaPlayerElement <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.#ctor <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.AreTransportControlsEnabled <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.AreTransportControlsEnabledProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.AutoPlay <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.AutoPlayProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.IsFullWindow <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.IsFullWindowProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.MediaPlayer <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.MediaPlayerProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.PosterSource <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.PosterSourceProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.Source <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.SourceProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.Stretch <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.StretchProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.TransportControls <br /> Windows.UI.Xaml.Controls.MediaPlayerElement.SetMediaPlayer(Windows.Media.Playback.MediaPlayer)
<hr>

**項目**

[Windows.UI.Xaml.Controls.MediaPlayerPresenter](/uwp/api/windows.ui.xaml.controls.mediaplayerpresenter)

**[プロパティ]**


Windows.UI.Xaml.Controls.MediaPlayerPresenter <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.#ctor <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.IsFullWindow <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.IsFullWindowProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.MediaPlayer <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.MediaPlayerProperty <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.Stretch <br /> Windows.UI.Xaml.Controls.MediaPlayerPresenter.StretchProperty
<hr>

**項目**

[Windows.UI.Xaml.Controls.PivotHeaderFocusVisualPlacement](/uwp/api/windows.ui.xaml.controls.pivotheaderfocusvisualplacement)

**[プロパティ]**


Windows.UI.Xaml.Controls.PivotHeaderFocusVisualPlacement <br /> Windows.UI.Xaml.Controls.PivotHeaderFocusVisualPlacement.ItemHeaders <br /> Windows.UI.Xaml.Controls.PivotHeaderFocusVisualPlacement.SelectedItemHeader
<hr>

**項目**

[Windows.UI.Xaml.Controls.RequiresPointer](/uwp/api/windows.ui.xaml.controls.requirespointer)

**[プロパティ]**


Windows.UI.Xaml.Controls.RequiresPointer <br /> Windows.UI.Xaml.Controls.RequiresPointer.Never <br /> Windows.UI.Xaml.Controls.RequiresPointer.WhenEngaged <br /> Windows.UI.Xaml.Controls.RequiresPointer.WhenFocused
<hr>

**項目**

[Windows.UI.Xaml.Controls.Maps.MapVisibleRegionKind](/uwp/api/windows.ui.xaml.controls.maps.mapvisibleregionkind)

**[プロパティ]**


Windows.UI.Xaml.Controls.Maps.MapVisibleRegionKind <br /> Windows.UI.Xaml.Controls.Maps.MapVisibleRegionKind.Full <br /> Windows.UI.Xaml.Controls.Maps.MapVisibleRegionKind.Near
<hr>

**項目**

[Windows.UI.Xaml.Controls.Primitives.FlyoutBaseClosingEventArgs](/uwp/api/windows.ui.xaml.controls.primitives.flyoutbaseclosingeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.Primitives.FlyoutBaseClosingEventArgs <br /> Windows.UI.Xaml.Controls.Primitives.FlyoutBaseClosingEventArgs.Cancel
<hr>

**項目**

[Windows.UI.Xaml.Input.AccessKeyDisplayDismissedEventArgs](/uwp/api/windows.ui.xaml.input.accesskeydisplaydismissedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Input.AccessKeyDisplayDismissedEventArgs <br /> Windows.UI.Xaml.Input.AccessKeyDisplayDismissedEventArgs.#ctor
<hr>

**項目**

[Windows.UI.Xaml.Input.AccessKeyDisplayRequestedEventArgs](/uwp/api/windows.ui.xaml.input.accesskeydisplayrequestedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Input.AccessKeyDisplayRequestedEventArgs <br /> Windows.UI.Xaml.Input.AccessKeyDisplayRequestedEventArgs.#ctor <br /> Windows.UI.Xaml.Input.AccessKeyDisplayRequestedEventArgs.PressedKeys
<hr>

**項目**

[Windows.UI.Xaml.Input.AccessKeyInvokedEventArgs](/uwp/api/windows.ui.xaml.input.accesskeyinvokedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Input.AccessKeyInvokedEventArgs <br /> Windows.UI.Xaml.Input.AccessKeyInvokedEventArgs.#ctor <br /> Windows.UI.Xaml.Input.AccessKeyInvokedEventArgs.Handled
<hr>

**項目**

[Windows.UI.Xaml.Input.AccessKeyManager](/uwp/api/windows.ui.xaml.input.accesskeymanager)

**[プロパティ]**


Windows.UI.Xaml.Input.AccessKeyManager <br /> Windows.UI.Xaml.Input.AccessKeyManager.IsDisplayModeEnabled <br /> Windows.UI.Xaml.Input.AccessKeyManager.IsDisplayModeEnabledChanged <br /> Windows.UI.Xaml.Input.AccessKeyManager.ExitDisplayMode
<hr>

**項目**

[Windows.UI.Xaml.Input.ContextRequestedEventArgs](/uwp/api/windows.ui.xaml.input.contextrequestedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Input.ContextRequestedEventArgs <br /> Windows.UI.Xaml.Input.ContextRequestedEventArgs.#ctor <br /> Windows.UI.Xaml.Input.ContextRequestedEventArgs.Handled <br /> Windows.UI.Xaml.Input.ContextRequestedEventArgs.TryGetPosition(Windows.UI.Xaml.UIElement,Windows.Foundation.Point@)
<hr>

**項目**

[Windows.UI.Xaml.Media.BrushCollection](/uwp/api/windows.ui.xaml.media.brushcollection)

**[プロパティ]**


Windows.UI.Xaml.Media.BrushCollection <br /> Windows.UI.Xaml.Media.BrushCollection.#ctor <br /> Windows.UI.Xaml.Media.BrushCollection.Size <br /> Windows.UI.Xaml.Media.BrushCollection.Append(Windows.UI.Xaml.Media.Brush) <br /> Windows.UI.Xaml.Media.BrushCollection.Clear <br /> Windows.UI.Xaml.Media.BrushCollection.First <br /> Windows.UI.Xaml.Media.BrushCollection.GetAt(System.UInt32) <br /> Windows.UI.Xaml.Media.BrushCollection.GetMany(System.UInt32,Windows.UI.Xaml.Media.Brush[]) <br /> Windows.UI.Xaml.Media.BrushCollection.GetView <br /> Windows.UI.Xaml.Media.BrushCollection.IndexOf(Windows.UI.Xaml.Media.Brush,System.UInt32@) <br /> Windows.UI.Xaml.Media.BrushCollection.InsertAt(System.UInt32,Windows.UI.Xaml.Media.Brush) <br /> Windows.UI.Xaml.Media.BrushCollection.RemoveAt(System.UInt32) <br /> Windows.UI.Xaml.Media.BrushCollection.RemoveAtEnd <br /> Windows.UI.Xaml.Media.BrushCollection.ReplaceAll(Windows.UI.Xaml.Media.Brush[]) <br /> Windows.UI.Xaml.Media.BrushCollection.SetAt(System.UInt32,Windows.UI.Xaml.Media.Brush)
<hr>

**項目**

[Windows.UI.Xaml.Media.FastPlayFallbackBehaviour](/uwp/api/windows.ui.xaml.media.fastplayfallbackbehaviour)

**[プロパティ]**


Windows.UI.Xaml.Media.FastPlayFallbackBehaviour <br /> Windows.UI.Xaml.Media.FastPlayFallbackBehaviour.Disable <br /> Windows.UI.Xaml.Media.FastPlayFallbackBehaviour.Hide <br /> Windows.UI.Xaml.Media.FastPlayFallbackBehaviour.Skip
<hr>

**項目**

[Windows.UI.Xaml.Media.MediaTransportControlsThumbnailRequestedEventArgs](/uwp/api/windows.ui.xaml.media.mediatransportcontrolsthumbnailrequestedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Media.MediaTransportControlsThumbnailRequestedEventArgs <br /> Windows.UI.Xaml.Media.MediaTransportControlsThumbnailRequestedEventArgs.GetDeferral <br /> Windows.UI.Xaml.Media.MediaTransportControlsThumbnailRequestedEventArgs.SetThumbnailImage(Windows.Storage.Streams.IInputStream)
<hr>

**項目**

[Windows.UI.Xaml.Media.Animation.ConnectedAnimation](/uwp/api/windows.ui.xaml.media.animation.connectedanimation)

**[プロパティ]**


Windows.UI.Xaml.Media.Animation.ConnectedAnimation <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimation.Completed <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimation.Cancel <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimation.TryStart(Windows.UI.Xaml.UIElement)
<hr>

**項目**

[Windows.UI.Xaml.Media.Animation.ConnectedAnimationService](/uwp/api/windows.ui.xaml.media.animation.connectedanimationservice)

**[プロパティ]**


Windows.UI.Xaml.Media.Animation.ConnectedAnimationService <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimationService.DefaultDuration <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimationService.DefaultEasingFunction <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimationService.GetAnimation(System.String) <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimationService.GetForCurrentView <br /> Windows.UI.Xaml.Media.Animation.ConnectedAnimationService.PrepareToAnimate(System.String,Windows.UI.Xaml.UIElement)
<hr>

**項目**

[Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs](/uwp/api/windows.web.http.filters.httpservercustomvalidationrequestedeventargs)

**[プロパティ]**


Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.RequestMessage <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.ServerCertificate <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.ServerCertificateErrors <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.ServerCertificateErrorSeverity <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.ServerIntermediateCertificates <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.GetDeferral <br /> Windows.Web.Http.Filters.HttpServerCustomValidationRequestedEventArgs.Reject
<hr>

**項目**

[Windows.Graphics.Printing3D.Printing3DFaceReductionOptions](/uwp/api/windows.graphics.printing3d.printing3dfacereductionoptions)

**[プロパティ]**


Windows.Graphics.Printing3D.Printing3DFaceReductionOptions <br /> Windows.Graphics.Printing3D.Printing3DFaceReductionOptions.#ctor <br /> Windows.Graphics.Printing3D.Printing3DFaceReductionOptions.MaxEdgeLength <br /> Windows.Graphics.Printing3D.Printing3DFaceReductionOptions.MaxReductionArea <br /> Windows.Graphics.Printing3D.Printing3DFaceReductionOptions.TargetTriangleCount
<hr>

**項目**

[Windows.Media.Capture.AppCaptureVideoEncodingFrameRateMode](/uwp/api/windows.media.capture.appcapturevideoencodingframeratemode)

**[プロパティ]**


Windows.Media.Capture.AppCaptureVideoEncodingFrameRateMode <br /> Windows.Media.Capture.AppCaptureVideoEncodingFrameRateMode.High <br /> Windows.Media.Capture.AppCaptureVideoEncodingFrameRateMode.Standard
<hr>

**項目**

[Windows.Security.EnterpriseData.ProtectionPolicyAuditAction](/uwp/api/windows.security.enterprisedata.protectionpolicyauditaction)

**[プロパティ]**


Windows.Security.EnterpriseData.ProtectionPolicyAuditAction <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditAction.CopyToLocation <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditAction.Decrypt <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditAction.Other <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditAction.SendToRecipient
<hr>

**項目**

[Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo](/uwp/api/windows.security.enterprisedata.protectionpolicyauditinfo)

**[プロパティ]**


Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.#ctor(Windows.Security.EnterpriseData.ProtectionPolicyAuditAction,System.String) <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.#ctor(Windows.Security.EnterpriseData.ProtectionPolicyAuditAction,System.String,System.String,System.String) <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.Action <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.DataDescription <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.SourceDescription <br /> Windows.Security.EnterpriseData.ProtectionPolicyAuditInfo.TargetDescription
<hr>

**項目**

[Windows.Security.EnterpriseData.ProtectionPolicyRequestAccessBehavior](/uwp/api/windows.security.enterprisedata.protectionpolicyrequestaccessbehavior)

**[プロパティ]**


Windows.Security.EnterpriseData.ProtectionPolicyRequestAccessBehavior <br /> Windows.Security.EnterpriseData.ProtectionPolicyRequestAccessBehavior.Decrypt <br /> Windows.Security.EnterpriseData.ProtectionPolicyRequestAccessBehavior.TreatOverridePolicyAsBlock
<hr>

**項目**

[Windows.Services.Maps.LocalSearch.LocalLocationHoursOfOperationItem](/uwp/api/windows.services.maps.localsearch.locallocationhoursofoperationitem)

**[プロパティ]**


Windows.Services.Maps.LocalSearch.LocalLocationHoursOfOperationItem <br /> Windows.Services.Maps.LocalSearch.LocalLocationHoursOfOperationItem.Day <br /> Windows.Services.Maps.LocalSearch.LocalLocationHoursOfOperationItem.Span <br /> Windows.Services.Maps.LocalSearch.LocalLocationHoursOfOperationItem.Start
<hr>

**項目**

[Windows.Services.Maps.LocalSearch.LocalLocationRatingInfo](/uwp/api/windows.services.maps.localsearch.locallocationratinginfo)

**[プロパティ]**


Windows.Services.Maps.LocalSearch.LocalLocationRatingInfo <br /> Windows.Services.Maps.LocalSearch.LocalLocationRatingInfo.AggregateRating <br /> Windows.Services.Maps.LocalSearch.LocalLocationRatingInfo.ProviderIdentifier <br /> Windows.Services.Maps.LocalSearch.LocalLocationRatingInfo.RatingCount
<hr>

**項目**

[Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerEnteredEventArgs](/uwp/api/windows.ui.xaml.controls.maps.mapcontrolbusinesslandmarkpointerenteredeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerEnteredEventArgs <br /> Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerEnteredEventArgs.#ctor <br /> Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerEnteredEventArgs.LocalLocations
<hr>

**項目**

[Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerExitedEventArgs](/uwp/api/windows.ui.xaml.controls.maps.mapcontrolbusinesslandmarkpointerexitedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerExitedEventArgs <br /> Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerExitedEventArgs.#ctor <br /> Windows.UI.Xaml.Controls.Maps.MapControlBusinessLandmarkPointerExitedEventArgs.LocalLocations
<hr>

**項目**

[Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs](/uwp/api/windows.ui.xaml.controls.maps.mapcontroltransitfeaturepointerenteredeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs.#ctor <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs.DisplayName <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs.Location <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerEnteredEventArgs.TransitProperties
<hr>

**項目**

[Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs](/uwp/api/windows.ui.xaml.controls.maps.mapcontroltransitfeaturepointerexitedeventargs)

**[プロパティ]**


Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs.#ctor <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs.DisplayName <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs.Location <br /> Windows.UI.Xaml.Controls.Maps.MapControlTransitFeaturePointerExitedEventArgs.TransitProperties
<hr>

**項目**

[Windows.Services.Store.StoreAcquireLicenseResult](/uwp/api/windows.services.store.storeacquirelicenseresult)

**[プロパティ]**


Windows.Services.Store.StoreAcquireLicenseResult <br /> Windows.Services.Store.StoreAcquireLicenseResult.ExtendedError <br /> Windows.Services.Store.StoreAcquireLicenseResult.StorePackageLicense
<hr>

**項目**

[Windows.Services.Store.StoreAppLicense](/uwp/api/windows.services.store.storeapplicense)

**[プロパティ]**


Windows.Services.Store.StoreAppLicense <br /> Windows.Services.Store.StoreAppLicense.AddOnLicenses <br /> Windows.Services.Store.StoreAppLicense.ExpirationDate <br /> Windows.Services.Store.StoreAppLicense.ExtendedJsonData <br /> Windows.Services.Store.StoreAppLicense.IsActive <br /> Windows.Services.Store.StoreAppLicense.IsTrial <br /> Windows.Services.Store.StoreAppLicense.IsTrialOwnedByThisUser <br /> Windows.Services.Store.StoreAppLicense.SkuStoreId <br /> Windows.Services.Store.StoreAppLicense.TrialTimeRemaining <br /> Windows.Services.Store.StoreAppLicense.TrialUniqueId
<hr>

**項目**

[Windows.Services.Store.StoreAvailability](/uwp/api/windows.services.store.storeavailability)

**[プロパティ]**


Windows.Services.Store.StoreAvailability <br /> Windows.Services.Store.StoreAvailability.EndDate <br /> Windows.Services.Store.StoreAvailability.ExtendedJsonData <br /> Windows.Services.Store.StoreAvailability.Price <br /> Windows.Services.Store.StoreAvailability.StoreId <br /> Windows.Services.Store.StoreAvailability.RequestPurchaseAsync <br /> Windows.Services.Store.StoreAvailability.RequestPurchaseAsync(Windows.Services.Store.StorePurchaseProperties)
<hr>

**項目**

[Windows.Services.Store.StoreCollectionData](/uwp/api/windows.services.store.storecollectiondata)

**[プロパティ]**


Windows.Services.Store.StoreCollectionData <br /> Windows.Services.Store.StoreCollectionData.AcquiredDate <br /> Windows.Services.Store.StoreCollectionData.CampaignId <br /> Windows.Services.Store.StoreCollectionData.DeveloperOfferId <br /> Windows.Services.Store.StoreCollectionData.EndDate <br /> Windows.Services.Store.StoreCollectionData.ExtendedJsonData <br /> Windows.Services.Store.StoreCollectionData.IsTrial <br /> Windows.Services.Store.StoreCollectionData.StartDate <br /> Windows.Services.Store.StoreCollectionData.TrialTimeRemaining
<hr>

**項目**

[Windows.Services.Store.StoreConsumableResult](/uwp/api/windows.services.store.storeconsumableresult)

**[プロパティ]**


Windows.Services.Store.StoreConsumableResult <br /> Windows.Services.Store.StoreConsumableResult.BalanceRemaining <br /> Windows.Services.Store.StoreConsumableResult.ExtendedError <br /> Windows.Services.Store.StoreConsumableResult.Status <br /> Windows.Services.Store.StoreConsumableResult.TrackingId
<hr>

**項目**

[Windows.Services.Store.StoreConsumableStatus](/uwp/api/windows.services.store.storeconsumablestatus)

**[プロパティ]**


Windows.Services.Store.StoreConsumableStatus <br /> Windows.Services.Store.StoreConsumableStatus.InsufficentQuantity <br /> Windows.Services.Store.StoreConsumableStatus.NetworkError <br /> Windows.Services.Store.StoreConsumableStatus.ServerError <br /> Windows.Services.Store.StoreConsumableStatus.Succeeded
<hr>

**項目**

[Windows.Services.Store.StoreContext](/uwp/api/windows.services.store.storecontext)

**[プロパティ]**


Windows.Services.Store.StoreContext <br /> Windows.Services.Store.StoreContext.User <br /> Windows.Services.Store.StoreContext.OfflineLicensesChanged <br /> Windows.Services.Store.StoreContext.AcquireStoreLicenseForOptionalPackageAsync(Windows.ApplicationModel.Package) <br /> Windows.Services.Store.StoreContext.GetAppAndOptionalStorePackageUpdatesAsync <br /> Windows.Services.Store.StoreContext.GetAppLicenseAsync <br /> Windows.Services.Store.StoreContext.GetAssociatedStoreProductsAsync(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Services.Store.StoreContext.GetAssociatedStoreProductsWithPagingAsync(Windows.Foundation.Collections.IIterable{System.String},System.UInt32) <br /> Windows.Services.Store.StoreContext.GetConsumableBalanceRemainingAsync(System.String) <br /> Windows.Services.Store.StoreContext.GetCustomerCollectionsIdAsync(System.String,System.String) <br /> Windows.Services.Store.StoreContext.GetCustomerPurchaseIdAsync(System.String,System.String) <br /> Windows.Services.Store.StoreContext.GetDefault <br /> Windows.Services.Store.StoreContext.GetForUser(Windows.System.User) <br /> Windows.Services.Store.StoreContext.GetStoreProductForCurrentAppAsync <br /> Windows.Services.Store.StoreContext.GetStoreProductsAsync(Windows.Foundation.Collections.IIterable{System.String},Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Services.Store.StoreContext.GetUserCollectionAsync(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Services.Store.StoreContext.GetUserCollectionWithPagingAsync(Windows.Foundation.Collections.IIterable{System.String},System.UInt32) <br /> Windows.Services.Store.StoreContext.ReportConsumableFulfillmentAsync(System.String,System.UInt32,System.Guid) <br /> Windows.Services.Store.StoreContext.RequestDownloadAndInstallStorePackagesAsync(Windows.Foundation.Collections.IIterable{System.String}) <br /> Windows.Services.Store.StoreContext.RequestDownloadAndInstallStorePackageUpdatesAsync(Windows.Foundation.Collections.IIterable{Windows.Services.Store.StorePackageUpdate}) <br /> Windows.Services.Store.StoreContext.RequestDownloadStorePackageUpdatesAsync(Windows.Foundation.Collections.IIterable{Windows.Services.Store.StorePackageUpdate}) <br /> Windows.Services.Store.StoreContext.RequestPurchaseAsync(System.String) <br /> Windows.Services.Store.StoreContext.RequestPurchaseAsync(System.String,Windows.Services.Store.StorePurchaseProperties)
<hr>

**項目**

[Windows.Services.Store.StoreDurationUnit](/uwp/api/windows.services.store.storedurationunit)

**[プロパティ]**


Windows.Services.Store.StoreDurationUnit <br /> Windows.Services.Store.StoreDurationUnit.Day <br /> Windows.Services.Store.StoreDurationUnit.Hour <br /> Windows.Services.Store.StoreDurationUnit.Minute <br /> Windows.Services.Store.StoreDurationUnit.Month <br /> Windows.Services.Store.StoreDurationUnit.Week <br /> Windows.Services.Store.StoreDurationUnit.Year
<hr>

**項目**

[Windows.Services.Store.StoreImage](/uwp/api/windows.services.store.storeimage)

**[プロパティ]**


Windows.Services.Store.StoreImage <br /> Windows.Services.Store.StoreImage.Caption <br /> Windows.Services.Store.StoreImage.Height <br /> Windows.Services.Store.StoreImage.ImagePurposeTag <br /> Windows.Services.Store.StoreImage.Uri <br /> Windows.Services.Store.StoreImage.Width
<hr>

**項目**

[Windows.Services.Store.StoreLicense](/uwp/api/windows.services.store.storelicense)

**[プロパティ]**


Windows.Services.Store.StoreLicense <br /> Windows.Services.Store.StoreLicense.ExpirationDate <br /> Windows.Services.Store.StoreLicense.ExtendedJsonData <br /> Windows.Services.Store.StoreLicense.InAppOfferToken <br /> Windows.Services.Store.StoreLicense.IsActive <br /> Windows.Services.Store.StoreLicense.SkuStoreId
<hr>

**項目**

[Windows.Services.Store.StorePackageLicense](/uwp/api/windows.services.store.storepackagelicense)

**[プロパティ]**


Windows.Services.Store.StorePackageLicense <br /> Windows.Services.Store.StorePackageLicense.IsValid <br /> Windows.Services.Store.StorePackageLicense.Package <br /> Windows.Services.Store.StorePackageLicense.LicenseLost <br /> Windows.Services.Store.StorePackageLicense.Close <br /> Windows.Services.Store.StorePackageLicense.ReleaseLicense
<hr>

**項目**

[Windows.Services.Store.StorePackageUpdate](/uwp/api/windows.services.store.storepackageupdate)

**[プロパティ]**


Windows.Services.Store.StorePackageUpdate <br /> Windows.Services.Store.StorePackageUpdate.Mandatory <br /> Windows.Services.Store.StorePackageUpdate.Package
<hr>

**項目**

[Windows.Services.Store.StorePackageUpdateResult](/uwp/api/windows.services.store.storepackageupdateresult)

**[プロパティ]**


Windows.Services.Store.StorePackageUpdateResult <br /> Windows.Services.Store.StorePackageUpdateResult.OverallState <br /> Windows.Services.Store.StorePackageUpdateResult.StorePackageUpdateStatuses
<hr>

**項目**

[Windows.Services.Store.StorePackageUpdateState](/uwp/api/windows.services.store.storepackageupdatestate)

**[プロパティ]**


Windows.Services.Store.StorePackageUpdateState <br /> Windows.Services.Store.StorePackageUpdateState.Canceled <br /> Windows.Services.Store.StorePackageUpdateState.Completed <br /> Windows.Services.Store.StorePackageUpdateState.Deploying <br /> Windows.Services.Store.StorePackageUpdateState.Downloading <br /> Windows.Services.Store.StorePackageUpdateState.ErrorLowBattery <br /> Windows.Services.Store.StorePackageUpdateState.ErrorWiFiRecommended <br /> Windows.Services.Store.StorePackageUpdateState.ErrorWiFiRequired <br /> Windows.Services.Store.StorePackageUpdateState.OtherError <br /> Windows.Services.Store.StorePackageUpdateState.Pending
<hr>

**項目**

[Windows.Services.Store.StorePackageUpdateStatus](/uwp/api/windows.services.store.storepackageupdatestatus)

**[プロパティ]**


Windows.Services.Store.StorePackageUpdateStatus <br /> Windows.Services.Store.StorePackageUpdateStatus.PackageBytesDownloaded <br /> Windows.Services.Store.StorePackageUpdateStatus.PackageDownloadProgress <br /> Windows.Services.Store.StorePackageUpdateStatus.PackageDownloadSizeInBytes <br /> Windows.Services.Store.StorePackageUpdateStatus.PackageFamilyName <br /> Windows.Services.Store.StorePackageUpdateStatus.PackageUpdateState <br /> Windows.Services.Store.StorePackageUpdateStatus.TotalDownloadProgress
<hr>

**項目**

[Windows.Services.Store.StorePrice](/uwp/api/windows.services.store.storeprice)

**[プロパティ]**


Windows.Services.Store.StorePrice <br /> Windows.Services.Store.StorePrice.CurrencyCode <br /> Windows.Services.Store.StorePrice.FormattedBasePrice <br /> Windows.Services.Store.StorePrice.FormattedPrice <br /> Windows.Services.Store.StorePrice.FormattedRecurrencePrice <br /> Windows.Services.Store.StorePrice.IsOnSale <br /> Windows.Services.Store.StorePrice.SaleEndDate
<hr>

**項目**

[Windows.Services.Store.StoreProduct](/uwp/api/windows.services.store.storeproduct)

**[プロパティ]**


Windows.Services.Store.StoreProduct <br /> Windows.Services.Store.StoreProduct.Description <br /> Windows.Services.Store.StoreProduct.ExtendedJsonData <br /> Windows.Services.Store.StoreProduct.HasDigitalDownload <br /> Windows.Services.Store.StoreProduct.Images <br /> Windows.Services.Store.StoreProduct.InAppOfferToken <br /> Windows.Services.Store.StoreProduct.IsInUserCollection <br /> Windows.Services.Store.StoreProduct.Keywords <br /> Windows.Services.Store.StoreProduct.Language <br /> Windows.Services.Store.StoreProduct.LinkUri <br /> Windows.Services.Store.StoreProduct.Price <br /> Windows.Services.Store.StoreProduct.ProductKind <br /> Windows.Services.Store.StoreProduct.Skus <br /> Windows.Services.Store.StoreProduct.StoreId <br /> Windows.Services.Store.StoreProduct.Title <br /> Windows.Services.Store.StoreProduct.Videos <br /> Windows.Services.Store.StoreProduct.GetIsAnySkuInstalledAsync <br /> Windows.Services.Store.StoreProduct.RequestPurchaseAsync <br /> Windows.Services.Store.StoreProduct.RequestPurchaseAsync(Windows.Services.Store.StorePurchaseProperties)
<hr>

**項目**

[Windows.Services.Store.StoreProductPagedQueryResult](/uwp/api/windows.services.store.storeproductpagedqueryresult)

**[プロパティ]**


Windows.Services.Store.StoreProductPagedQueryResult <br /> Windows.Services.Store.StoreProductPagedQueryResult.ExtendedError <br /> Windows.Services.Store.StoreProductPagedQueryResult.HasMoreResults <br /> Windows.Services.Store.StoreProductPagedQueryResult.Products <br /> Windows.Services.Store.StoreProductPagedQueryResult.GetNextAsync
<hr>

**項目**

[Windows.Services.Store.StoreProductQueryResult](/uwp/api/windows.services.store.storeproductqueryresult)

**[プロパティ]**


Windows.Services.Store.StoreProductQueryResult <br /> Windows.Services.Store.StoreProductQueryResult.ExtendedError <br /> Windows.Services.Store.StoreProductQueryResult.Products
<hr>

**項目**

[Windows.Services.Store.StoreProductResult](/uwp/api/windows.services.store.storeproductresult)

**[プロパティ]**


Windows.Services.Store.StoreProductResult <br /> Windows.Services.Store.StoreProductResult.ExtendedError <br /> Windows.Services.Store.StoreProductResult.Product
<hr>

**項目**

[Windows.Services.Store.StorePurchaseProperties](/uwp/api/windows.services.store.storepurchaseproperties)

**[プロパティ]**


Windows.Services.Store.StorePurchaseProperties <br /> Windows.Services.Store.StorePurchaseProperties.#ctor <br /> Windows.Services.Store.StorePurchaseProperties.#ctor(System.String) <br /> Windows.Services.Store.StorePurchaseProperties.ExtendedJsonData <br /> Windows.Services.Store.StorePurchaseProperties.Name
<hr>

**項目**

[Windows.Services.Store.StorePurchaseResult](/uwp/api/windows.services.store.storepurchaseresult)

**[プロパティ]**


Windows.Services.Store.StorePurchaseResult <br /> Windows.Services.Store.StorePurchaseResult.ExtendedError <br /> Windows.Services.Store.StorePurchaseResult.Status
<hr>

**項目**

[Windows.Services.Store.StorePurchaseStatus](/uwp/api/windows.services.store.storepurchasestatus)

**[プロパティ]**


Windows.Services.Store.StorePurchaseStatus <br /> Windows.Services.Store.StorePurchaseStatus.AlreadyPurchased <br /> Windows.Services.Store.StorePurchaseStatus.NetworkError <br /> Windows.Services.Store.StorePurchaseStatus.NotPurchased <br /> Windows.Services.Store.StorePurchaseStatus.ServerError <br /> Windows.Services.Store.StorePurchaseStatus.Succeeded
<hr>

**項目**

[Windows.Services.Store.StoreRequestHelper](/uwp/api/windows.services.store.storerequesthelper)

**[プロパティ]**


Windows.Services.Store.StoreRequestHelper <br /> Windows.Services.Store.StoreRequestHelper.SendRequestAsync(Windows.Services.Store.StoreContext,System.UInt32,System.String)
<hr>

**項目**

[Windows.Services.Store.StoreSendRequestResult](/uwp/api/windows.services.store.storesendrequestresult)

**[プロパティ]**


Windows.Services.Store.StoreSendRequestResult <br /> Windows.Services.Store.StoreSendRequestResult.ExtendedError <br /> Windows.Services.Store.StoreSendRequestResult.Response
<hr>

**項目**

[Windows.Services.Store.StoreSku](/uwp/api/windows.services.store.storesku)

**[プロパティ]**


Windows.Services.Store.StoreSku <br /> Windows.Services.Store.StoreSku.Availabilities <br /> Windows.Services.Store.StoreSku.BundledSkus <br /> Windows.Services.Store.StoreSku.CollectionData <br /> Windows.Services.Store.StoreSku.CustomDeveloperData <br /> Windows.Services.Store.StoreSku.Description <br /> Windows.Services.Store.StoreSku.ExtendedJsonData <br /> Windows.Services.Store.StoreSku.Images <br /> Windows.Services.Store.StoreSku.IsInUserCollection <br /> Windows.Services.Store.StoreSku.IsSubscription <br /> Windows.Services.Store.StoreSku.IsTrial <br /> Windows.Services.Store.StoreSku.Language <br /> Windows.Services.Store.StoreSku.Price <br /> Windows.Services.Store.StoreSku.StoreId <br /> Windows.Services.Store.StoreSku.SubscriptionInfo <br /> Windows.Services.Store.StoreSku.Title <br /> Windows.Services.Store.StoreSku.Videos <br /> Windows.Services.Store.StoreSku.GetIsInstalledAsync <br /> Windows.Services.Store.StoreSku.RequestPurchaseAsync <br /> Windows.Services.Store.StoreSku.RequestPurchaseAsync(Windows.Services.Store.StorePurchaseProperties)
<hr>

**項目**

[Windows.Services.Store.StoreSubscriptionInfo](/uwp/api/windows.services.store.storesubscriptioninfo)

**[プロパティ]**


Windows.Services.Store.StoreSubscriptionInfo <br /> Windows.Services.Store.StoreSubscriptionInfo.BillingPeriod <br /> Windows.Services.Store.StoreSubscriptionInfo.BillingPeriodUnit <br /> Windows.Services.Store.StoreSubscriptionInfo.HasTrialPeriod <br /> Windows.Services.Store.StoreSubscriptionInfo.TrialPeriod <br /> Windows.Services.Store.StoreSubscriptionInfo.TrialPeriodUnit
<hr>

**項目**

[Windows.Services.Store.StoreVideo](/uwp/api/windows.services.store.storevideo)

**[プロパティ]**


Windows.Services.Store.StoreVideo <br /> Windows.Services.Store.StoreVideo.Caption <br /> Windows.Services.Store.StoreVideo.Height <br /> Windows.Services.Store.StoreVideo.PreviewImage <br /> Windows.Services.Store.StoreVideo.Uri <br /> Windows.Services.Store.StoreVideo.VideoPurposeTag <br /> Windows.Services.Store.StoreVideo.Width
<hr>