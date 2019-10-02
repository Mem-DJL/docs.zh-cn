---
title: 程序集版本控制
ms.date: 08/20/2019
helpviewer_keywords:
- informational versions
- version numbers, assemblies
- assemblies [.NET Framework], versioning
- resolving assembly binding requests
- versioning, assemblies
ms.assetid: 775ad4fb-914f-453c-98ef-ce1089b6f903
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1363ce758929414f054e3d28dc6cd02bd618a8ac
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053962"
---
# <a name="assembly-versioning"></a><span data-ttu-id="69349-102">程序集版本控制</span><span class="sxs-lookup"><span data-stu-id="69349-102">Assembly versioning</span></span>

<span data-ttu-id="69349-103">使用公共语言运行时的程序集的所有版本控制都在程序集级别上进行。</span><span class="sxs-lookup"><span data-stu-id="69349-103">All versioning of assemblies that use the common language runtime is done at the assembly level.</span></span> <span data-ttu-id="69349-104">一个程序集的特定版本和依赖程序集的版本在该程序集的清单中记录下来。</span><span class="sxs-lookup"><span data-stu-id="69349-104">The specific version of an assembly and the versions of dependent assemblies are recorded in the assembly's manifest.</span></span> <span data-ttu-id="69349-105">除非被配置文件（应用程序配置文件、发行者策略文件和计算机的管理员配置文件）中的显式版本策略重写，否则运行时的默认版本策略是，应用程序只与它们生成和测试时所用的程序集版本一起运行。</span><span class="sxs-lookup"><span data-stu-id="69349-105">The default version policy for the runtime is that applications run only with the versions they were built and tested with, unless overridden by explicit version policy in configuration files (the application configuration file, the publisher policy file, and the computer's administrator configuration file).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="69349-106">仅对具有强名称的程序集进行版本控制。</span><span class="sxs-lookup"><span data-stu-id="69349-106">Versioning is done only on assemblies with strong names.</span></span>  
  
<span data-ttu-id="69349-107">运行时执行以下几步来解析程序集绑定请求：</span><span class="sxs-lookup"><span data-stu-id="69349-107">The runtime performs several steps to resolve an assembly binding request:</span></span>  
  
1. <span data-ttu-id="69349-108">检查原程序集引用，以确定该程序集的版本是否被绑定。</span><span class="sxs-lookup"><span data-stu-id="69349-108">Checks the original assembly reference to determine the version of the assembly to be bound.</span></span>  
  
2. <span data-ttu-id="69349-109">检查所有适用的配置文件以应用版本策略。</span><span class="sxs-lookup"><span data-stu-id="69349-109">Checks for all applicable configuration files to apply version policy.</span></span>  
  
3. <span data-ttu-id="69349-110">通过原程序集引用和配置文件中指定的任何重定向来确定正确的程序集，并且确定应绑定到调用程序集的版本。</span><span class="sxs-lookup"><span data-stu-id="69349-110">Determines the correct assembly from the original assembly reference and any redirection specified in the configuration files, and determines the version that should be bound to the calling assembly.</span></span>  
  
4. <span data-ttu-id="69349-111">检查全局程序集缓存和在配置文件中指定的基本代码，然后使用在[运行时如何定位程序集](../../framework/deployment/how-the-runtime-locates-assemblies.md)中解释的探测规则检查该应用程序的目录和子目录。</span><span class="sxs-lookup"><span data-stu-id="69349-111">Checks the global assembly cache, codebases specified in configuration files, and then checks the application's directory and subdirectories using the probing rules explained in [How the runtime locates assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).</span></span>  
  
<span data-ttu-id="69349-112">下图说明了这些步骤：</span><span class="sxs-lookup"><span data-stu-id="69349-112">The following illustration shows these steps:</span></span>  
  
![显示程序集绑定请求解析中的步骤的图表。](./media/versioning/resolve-assembly-binding-request.gif)
  
<span data-ttu-id="69349-114">有关配置应用程序的更多信息，请参阅[配置应用](../../framework/configure-apps/index.md)。</span><span class="sxs-lookup"><span data-stu-id="69349-114">For more information about configuring applications, see [Configure apps](../../framework/configure-apps/index.md).</span></span> <span data-ttu-id="69349-115">有关绑定策略的更多信息，请参阅[运行时如何定位程序集](../../framework/deployment/how-the-runtime-locates-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="69349-115">For more information about binding policy, see [How the runtime locates assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).</span></span>  
  
## <a name="version-information"></a><span data-ttu-id="69349-116">版本信息</span><span class="sxs-lookup"><span data-stu-id="69349-116">Version information</span></span>  

<span data-ttu-id="69349-117">每一程序集都用两种截然不同的方法来表示版本信息：</span><span class="sxs-lookup"><span data-stu-id="69349-117">Each assembly has two distinct ways of expressing version information:</span></span>  
  
- <span data-ttu-id="69349-118">程序集的版本号，该版本号与程序集名称及区域性信息都是程序集标识的组成部分。</span><span class="sxs-lookup"><span data-stu-id="69349-118">The assembly's version number, which, together with the assembly name and culture information, is part of the assembly's identity.</span></span> <span data-ttu-id="69349-119">该号码将由运行时用来强制实施版本策略，它在运行时的类型解析进程中起着重要的作用。</span><span class="sxs-lookup"><span data-stu-id="69349-119">This number is used by the runtime to enforce version policy and plays a key part in the type resolution process at run time.</span></span>  
  
- <span data-ttu-id="69349-120">信息性版本，这是一个字符串，表示仅为提醒的目的而包括的附加版本信息。</span><span class="sxs-lookup"><span data-stu-id="69349-120">An informational version, which is a string that represents additional version information included for informational purposes only.</span></span>  
  
### <a name="assembly-version-number"></a><span data-ttu-id="69349-121">程序集版本号</span><span class="sxs-lookup"><span data-stu-id="69349-121">Assembly version number</span></span>  

<span data-ttu-id="69349-122">每一程序集都有一个版本号作为其标识的一部分。</span><span class="sxs-lookup"><span data-stu-id="69349-122">Each assembly has a version number as part of its identity.</span></span> <span data-ttu-id="69349-123">因此，如果两个程序集具有不同的版本号，运行时就会将它们视作完全不同的程序集。</span><span class="sxs-lookup"><span data-stu-id="69349-123">As such, two assemblies that differ by version number are considered by the runtime to be completely different assemblies.</span></span> <span data-ttu-id="69349-124">此版本号实际表示为具有以下格式的四部分号码：</span><span class="sxs-lookup"><span data-stu-id="69349-124">This version number is physically represented as a four-part string with the following format:</span></span>  
  
<span data-ttu-id="69349-125">\<*主版本*>.\<*次版本*>.\<*生成号*>.\<*修订版本*></span><span class="sxs-lookup"><span data-stu-id="69349-125">\<*major version*>.\<*minor version*>.\<*build number*>.\<*revision*></span></span>  
  
<span data-ttu-id="69349-126">例如，版本 1.5.1254.0 中的 1 表示主版本，5 表示次版本，1254 表示生成号，而 0 则表示修订号。</span><span class="sxs-lookup"><span data-stu-id="69349-126">For example, version 1.5.1254.0 indicates 1 as the major version, 5 as the minor version, 1254 as the build number, and 0 as the revision number.</span></span>  
  
<span data-ttu-id="69349-127">版本号与其他标识信息（包括程序集名称和公钥，以及与该应用程序所连接的其他程序集的关系和标识有关的信息）一起存储在程序集清单中。</span><span class="sxs-lookup"><span data-stu-id="69349-127">The version number is stored in the assembly manifest along with other identity information, including the assembly name and public key, as well as information on relationships and identities of other assemblies connected with the application.</span></span>  
  
<span data-ttu-id="69349-128">在生成程序集时，开发工具将把每一个被引用程序集的依赖项信息记录在程序集清单中。</span><span class="sxs-lookup"><span data-stu-id="69349-128">When an assembly is built, the development tool records dependency information for each assembly that is referenced in the assembly manifest.</span></span> <span data-ttu-id="69349-129">运行时将这些版本号与管理员、应用程序或发行者设置的配置信息结合使用，以加载被引用程序集的正确版本。</span><span class="sxs-lookup"><span data-stu-id="69349-129">The runtime uses these version numbers, in conjunction with configuration information set by an administrator, an application, or a publisher, to load the proper version of a referenced assembly.</span></span>  
  
<span data-ttu-id="69349-130">为进行版本控制，运行时会区分常规程序集和具有强名称的程序集。</span><span class="sxs-lookup"><span data-stu-id="69349-130">The runtime distinguishes between regular and strong-named assemblies for the purposes of versioning.</span></span> <span data-ttu-id="69349-131">只对具有强名称的程序集执行版本检查。</span><span class="sxs-lookup"><span data-stu-id="69349-131">Version checking only occurs with strong-named assemblies.</span></span>  
  
<span data-ttu-id="69349-132">有关指定版本绑定策略的信息，请参阅[配置应用](../../framework/configure-apps/index.md)。</span><span class="sxs-lookup"><span data-stu-id="69349-132">For information about specifying version binding policies, see [Configure apps](../../framework/configure-apps/index.md).</span></span> <span data-ttu-id="69349-133">有关运行时如何使用版本信息查找特定程序集的信息，请参阅[运行时如何定位程序集](../../framework/deployment/how-the-runtime-locates-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="69349-133">For information about how the runtime uses version information to find a particular assembly, see [How the runtime locates assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).</span></span>  
  
### <a name="assembly-informational-version"></a><span data-ttu-id="69349-134">程序集信息性版本</span><span class="sxs-lookup"><span data-stu-id="69349-134">Assembly informational version</span></span>  

<span data-ttu-id="69349-135">信息性版本是一个字符串，它仅出于提醒的目的将附加的版本信息附加到一个程序集；此信息不在运行时使用。</span><span class="sxs-lookup"><span data-stu-id="69349-135">The informational version is a string that attaches additional version information to an assembly for informational purposes only; this information is not used at run time.</span></span> <span data-ttu-id="69349-136">基于文本的信息性版本相当于产品的营销广告、包装或产品名称，不被运行时使用。</span><span class="sxs-lookup"><span data-stu-id="69349-136">The text-based informational version corresponds to the product's marketing literature, packaging, or product name and is not used by the runtime.</span></span> <span data-ttu-id="69349-137">例如，信息性版本可以是“公共语言运行时 1.0 版”或“NET Control SP 2”。</span><span class="sxs-lookup"><span data-stu-id="69349-137">For example, an informational version could be "Common Language Runtime version 1.0" or "NET Control SP 2".</span></span> <span data-ttu-id="69349-138">在 Microsoft Windows 中的文件属性对话框的“版本”选项卡上，此信息显示在“产品版本”项中。</span><span class="sxs-lookup"><span data-stu-id="69349-138">On the Version tab of the file properties dialog in Microsoft Windows, this information appears in the item "Product Version".</span></span>  
  
> [!NOTE]
> <span data-ttu-id="69349-139">虽然可以指定任意文本，但是如果字符串的格式不是程序集版本号使用的格式，或者虽然是这种格式但包含通配符，则在编译时会显示一条警告消息。</span><span class="sxs-lookup"><span data-stu-id="69349-139">Although you can specify any text, a warning message appears on compilation if the string is not in the format used by the assembly version number, or if it is in that format but contains wildcards.</span></span> <span data-ttu-id="69349-140">此警告无碍。</span><span class="sxs-lookup"><span data-stu-id="69349-140">This warning is harmless.</span></span>  
  
<span data-ttu-id="69349-141">信息性版本用自定义特性 <xref:System.Reflection.AssemblyInformationalVersionAttribute?displayProperty=nameWithType> 表示。</span><span class="sxs-lookup"><span data-stu-id="69349-141">The informational version is represented using the custom attribute <xref:System.Reflection.AssemblyInformationalVersionAttribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="69349-142">有关信息性版本属性的更多信息，请参阅[设置程序集属性](set-attributes.md)。</span><span class="sxs-lookup"><span data-stu-id="69349-142">For more information about the informational version attribute, see [Set assembly attributes](set-attributes.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="69349-143">请参阅</span><span class="sxs-lookup"><span data-stu-id="69349-143">See also</span></span>

- [<span data-ttu-id="69349-144">运行时如何定位程序集</span><span class="sxs-lookup"><span data-stu-id="69349-144">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="69349-145">配置应用</span><span class="sxs-lookup"><span data-stu-id="69349-145">Configure apps</span></span>](../../framework/configure-apps/index.md)
- [<span data-ttu-id="69349-146">设置程序集特性</span><span class="sxs-lookup"><span data-stu-id="69349-146">Set assembly attributes</span></span>](set-attributes.md)
- [<span data-ttu-id="69349-147">.NET 中的程序集</span><span class="sxs-lookup"><span data-stu-id="69349-147">Assemblies in .NET</span></span>](index.md)