---
title: Nouveautés de .NET Core 2.1
description: Découvrez les nouvelles fonctionnalités de .NET Core 2.1.
author: rpetrusha
ms.author: ronpet
ms.date: 06/06/2018
ms.openlocfilehash: 52fe2d47dbca9bc43c2f1274b0d9e535ba9f9abc
ms.sourcegitcommit: 59b51cd7c95c75be85bd6ef715e9ef8c85720bac
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37874570"
---
# <a name="whats-new-in-net-core-21"></a><span data-ttu-id="46ab5-103">Nouveautés de .NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="46ab5-103">What's new in .NET Core 2.1</span></span>

<span data-ttu-id="46ab5-104">.NET Core 2.1 inclut les nouvelles fonctionnalités et améliorations dans les domaines suivants :</span><span class="sxs-lookup"><span data-stu-id="46ab5-104">.NET Core 2.1 includes enhancements and new features in the following areas:</span></span>

- [<span data-ttu-id="46ab5-105">Outillage</span><span class="sxs-lookup"><span data-stu-id="46ab5-105">Tooling</span></span>](#tooling)
- [<span data-ttu-id="46ab5-106">Restauration par progression</span><span class="sxs-lookup"><span data-stu-id="46ab5-106">Roll forward</span></span>](#roll-forward)
- [<span data-ttu-id="46ab5-107">Déploiement</span><span class="sxs-lookup"><span data-stu-id="46ab5-107">Deployment</span></span>](#deployment)
- [<span data-ttu-id="46ab5-108">Pack de compatibilité Windows</span><span class="sxs-lookup"><span data-stu-id="46ab5-108">Windows Compatibility Pack</span></span>](#windows-compatibility-pack)
- [<span data-ttu-id="46ab5-109">Améliorations de la compilation JIT</span><span class="sxs-lookup"><span data-stu-id="46ab5-109">JIT compilation improvements</span></span>](#jit-compiler-improvements)
- [<span data-ttu-id="46ab5-110">Modifications d'API</span><span class="sxs-lookup"><span data-stu-id="46ab5-110">API changes</span></span>](#api-changes)

## <a name="tooling"></a><span data-ttu-id="46ab5-111">Outillage</span><span class="sxs-lookup"><span data-stu-id="46ab5-111">Tooling</span></span>

<span data-ttu-id="46ab5-112">Le Kit SDK.NET Core 2.1 (2.1.300), les outils inclus avec .NET Core 2.1, intègrent les modifications et améliorations suivantes :</span><span class="sxs-lookup"><span data-stu-id="46ab5-112">The .NET Core 2.1 SDK (v 2.1.300), the tooling included with .NET Core 2.1, includes the following changes and enhancements:</span></span>

### <a name="build-performance-improvements"></a><span data-ttu-id="46ab5-113">Amélioration des performances des builds</span><span class="sxs-lookup"><span data-stu-id="46ab5-113">Build performance improvements</span></span>

<span data-ttu-id="46ab5-114">Un objectif majeur de .NET Core 2.1 est l’amélioration des performances des builds, en particulier pour les builds incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="46ab5-114">A major focus of .NET Core 2.1 is improving build-time performance, particularly for incremental builds.</span></span> <span data-ttu-id="46ab5-115">Ces améliorations des performances s’appliquent aux builds en ligne de commande à l’aide de `dotnet build` et aux builds dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46ab5-115">These performance improvements apply to both command-line builds using `dotnet build` and to builds in Visual Studio.</span></span> <span data-ttu-id="46ab5-116">Certaines zones individuelles d’amélioration incluent :</span><span class="sxs-lookup"><span data-stu-id="46ab5-116">Some individual areas of improvement include:</span></span>

- <span data-ttu-id="46ab5-117">Pour la résolution de ressources de package, résolution uniquement des ressources utilisées par une build plutôt que de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="46ab5-117">For package asset resolution, resolving only assets used by a build rather than all assets.</span></span>

- <span data-ttu-id="46ab5-118">Mise en cache des références d’assembly.</span><span class="sxs-lookup"><span data-stu-id="46ab5-118">Caching of assembly references.</span></span>

- <span data-ttu-id="46ab5-119">Utilisation de serveurs de build SDK de longue durée, représentant des processus qui couvrent des appels `dotnet build` individuels.</span><span class="sxs-lookup"><span data-stu-id="46ab5-119">Use of long-running SDK build servers, which are processes that span across individual `dotnet build` invocations.</span></span> <span data-ttu-id="46ab5-120">Ils suppriment la nécessité de la compilation JIT de grands blocs de code à chaque exécution de `dotnet build`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-120">They eliminate the need to JIT-compile large blocks of code every time `dotnet build` is run.</span></span> <span data-ttu-id="46ab5-121">Les processus d’un serveur de build peuvent être automatiquement terminés avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="46ab5-121">Build server processes can be automatically terminated with the following command:</span></span>

   ```console
   dotnet buildserver shutdown
   ```

### <a name="new-cli-commands"></a><span data-ttu-id="46ab5-122">Nouvelles commandes CLI</span><span class="sxs-lookup"><span data-stu-id="46ab5-122">New CLI commands</span></span>

<span data-ttu-id="46ab5-123">Un certain nombre d’outils qui étaient disponibles uniquement par projet à l’aide de [`DotnetCliToolReference`](../tools/extensibility.md) sont désormais disponibles dans le cadre du Kit de développement .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-123">A number of tools that were available only on a per project basis using [`DotnetCliToolReference`](../tools/extensibility.md) are now available as part of the .NET Core SDK.</span></span> <span data-ttu-id="46ab5-124">Ces outils incluent :</span><span class="sxs-lookup"><span data-stu-id="46ab5-124">These tools include:</span></span>

- <span data-ttu-id="46ab5-125">`dotnet watch` fournit un observateur de système de fichiers qui attend la modification d’un fichier avant d’exécuter un ensemble désigné de commandes.</span><span class="sxs-lookup"><span data-stu-id="46ab5-125">`dotnet watch` provides a file system watcher that waits for a file to change before executing a designated set of commands.</span></span> <span data-ttu-id="46ab5-126">Par exemple, la commande suivante reconstruit automatiquement le projet actuel et génère une sortie détaillée à chaque modification d’un fichier :</span><span class="sxs-lookup"><span data-stu-id="46ab5-126">For example, the following command automatically rebuilds the current project and generates verbose output whenever a file in it changes:</span></span>

   ```console
   dotnet watch -- --verbose build
   ```
  
   <span data-ttu-id="46ab5-127">Remarquez l’option `--` qui précède l’option `--verbose`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-127">Note the `--` option that precedes the `--verbose` option.</span></span> <span data-ttu-id="46ab5-128">Elle délimite les options passées directement à la commande `dotnet watch` à partir des arguments passés au processus enfant `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-128">It delimits the options passed directly to the `dotnet watch` command from the arguments that are passed to the child `dotnet` process.</span></span> <span data-ttu-id="46ab5-129">Sans elle, l’option `--verbose` s’applique à la commande `dotnet watch`, et non à la commande `dotnet build`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-129">Without it, the `--verbose` option applies to the `dotnet watch` command, not the `dotnet build` command.</span></span>
  
   <span data-ttu-id="46ab5-130">Pour plus d’informations, consultez [Développer des applications ASP.NET Core à l’aide de dotnet watch](/aspnet/core/tutorials/dotnet-watch)</span><span class="sxs-lookup"><span data-stu-id="46ab5-130">For more information, see [Develop ASP.NET Core apps using dotnet watch](/aspnet/core/tutorials/dotnet-watch)</span></span>

- <span data-ttu-id="46ab5-131">`dotnet dev-certs` génère et gère les certificats utilisés pendant le développement dans les applications ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-131">`dotnet dev-certs` generates and manages certificates used during development in ASP.NET Core applications.</span></span>

- <span data-ttu-id="46ab5-132">`dotnet user-secrets` gère les secrets d’un magasin de secrets d’un utilisateur dans les applications ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-132">`dotnet user-secrets` manages the secrets in a user secret store in ASP.NET Core applications.</span></span>

- <span data-ttu-id="46ab5-133">`dotnet sql-cache` crée un tableau et des index dans une base de données Microsoft SQL Server à utiliser pour la mise en cache distribuée.</span><span class="sxs-lookup"><span data-stu-id="46ab5-133">`dotnet sql-cache` creates a table and indexes in a Microsoft SQL Server database to be used for distributed caching.</span></span>

- <span data-ttu-id="46ab5-134">`dotnet ef` est un outil de gestion des bases de données, des objets <xref:Microsoft.EntityFrameworkCore.DbContext> et des migrations dans les applications Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-134">`dotnet ef` is a tool for managing databases, <xref:Microsoft.EntityFrameworkCore.DbContext> objects, and migrations in Entity Framework Core applications.</span></span> <span data-ttu-id="46ab5-135">Pour plus d’informations, consultez [Outils en ligne de commande EF Core .NET](/ef/core/miscellaneous/cli/dotnet).</span><span class="sxs-lookup"><span data-stu-id="46ab5-135">For more information, see [EF Core .NET Command-line Tools](/ef/core/miscellaneous/cli/dotnet).</span></span>

### <a name="global-tools"></a><span data-ttu-id="46ab5-136">Outils globaux</span><span class="sxs-lookup"><span data-stu-id="46ab5-136">Global Tools</span></span>

<span data-ttu-id="46ab5-137">.NET Core 2.1 prend en charge les *outils globaux*, autrement dit des outils personnalisés disponibles globalement à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="46ab5-137">.NET Core 2.1 supports *Global Tools* -- that is, custom tools that are available globally from the command line.</span></span> <span data-ttu-id="46ab5-138">Le modèle d’extensibilité des versions précédentes de .NET Core proposant des outils personnalisés par projet uniquement à l’aide de [`DotnetCliToolReference`](../tools/extensibility.md#consuming-per-project-tools).</span><span class="sxs-lookup"><span data-stu-id="46ab5-138">The extensibility model in previous versions of .NET Core made custom tools available on a per project basis only by using [`DotnetCliToolReference`](../tools/extensibility.md#consuming-per-project-tools).</span></span>

<span data-ttu-id="46ab5-139">Pour installer un outil global, vous utilisez la commande [dotnet tool install](..\tools\dotnet-tool-install.md).</span><span class="sxs-lookup"><span data-stu-id="46ab5-139">To install a Global Tool, you use the [dotnet tool install](..\tools\dotnet-tool-install.md) command.</span></span> <span data-ttu-id="46ab5-140">Exemple :</span><span class="sxs-lookup"><span data-stu-id="46ab5-140">For example:</span></span>

```console
dotnet tool install -g dotnetsay
```

<span data-ttu-id="46ab5-141">Une fois installé, l’outil peut être exécuté à partir de la ligne de commande en spécifiant le nom de l’outil.</span><span class="sxs-lookup"><span data-stu-id="46ab5-141">Once installed, the tool can be run from the command line by specifying the tool name.</span></span> <span data-ttu-id="46ab5-142">Pour plus d’informations, consultez [Vue d’ensemble des outils globaux .NET Core](../tools/global-tools.md).</span><span class="sxs-lookup"><span data-stu-id="46ab5-142">For more information, see [.NET Core Global Tools overview](../tools/global-tools.md).</span></span>

### <a name="tool-management-with-the-dotnet-tool-command"></a><span data-ttu-id="46ab5-143">Gestion des outils avec la commande `dotnet tool`</span><span class="sxs-lookup"><span data-stu-id="46ab5-143">Tool management with the `dotnet tool` command</span></span>

<span data-ttu-id="46ab5-144">Dans .NET Core SDK 2.1 (2.1.300), toutes les opérations avec les outils utilisent la commande `dotnet tool`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-144">In .NET Core SDK 2.1 (v 2.1.300), all tools operations use the `dotnet tool` command.</span></span> <span data-ttu-id="46ab5-145">Les options ci-dessous sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="46ab5-145">The following options are available:</span></span>

- <span data-ttu-id="46ab5-146">[`dotnet tool install`](../tools/dotnet-tool-install.md) pour installer un outil.</span><span class="sxs-lookup"><span data-stu-id="46ab5-146">[`dotnet tool install`](../tools/dotnet-tool-install.md) to install a tool.</span></span>

- <span data-ttu-id="46ab5-147">[`dotnet tool update`](../tools/dotnet-tool-update.md) pour désinstaller et réinstaller un outil (et donc le mettre à jour).</span><span class="sxs-lookup"><span data-stu-id="46ab5-147">[`dotnet tool update`](../tools/dotnet-tool-update.md) to uninstall and reinstall a tool, which effectively updates it.</span></span>

- <span data-ttu-id="46ab5-148">[`dotnet tool list`](../tools/dotnet-tool-list.md) pour répertorier les outils actuellement installés.</span><span class="sxs-lookup"><span data-stu-id="46ab5-148">[`dotnet tool list`](../tools/dotnet-tool-list.md) to list currently installed tools.</span></span>

- <span data-ttu-id="46ab5-149">[`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) pour désinstaller des outils actuellement installés.</span><span class="sxs-lookup"><span data-stu-id="46ab5-149">[`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) to uninstall currently installed tools.</span></span>

## <a name="roll-forward"></a><span data-ttu-id="46ab5-150">Restauration par progression</span><span class="sxs-lookup"><span data-stu-id="46ab5-150">Roll forward</span></span>

<span data-ttu-id="46ab5-151">Toutes les applications .NET Core depuis .NET Core 2.0 peuvent être restaurées par progression vers la dernière *version mineure* installée sur un système.</span><span class="sxs-lookup"><span data-stu-id="46ab5-151">All .NET Core applications starting with the .NET Core 2.0 automatically roll forward to the latest *minor version* installed on a system.</span></span> 

<span data-ttu-id="46ab5-152">À compter de .NET Core 2.0, si la version de .NET Core avec laquelle une application a été créée n’est pas présente lors de l’exécution, l’application s’exécute automatiquement avec la dernière *version mineure* installée de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-152">Starting with .NET Core 2.0, if the version of .NET Core that an application was built with is not present at runtime, the application automatically runs against the latest installed *minor version* of .NET Core.</span></span> <span data-ttu-id="46ab5-153">En d’autres termes, si une application est générée avec .NET Core 2.0 et que .NET Core 2.0 n’est pas présent sur le système hôte, mais que .NET Core 2.1 l’est, l’application s’exécute avec .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="46ab5-153">In other words, if an application is built with .NET Core 2.0, and .NET Core 2.0 is not present on the host system but .NET Core 2.1 is, the application runs with .NET Core 2.1.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46ab5-154">Ce comportement de restauration par progression ne s’applique pas aux préversions,</span><span class="sxs-lookup"><span data-stu-id="46ab5-154">This roll-forward behavior doesn't apply to preview releases.</span></span> <span data-ttu-id="46ab5-155">ni aux versions majeures.</span><span class="sxs-lookup"><span data-stu-id="46ab5-155">Nor does it apply to major releases.</span></span> <span data-ttu-id="46ab5-156">Par exemple, une application .NET Core 1.0 ne peut pas être restaurée par progression vers .NET Core 2.0 ou .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="46ab5-156">For example, a .NET Core 1.0 application wouldn't roll forward to .NET Core 2.0 or .NET Core 2.1.</span></span>

<span data-ttu-id="46ab5-157">Vous pouvez également désactiver la restauration par progression d’une version mineure de trois manières :</span><span class="sxs-lookup"><span data-stu-id="46ab5-157">You can also disable minor version roll forward in any of three ways:</span></span>

- <span data-ttu-id="46ab5-158">Définissez la variable d’environnement `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX` sur 0.</span><span class="sxs-lookup"><span data-stu-id="46ab5-158">Set the `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX` environment variable to 0.</span></span>

- <span data-ttu-id="46ab5-159">Ajoutez la ligne suivante au fichier runtimeconfig.json :</span><span class="sxs-lookup"><span data-stu-id="46ab5-159">Add the following line to the runtimeconfig.json file:</span></span>

   ```json
   "rollForwardOnNoCandidateFx" : 0
   ```

- <span data-ttu-id="46ab5-160">Lorsque vous utilisez les [outils CLI .NET Core](../tools/index.md), incluez l’option suivante dans une commande .NET Core telle que `run` :</span><span class="sxs-lookup"><span data-stu-id="46ab5-160">When using [.NET Core CLI tools](../tools/index.md), include the following option with a .NET Core command such as `run`:</span></span>

   ```console
   dotnet run --rollForwardOnNoCandidateFx=0
   ```

## <a name="deployment"></a><span data-ttu-id="46ab5-161">Déploiement</span><span class="sxs-lookup"><span data-stu-id="46ab5-161">Deployment</span></span>

### <a name="self-contained-application-servicing"></a><span data-ttu-id="46ab5-162">Maintenance d’une application autonome</span><span class="sxs-lookup"><span data-stu-id="46ab5-162">Self-contained application servicing</span></span>

<span data-ttu-id="46ab5-163">`dotnet publish` publie désormais des applications autonomes avec une version de runtime révisée.</span><span class="sxs-lookup"><span data-stu-id="46ab5-163">`dotnet publish` now publishes self-contained applications with a serviced runtime version.</span></span> <span data-ttu-id="46ab5-164">Lorsque vous publiez une application autonome avec le Kit de développement .NET Core 2.1 (2.1.300), votre application inclut la dernière version du runtime révisée et identifiée par ce SDK.</span><span class="sxs-lookup"><span data-stu-id="46ab5-164">When you publish a self-contained application with the .NET Core 2.1 SDK (v 2.1.300), your application includes the latest serviced runtime version known by that SDK.</span></span> <span data-ttu-id="46ab5-165">Lorsque vous effectuez une mise à niveau avec la dernière version du SDK, vous publiez la dernière version du runtime .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-165">When you upgrade to the latest SDK, you’ll publish with the latest .NET Core runtime version.</span></span> <span data-ttu-id="46ab5-166">Cela s’applique aux runtimes .NET Core 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="46ab5-166">This applies for .NET Core 1.0 runtimes and later.</span></span>

<span data-ttu-id="46ab5-167">La publication autonome s’appuie sur les versions de runtime de NuGet.org. Vous n’avez pas besoin du runtime révisé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="46ab5-167">Self-contained publishing relies on runtime versions on NuGet.org. You do not need to have the serviced runtime on your machine.</span></span>

<span data-ttu-id="46ab5-168">À l’aide du Kit de développement logiciel .NET Core 2.0, les applications autonomes sont publiées avec le runtime .NET Core 2.0.0, sauf si une version différente est spécifiée via la propriété `RuntimeFrameworkVersion`.</span><span class="sxs-lookup"><span data-stu-id="46ab5-168">Using the .NET Core 2.0 SDK, self-contained applications are published with the .NET Core 2.0.0 runtime unless a different version is specified via the `RuntimeFrameworkVersion` property.</span></span> <span data-ttu-id="46ab5-169">Avec ce nouveau comportement, vous n’aurez plus besoin de définir cette propriété afin de sélectionner une version de runtime ultérieure pour une application autonome.</span><span class="sxs-lookup"><span data-stu-id="46ab5-169">With this new behavior, you’ll no longer need to set this property to select a higher runtime version for a self-contained application.</span></span> <span data-ttu-id="46ab5-170">Dorénavant, l’approche la plus simple consiste à toujours publier avec le Kit de développement .NET Core 2.1 (2.1.300).</span><span class="sxs-lookup"><span data-stu-id="46ab5-170">The easiest approach going forward is to always publish with .NET Core 2.1 SDK (v 2.1.300).</span></span>

## <a name="windows-compatibility-pack"></a><span data-ttu-id="46ab5-171">Pack de compatibilité Windows</span><span class="sxs-lookup"><span data-stu-id="46ab5-171">Windows Compatibility Pack</span></span>

<span data-ttu-id="46ab5-172">Lorsque vous portez du code existant de .NET Framework vers .NET Core, vous pouvez utiliser le [pack de compatibilité Windows](https://www.nuget.org/packages/Microsoft.Windows.Compatibility).</span><span class="sxs-lookup"><span data-stu-id="46ab5-172">When you port existing code from the .NET Framework to .NET Core, you can use the [Windows Compatibility Pack](https://www.nuget.org/packages/Microsoft.Windows.Compatibility).</span></span> <span data-ttu-id="46ab5-173">Il permet d’accéder aux plus de 20 000 API disponibles dans .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-173">It provides access to 20,000 more APIs than are available in .NET Core.</span></span> <span data-ttu-id="46ab5-174">Ces API incluent les types dans l’espace de noms <xref:System.Drawing?displayProperty="nameWithType">, la classe <xref:System.Diagnostics.EventLog>, WMI, les compteurs de performances, les services Windows, ainsi que les types et membres de registre Windows.</span><span class="sxs-lookup"><span data-stu-id="46ab5-174">These APIs include types in the <xref:System.Drawing?displayProperty="nameWithType"> namespace, the <xref:System.Diagnostics.EventLog> class, WMI, Performance Counters, Windows Services, and the Windows registry types and members.</span></span>

## <a name="jit-compiler-improvements"></a><span data-ttu-id="46ab5-175">Améliorations du compilateur JIT</span><span class="sxs-lookup"><span data-stu-id="46ab5-175">JIT compiler improvements</span></span>

<span data-ttu-id="46ab5-176">.NET Core intègre une nouvelle technologie de compilateur JIT appelée *compilation à plusieurs niveaux* (ou également *optimisation adaptative*), qui peut améliorer considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="46ab5-176">.NET Core incorporates a new JIT compiler technology called *tiered compilation* (also known as *adaptive optimization*) that can significantly improve performance.</span></span> <span data-ttu-id="46ab5-177">La compilation à plusieurs niveaux n’est pas activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="46ab5-177">Tiered compilation is an opt-in setting.</span></span>

<span data-ttu-id="46ab5-178">Une des tâches importantes effectuées par le compilateur JIT est l’optimisation de l’exécution du code.</span><span class="sxs-lookup"><span data-stu-id="46ab5-178">One of the important tasks performed by the JIT compiler is optimizing code execution.</span></span> <span data-ttu-id="46ab5-179">Toutefois, pour les chemins de code peu utilisés, le compilateur peut passer plus de temps à optimiser le code que le runtime passe à exécuter du code non optimisé.</span><span class="sxs-lookup"><span data-stu-id="46ab5-179">For little-used code paths, however, the compiler may spend more time optimizing code than the runtime spends running unoptimized code.</span></span> <span data-ttu-id="46ab5-180">La compilation à plusieurs niveaux ajoute deux étapes à la compilation JIT :</span><span class="sxs-lookup"><span data-stu-id="46ab5-180">Tiered compilation introduces two stages in JIT compilation:</span></span>

- <span data-ttu-id="46ab5-181">Un **premier niveau**, qui génère du code aussi rapidement que possible.</span><span class="sxs-lookup"><span data-stu-id="46ab5-181">A **first tier**, which generates code as quickly as possible.</span></span>

- <span data-ttu-id="46ab5-182">Un **second niveau**, qui génère un code optimisé pour les méthodes fréquemment exécutées.</span><span class="sxs-lookup"><span data-stu-id="46ab5-182">A **second tier**, which generates optimized code for those methods that are executed frequently.</span></span> <span data-ttu-id="46ab5-183">Le second niveau de compilation est effectué en parallèle pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="46ab5-183">The second tier of compilation is performed in parallel for enhanced performance.</span></span>

<span data-ttu-id="46ab5-184">Vous pouvez activer la compilation à plusieurs niveaux de deux manières.</span><span class="sxs-lookup"><span data-stu-id="46ab5-184">You can opt into tiered compilation in either of two ways.</span></span>

- <span data-ttu-id="46ab5-185">Pour utiliser la compilation à plusieurs niveaux dans tous les projets qui utilisent le Kit de développement .NET Core 2.1, définissez la variable d’environnement suivante :</span><span class="sxs-lookup"><span data-stu-id="46ab5-185">To use tiered compilation in all projects that use the .NET Core 2.1 SDK, set the following environment variable:</span></span>

  ```console
  COMPlus_TieredCompilation="1"
  ```

- <span data-ttu-id="46ab5-186">Pour utiliser la compilation à plusieurs niveaux par projet, ajoutez la propriété `<TieredCompilation>` à la section `<PropertyGroup>` du fichier projet MSBuild, comme le montre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="46ab5-186">To use tiered compilation on a per-project basis, add the `<TieredCompilation>` property to the `<PropertyGroup>` section of the MSBuild project file, as the following example shows:</span></span>

   ```xml
   <PropertyGroup>
      <!-- other property definitions -->

      <TieredCompilation>true</TieredCompilation>
   </PropertyGroup>
   ```

## <a name="api-changes"></a><span data-ttu-id="46ab5-187">Modifications d'API</span><span class="sxs-lookup"><span data-stu-id="46ab5-187">API changes</span></span>

### <a name="spant-and-memoryt"></a><span data-ttu-id="46ab5-188">`Span<T>` et `Memory<T>`</span><span class="sxs-lookup"><span data-stu-id="46ab5-188">`Span<T>` and `Memory<T>`</span></span>

<span data-ttu-id="46ab5-189">.NET Core 2.1 inclut certains nouveaux types qui facilitent l’utilisation de tableaux et d’autres types de mémoire beaucoup plus efficaces.</span><span class="sxs-lookup"><span data-stu-id="46ab5-189">.NET Core 2.1 includes some new types that make working with arrays and other types of memory much more efficient.</span></span> <span data-ttu-id="46ab5-190">Ces nouveaux types incluent :</span><span class="sxs-lookup"><span data-stu-id="46ab5-190">The new types include:</span></span>

- <span data-ttu-id="46ab5-191">Voir <xref:System.Span%601?displayProperty=nameWithType> et <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-191"><xref:System.Span%601?displayProperty=nameWithType> and <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="46ab5-192">Voir <xref:System.Memory%601?displayProperty=nameWithType> et <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-192"><xref:System.Memory%601?displayProperty=nameWithType> and <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="46ab5-193">Sans ces types, lorsque vous passez des éléments de ce type comme une partie d’un tableau ou d’une section d’une mémoire tampon, vous devez créer une copie d’une partie des données avant de les passer à une méthode.</span><span class="sxs-lookup"><span data-stu-id="46ab5-193">Without these types, when passing such items as a portion of an array or a section of a memory buffer, you have to make a copy of some portion of the data before passing it to a method.</span></span> <span data-ttu-id="46ab5-194">Ces types fournissent une représentation virtuelle des données, qui supprime les opérations supplémentaires d’allocation de mémoire et de copie.</span><span class="sxs-lookup"><span data-stu-id="46ab5-194">These types provide a virtual view of that data that eliminates the need for the additional memory allocation and copy operations.</span></span>

<span data-ttu-id="46ab5-195">L’exemple suivant utilise une instance <xref:System.Span%601> pour fournir une représentation virtuelle de 10 éléments d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="46ab5-195">The following example uses a <xref:System.Span%601> instance to provide a virtual view of 10 elements of an array.</span></span>

[!CODE-csharp[Span\<T>](~/samples/core/whats-new/whats-new-in-21/cs/program.cs)]

### <a name="brotli-compression"></a><span data-ttu-id="46ab5-196">Compression de Brotli</span><span class="sxs-lookup"><span data-stu-id="46ab5-196">Brotli compression</span></span>

<span data-ttu-id="46ab5-197">.NET Core 2.1 prend en charge la compression et la décompression de Brotli.</span><span class="sxs-lookup"><span data-stu-id="46ab5-197">.NET Core 2.1 adds support for Brotli compression and decompression.</span></span> <span data-ttu-id="46ab5-198">Brotli est un algorithme de compression sans perte à usage général, défini dans [RFC 7932](https://www.ietf.org/rfc/rfc7932.txt), et pris en charge par la plupart des navigateurs web et les principaux serveurs web.</span><span class="sxs-lookup"><span data-stu-id="46ab5-198">Brotli is a general-purpose lossless compression algorithm that is defined in [RFC 7932](https://www.ietf.org/rfc/rfc7932.txt) and is supported by most web browsers and major web servers.</span></span> <span data-ttu-id="46ab5-199">Vous pouvez utiliser une classe <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> basée sur les flux ou des classes hautes performances <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> et <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> basées sur la portée.</span><span class="sxs-lookup"><span data-stu-id="46ab5-199">You can use the stream-based <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> class or the high-performance span-based <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> and <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> classes.</span></span> <span data-ttu-id="46ab5-200">L'exemple suivant montre une compression avec la classe <xref:System.IO.Compression.BrotliStream> :</span><span class="sxs-lookup"><span data-stu-id="46ab5-200">The following example illustrates compression with the <xref:System.IO.Compression.BrotliStream> class:</span></span>

[!CODE-csharp[Brotli compression](~/samples/core/whats-new/whats-new-in-21/cs/brotli.cs#1)]

<span data-ttu-id="46ab5-201">Le comportement de <xref:System.IO.Compression.BrotliStream> est identique à <xref:System.IO.Compression.DeflateStream> et <xref:System.IO.Compression.GZipStream>, ce qui facilite la convertir du code qui appelle ces API pour <xref:System.IO.Compression.BrotliStream>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-201">The <xref:System.IO.Compression.BrotliStream> behavior is the same as <xref:System.IO.Compression.DeflateStream> and <xref:System.IO.Compression.GZipStream>, which makes it easy to convert code that calls these APIs to <xref:System.IO.Compression.BrotliStream>.</span></span>

### <a name="new-cryptography-apis-and-cryptography-improvements"></a><span data-ttu-id="46ab5-202">Nouvelles API de chiffrement et améliorations du chiffrement</span><span class="sxs-lookup"><span data-stu-id="46ab5-202">New cryptography APIs and cryptography improvements</span></span>

<span data-ttu-id="46ab5-203">.NET Core 2.1 inclut de nombreuses améliorations des API de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="46ab5-203">.NET Core 2.1 includes numerous enhancements to the cryptography APIs:</span></span>

- <span data-ttu-id="46ab5-204"><xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType> est disponible dans le package System.Security.Cryptography.Pkcs.</span><span class="sxs-lookup"><span data-stu-id="46ab5-204"><xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType> is available in the System.Security.Cryptography.Pkcs package.</span></span> <span data-ttu-id="46ab5-205">L’implémentation est identique à la classe <xref:System.Security.Cryptography.Pkcs.SignedCms> du .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="46ab5-205">The implementation is the same as the <xref:System.Security.Cryptography.Pkcs.SignedCms> class in the .NET Framework.</span></span>

- <span data-ttu-id="46ab5-206">De nouvelles surcharges des méthodes <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> et <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> acceptent un identificateur d’algorithme de hachage permettant aux appelants d’obtenir les valeurs d’empreinte numérique de certificat à l’aide d’algorithmes autres que SHA-1.</span><span class="sxs-lookup"><span data-stu-id="46ab5-206">New overloads of the <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> and <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> methods accept a hash algorithm identifier to enable callers to get certificate thumbprint values using algorithms other than SHA-1.</span></span>

- <span data-ttu-id="46ab5-207">De nouvelles API de chiffrement basées sur <xref:System.Span%601> sont disponibles pour le hachage, HMAC, la génération de codes de chiffrement aléatoires, la génération de signatures asymétriques, le traitement de signatures asymétriques et le chiffrement RSA.</span><span class="sxs-lookup"><span data-stu-id="46ab5-207">New <xref:System.Span%601>-based cryptography APIs are available for hashing, HMAC, cryptographic random number generation, asymmetric signature generation, asymmetric signature processing, and RSA encryption.</span></span>

- <span data-ttu-id="46ab5-208">Les performances de <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType> ont été améliorées d’environ 15 % grâce à une implémentation <xref:System.Span%601>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-208">The performance of <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType> has improved by about 15% by using a <xref:System.Span%601>-based implementation.</span></span>

- <span data-ttu-id="46ab5-209">La nouvelle classe <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> inclut deux nouvelles méthodes :</span><span class="sxs-lookup"><span data-stu-id="46ab5-209">The new <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> class includes two new methods:</span></span>

  - <span data-ttu-id="46ab5-210"><xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A> prend une quantité fixe de temps pour renvoyer deux entrées de même longueur, ce qui permet de l’utiliser dans une vérification du chiffrement afin d’éviter la temporisation des informations sur le canal auxiliaire.</span><span class="sxs-lookup"><span data-stu-id="46ab5-210"><xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A> takes a fixed amount of time to return for any two inputs of the same length, which makes it suitable for use in cryptographic verification to avoid contributing to timing side-channel information.</span></span>

  - <span data-ttu-id="46ab5-211"><xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A> est une routine de nettoyage de la mémoire qui ne peut pas être optimisée.</span><span class="sxs-lookup"><span data-stu-id="46ab5-211"><xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A> is a memory-clearing routine that cannot be optimized.</span></span>

- <span data-ttu-id="46ab5-212">La méthode statique <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=fullName> remplit <xref:System.Span%601> de valeurs aléatoires.</span><span class="sxs-lookup"><span data-stu-id="46ab5-212">The static <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=fullName> method fills a <xref:System.Span%601> with random values.</span></span>

- <span data-ttu-id="46ab5-213"><xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType> est maintenant pris en charge sous Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="46ab5-213">The <xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType> is now supported on Linux and maxOS.</span></span>

- <span data-ttu-id="46ab5-214">Diffie-Hellman à courbe elliptique (ECDH) est désormais disponible dans la famille de classe <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-214">Elliptic-Curve Diffie-Hellman (ECDH) is now available in the <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType> class family.</span></span> <span data-ttu-id="46ab5-215">La surface d’exposition est la même que dans le .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="46ab5-215">The surface area is the same as in the .NET Framework.</span></span>

- <span data-ttu-id="46ab5-216">L’instance retournée par <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> peut chiffrer ou déchiffrer avec OAEP à l’aide d’un condensat SHA-2, et permet de générer ou de valider des signatures à l’aide de RSA-PSS.</span><span class="sxs-lookup"><span data-stu-id="46ab5-216">The instance returned by <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> can encrypt or decrypt with OAEP using a SHA-2 digest, as well as generate or validate signatures using RSA-PSS.</span></span>

### <a name="sockets-improvements"></a><span data-ttu-id="46ab5-217">Améliorations des sockets</span><span class="sxs-lookup"><span data-stu-id="46ab5-217">Sockets improvements</span></span>

<span data-ttu-id="46ab5-218">.NET Core inclut un nouveau type, <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>, et une <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType> réécrite, qui constituent la base des API de mise en réseau de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="46ab5-218">.NET Core includes a new type, <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>, and a rewritten <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType>, that form the basis of higher-level networking APIs.</span></span>  <span data-ttu-id="46ab5-219"><xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>, par exemple, est la base de l’implémentation <xref:System.Net.Http.HttpClient>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-219"><xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>, for example, is the basis of the <xref:System.Net.Http.HttpClient> implementation.</span></span> <span data-ttu-id="46ab5-220">Dans les versions précédentes de .NET Core, les API de niveau supérieur étaient basées sur des implémentations de mise en réseau natives.</span><span class="sxs-lookup"><span data-stu-id="46ab5-220">In previous versions of .NET Core, higher-level APIs were based on native networking implementations.</span></span>

<span data-ttu-id="46ab5-221">L’implémentation de sockets introduite dans .NET Core 2.1 présente plusieurs avantages :</span><span class="sxs-lookup"><span data-stu-id="46ab5-221">The sockets implementation introduced in .NET Core 2.1 has a number of advantages:</span></span>

- <span data-ttu-id="46ab5-222">Une amélioration significative des performances par rapport à l’implémentation précédente.</span><span class="sxs-lookup"><span data-stu-id="46ab5-222">A significant performance improvement when compared with the previous implementation.</span></span>

- <span data-ttu-id="46ab5-223">La suppression des dépendances de plateforme, qui simplifie le déploiement et la maintenance.</span><span class="sxs-lookup"><span data-stu-id="46ab5-223">Elimination of platform dependencies, which simplifies deployment and servicing.</span></span>

- <span data-ttu-id="46ab5-224">Comportement cohérent sur toutes les plates-formes .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46ab5-224">Consistent behavior across all .NET Core platforms.</span></span>

<span data-ttu-id="46ab5-225"><xref:System.Net.Http.SocketsHttpHandler> est l’implémentation par défaut dans .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="46ab5-225"><xref:System.Net.Http.SocketsHttpHandler> is the default implementation in .NET Core 2.1.</span></span> <span data-ttu-id="46ab5-226">Toutefois, vous pouvez configurer votre application pour utiliser l’ancienne classe <xref:System.Net.Http.HttpClientHandler> en appelant la méthode <xref:System.AppContext.SetSwitch%2A?displayProperty="nameWithType"> :</span><span class="sxs-lookup"><span data-stu-id="46ab5-226">However, you can configure your application to use the older <xref:System.Net.Http.HttpClientHandler> class by calling the <xref:System.AppContext.SetSwitch%2A?displayProperty="nameWithType"> method:</span></span>

```csharp
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", false);
```

```vb
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", False)
```

<span data-ttu-id="46ab5-227">Vous pouvez également utiliser une variable d’environnement pour désactiver l’utilisation des implémentations de sockets basées sur <xref:System.Net.Http.SocketsHttpHandler>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-227">You can also use an environment variable to opt out of using sockets implementations based on <xref:System.Net.Http.SocketsHttpHandler>.</span></span> <span data-ttu-id="46ab5-228">Pour cela, définissez `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` sur `false` ou 0.</span><span class="sxs-lookup"><span data-stu-id="46ab5-228">To do this, set the `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` to either `false` or 0.</span></span>

<span data-ttu-id="46ab5-229">Sous Windows, vous pouvez également choisir d’utiliser <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType>, repose sur une implémentation native, ou la classe <xref:System.Net.Http.SocketsHttpHandler> en passant une instance de la classe au constructeur <xref:System.Net.Http.HttpClient>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-229">On Windows, you can also choose to use <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType>, which relies on a native implementation, or the <xref:System.Net.Http.SocketsHttpHandler> class by passing an instance of the class to the <xref:System.Net.Http.HttpClient> constructor.</span></span>

<span data-ttu-id="46ab5-230">Sous Linux et macOS, vous pouvez uniquement configurer <xref:System.Net.Http.HttpClient> par processus.</span><span class="sxs-lookup"><span data-stu-id="46ab5-230">On Linux and macOS, you can only configure <xref:System.Net.Http.HttpClient> on a per-process basis.</span></span> <span data-ttu-id="46ab5-231">Sous Linux, vous devez déployer [libcurl](https://curl.haxx.se/libcurl/) si vous souhaitez utiliser l’ancienne implémentation <xref:System.Net.Http.HttpClient>.</span><span class="sxs-lookup"><span data-stu-id="46ab5-231">On Linux, you need to deploy [libcurl](https://curl.haxx.se/libcurl/) if you want to use the old <xref:System.Net.Http.HttpClient> implementation.</span></span> <span data-ttu-id="46ab5-232">(Il est installé avec .NET Core 2.0.)</span><span class="sxs-lookup"><span data-stu-id="46ab5-232">(It is installed with .NET Core 2.0.)</span></span>

## <a name="see-also"></a><span data-ttu-id="46ab5-233">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="46ab5-233">See also</span></span>

[<span data-ttu-id="46ab5-234">Nouveautés de .NET Core</span><span class="sxs-lookup"><span data-stu-id="46ab5-234">What's new in .NET Core</span></span>](index.md)  
[<span data-ttu-id="46ab5-235">Nouvelles fonctionnalités d’EF Core 2.1</span><span class="sxs-lookup"><span data-stu-id="46ab5-235">New features in EF Core 2.1</span></span>](/ef/core/what-is-new/ef-core-2.1)  
[<span data-ttu-id="46ab5-236">Nouveautés d’ASP.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="46ab5-236">What's new in ASP.NET Core 2.1</span></span>](/aspnet/core/aspnetcore-2.1)