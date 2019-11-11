---
ms.openlocfilehash: a56c5fc32b5fd274d5da0d9b295918f5ea3b345e
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394466"
---
### <a name="signalr-hubconnection-resetsendping-and-resettimeout-methods-removed"></a>SignalR：已删除 HubConnection ResetSendPing 和 ResetTimeout 方法

已从 SignalR `HubConnection` API 中删除了 `ResetSendPing` 和 `ResetTimeout` 方法。 这些方法最初仅供内部使用，但已在 ASP.NET Core 2.2 中公开。 从 ASP.NET Core 3.0 预览版 4 开始，这些方法将不可用。 有关讨论，请参阅 [aspnet/AspNetCore#8543](https://github.com/aspnet/AspNetCore/issues/8543)。

#### <a name="version-introduced"></a>引入的版本

3.0

#### <a name="old-behavior"></a>旧行为

API 可用。

#### <a name="new-behavior"></a>新行为

API 已删除。

#### <a name="reason-for-change"></a>更改原因

这些方法最初仅供内部使用，但已在 ASP.NET Core 2.2 中公开。

#### <a name="recommended-action"></a>建议的操作

不要使用这些方法。

#### <a name="category"></a>类别

ASP.NET Core

#### <a name="affected-apis"></a>受影响的 API

- <xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.ResetSendPing?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.ResetTimeout?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:Microsoft.AspNetCore.SignalR.Client.HubConnection.ResetSendPing`
- `M:Microsoft.AspNetCore.SignalR.Client.HubConnection.ResetTimeout`

-->