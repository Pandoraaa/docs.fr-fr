---
title: Bonnes pratiques pour l’écriture de tests unitaires
description: Découvrez les bonnes pratiques pour écrire des tests unitaires qui améliorent la qualité du code et la résilience
author: jpreese
ms.author: wiwagn
ms.date: 07/28/2018
ms.openlocfilehash: 69fe0cae141d1ed1e1281eecd78bf03e6e8be961
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43527733"
---
# <a name="unit-testing-best-practices"></a><span data-ttu-id="21a06-103">Bonnes pratiques relatives aux tests unitaires</span><span class="sxs-lookup"><span data-stu-id="21a06-103">Unit testing best practices</span></span>

<span data-ttu-id="21a06-104">Par [John Reese](http://reesespieces.io) avec des remerciements particuliers à [Roy Osherove](http://osherove.com/)</span><span class="sxs-lookup"><span data-stu-id="21a06-104">By [John Reese](http://reesespieces.io) with special thanks to [Roy Osherove](http://osherove.com/)</span></span>

<span data-ttu-id="21a06-105">Il existe de nombreux avantages à écrire des tests unitaires. Ils facilitent la régression, fournissent de la documentation et simplifient la conception.</span><span class="sxs-lookup"><span data-stu-id="21a06-105">There are numerous benefits to writing unit tests; they help with regression, provide documentation, and facilitate good design.</span></span> <span data-ttu-id="21a06-106">Toutefois, les tests unitaires difficiles à lire et fragiles peuvent faire des ravages dans votre code base.</span><span class="sxs-lookup"><span data-stu-id="21a06-106">However, hard to read and brittle unit tests can wreak havoc on your code base.</span></span>

<span data-ttu-id="21a06-107">Dans ce guide, vous allez découvrir certaines bonnes pratiques à suivre pour écrire des tests unitaires résilients et faciles à comprendre.</span><span class="sxs-lookup"><span data-stu-id="21a06-107">In this guide, you'll learn some best practices when writing unit tests to keep your tests resilient and easy to understand.</span></span>

## <a name="why-unit-test"></a><span data-ttu-id="21a06-108">Pourquoi un test unitaire ?</span><span class="sxs-lookup"><span data-stu-id="21a06-108">Why unit test?</span></span>

### <a name="less-time-performing-functional-tests"></a><span data-ttu-id="21a06-109">Moins de temps pour effectuer des tests fonctionnels</span><span class="sxs-lookup"><span data-stu-id="21a06-109">Less time performing functional tests</span></span>
<span data-ttu-id="21a06-110">Les tests fonctionnels sont coûteux.</span><span class="sxs-lookup"><span data-stu-id="21a06-110">Functional tests are expensive.</span></span> <span data-ttu-id="21a06-111">Ils impliquent généralement d’ouvrir l’application et d’effectuer une série d’étapes que vous (ou quelqu’un d’autre) devez suivre pour valider le comportement attendu.</span><span class="sxs-lookup"><span data-stu-id="21a06-111">They typically involve opening up the application and performing a series of steps that you (or someone else), must follow in order to validate the expected behavior.</span></span> <span data-ttu-id="21a06-112">Dans la mesure où le testeur ne connaît pas toujours ces étapes, il doit contacter une personne plus compétente dans le domaine concerné pour effectuer le test.</span><span class="sxs-lookup"><span data-stu-id="21a06-112">These steps may not always be known to the tester, which means they will have to reach out to someone more knowledgeable in the area in order to carry out the test.</span></span> <span data-ttu-id="21a06-113">Le test lui-même peut prendre quelques secondes pour des changements mineurs, ou quelques minutes pour des changements plus importants.</span><span class="sxs-lookup"><span data-stu-id="21a06-113">Testing itself could take seconds for trivial changes, or minutes for larger changes.</span></span> <span data-ttu-id="21a06-114">Enfin, ce processus doit être répété pour chaque changement apporté au système.</span><span class="sxs-lookup"><span data-stu-id="21a06-114">Lastly, this process must be repeated for every change that you make in the system.</span></span>

<span data-ttu-id="21a06-115">Les tests unitaires, en revanche, prennent quelques millisecondes. Vous pouvez les exécuter en appuyant sur un bouton sans nécessairement connaître le système dans son ensemble.</span><span class="sxs-lookup"><span data-stu-id="21a06-115">Unit tests, on the other hand, take milliseconds, can be run at the press of a button and do not necessarily require any knowledge of the system at large.</span></span> <span data-ttu-id="21a06-116">La réussite ou non du test dépend du programme d’exécution de tests et non de la personne qui effectue le test.</span><span class="sxs-lookup"><span data-stu-id="21a06-116">Whether or not the test passes or fails is up to the test runner, not the individual.</span></span>

### <a name="protection-against-regression"></a><span data-ttu-id="21a06-117">Protection contre la régression</span><span class="sxs-lookup"><span data-stu-id="21a06-117">Protection against regression</span></span>
<span data-ttu-id="21a06-118">Les défauts de régression sont des défauts introduits quand un changement est apporté à l’application.</span><span class="sxs-lookup"><span data-stu-id="21a06-118">Regression defects are defects that are introduced when a change is made to the application.</span></span> <span data-ttu-id="21a06-119">Il est courant pour les testeurs de tester non seulement les nouvelles fonctionnalités, mais également les fonctionnalités antérieures afin de vérifier que ces dernières fonctionnent toujours comme prévu.</span><span class="sxs-lookup"><span data-stu-id="21a06-119">It is common for testers to not only test their new feature but also features that existed beforehand in order to verify that previously implemented features still function as expected.</span></span>

<span data-ttu-id="21a06-120">Avec les tests unitaires, vous pouvez réexécuter l’intégralité de votre suite de tests après chaque build ou même après avoir changé une ligne de code.</span><span class="sxs-lookup"><span data-stu-id="21a06-120">With unit testing, it's possible to rerun your entire suite of tests after every build or even after you change a line of code.</span></span> <span data-ttu-id="21a06-121">Ainsi, vous avez l’assurance que votre nouveau code ne perturbe pas les fonctionnalités existantes.</span><span class="sxs-lookup"><span data-stu-id="21a06-121">Giving you confidence that your new code does not break existing functionality.</span></span>

### <a name="executable-documentation"></a><span data-ttu-id="21a06-122">Documentation exécutable</span><span class="sxs-lookup"><span data-stu-id="21a06-122">Executable documentation</span></span>
<span data-ttu-id="21a06-123">Il n’est pas toujours évident de déterminer ce que fait une méthode particulière, ou comment elle se comporte en fonction d’une entrée spécifique.</span><span class="sxs-lookup"><span data-stu-id="21a06-123">It may not always be obvious what a particular method does or how it behaves given a certain input.</span></span> <span data-ttu-id="21a06-124">Vous pouvez vous demander : comment se comporte cette méthode si je lui passe une chaîne vide ?</span><span class="sxs-lookup"><span data-stu-id="21a06-124">You may ask yourself: How does this method behave if I pass it a blank string?</span></span> <span data-ttu-id="21a06-125">Null ?</span><span class="sxs-lookup"><span data-stu-id="21a06-125">Null?</span></span>

<span data-ttu-id="21a06-126">Quand vous avez une suite de tests unitaires correctement nommés, chaque test doit pouvoir expliquer clairement la sortie attendue pour une entrée donnée.</span><span class="sxs-lookup"><span data-stu-id="21a06-126">When you have a suite of well-named unit tests, each test should be able to clearly explain the expected output for a given input.</span></span> <span data-ttu-id="21a06-127">De plus, il doit pouvoir vérifier son bon fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="21a06-127">In addition, it should be able to verify that it actually works.</span></span>

### <a name="less-coupled-code"></a><span data-ttu-id="21a06-128">Code moins couplé</span><span class="sxs-lookup"><span data-stu-id="21a06-128">Less coupled code</span></span>
<span data-ttu-id="21a06-129">Quand le code est fortement couplé, il peut être difficile d’effectuer des tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="21a06-129">When code is tightly coupled, it can be difficult to unit test.</span></span> <span data-ttu-id="21a06-130">Si vous ne créez pas de tests unitaires pour le code que vous écrivez, le couplage peut être moins apparent.</span><span class="sxs-lookup"><span data-stu-id="21a06-130">Without creating unit tests for the code that you're writing, coupling may be less apparent.</span></span>

<span data-ttu-id="21a06-131">L’écriture de tests pour votre code permet de le découpler de manière naturelle. Sinon, il est plus difficile à tester.</span><span class="sxs-lookup"><span data-stu-id="21a06-131">Writing tests for your code will naturally decouple your code, because it would be more difficult to test otherwise.</span></span>

## <a name="characteristics-of-a-good-unit-test"></a><span data-ttu-id="21a06-132">Caractéristiques d’un bon test unitaire</span><span class="sxs-lookup"><span data-stu-id="21a06-132">Characteristics of a good unit test</span></span>
- <span data-ttu-id="21a06-133">**Rapide**.</span><span class="sxs-lookup"><span data-stu-id="21a06-133">**Fast**.</span></span> <span data-ttu-id="21a06-134">Il n’est pas rare pour des projets matures de comporter des milliers de tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="21a06-134">It is not uncommon for mature projects to have thousands of unit tests.</span></span> <span data-ttu-id="21a06-135">Les tests unitaires doivent durer très peu de temps.</span><span class="sxs-lookup"><span data-stu-id="21a06-135">Unit tests should take very little time to run.</span></span> <span data-ttu-id="21a06-136">Millisecondes.</span><span class="sxs-lookup"><span data-stu-id="21a06-136">Milliseconds.</span></span>
- <span data-ttu-id="21a06-137">**Isolé**.</span><span class="sxs-lookup"><span data-stu-id="21a06-137">**Isolated**.</span></span> <span data-ttu-id="21a06-138">Les tests unitaires sont autonomes et peuvent être exécutés de manière isolée. Ils ne dépendent d’aucun facteur externe, par exemple un système de fichiers ou une base de données.</span><span class="sxs-lookup"><span data-stu-id="21a06-138">Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.</span></span>
- <span data-ttu-id="21a06-139">**Répétable**.</span><span class="sxs-lookup"><span data-stu-id="21a06-139">**Repeatable**.</span></span> <span data-ttu-id="21a06-140">L’exécution d’un test unitaire doit être cohérente avec ses résultats. En d’autres termes, il retourne toujours le même résultat si vous ne changez rien entre les exécutions.</span><span class="sxs-lookup"><span data-stu-id="21a06-140">Running a unit test should be consistent with its results, that is, it always returns the same result if you do not change anything in between runs.</span></span>
- <span data-ttu-id="21a06-141">**Autovérification**.</span><span class="sxs-lookup"><span data-stu-id="21a06-141">**Self-Checking**.</span></span> <span data-ttu-id="21a06-142">Le test doit pouvoir détecter automatiquement son état de réussite ou d’échec sans aucune interaction humaine.</span><span class="sxs-lookup"><span data-stu-id="21a06-142">The test should be able to automatically detect if it passed or failed without any human interaction.</span></span>
- <span data-ttu-id="21a06-143">**Délai approprié**.</span><span class="sxs-lookup"><span data-stu-id="21a06-143">**Timely**.</span></span> <span data-ttu-id="21a06-144">Un test unitaire ne doit pas prendre beaucoup plus de temps à écrire que le code testé.</span><span class="sxs-lookup"><span data-stu-id="21a06-144">A unit test should not take a disproportionally long time to write compared to the code being tested.</span></span> <span data-ttu-id="21a06-145">Si vous trouvez que le test du code prend beaucoup de temps par rapport à son écriture, optez pour une conception plus facile à tester.</span><span class="sxs-lookup"><span data-stu-id="21a06-145">If you find testing the code taking a large amount of time compared to writing the code, consider a design that is more testable.</span></span>

## <a name="lets-speak-the-same-language"></a><span data-ttu-id="21a06-146">Parlons la même langue</span><span class="sxs-lookup"><span data-stu-id="21a06-146">Let's speak the same language</span></span>
<span data-ttu-id="21a06-147">Le terme *mock* (élément fictif) est malheureusement utilisé à très mauvais escient quand il s’agit de tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-147">The term *mock* is unfortunately very misused when talking about testing.</span></span> <span data-ttu-id="21a06-148">Voici une définition des types les plus courants de *fakes* (éléments fictifs) pour l’écriture de tests unitaires :</span><span class="sxs-lookup"><span data-stu-id="21a06-148">The following defines the most common types of *fakes* when writing unit tests:</span></span>

<span data-ttu-id="21a06-149">*Fake* - Il s’agit d’un terme générique qui permet de décrire un stub ou un mock (objet fictif).</span><span class="sxs-lookup"><span data-stu-id="21a06-149">*Fake* - A fake is a generic term which can be used to describe either a stub or a mock object.</span></span> <span data-ttu-id="21a06-150">Seul le contexte permet de déterminer s’il s’agit d’un stub ou d’un mock (objet fictif).</span><span class="sxs-lookup"><span data-stu-id="21a06-150">Whether it is a stub or a mock depends on the context in which it's used.</span></span> <span data-ttu-id="21a06-151">En d’autres termes, un fake (élément fictif) peut être un stub ou un mob (objet fictif).</span><span class="sxs-lookup"><span data-stu-id="21a06-151">So in other words, a fake can be a stub or a mock.</span></span>

<span data-ttu-id="21a06-152">*Mock* - Il s’agit d’un objet fictif du système qui détermine la réussite ou l’échec d’un test unitaire.</span><span class="sxs-lookup"><span data-stu-id="21a06-152">*Mock* - A mock object is a fake object in the system that decides whether or not a unit test has passed or failed.</span></span> <span data-ttu-id="21a06-153">Un mock commence par être un Fake jusqu’à ce qu’il soit différencié par une assertion.</span><span class="sxs-lookup"><span data-stu-id="21a06-153">A mock starts out as a Fake until it is asserted against.</span></span>

<span data-ttu-id="21a06-154">*Stub* - Un stub permet de remplacer de manière contrôlée une dépendance existante (ou collaborateur) dans le système.</span><span class="sxs-lookup"><span data-stu-id="21a06-154">*Stub* - A stub is a controllable replacement for an existing dependency (or collaborator) in the system.</span></span> <span data-ttu-id="21a06-155">À l’aide d’un stub, vous pouvez tester votre code sans avoir à gérer directement la dépendance.</span><span class="sxs-lookup"><span data-stu-id="21a06-155">By using a stub, you can test your code without dealing with the dependency directly.</span></span> <span data-ttu-id="21a06-156">Par défaut, un fake commence comme par être un stub.</span><span class="sxs-lookup"><span data-stu-id="21a06-156">By default, a fake starts out as a stub.</span></span>

<span data-ttu-id="21a06-157">Examinez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="21a06-157">Consider the following code snippet:</span></span>

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="21a06-158">Il s’agit d’un exemple de stub appelé mock.</span><span class="sxs-lookup"><span data-stu-id="21a06-158">This would be an example of stub being referred to as a mock.</span></span> <span data-ttu-id="21a06-159">Dans le cas présent, il s’agit bien d’un stub.</span><span class="sxs-lookup"><span data-stu-id="21a06-159">In this case, it is a stub.</span></span> <span data-ttu-id="21a06-160">Vous passez simplement Order pour instancier `Purchase` (le système testé).</span><span class="sxs-lookup"><span data-stu-id="21a06-160">You're just passing in the Order as a means to be able to instantiate `Purchase` (the system under test).</span></span> <span data-ttu-id="21a06-161">Le nom `MockOrder` est également très trompeur, car encore une fois, order n’est pas un mock.</span><span class="sxs-lookup"><span data-stu-id="21a06-161">The name `MockOrder` is also very misleading because again, the order is not a mock.</span></span>

<span data-ttu-id="21a06-162">Il existe une meilleure approche</span><span class="sxs-lookup"><span data-stu-id="21a06-162">A better approach would be</span></span>

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

<span data-ttu-id="21a06-163">En renommant la classe en `FakeOrder`, vous avez rendu celle-ci beaucoup plus générique. Vous pouvez utiliser la classe en tant que mock ou stub.</span><span class="sxs-lookup"><span data-stu-id="21a06-163">By renaming the class to `FakeOrder`, you've made the class a lot more generic, the class can be used as a mock or a stub.</span></span> <span data-ttu-id="21a06-164">Selon ce qui est le plus approprié pour le cas de test.</span><span class="sxs-lookup"><span data-stu-id="21a06-164">Whichever is better for the test case.</span></span> <span data-ttu-id="21a06-165">Dans l’exemple ci-dessus, `FakeOrder` est utilisé en tant que stub.</span><span class="sxs-lookup"><span data-stu-id="21a06-165">In the above example, `FakeOrder` is used as a stub.</span></span> <span data-ttu-id="21a06-166">Vous n’utilisez pas `FakeOrder` sous quelque forme que ce soit durant l’assertion.</span><span class="sxs-lookup"><span data-stu-id="21a06-166">You're not using the `FakeOrder` in any shape or form during the assert.</span></span> <span data-ttu-id="21a06-167">`FakeOrder` a simplement été passé à la classe `Purchase` pour répondre aux exigences du constructeur.</span><span class="sxs-lookup"><span data-stu-id="21a06-167">`FakeOrder` was just passed into the `Purchase` class to satisfy the requirements of the constructor.</span></span>

<span data-ttu-id="21a06-168">Pour l’utiliser en tant que Mock, vous pouvez faire quelque chose qui ressemble à ceci</span><span class="sxs-lookup"><span data-stu-id="21a06-168">To use it as a Mock, you could do something like this</span></span>

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

<span data-ttu-id="21a06-169">Dans le cas présent, vous vérifiez une propriété sur le Fake (en le différenciant par assertion). Ainsi, dans l’extrait de code ci-dessus, `mockOrder` est un Mock.</span><span class="sxs-lookup"><span data-stu-id="21a06-169">In this case, you are checking a property on the Fake (asserting against it), so in the above code snippet, the `mockOrder` is a Mock.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21a06-170">Il est important que cette terminologie soit correcte.</span><span class="sxs-lookup"><span data-stu-id="21a06-170">It's important to get this terminology correct.</span></span> <span data-ttu-id="21a06-171">Si vous appelez vos stubs « mocks », les autres développeurs vont faire de fausses hypothèses par rapport à votre intention.</span><span class="sxs-lookup"><span data-stu-id="21a06-171">If you call your stubs "mocks", other developers are going to make false assumptions about your intent.</span></span>

<span data-ttu-id="21a06-172">Le point principal à retenir à propos des mocks et des stubs est que les mocks sont comme des stubs. Toutefois, vous différenciez le mock (objet fictif) par assertion, contrairement au stub.</span><span class="sxs-lookup"><span data-stu-id="21a06-172">The main thing to remember about mocks versus stubs is that mocks are just like stubs, but you assert against the mock object, whereas you do not assert against a stub.</span></span>

## <a name="best-practices"></a><span data-ttu-id="21a06-173">meilleures pratiques recommandées.</span><span class="sxs-lookup"><span data-stu-id="21a06-173">Best practices</span></span>

### <a name="naming-your-tests"></a><span data-ttu-id="21a06-174">Nommage de vos tests</span><span class="sxs-lookup"><span data-stu-id="21a06-174">Naming your tests</span></span>
<span data-ttu-id="21a06-175">Le nom de votre test doit être composé de trois parties :</span><span class="sxs-lookup"><span data-stu-id="21a06-175">The name of your test should consist of three parts:</span></span>
- <span data-ttu-id="21a06-176">Nom de la méthode testée</span><span class="sxs-lookup"><span data-stu-id="21a06-176">The name of the method being tested.</span></span>
- <span data-ttu-id="21a06-177">Scénario de test utilisé</span><span class="sxs-lookup"><span data-stu-id="21a06-177">The scenario under which it's being tested.</span></span>
- <span data-ttu-id="21a06-178">Comportement attendu quand le scénario est appelé</span><span class="sxs-lookup"><span data-stu-id="21a06-178">The expected behavior when the scenario is invoked.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-179">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-179">Why?</span></span>
- <span data-ttu-id="21a06-180">Les standards de nommage sont importants, car ils expriment explicitement la finalité du test.</span><span class="sxs-lookup"><span data-stu-id="21a06-180">Naming standards are important because they explicitly express the intent of the test.</span></span>

<span data-ttu-id="21a06-181">Les tests ne se limitent pas à la vérification du bon fonctionnement de votre code, ils fournissent également de la documentation.</span><span class="sxs-lookup"><span data-stu-id="21a06-181">Tests are more than just making sure your code works, they also provide documentation.</span></span> <span data-ttu-id="21a06-182">En examinant simplement la suite de tests unitaires, vous devez pouvoir en déduire le comportement de votre code.</span><span class="sxs-lookup"><span data-stu-id="21a06-182">Just by looking at the suite of unit tests, you should be able to infer the behavior of your code without even looking at the code itself.</span></span> <span data-ttu-id="21a06-183">De plus, en cas d’échec des tests, vous pouvez voir exactement quels sont les scénarios qui ne répondent pas à vos attentes.</span><span class="sxs-lookup"><span data-stu-id="21a06-183">Additionally, when tests fail, you can see exactly which scenarios do not meet your expectations.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-184">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-184">Bad:</span></span>
[!code-csharp[BeforeNaming](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a><span data-ttu-id="21a06-185">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-185">Better:</span></span>
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a><span data-ttu-id="21a06-186">Organisation de vos tests</span><span class="sxs-lookup"><span data-stu-id="21a06-186">Arranging your tests</span></span>
<span data-ttu-id="21a06-187">**Organisation, Action, Assertion** est un modèle courant pour les tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="21a06-187">**Arrange, Act, Assert** is a common pattern when unit testing.</span></span> <span data-ttu-id="21a06-188">Comme son nom l’indique, il comporte trois actions principales :</span><span class="sxs-lookup"><span data-stu-id="21a06-188">As the name implies, it consists of three main actions:</span></span>
- <span data-ttu-id="21a06-189">*Organisation*, création et configuration des objets selon les besoins</span><span class="sxs-lookup"><span data-stu-id="21a06-189">*Arrange* your objects, creating and setting them up as necessary.</span></span>
- <span data-ttu-id="21a06-190">*Action* sur un objet</span><span class="sxs-lookup"><span data-stu-id="21a06-190">*Act* on an object.</span></span>
- <span data-ttu-id="21a06-191">*Assertion* de ce qui est prévu</span><span class="sxs-lookup"><span data-stu-id="21a06-191">*Assert* that something is as expected.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-192">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-192">Why?</span></span>
- <span data-ttu-id="21a06-193">Permet de séparer clairement ce qui est testé des étapes *organisation* et *assertion*.</span><span class="sxs-lookup"><span data-stu-id="21a06-193">Clearly separates what is being tested from the *arrange* and *assert* steps.</span></span>
- <span data-ttu-id="21a06-194">Moins de risques de mélanger les assertions avec le code de l’étape « Action ».</span><span class="sxs-lookup"><span data-stu-id="21a06-194">Less chance to intermix assertions with "Act" code.</span></span>

<span data-ttu-id="21a06-195">La lisibilité est l’un des aspects les plus importants durant l’écriture d’un test.</span><span class="sxs-lookup"><span data-stu-id="21a06-195">Readability is one of the most important aspects when writing a test.</span></span> <span data-ttu-id="21a06-196">La séparation de chacune de ces actions dans le test met clairement en évidence les dépendances nécessaires à l’appel du code, le mode d’appel du code, ainsi que le contenu de l’assertion.</span><span class="sxs-lookup"><span data-stu-id="21a06-196">Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you are trying to assert.</span></span> <span data-ttu-id="21a06-197">Bien qu’il soit possible de combiner certaines étapes et de réduire la taille du test, l’objectif principal est de rendre le test aussi lisible que possible.</span><span class="sxs-lookup"><span data-stu-id="21a06-197">While it may be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-198">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-198">Bad:</span></span>
[!code-csharp[BeforeArranging](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a><span data-ttu-id="21a06-199">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-199">Better:</span></span>
[!code-csharp[AfterArranging](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a><span data-ttu-id="21a06-200">Écrire des tests concluants minimaux</span><span class="sxs-lookup"><span data-stu-id="21a06-200">Write minimally passing tests</span></span>
<span data-ttu-id="21a06-201">L’entrée à utiliser dans un test unitaire doit être la plus simple possible pour vérifier le comportement testé.</span><span class="sxs-lookup"><span data-stu-id="21a06-201">The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-202">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-202">Why?</span></span>
- <span data-ttu-id="21a06-203">Les tests deviennent plus résilients face aux futurs changements du code base.</span><span class="sxs-lookup"><span data-stu-id="21a06-203">Tests become more resilient to future changes in the codebase.</span></span>
- <span data-ttu-id="21a06-204">Plus proche du comportement de test que de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="21a06-204">Closer to testing behavior over implementation.</span></span>

<span data-ttu-id="21a06-205">Les tests qui contiennent plus d’informations que nécessaire pour être réussis ont plus de chances d’introduire des erreurs et peuvent rendre l’intention moins claire.</span><span class="sxs-lookup"><span data-stu-id="21a06-205">Tests that include more information than required to pass the test have a higher chance of introducing errors into the test and can make the intent of the test less clear.</span></span> <span data-ttu-id="21a06-206">Quand vous écrivez des tests, vous devez vous concentrer sur le comportement.</span><span class="sxs-lookup"><span data-stu-id="21a06-206">When writing tests you want to focus on the behavior.</span></span> <span data-ttu-id="21a06-207">La définition de propriétés supplémentaires pour les modèles ou l’utilisation de valeurs différentes de zéro quand cela n’est pas nécessaire, ne fait que nuire à ce que vous essayez de prouver.</span><span class="sxs-lookup"><span data-stu-id="21a06-207">Setting extra properties on models or using non-zero values when not required, only detracts from what you are trying to prove.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-208">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-208">Bad:</span></span>
[!code-csharp[BeforeMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a><span data-ttu-id="21a06-209">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-209">Better:</span></span>
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a><span data-ttu-id="21a06-210">Éviter les chaînes magiques</span><span class="sxs-lookup"><span data-stu-id="21a06-210">Avoid magic strings</span></span>
<span data-ttu-id="21a06-211">Le nommage des variables dans les tests unitaires est aussi important, sinon plus, que le nommage des variables dans le code de production.</span><span class="sxs-lookup"><span data-stu-id="21a06-211">Naming variables in unit tests is as important, if not more important, than naming variables in production code.</span></span> <span data-ttu-id="21a06-212">Les tests unitaires ne doivent pas contenir de chaînes magiques.</span><span class="sxs-lookup"><span data-stu-id="21a06-212">Unit tests should not contain magic strings.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-213">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-213">Why?</span></span>
- <span data-ttu-id="21a06-214">Évite au lecteur du test d’inspecter le code de production pour déterminer ce qui rend la valeur spéciale.</span><span class="sxs-lookup"><span data-stu-id="21a06-214">Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.</span></span>
- <span data-ttu-id="21a06-215">Montre explicitement ce que vous essayez de *prouver* et non ce que vous essayez d’*accomplir*.</span><span class="sxs-lookup"><span data-stu-id="21a06-215">Explicitly shows what you're trying to *prove* rather than trying to *accomplish*.</span></span>

<span data-ttu-id="21a06-216">Les chaînes magiques peuvent être sources de confusion pour le lecteur de vos tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-216">Magic strings can cause confusion to the reader of your tests.</span></span> <span data-ttu-id="21a06-217">Si une chaîne semble inhabituelle, il peut se demander pourquoi une certaine valeur a été choisie pour un paramètre ou une valeur de retour.</span><span class="sxs-lookup"><span data-stu-id="21a06-217">If a string looks out of the ordinary, they may wonder why a certain value was chosen for a parameter or return value.</span></span> <span data-ttu-id="21a06-218">Cela peut l’amener à examiner de plus près les détails de l’implémentation, au lieu de se concentrer sur le test.</span><span class="sxs-lookup"><span data-stu-id="21a06-218">This may lead them to take a closer look at the implementation details, rather than focus on the test.</span></span>

> [!TIP] 
> <span data-ttu-id="21a06-219">Quand vous écrivez des tests, concentrez-vous au maximum sur l’expression de l’intention.</span><span class="sxs-lookup"><span data-stu-id="21a06-219">When writing tests, you should aim to express as much intent as possible.</span></span> <span data-ttu-id="21a06-220">Dans le cas des chaînes magiques, une bonne approche consiste à assigner ces valeurs à des constantes.</span><span class="sxs-lookup"><span data-stu-id="21a06-220">In the case of magic strings, a good approach is to assign these values to constants.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-221">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-221">Bad:</span></span>
[!code-csharp[BeforeMagicString](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a><span data-ttu-id="21a06-222">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-222">Better:</span></span>
[!code-csharp[AfterMagicString](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a><span data-ttu-id="21a06-223">Éviter la logique dans les tests</span><span class="sxs-lookup"><span data-stu-id="21a06-223">Avoid logic in tests</span></span>
<span data-ttu-id="21a06-224">Durant l’écriture des tests unitaires, évitez la concaténation manuelle des chaînes et les conditions logiques telles que `if`, `while`, `for`, `switch`, etc.</span><span class="sxs-lookup"><span data-stu-id="21a06-224">When writing your unit tests avoid manual string concatenation and logical conditions such as `if`, `while`, `for`, `switch`, etc.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-225">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-225">Why?</span></span>
- <span data-ttu-id="21a06-226">Moins de risques d’introduire un bogue dans vos tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-226">Less chance to introduce a bug inside of your tests.</span></span>
- <span data-ttu-id="21a06-227">Concentrez-vous sur le résultat final plutôt que sur les détails de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="21a06-227">Focus on the end result, rather than implementation details.</span></span>

<span data-ttu-id="21a06-228">Quand vous introduisez une logique dans votre suite de tests, le risque d’introduction d’un bogue augmente considérablement.</span><span class="sxs-lookup"><span data-stu-id="21a06-228">When you introduce logic into your test suite, the chance of introducing a bug into it increases dramatically.</span></span> <span data-ttu-id="21a06-229">Votre suite de tests est bien le dernier endroit où vous devez trouver un bogue.</span><span class="sxs-lookup"><span data-stu-id="21a06-229">The last place that you want to find a bug is within your test suite.</span></span> <span data-ttu-id="21a06-230">Le fonctionnement de vos tests doit présenter un niveau de fiabilité élevé, sinon vous n’aurez pas confiance en ces derniers.</span><span class="sxs-lookup"><span data-stu-id="21a06-230">You should have a high level of confidence that your tests work, otherwise, you will not trust them.</span></span> <span data-ttu-id="21a06-231">Les tests auxquels vous ne faites pas confiance n’ont aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="21a06-231">Tests that you do not trust, do not provide any value.</span></span> <span data-ttu-id="21a06-232">L’échec d’un test vous donne l’impression que quelque chose ne va pas dans votre code, et que vous ne pouvez pas l’ignorer.</span><span class="sxs-lookup"><span data-stu-id="21a06-232">When a test fails, you want to have a sense that something is actually wrong with your code and that it cannot be ignored.</span></span>

> [!TIP]
> <span data-ttu-id="21a06-233">Si le recours à la logique dans votre test semble inévitable, scindez-le en deux ou plusieurs tests distincts.</span><span class="sxs-lookup"><span data-stu-id="21a06-233">If logic in your test seems unavoidable, consider splitting the test up into two or more different tests.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-234">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-234">Bad:</span></span>
[!code-csharp[LogicInTests](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a><span data-ttu-id="21a06-235">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-235">Better:</span></span>
[!code-csharp[AfterTestLogic](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a><span data-ttu-id="21a06-236">Préférez les méthodes d’assistance à setup et teardown</span><span class="sxs-lookup"><span data-stu-id="21a06-236">Prefer helper methods to setup and teardown</span></span>
<span data-ttu-id="21a06-237">Si vous avez besoin d’un objet ou d’un état similaire pour vos tests, préférez une méthode d’assistance aux attributs Setup et Teardown, s’ils existent.</span><span class="sxs-lookup"><span data-stu-id="21a06-237">If you require a similar object or state for your tests, prefer a helper method than leveraging Setup and Teardown attributes if they exist.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-238">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-238">Why?</span></span>
- <span data-ttu-id="21a06-239">Moins de confusion durant la lecture des tests, car l’ensemble du code est visible à partir de chaque test.</span><span class="sxs-lookup"><span data-stu-id="21a06-239">Less confusion when reading the tests since all of the code is visible from within each test.</span></span>
- <span data-ttu-id="21a06-240">Moins de risques d’effectuer une configuration excessive ou insuffisante pour le test donné.</span><span class="sxs-lookup"><span data-stu-id="21a06-240">Less chance of setting up too much or too little for the given test.</span></span>
- <span data-ttu-id="21a06-241">Moins de risques de partager l’état entre les tests, ce qui entraîne la création de dépendances indésirables entre eux.</span><span class="sxs-lookup"><span data-stu-id="21a06-241">Less chance of sharing state between tests which creates unwanted dependencies between them.</span></span>

<span data-ttu-id="21a06-242">Dans les frameworks de tests unitaires, `Setup` est appelé avant chaque test unitaire de votre suite de tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-242">In unit testing frameworks, `Setup` is called before each and every unit test within your test suite.</span></span> <span data-ttu-id="21a06-243">Bien que certains puissent le voir comme un outil utile, cela aboutit généralement à des tests compliqués et difficiles à lire.</span><span class="sxs-lookup"><span data-stu-id="21a06-243">While some may see this as a useful tool, it generally ends up leading to bloated and hard to read tests.</span></span> <span data-ttu-id="21a06-244">Chaque test a généralement des exigences différentes pour être opérationnel.</span><span class="sxs-lookup"><span data-stu-id="21a06-244">Each test will generally have different requirements in order to get the test up and running.</span></span> <span data-ttu-id="21a06-245">Malheureusement, `Setup` vous oblige à utiliser exactement les mêmes exigences pour chaque test.</span><span class="sxs-lookup"><span data-stu-id="21a06-245">Unfortunately, `Setup` forces you to use the exact same requirements for each test.</span></span>

> [!NOTE] 
> <span data-ttu-id="21a06-246">xUnit a supprimé SetUp et TearDown depuis la version 2.x</span><span class="sxs-lookup"><span data-stu-id="21a06-246">xUnit has removed both SetUp and TearDown as of version 2.x</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-247">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-247">Bad:</span></span>
[!code-csharp[BeforeSetup](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a><span data-ttu-id="21a06-248">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-248">Better:</span></span>
[!code-csharp[AfterHelperMethod](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a><span data-ttu-id="21a06-249">Éviter les assertions multiples</span><span class="sxs-lookup"><span data-stu-id="21a06-249">Avoid multiple asserts</span></span>
<span data-ttu-id="21a06-250">Durant l’écriture des tests, essayez d’inclure uniquement une instruction Assert par test.</span><span class="sxs-lookup"><span data-stu-id="21a06-250">When writing your tests, try to only include one Assert per test.</span></span> <span data-ttu-id="21a06-251">Voici les approches courantes pour utiliser une seule assertion :</span><span class="sxs-lookup"><span data-stu-id="21a06-251">Common approaches to using only one assert include:</span></span>
- <span data-ttu-id="21a06-252">Créez un test distinct pour chaque assertion.</span><span class="sxs-lookup"><span data-stu-id="21a06-252">Create a separate test for each assert.</span></span>
- <span data-ttu-id="21a06-253">Utilisez des tests paramétrables.</span><span class="sxs-lookup"><span data-stu-id="21a06-253">Use parameterized tests.</span></span>

#### <a name="why"></a><span data-ttu-id="21a06-254">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="21a06-254">Why?</span></span>
- <span data-ttu-id="21a06-255">En cas d’échec d’une instruction Assert, les assertions qui suivent ne sont pas évaluées.</span><span class="sxs-lookup"><span data-stu-id="21a06-255">If one Assert fails, the subsequent Asserts will not be evaluated.</span></span>
- <span data-ttu-id="21a06-256">Permet de vérifier que vous n’effectuez pas l’assertion de plusieurs cas dans vos tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-256">Ensures you are not asserting multiple cases in your tests.</span></span>
- <span data-ttu-id="21a06-257">Vous donne une idée complète des causes de l’échec des tests.</span><span class="sxs-lookup"><span data-stu-id="21a06-257">Gives you the entire picture as to why your tests are failing.</span></span> 

<span data-ttu-id="21a06-258">Quand vous introduisez plusieurs assertions dans un cas de test, vous n’avez pas la garantie que toutes les assertions vont être exécutées.</span><span class="sxs-lookup"><span data-stu-id="21a06-258">When introducing multiple asserts into a test case, it is not guaranteed that all of the asserts will be executed.</span></span> <span data-ttu-id="21a06-259">Dans la plupart des frameworks de tests unitaires, une fois qu’une assertion a été l’objet d’un échec dans un test unitaire, les tests en cours d’exécution sont automatiquement considérés comme défaillants.</span><span class="sxs-lookup"><span data-stu-id="21a06-259">In most unit testing frameworks, once an assertion fails in a unit test, the proceeding tests are automatically considered to be failing.</span></span> <span data-ttu-id="21a06-260">Cela peut être déroutant, car les fonctionnalités qui fonctionnent réellement indiquent un état d’échec.</span><span class="sxs-lookup"><span data-stu-id="21a06-260">This can be confusing as functionality that is actually working, will be shown as failing.</span></span>

> [!NOTE]
> <span data-ttu-id="21a06-261">Il existe une exception usuelle à cette règle : l’assertion d’un objet par différenciation.</span><span class="sxs-lookup"><span data-stu-id="21a06-261">A common exception to this rule is when asserting against an object.</span></span> <span data-ttu-id="21a06-262">Dans ce cas, il est généralement acceptable d’avoir plusieurs assertions sur chaque propriété pour vérifier que l’objet se trouve dans l’état prévu.</span><span class="sxs-lookup"><span data-stu-id="21a06-262">In this case, it is generally acceptable to have multiple asserts against each property to ensure the object is in the state that you expect it to be in.</span></span>

#### <a name="bad"></a><span data-ttu-id="21a06-263">Mauvais :</span><span class="sxs-lookup"><span data-stu-id="21a06-263">Bad:</span></span>
[!code-csharp[BeforeMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a><span data-ttu-id="21a06-264">Mieux :</span><span class="sxs-lookup"><span data-stu-id="21a06-264">Better:</span></span>
[!code-csharp[AfterMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a><span data-ttu-id="21a06-265">Valider les méthodes privées en effectuant un test unitaire des méthodes publiques</span><span class="sxs-lookup"><span data-stu-id="21a06-265">Validate private methods by unit testing public methods</span></span>
<span data-ttu-id="21a06-266">Dans la plupart des cas, il n’est pas nécessaire de tester une méthode privée.</span><span class="sxs-lookup"><span data-stu-id="21a06-266">In most cases, there should not be a need to test a private method.</span></span> <span data-ttu-id="21a06-267">Les méthodes privées sont un détail d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="21a06-267">Private methods are an implementation detail.</span></span> <span data-ttu-id="21a06-268">Vous pouvez considérer la chose ainsi : les méthodes privées n’existent jamais de manière isolée.</span><span class="sxs-lookup"><span data-stu-id="21a06-268">You can think of it this way: private methods never exist in isolation.</span></span> <span data-ttu-id="21a06-269">À un moment donné, une méthode publique appelle la méthode privée dans le cadre de son implémentation.</span><span class="sxs-lookup"><span data-stu-id="21a06-269">At some point, there is going to be a public facing method that calls the private method as part of its implementation.</span></span> <span data-ttu-id="21a06-270">Vous devez prendre en compte le résultat final de la méthode publique qui appelle la méthode privée.</span><span class="sxs-lookup"><span data-stu-id="21a06-270">What you should care about is the end result of the public method that calls into the private one.</span></span> 

<span data-ttu-id="21a06-271">Prenons le cas suivant</span><span class="sxs-lookup"><span data-stu-id="21a06-271">Consider the following case</span></span>

```csharp
public string ParseLogLine(string input)
{
    var sanitizedInput = trimInput(input);
    return sanitizedInput;
}

private string trimInput(string input)
{
    return input.Trim();
}
```

<span data-ttu-id="21a06-272">Votre première réaction peut être de commencer à écrire un test pour `trimInput`, car vous souhaitez vérifier que la méthode fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="21a06-272">Your first reaction may be to start writing a test for `trimInput` because you want to make sure that the method is working as expected.</span></span> <span data-ttu-id="21a06-273">Toutefois, il est tout à fait possible que `ParseLogLine` manipule `sanitizedInput` de manière inattendue, ce qui rend inutile tout test de `trimInput`.</span><span class="sxs-lookup"><span data-stu-id="21a06-273">However, it is entirely possible that `ParseLogLine` manipulates `sanitizedInput` in such a way that you do not expect, rendering a test against `trimInput` useless.</span></span> 

<span data-ttu-id="21a06-274">Le véritable test doit être effectué sur la méthode publique `ParseLogLine`, car c’est ce qui vous intéresse en fin de compte.</span><span class="sxs-lookup"><span data-stu-id="21a06-274">The real test should be done against the public facing method `ParseLogLine` because that is what you should ultimately care about.</span></span> 

```csharp
public void ParseLogLine_ByDefault_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

<span data-ttu-id="21a06-275">Ainsi, si vous voyez une méthode privée, recherchez la méthode publique et écrivez vos tests par rapport à cette méthode.</span><span class="sxs-lookup"><span data-stu-id="21a06-275">With this viewpoint, if you see a private method, find the public method and write your tests against that method.</span></span> <span data-ttu-id="21a06-276">Le fait qu’une méthode privée retourne le résultat attendu ne signifie pas que le système qui appelle la méthode privée utilise ce résultat correctement.</span><span class="sxs-lookup"><span data-stu-id="21a06-276">Just because a private method returns the expected result, does not mean the system that eventually calls the private method uses the result correctly.</span></span>

### <a name="stub-static-references"></a><span data-ttu-id="21a06-277">Références statiques de stub</span><span class="sxs-lookup"><span data-stu-id="21a06-277">Stub static references</span></span>
<span data-ttu-id="21a06-278">L’un des principes d’un test unitaire est qu’il doit avoir le contrôle total du système testé.</span><span class="sxs-lookup"><span data-stu-id="21a06-278">One of the principles of a unit test is that it must have full control of the system under test.</span></span> <span data-ttu-id="21a06-279">Cela peut être problématique quand le code de production inclut des appels à des références statiques (par exemple `DateTime.Now`).</span><span class="sxs-lookup"><span data-stu-id="21a06-279">This can be problematic when production code includes calls to static references (e.g. `DateTime.Now`).</span></span> <span data-ttu-id="21a06-280">Examinez le code suivant</span><span class="sxs-lookup"><span data-stu-id="21a06-280">Consider the following code</span></span>

```csharp
public int GetDiscountedPrice(int price)
{
    if(DateTime.Now == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

<span data-ttu-id="21a06-281">Comment ce code peut-il faire l’objet d’un test unitaire ?</span><span class="sxs-lookup"><span data-stu-id="21a06-281">How can this code possibly be unit tested?</span></span> <span data-ttu-id="21a06-282">Vous pouvez tenter l’approche suivante</span><span class="sxs-lookup"><span data-stu-id="21a06-282">You may try an approach such as</span></span>

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(2, actual)
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(1, actual);
}
```

<span data-ttu-id="21a06-283">Malheureusement, vous allez vite réaliser que vos tests posent quelques problèmes.</span><span class="sxs-lookup"><span data-stu-id="21a06-283">Unfortunately, you will quickly realize that there are a couple problems with your tests.</span></span> 

- <span data-ttu-id="21a06-284">Si la suite de tests est exécutée un mardi, le second test est une réussite, mais le premier test est un échec.</span><span class="sxs-lookup"><span data-stu-id="21a06-284">If the test suite is run on a Tuesday, the second test will pass, but the first test will fail.</span></span>
- <span data-ttu-id="21a06-285">Si la suite de tests est exécutée un autre jour, le premier test est une réussite, mais le second test est un échec.</span><span class="sxs-lookup"><span data-stu-id="21a06-285">If the test suite is run on any other day, the first test will pass, but the second test will fail.</span></span>

<span data-ttu-id="21a06-286">Pour résoudre ces problèmes, vous allez devoir introduire un *seam* dans votre code de production.</span><span class="sxs-lookup"><span data-stu-id="21a06-286">To solve these problems, you'll need to introduce a *seam* into your production code.</span></span> <span data-ttu-id="21a06-287">Il existe une approche qui consiste à inclure dans un wrapper le code que vous devez contrôler dans une interface, et à faire en sorte que le code de production dépende de cette interface.</span><span class="sxs-lookup"><span data-stu-id="21a06-287">One approach is to wrap the code that you need to control in an interface and have the production code depend on that interface.</span></span>

```csharp
public interface IDateTimeProvider
{
    DayOfWeek DayOfWeek();
}

public bool GetDiscountedPrice(int price, IDateTimeProvider dateTimeProvider)
{
    if(dateTimeProvider.DayOfWeek() == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

<span data-ttu-id="21a06-288">Votre suite de tests devient</span><span class="sxs-lookup"><span data-stu-id="21a06-288">Your test suite now becomes</span></span>

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Monday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(2, actual);
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Tuesday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(1, actual);
}
```

<span data-ttu-id="21a06-289">Désormais, la suite de tests a un contrôle total sur `DateTime.Now` et peut créer un stub de n’importe quelle valeur au moment d’appeler la méthode.</span><span class="sxs-lookup"><span data-stu-id="21a06-289">Now the test suite has full control over `DateTime.Now` and can stub any value when calling into the method.</span></span>