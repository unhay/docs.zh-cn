---
ms.openlocfilehash: 5b49dcae45e44bfd9ec3e150ad25c3f21d62c18e
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955327"
---
### <a name="jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null"></a>JsonSerializer.Serialize 在类型参数为 null 时引发 ArgumentNullException

现在，每当为 <xref:System.Type> 参数传递 `null` 时，具有 <xref:System.Type> 参数的 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>、<xref:System.Text.Json.JsonSerializer.SerializeAsync%2A?displayProperty=nameWithType> 和 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> 重载就会引发 <xref:System.ArgumentNullException>。

#### <a name="change-description"></a>更改描述

在 .NET Core 3.1 中，当为 `Type inputType` 参数传递 `null` 时，具有 <xref:System.Type> 参数的 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>、<xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=nameWithType> 和 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> 重载会引发 <xref:System.ArgumentNullException>，但如果 `Object value` 参数也为 `null`，则不会引发该异常。 从 .NET 5.0 开始，当为 <xref:System.Type> 参数传递 `null` 时，这些方法始终会引发 <xref:System.ArgumentNullException>。

在 .NET Core 3.1 中的行为：

```csharp
// Returns a string with value "null".
JsonSerializer.Serialize(null, null);

// Returns a byte array with value "null".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

在 .NET 5.0 和更高版本中的行为：

```csharp
// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.Serialize(null, null);

// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

#### <a name="version-introduced"></a>引入的版本

5.0

#### <a name="reason-for-change"></a>更改原因

为 `Type inputType` 参数传入 `null` 是不被接受的，应始终引发 <xref:System.ArgumentNullException>。

#### <a name="recommended-action"></a>建议的操作

请确保不会为这些方法的 `Type inputType` 参数传递 `null`。

#### <a name="category"></a>类别

序列化

#### <a name="affected-apis"></a>受影响的 API

- <xref:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)`
- `M:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`

-->
