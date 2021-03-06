---
Description: 役割またはユーザーのアカウントのカスタム アクセス許可を設定します。
title: アカウント ユーザーの役割またはカスタムのアクセス許可の設定
ms.assetid: 99f3aa18-98b4-4919-bd7b-d78356b0bf78
ms.date: 10/31/2018
ms.topic: article
keywords: Windows 10, uwp, ユーザー ロール, ユーザーのアクセス許可, カスタム ロール, ユーザー アクセス, アクセス許可のカスタマイズ, 標準ロール
ms.localizationpriority: medium
ms.openlocfilehash: dc2786df57ebe1364f045795c52b301ef5feed0f
ms.sourcegitcommit: 94316b8daf60a89a90a661ea17428c3d2734fee8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66814407"
---
# <a name="set-roles-or-custom-permissions-for-account-users"></a>アカウント ユーザーの役割またはカスタムのアクセス許可の設定

ときにする[、パートナー センター アカウントにユーザーを追加](add-users-groups-and-azure-ad-applications.md)アカウント内のどのようなアクセスを指定する必要があります。 それには、アカウント全体に適用される[標準ロール](#roles)を割り当てます。または、[ユーザーのアクセス許可をカスタマイズ](#custom)して、適切なレベルのアクセスを提供することもできます。 カスタムのアクセス許可はアカウント全体に適用されるものもあれば、特定の 1 つまたは複数の製品のみを対象にできるものもあります (必要に応じて全製品を対象にすることもできます)。

> [!NOTE] 
> ユーザー、グループ、Azure AD アプリケーションのどれを追加する場合でも、適用できるロールやアクセス許可は同じです。

適用するロールまたはアクセス許可を決めるときは、次のことに注意してください。 
-   ユーザー (グループと Azure AD アプリケーションを含む) がない限り、自分に割り当てられたロールに関連付けられているアクセス許可を持つパートナー センター アカウント全体にアクセスできなく[アクセス許可のカスタマイズ](#custom)割り当てる[製品レベルのアクセス許可](#product-level-permissions)と、特定のアプリやアドオンのみを操作できるようにします。
-   複数のロールを選択するか、カスタムのアクセス許可を使って必要なアクセス許可を付与することにより、ユーザー、グループ、または Azure AD アプリケーションが複数のロールの機能にアクセスできるようにすることができます。
-   特定の 1 つのロール (またはカスタムのアクセス許可のセット) を持つユーザーは、別のロール (またはアクセス許可のセット) を持つグループの一部となることも可能です。 その場合ユーザーは、グループと個人アカウントの両方に関連付けられた機能のすべてにアクセスできます。

> [!TIP]
> このトピックでは、Windows アプリ開発者プログラムに特定されて[パートナー センター](https://partner.microsoft.com/dashboard)します。 ハードウェア開発者プログラムでのユーザー ロールについて詳しくは、「[ユーザー ロールの管理](https://docs.microsoft.com/windows-hardware/drivers/dashboard/managing-user-roles)」をご覧ください。 Windows デスクトップ アプリケーション プログラムでのユーザー ロールについて詳しくは、「[Windows デスクトップ アプリケーション プログラム](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#add-and-manage-account-users)」をご覧ください。


<span id="roles" />

## <a name="assign-roles-to-account-users"></a>アカウント ユーザーへの役割の割り当て

既定では、ユーザー、グループ、またはパートナー センター アカウントに Azure AD アプリケーションを追加するときに選択するための一連の標準的な役割が表示されます。 各ロールには、アカウント内で特定の機能を実行するための特定のアクセス許可セットが付与されています。 

**[アクセス許可のカスタマイズ]** を選び、[カスタムのアクセス許可](#custom)を定義していない場合は、アカウントに追加するユーザー、グループ、または Azure AD アプリケーションそれぞれに、少なくとも次の標準ロールのいずれかを割り当てる必要があります。 

> [!NOTE]
> アカウントの**オーナー**は、最初に Microsoft アカウントでそのアカウントを作成したユーザーです (Azure AD によって追加されたユーザーではありません)。 このアカウント所有者のみが、アカウントに完全にアクセスして、アプリを削除したり、すべてのアカウント ユーザーを作成および編集したり、すべての財務およびアカウント設定を変更したりできます。 


| ロール                 | 説明              |
|----------------------|--------------------------|
| マネージャー              | アカウントに完全にアクセスできます (税金と支払いの設定の変更を除く)。 これは、パートナー センターのユーザーの管理が含まれていますが、作成し、Azure AD テナント内のユーザーを削除する機能が Azure ad アカウントのアクセス許可に依存することに注意してください。 つまり、ユーザーがマネージャーの役割が割り当てられている組織のグローバル管理者のアクセス許可がない場合、Azure AD がないできる新しいユーザーを作成したり、ディレクトリからユーザーを削除する (ただし、ユーザのパートナー センターの役割を変更することができます)。 <p> パートナー センター アカウントが 1 つ以上の Azure AD テナントと関連付けられている場合は、マネージャーは、ユーザーの完全な詳細を表示することはできないことに注意してください (名、姓、名、パスワード回復の電子メールを含む、Azure AD グローバル管理者であるか、) ある場合を除いてそのテナントのグローバル管理者のアクセス許可を持つアカウントを使用して、そのユーザーとして同じテナントにサインインします。 ただし、追加したりをパートナー センター アカウントに関連付けられている任意のテナントにユーザーを削除します。 |
| Developer            | パッケージをアップロードし、アプリおよびアドオンを申請できます。また、[使用状況レポート](usage-report.md)で統計情報の詳細を確認できます。 アクセスできる[クロス デバイス エクスペリエンス](https://go.microsoft.com/fwlink/?linkid=874042)機能します。 財務情報やアカウントの設定を表示することはできません。   |
| 経営担当者 | [[正常性]](health-report.md) レポートと [[使用状況]](usage-report.md) レポートを表示できます。 製品の作成や申請、アカウント設定の変更、財務情報の表示はできません。   |
| 財務担当者  | [支払いレポート](payout-summary.md)、財務情報、取得レポートを表示できます。 アプリ、アドオン、またはアカウント設定を変更することはできません。    |
| マーケター             | [顧客のレビューに返信](respond-to-customer-reviews.md)したり、非財務[分析レポート](analytics.md)を表示したりできます。 アプリ、アドオン、またはアカウント設定を変更することはできません。      |

以下の表は、これらの各ロール (およびアカウント所有者) が使用できる特定の機能の一部を示しています。

|                                                       |    アカウント所有者                 |    マネージャー                       |    Developer                     |    経営担当者    |    財務担当者    |    マーケター                      |
|-------------------------------------------------------|----------------------------------|----------------------------------|----------------------------------|----------------------------|---------------------------|----------------------------------|
|    (ほぼリアルタイムのデータを含む) の購入レポート |    表示可能                      |    表示可能                      |    アクセスなし                     |    アクセスなし               |    表示可能               |    アクセスなし                     |
|    フィードバック レポート/応答                          |    表示とフィードバックの送信が可能    |    表示とフィードバックの送信が可能    |    表示とフィードバックの送信が可能    |    アクセスなし               |    アクセスなし              |    表示とフィードバックの送信が可能    |
|    (ほぼリアルタイムのデータを含む) の正常性レポート      |    表示可能                      |    表示可能                      |    表示可能                      |    表示可能                |    アクセスなし              |    アクセスなし                     |
|    利用状況レポート                                       |    表示可能                      |    表示可能                      |    表示可能                      |    表示可能                |    アクセスなし              |    アクセスなし                     |
|    受取りアカウント                                     |    更新可能                    |    アクセスなし                     |    アクセスなし                     |    アクセスなし               |    表示可能               |    アクセスなし                     |
|    税務プロファイル                                        |    更新可能                    |    アクセスなし                     |    アクセスなし                     |    アクセスなし               |    表示可能               |    アクセスなし                     |
|    支払いの概要                                     |    表示可能                      |    アクセスなし                     |    アクセスなし                     |    アクセスなし               |    表示可能               |    アクセスなし                     |

適切な標準ロールがない場合や、特定のアプリやアドオンへのアクセスを制限する場合は、以下の説明に従って **[アクセス許可のカスタマイズ]** を選んでユーザーにカスタムのアクセス許可を付与できます。


<span id="custom" />

## <a name="assign-custom-permissions-to-account-users"></a>アカウント ユーザーへのカスタムのアクセス許可の割り当て

標準ロールではなく、カスタムのアクセス許可を割り当てるには、ユーザー アカウントを追加または編集するときに、 **[ロール]** セクションの **[アクセス許可のカスタマイズ]** をクリックします。 

ユーザーのアクセス許可を有効にするには、ボックスを適切な設定に切り替えます。 

![アクセス設定のガイド](images/permission_key.png)

- **アクセスなし**:ユーザーには、指定されたアクセス許可がありません。
- **読み取り専用**:ユーザーは、表示対象の領域に関連する機能にアクセスできますが、変更を加えることはできません。 
- **読み取り/書き込み**:ユーザーは、表示するほか、領域に関連付けられた変更を加えるへのアクセスがあります。
- **混合**:直接、このオプションを選択することはできませんが、 **Mixed**を組み合わせたそのアクセス許可のアクセスが許可されているかどうかのインジケーターが表示されます。 たとえば、 **[すべての製品]** に対して **[価格と使用可能状況]** への**読み取り専用**アクセスを付与しているときに、ある特定の製品に対して **[価格と使用可能状況]** への**読み取り/書き込み**アクセスを付与する場合は、 **[すべての製品]** の **[価格と使用可能状況]** インジケーターが [混合] として表示されます。 これは、一部の製品にアクセス許可の**アクセス権なし**が設定されているときに、他の製品に**読み取り/書き込み**と**読み取り専用**の両方またはそのいずれかのアクセスが設定されている場合も、同様に適用されます。

分析データの表示に関連するものなど、一部のアクセス許可で付与できるのは、**読み取り専用**アクセスのみです。 現在の実装では、**読み取り専用**と**読み取り/書き込み**のアクセスが区別されないアクセス許可もありますので注意してください。 **読み取り専用**アクセスまたは**読み取り/書き込み**アクセス、あるいはその両方によって付与される特定の機能を理解するには、各アクセス許可の詳細を確認してください。

それぞれのアクセス許可に関する特定の詳細については、下記の表で説明します。

## <a name="account-level-permissions"></a>アカウント レベルのアクセス許可

このセクションのアクセス許可を特定の製品に対して制限することはできません。 これらのアクセス許可のいずれかにアクセス権を付与すると、ユーザーは該当するアクセス許可をアカウント全体に対して獲得します。

<table>
    <colgroup>
    <col width="20%" />
    <col width="40%" />
    <col width="40%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">アクセス許可名</th>
    <th align="left">読み取り専用かどうか</th>
    <th align="left">読み取り/書き込み</th>
    </tr>
    </thead>
    <tbody>
<tr><td align="left">    <b>アカウントの設定</b>                    </td><td align="left">  <a href="managing-your-profile.md">連絡先情報</a>など、<b>[アカウント設定]</b> セクションのすべてのページを表示できます。       </td><td align="left">  <b>アカウント設定</b>セクションのすべてのページを表示できます。 <a href="managing-your-profile.md">連絡先情報</a>と他のページを変更できますが、支払いアカウントや税プロファイルは変更できません (アクセス許可が個別に付与されている場合を除く)。            </td></tr>
<tr><td align="left">    <b>アカウントのユーザー</b>                       </td><td align="left">  <b>[ユーザー]</b> セクションでアカウントに追加されているユーザーを表示できます。          </td><td align="left">  <b>[ユーザー]</b> セクションで、ユーザーのアカウントへの追加と既存のユーザーの変更ができます。             </td></tr>
<tr><td align="left">    <b>Ad のアカウント レベルのパフォーマンス レポート</b> </td><td align="left">  アカウント レベルの <a href="advertising-performance-report.md">[広告パフォーマンス] レポート</a>を表示できます。      </td><td align="left">  なし   </td></tr>
<tr><td align="left">    <b>広告キャンペーン</b>                        </td><td align="left">  アカウントで作成した<a href="create-an-ad-campaign-for-your-app.md">広告キャンペーン</a>を表示できます。      </td><td align="left">  アカウントで作成した<a href="create-an-ad-campaign-for-your-app.md">広告キャンペーン</a>を作成、管理、および表示できます。          </td></tr>
<tr><td align="left">    <b>Ad 仲介</b>                        </td><td align="left">  アカウントには、すべての製品 ad 仲介の構成を確認できます。    </td><td align="left">  表示、およびアカウントのすべての製品の ad 仲介の構成を変更できます。        </td></tr>
<tr><td align="left">    <b>Ad 仲介レポート</b>                </td><td align="left">  アカウント内のすべての製品の<a href="ad-mediation-report.md">広告仲介レポート</a>を表示できます。    </td><td align="left">  なし    </td></tr>
<tr><td align="left">    <b>Ad パフォーマンス レポート</b>              </td><td align="left">  アカウント内のすべての製品の <a href="advertising-performance-report.md">[広告パフォーマンス] レポート</a>を表示できます。       </td><td align="left">  なし         </td></tr>
<tr><td align="left">    <b>Ad ユニット</b>                            </td><td align="left">  アカウント用に作成された<a href="in-app-ads.md">広告ユニット</a>を表示できます。    </td><td align="left">  アカウントの<a href="in-app-ads.md">広告ユニット</a>を作成、管理、および表示できます。             </td></tr>
<tr><td align="left">    <b>広告を関連します。</b>                       </td><td align="left">  アカウント内のすべての製品で<a href="about-affiliate-ads.md">アフィリエイト広告</a>の利用状況を表示できます。    </td><td align="left">  アカウント内のすべての製品に対して<a href="about-affiliate-ads.md">アフィリエイト広告</a>の利用状況の管理と表示ができます。                </td></tr>
<tr><td align="left">    <b>関連会社のパフォーマンス レポート</b>      </td><td align="left">  アカウント内のすべての製品の<a href="affiliates-performance-report.md">アフィリエイト パフォーマンス レポート</a>を表示できます。   </td><td align="left">  なし   </td></tr>
<tr><td align="left">    <b>アプリ インストールの広告レポート</b>             </td><td align="left">  <a href="promote-your-app-report.md">[広告キャンペーン] レポート</a>を表示できます。           </td><td align="left">  なし   </td></tr>
<tr><td align="left">    <b>コミュニティの広告</b>                       </td><td align="left">  アカウント内のすべての製品の無料<a href="about-community-ads.md">コミュニティ広告</a>の利用状況を表示できます。          </td><td align="left">  アカウント内のすべての製品の無料<a href="about-community-ads.md">コミュニティ広告</a>の利用状況を作成、管理、および表示できます。               </td></tr>
<tr><td align="left">    <b>連絡先情報</b>                        </td><td align="left">  [アカウント設定] セクションで<a href="managing-your-profile.md">連絡先情報</a>を表示できます。        </td><td align="left">  [アカウント設定] セクションで<a href="managing-your-profile.md">連絡先情報</a>の編集と表示ができます。            </td></tr>
<tr><td align="left">    <b>COPPA コンプライアンス</b>                    </td><td align="left">  アカウント内のすべての製品の <a href="in-app-ads.md#coppa-compliance">COPPA 準拠</a>の選択 (製品が13歳未満の子供を対象とするかどうかを示す) を表示できます。                                            </td><td align="left">  アカウント内のすべての製品の <a href="in-app-ads.md#coppa-compliance">COPPA 準拠</a>の選択 (製品が13歳未満の子供を対象とするかどうかを示す) の編集と表示ができます。         </td></tr>
<tr><td align="left">    <b>顧客グループ</b>                     </td><td align="left">  表示できる<a href="create-customer-groups.md">顧客グループ</a>(セグメントと既知のユーザー グループ)。      </td><td align="left">  作成、編集、および表示<a href="create-customer-groups.md">顧客グループ</a>(セグメントと既知のユーザー グループ)。       </td></tr>
<tr><td align="left">    <b>製品グループの管理</b>&nbsp;*                            </td><td align="left">  新しい製品グループの作成ページを表示できますが、実際に新しい製品グループを作成することはできません。    </td><td align="left">  製品グループを作成して編集できます。     </td></tr>
<tr><td align="left">    <b>新しいアプリ</b>                            </td><td align="left">  新しいアプリの作成ページを表示できますが、実際にはアカウントに新しいアプリを作成することはできません。    </td><td align="left">  新しいアプリの名前を予約することで、アカウントで<a href="create-your-app-by-reserving-a-name.md">新しいアプリを作成</a>できます。また、申請を作成してアプリをストアに提出できます。     </td></tr>
<tr><td align="left">    <b>新しいバンドル</b>&nbsp;*                       </td><td align="left">  新しいバンドルの作成ページを表示できますが、実際にはアカウントに新しいバンドルを作成することはできません。     </td><td align="left">  製品の新しいバンドルを作成できます。          </td></tr>
<tr><td align="left">    <b>パートナー サービス</b>&nbsp;*                  </td><td align="left">  XToken を取得するサービスをインストールするための証明書を表示できます。     </td><td align="left">  XToken を取得するサービスをインストールするための証明書の管理と表示ができます。       </td></tr>
<tr><td align="left">    <b>支払いアカウント</b>                      </td><td align="left">  <b>[アカウント設定]</b> に<a href="setting-up-your-payout-account-and-tax-forms.md#payout-account">支払いアカウントの情報</a>を表示できます。     </td><td align="left">  <b>[アカウント設定]</b> で <a href="setting-up-your-payout-account-and-tax-forms.md#payout-account">支払いアカウントの情報</a> の編集と表示ができます。       </td></tr>
<tr><td align="left">    <b>支払いの概要</b>                      </td><td align="left">  <a href="payout-summary.md">支払いの概要</a>を表示して、支払いレポート情報にアクセスしてダウンロードできます。       </td><td align="left">  <a href="payout-summary.md">支払いの概要</a>を表示して、支払いレポート情報にアクセスしてダウンロードできます。   </td></tr>
<tr><td align="left">    <b>証明書利用者</b>&nbsp;*                   </td><td align="left">  XToken を取得する証明書利用者を表示できます。    </td><td align="left">  XToken を取得する証明書利用者の管理と表示ができます。     </td></tr>
<tr><td align="left">    <b>サンドボックス</b>&nbsp;*                         </td><td align="left">  <b>サンドボックス</b> ページにアクセスして、アカウント内のサンドボックスとそれらのサンドボックスに適用可能なすべての構成を表示できます。 適切な製品レベルのアクセス許可が付与されている場合を除き、サンドボックスごとに製品と申請を表示することはできません。 </td><td align="left">  <b>サンドボックス</b> ページにアクセスして、サンドボックスの作成と削除、およびサンドボックスの構成の管理など、アカウントでサンドボックスを表示して管理できます。 適切な製品レベルのアクセス許可が付与されている場合を除き、サンドボックスごとに製品と申請を表示することはできません。    </td></tr>
<tr><td align="left">    <b>Microsoft Store セール イベント</b>&nbsp;*                            </td><td align="left">  なし    </td><td align="left">  Microsoft Store セール イベントに製品を自動的に含めるオプションを構成できます。     </td></tr>
<tr><td align="left">    <b>税務プロファイル</b>                         </td><td align="left">  <b>[アカウント設定]</b> に<a href="setting-up-your-payout-account-and-tax-forms.md#tax-forms">税プロファイルの情報とフォーム</a>を表示できます。     </td><td align="left">  <b>[アカウント設定]</b> で税フォームに入力して、<a href="setting-up-your-payout-account-and-tax-forms.md#tax-forms">税プロファイル情報</a>を更新できます。     </td></tr>
<tr><td align="left">    <b>テスト アカウント</b>&nbsp;*                     </td><td align="left">  Xbox Live の構成をテストするためのアカウントを表示できます。      </td><td align="left">  Xbox Live の構成をテストするためのアカウントを作成、管理、および表示できます。      </td></tr>
<tr><td align="left">    <b>Xbox デバイス</b>                        </td><td align="left">  <b>[アカウント設定]</b> セクションでアカウントに対して有効にされている Xbox 開発コンソールを表示できます。       </td><td align="left">  <b>[アカウント設定]</b> セクションでアカウントに対して有効にされている Xbox 開発コンソールを追加、削除、および表示できます。     </td></tr>
    </tbody>
    </table>

\* アクセス許可はすべてのアカウントを使用できない機能に、アクセスをアスタリスク (*) 許可でマークされます。 これらの機能に対してアカウントが有効になっていない場合は、これらのアクセス許可の選択内容には一切影響はありません。   


## <a name="product-level-permissions"></a>製品レベルのアクセス許可

このセクションのアクセス許可は、アカウント内のすべての製品に付与するか、または 1 つ以上の特定の製品に対してのみアクセス許可を付与するようにカスタマイズできます。 

製品レベルのアクセス許可は、4 つのカテゴリに分類されます。**Analytics**、**収益**、**発行**、および**Xbox Live**します。 各カテゴリを展開して、カテゴリごとに個々のアクセス許可を表示できます。 また、1 つ以上の特定の製品に対して**すべてのアクセス許可**を有効にすることもできます。

アカウント内のすべての製品にアクセス許可を付与するには、 **[すべての製品]** とマークされている行でアクセス許可 を選択 (トグルして **[読み取り専用]** または **[読み取り/書き込み]** を指定) します。 
 
> [!TIP]
> **[すべての製品]** に対する選択内容は、現在アカウント内にあるすべての製品だけでなく、アカウント内で作成される将来の製品にも適用されます。 今後の製品にアクセス許可が適用されないようにするには、 **[すべての製品]** を選ぶのではなく、全製品を個別に選びます。

**[すべての製品]** 行の下に、別の行に記載されているアカウントに各製品が表示されます。 特定の製品にのみアクセス許可を付与するには、該当する製品の行でアクセス許可を選択します。

各アドオンは、親製品の下で個々の行と **[すべてのアドオン]** 行に一覧表示されます。 **[すべてのアドオン]** に対する選択内容は、その製品に対するすべての現在のアドオンだけでなく、その製品用に作成される将来のアドオンにも適用されます。

アドオンに対して設定できないアクセス許可もありますので注意してください。 これは、アクセス許可がアドオン (**カスタマー フィードバック** アクセス許可など) に適用されない、または親製品レベルで付与されたアクセス許可がその製品のすべてのアドオン (**プロモーション コード**など) に適用されるためです。 ただし、アドオンに対して適用可能なすべてのアクセス許可は個別に設定する必要があることに注意してください。アドオンは親製品に対する選択内容を継承しません。 たとえば、ユーザーがアドオンの価格と使用可能状況をを選択できるようにする場合、親製品に **[価格と使用可能状況]** アクセス許可を付与しているかどうかに関係なく、アドオン (または **[すべてのアドオン]** ) に対して **[価格と使用可能状況]** アクセス許可を有効にする必要があります。 


### <a name="analytics"></a>分析

<table>
    <thead>
    <tr class="header">
    <th align="left">アクセス許可名&nbsp;</th>
    <th align="left">読み取り専用&nbsp;</th>
    <th align="left">読み取り/書き込み</th>
    <th align="left">読み取り専用&nbsp;(アドオン)&nbsp; </th>
    <th align="left">読み取り/書き込み&nbsp;(アドオン)</th>
    </tr>
    </thead>
    <tbody>
    <tr><td align="left">    <b>買収</b>(ほぼリアルタイムのデータを含む) </td><td>    製品の <a href="acquisitions-report.md">[取得]</a> レポートと <a href="add-on-acquisitions-report.md">[アドオン取得]</a> レポートを表示できます。        </td><td>    なし    </td><td>    該当なし (親製品の設定が含まれて、**アドオン買収**レポート)        </td><td>    なし                         </td></tr>
    <tr><td align="left">    <b>使用状況</b> </td><td>    製品の <a href="usage-report.md">[使用状況] レポート</a>を表示できます。     </td><td>    なし       </td><td>    なし     </td><td>    なし         </td></tr>
    <tr><td align="left">    <b>正常性</b>(ほぼリアルタイムのデータを含む) </td><td>    製品の<a href="health-report.md">正常性レポート</a>を表示できます。    </td><td>    なし     </td><td>    なし     </td><td>    なし         </td></tr>
    <tr><td align="left">    <b>お客様からのフィードバック</b>    </td><td>    製品の <a href="reviews-report.md">[レビュー]</a> レポートと <a href="feedback-report.md">[フィードバック]</a> レポートを表示できます。       </td><td>    該当なし (フィードバックやレビューに返信するには、<b>[顧客への連絡]</b> アクセス許可を付与する必要があります)   </td><td>    なし     </td><td>    なし         </td></tr>
    <tr><td align="left">    <b>Xbox の分析</b> </td><td>    表示できます、 <a href="xbox-analytics-report.md">Xbox analytics レポート</a>製品です。    </td><td>    なし   </td><td>    なし       </td><td>    なし          </td></tr>
    </tbody>
    </table>

### <a name="monetization"></a>収益化

<table>
    <thead>
    <tr class="header">
    <th align="left">アクセス許可名&nbsp;</th>
    <th align="left">読み取り専用&nbsp;</th>
    <th align="left">読み取り/書き込み</th>
    <th align="left">読み取り専用&nbsp;(アドオン)&nbsp; </th>
    <th align="left">読み取り/書き込み&nbsp;(アドオン)</th>
    </tr>
    </thead>
    <tbody>
    <tr><td align="left">    <b>プロモーション コード</b>     </td><td>    製品とそのアドオンの<a href="generate-promotional-codes.md">プロモーション コード</a>の注文と利用状況の情報、また利用状況情報を表示できます。         </td><td>    製品とそのアドオンの<a href="generate-promotional-codes.md">プロモーション コード</a>の注文の表示、管理、および作成、また利用状況情報の表示ができます。          </td><td>    該当なし (すべてのアドオンに親製品の設定が適用されます)     </td><td>    該当なし (すべてのアドオンに親製品の設定が適用されます)     </td></tr>
    <tr><td align="left">    <b>対象となるプラン</b>     </td><td>    製品の<a href="use-targeted-offers-to-maximize-engagement-and-conversions.md">対象プラン</a>を表示できます。         </td><td>    製品の<a href="use-targeted-offers-to-maximize-engagement-and-conversions.md">対象プラン</a>を表示、管理、作成できます。          </td><td>    なし     </td><td>    なし      </td></tr>
    <tr><td align="left">    <b>お客様にお問い合わせください。</b>  </td><td>    <b>カスタマー フィードバック</b> アクセス許可も付与されている限り、<a href="respond-to-customer-feedback.md">カスタマー フィードバックへの返信</a>と<a href="respond-to-customer-reviews.md">カスタマー レビューへの返信</a>を表示できます。 製品に対して作成された<a href="send-push-notifications-to-your-apps-customers.md">ターゲット通知</a>も表示できます。    </td><td>    できます<a href="respond-to-customer-feedback.md">お客様からのフィードバックに応答</a>と<a href="respond-to-customer-reviews.md">顧客レビューに応答</a>だけであれば、<b>お客様からのフィードバック</b>アクセス許可が与えられても。 製品に対する<a href="send-push-notifications-to-your-apps-customers.md">ターゲット通知の作成と送信</a>もできます。                   </td><td>    なし         </td><td>    なし                          </td></tr>
    <tr><td align="left">    <b>実験</b></td><td>    製品の<a href="../monetize/run-app-experiments-with-a-b-testing.md">実験 (A/Bテスト)</a>と実験データを表示できます。   </td><td>    製品の<a href="../monetize/run-app-experiments-with-a-b-testing.md">実験 (A/B テスト)</a> の作成、管理、および表示と、実験データの表示ができます。     </td><td>    なし  </td><td>    なし                 </td></tr>
    <tr><td align="left">    <b>Microsoft Store セール イベント</b>&nbsp;*</td><td>    製品のセール イベントの状態を表示できます。   </td><td>    製品をセール イベントに追加して、割引を構成できます。      </td><td>    製品のセール イベントの状態を表示できます。   </td><td>    製品をセール イベントに追加して、割引を構成できます。      </td></tr>
    </tbody>
    </table>

### <a name="publishing"></a>公開 

<table>
    <thead>
    <tr class="header">
    <th align="left">アクセス許可名&nbsp;</th>
    <th align="left">読み取り専用&nbsp;</th>
    <th align="left">読み取り/書き込み</th>
    <th align="left">読み取り専用&nbsp;(アドオン)&nbsp; </th>
    <th align="left">読み取り/書き込み&nbsp;(アドオン)</th>
    </tr>
    </thead>
    <tbody>
    <tr><td align="left">    <b>製品のセットアップ</b>  </td><td>    製品の製品のセットアップ ページを表示できます。     </td><td>    表示、および製品の製品のセットアップ ページを編集できます。 </td><td>    アドオンの製品のセットアップ ページを表示できます。   </td><td>    表示、および製品のセットアップ ページのアドオンを編集できます。          </td></tr>
    <tr><td align="left">    <b>価格と可用性</b>  </td><td>    表示できます、<a href="set-app-pricing-and-availability.md">価格と可用性</a>製品のページ。     </td><td>    表示および編集できます、<a href="set-app-pricing-and-availability.md">価格と可用性</a>製品のページ。 </td><td>    表示できます、<a href="set-add-on-pricing-and-availability.md">価格と可用性</a>アドオンのページ。   </td><td>    表示および編集できます、<a href="set-add-on-pricing-and-availability.md">価格と可用性</a>アドオンのページ。          </td></tr>
    <tr><td align="left">    <b>プロパティ</b>   </td><td>    表示できます、<a href="enter-app-properties.md">プロパティ</a>製品のページ。      </td><td>    表示および編集できます、<a href="enter-app-properties.md">プロパティ</a>製品のページ。       </td><td>    表示できます、<a href="enter-add-on-properties.md">プロパティ</a>アドオンのページ。     </td><td>    表示および編集できます、<a href="enter-add-on-properties.md">プロパティ</a>アドオンのページ。               </td></tr>
    <tr><td align="left">    <b>年齢別規制</b>    </td><td>    表示できます、<a href="age-ratings.md">評価期間を表す</a>製品のページ。       </td><td>    表示および編集できます、<a href="age-ratings.md">評価期間を表す</a>製品のページ。    </td><td>    アドオンの経過時間の評価 ページを表示できます。          </td><td>     表示、およびアドオンの経過時間の評価 ページを編集できます。       </td></tr>
    <tr><td align="left">    <b>パッケージ</b>        </td><td>    表示できます、<a href="upload-app-packages.md">パッケージ</a>製品のページ。  </td><td>    表示および編集できます、<a href="upload-app-packages.md">パッケージ</a>パッケージのアップロードなど、製品のページ。     </td><td>   表示できます、<a href="upload-app-packages.md">パッケージ</a>アドオン (該当する) 場合のページ。   </td><td>     表示および編集できます<a href="upload-app-packages.md">パッケージ</a>アドオン (該当する) 場合のページ。             </td></tr>
    <tr><td align="left">    <b>ストアの一覧</b>  </td><td>    表示できます、<a href="create-app-store-listings.md">ページの一覧を格納</a>製品です。  </td><td>    表示および編集できます、<a href="create-app-store-listings.md">ページの一覧を格納</a>製品のさまざまな言語の新しいストアの一覧を追加することができます。     </td><td>    表示できます、<a href="create-add-on-store-listings.md">ページの一覧を格納</a>のアドオンです。            </td><td>    表示および編集できます、<a href="create-add-on-store-listings.md">ページの一覧を格納</a>アドオンのさまざまな言語のストアの一覧を追加することができます。                 </td></tr>
    <tr><td align="left">    <b>ストアに提出</b>     </td><td>    このアクセス許可が読み取り専用に設定されている場合は、アクセスは一切付与されません。           </td><td>    ストアに製品を提出して、証明レポートを表示できます。 新規および更新済みの両方の申請が含まれます。 </td><td>このアクセス許可が読み取り専用に設定されている場合は、アクセスは一切付与されません。     </td><td>    ストアにアドオンを提出して、証明レポートを表示できます。 新規および更新済みの両方の申請が含まれます。</td></tr>
    <tr><td align="left">    <b>新しい送信の作成</b>       </td><td>    このアクセス許可が読み取り専用に設定されている場合は、アクセスは一切付与されません。        </td><td>    製品の新しい<a href="app-submissions.md">申請</a>を作成できます。  </td><td>    このアクセス許可が読み取り専用に設定されている場合は、アクセスは一切付与されません。   </td><td>    アドオンの新しい<a href="add-on-submissions.md">申請</a>を作成できます。        </td></tr>
    <tr><td align="left">    <b>新しいアドオン</b>    </td><td>    このアクセス許可が読み取り専用に設定されている場合は、アクセスは一切付与されません。 </td><td>    製品の<a href="set-your-add-on-product-id.md">新しいアドオンを作成</a>できます。 </td><td>    なし    </td><td>    なし        </td></tr>
    <tr><td align="left">    <b>名前の予約</b>   </td><td>    製品の<a href="manage-app-names.md">アプリ名の管理</a>ページを表示できます。</td><td>    追加の名前の予約や予約済みの名前の削除など、製品の<a href="manage-app-names.md">アプリ名の管理</a>ページの表示と編集ができます。 </td><td>   アドオンの予約済みの名前を表示できます。    </td><td>   アドオンの予約済みの名前の表示と編集ができます。          </td></tr>
    <tr><td align="left">    <b>ディスクの要求</b>   </td><td>    ディスク要求ページを表示できます。 </td><td>    ディスクの要求を作成することができます。 </td><td>   なし    </td><td>   なし          </td></tr>
    <tr><td align="left">    <b>ディスクのロイヤリティ </b>   </td><td>    ディスク ロイヤリティ ページを表示できます。</td><td>    ディスクのロイヤリティを作成できます。 </td><td>   なし    </td><td>   なし          </td></tr>
    </tbody>
    </table>

### <a name="xbox-live-"></a>Xbox Live \*

<table>
    <thead>
    <tr class="header">
    <th align="left">アクセス許可名&nbsp;</th>
    <th align="left">読み取り専用&nbsp;</th>
    <th align="left">読み取り/書き込み</th>
    <th align="left">読み取り専用&nbsp;(アドオン)&nbsp; </th>
    <th align="left">読み取り/書き込み&nbsp;(アドオン)</th>
    </tr>
    </thead>
    <tbody>
    <tr><td align="left">    <b>証明書利用者</b>&nbsp;*</td><td>    アカウントの証明書利用者のパーティのページを表示できます。   </td><td>    表示、およびアカウントの証明書利用者のパーティのページを編集できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>パートナー サービス</b>&nbsp;*</td><td>    アカウントの Web サービスのページを表示できます。  </td><td>    表示、および Web サービスのアカウントのページを編集できます。      </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>Xbox テスト アカウント</b>&nbsp;*</td><td>    アカウントの Xbox テスト アカウントのページを表示できます。  </td><td>    表示、およびアカウントの Xbox テスト アカウントのページを編集できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>サンド ボックスごとの Xbox テスト アカウント</b>&nbsp;*</td><td>    アカウントの指定したサンド ボックスのみの Xbox テスト アカウントのページを表示できます。  </td><td>    表示、および Xbox テストを編集できます。   <tr><td align="left">    <b>アカウントの指定したサンド ボックスのみのアカウント ページ    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>Xbox デバイス</b>&nbsp;*</td><td>    アカウントの Xbox 1 開発コンソール ページを表示できます。  </td><td>    表示、およびアカウントの Xbox 1 開発コンソール ページを編集できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>サンド ボックスごとのデバイスの Xbox</b>&nbsp;*</td><td>    アカウントの指定したサンド ボックスのみの Xbox 1 開発コンソール ページを表示できます。  </td><td>    表示、およびアカウントの指定したサンド ボックスのみの Xbox 1 開発コンソール ページを編集できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>アプリのチャンネル</b>&nbsp;*</td><td>    なし  </td><td>    OneGuide を通じて表示するために、Xbox コンソールにプロモーション用のビデオ チャンネルを公開できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>サービスの構成</b>&nbsp;*</td><td>    製品の Xbox Live サービスの構成 ページを表示できます。  </td><td>    表示、および製品の Xbox Live サービスの構成 ページを編集できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
    <tr><td align="left">    <b>ツールへのアクセス</b>&nbsp;*</td><td>    ビューのデータのみの製品の Xbox Live のツールを実行できます。  </td><td>    データを表示および編集の製品では、Xbox Live のツールを実行できます。    </td><td>    なし    </td><td>    なし                      </td></tr>
</tbody>
</table>

\* アクセス許可はすべてのアカウントを使用できない機能に、アクセスをアスタリスク (*) 許可でマークされます。 これらの機能に対してアカウントが有効になっていない場合は、これらのアクセス許可の選択内容には一切影響はありません。  
