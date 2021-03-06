---
title: Partial Tag Helper
author: scottaddie
description: Discover the ASP.NET Core Partial Tag Helper and the role each of its attributes play in rendering a partial view.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/23/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
---
# Partial Tag Helper

By [Scott Addie](https://github.com/scottaddie)

[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))

## Overview

The Partial Tag Helper is used for rendering a [partial view](xref:mvc/views/partial) in Razor Pages and MVC apps. Consider that it:

* Requires ASP.NET Core 2.1 or later.
* Is an alternative to [HTML Helper syntax](xref:mvc/views/partial#referencing-a-partial-view).

To recap, the HTML Helper options for rendering a partial view include:

* [@await Html.PartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [@await Html.RenderPartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

The *Product* model is used in samples throughout this document:

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

An inventory of the Partial Tag Helper attributes follows.

## name

The `name` attribute is required. It indicates the name or the path of the partial view to be rendered. When a partial view name is provided, the [view discovery](xref:mvc/views/overview#view-discovery) process is initiated. That process is bypassed when an explicit path is provided.

The following markup uses an explicit path, indicating that *_ProductPartial.cshtml* is to be loaded from the *Shared* folder. Using the [asp-for](#asp-for) attribute, a model is passed to the partial view for binding.

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## asp-for

The `asp-for` attribute assigns a [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression) to be evaluated against the current model. A `ModelExpression` infers the `@Model.` syntax. For example, `asp-for="Product"` can be used instead of `asp-for="@Model.Product"`. This default inference behavior is overridden by using the `@` symbol to define an inline expression.

The following markup loads *_ProductPartial.cshtml*:

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_AspFor)]

The partial view is bound to the associated page model's `Product` property:

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## view-data

The `view-data` attribute assigns a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to pass to the partial view. The following markup makes the entire ViewData collection accessible to the partial view:

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

In the preceding code, the `IsNumberReadOnly` key value is set to `true` and added to the ViewData collection. Consequently, `ViewData["IsNumberReadOnly"]` is made accessible within the following partial view:

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

In this example, the value of `ViewData["IsNumberReadOnly"]` determines whether the *Number* field is displayed as read only.

## Additional resources

* [Partial views](xref:mvc/views/partial)
* [Weakly typed data (ViewData and ViewBag)](xref:mvc/views/overview#weakly-typed-data-viewdata-and-viewbag)
