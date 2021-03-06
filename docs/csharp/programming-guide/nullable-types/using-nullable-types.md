---
title: Utilisation de types Nullable (Guide de programmation C#)
description: Découvrez comment utiliser les types Nullable C#.
ms.date: 08/02/2018
helpviewer_keywords:
- nullable types [C#], about nullable types
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
ms.openlocfilehash: 8ef875aee8c40f60472df52c19d1c1f2c73e95e8
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43515435"
---
# <a name="using-nullable-types-c-programming-guide"></a>Utilisation de types Nullable (Guide de programmation C#)

Les types Nullable sont des types qui représentent toutes les valeurs d’un type sous-jacent `T` ainsi qu’une autre valeur [null](../../language-reference/keywords/null.md). Pour plus d’informations, consultez la rubrique [Types Nullable](index.md).

Vous pouvez faire référence à un type Nullable dans l’un des formats suivants : `Nullable<T>` ou `T?`. Ces deux formats sont interchangeables.  
  
## <a name="declaration-and-assignment"></a>Déclaration et affectation

Comme un type valeur peut être converti implicitement en type Nullable correspondant, vous affectez une valeur à un type Nullable comme vous le feriez pour son type valeur sous-jacent. Vous pouvez également affecter la valeur `null`.  Exemple :
  
[!code-csharp[declare and assign](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#1)]

## <a name="examination-of-a-nullable-type-value"></a>Examen d’une valeur de type Nullable

Pour examiner une instance d’un type Nullable à la recherche de la valeur null et récupérer une valeur d’un type sous-jacent, utilisez les propriétés en lecture seule suivantes :  
  
- <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> indique si une instance d’un type Nullable a une valeur de son type sous-jacent.
  
- <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> obtient la valeur d’un type sous-jacent si <xref:System.Nullable%601.HasValue%2A> est `true`. Si <xref:System.Nullable%601.HasValue%2A> est `false`, la propriété <xref:System.Nullable%601.Value%2A> lève une <xref:System.InvalidOperationException>.
  
Le code dans l’exemple suivant utilise la propriété `HasValue` pour tester si la variable contient une valeur avant de l’afficher :
  
[!code-csharp-interactive[use HasValue](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#2)]
  
Vous pouvez également comparer une variable de type Nullable avec `null` au lieu d’utiliser la propriété `HasValue`, comme le montre l’exemple suivant :  
  
[!code-csharp-interactive[use comparison with null](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#3)]

À compter de C# 7.0, vous pouvez utiliser les [critères spéciaux](../../pattern-matching.md) pour examiner et obtenir une valeur d’un type Nullable :

[!code-csharp-interactive[use pattern matching](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#4)]

## <a name="conversion-from-a-nullable-type-to-an-underlying-type"></a>Conversion d’un type Nullable en type sous-jacent

Si vous devez affecter une valeur de type Nullable à un type non Nullable, utilisez l’[opérateur de fusion null `??`](../../language-reference/operators/null-coalescing-operator.md) pour spécifier la valeur à affecter si une valeur de type Nullable est null (vous pouvez également utiliser pour cela la méthode <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType>) :
  
[!code-csharp-interactive[?? operator](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#5)]

Utilisez la méthode <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> si la valeur à utiliser quand une valeur de type Nullable est null doit être la valeur par défaut du type valeur sous-jacent.
  
Vous pouvez convertir explicitement un type Nullable en un type non Nullable. Exemple :  
  
[!code-csharp[explicit cast](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#6)]

Au moment de l’exécution, si la valeur d’un type Nullable est null, le cast explicite lève une <xref:System.InvalidOperationException>.

Un type valeur non Nullable est implicitement converti en type Nullable correspondant.
  
## <a name="operators"></a>Opérateurs

Les opérateurs unaire et binaire prédéfinis et tous les opérateurs définis par l’utilisateur existant pour les types valeur peuvent également être utilisés par les types Nullable. Ces opérateurs produisent une valeur null si l’un des opérandes ou les deux sont null ; sinon, l’opérateur utilise les valeurs contenues pour calculer le résultat. Exemple :  
  
[!code-csharp[operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#7)]
  
Pour les opérateurs relationnels (`<`, `>`, `<=`, `>=`), si l’un des opérandes ou les deux sont null, le résultat est `false`. Ne partez pas du principe que parce qu’une comparaison spécifique (par exemple `<=`) retourne `false`, la comparaison opposée (`>`) retourne `true`. L’exemple suivant montre que 10 n’est

- ni supérieur ou égal à null,
- ni inférieur à null.
  
[!code-csharp-interactive[relational and equality operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#8)]
  
L’exemple ci-dessus montre également qu’une comparaison d’égalité de deux types Nullable tous deux null donne la valeur `true`.

## <a name="boxing-and-unboxing"></a>Boxing et unboxing

Un type valeur Nullable est [boxed](../types/boxing-and-unboxing.md) d’après les règles suivantes :

- Si <xref:System.Nullable%601.HasValue%2A> retourne `false`, la référence null est générée.  
- Si <xref:System.Nullable%601.HasValue%2A> retourne `true`, une valeur du type valeur sous-jacent `T` est boxed, pas l’instance de <xref:System.Nullable%601>.

Vous pouvez effectuer l’unboxing du type valeur boxed vers le type Nullable correspondant, comme le montre l’exemple suivant :

[!code-csharp-interactive[boxing and unboxing](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#9)]

## <a name="the-bool-type"></a>Type bool?

Le type Nullable `bool?` peut contenir trois valeurs différentes : [true](../../language-reference/keywords/true-literal.md), [false](../../language-reference/keywords/false-literal.md) et [null](../../language-reference/keywords/null.md). Le type `bool?` est comme le type de variable booléen utilisé dans SQL. Pour vérifier que les résultats produits par les opérateurs `&` et `|` sont cohérents avec le type booléen à trois valeurs dans SQL, les opérateurs prédéfinis suivants sont fournis :

- `bool? operator &(bool? x, bool? y)`  
- `bool? operator |(bool? x, bool? y)`  
  
La sémantique de ces opérateurs est définie par le tableau suivant :  
  
|x|o|x&y|x&#124;y|  
|-------|-------|---------|--------------|  
|true|true|true|true|  
|true|False|false|true|  
|true|null|null|true|  
|False|true|False|true|  
|False|False|False|False|  
|False|null|False|null|  
|null|true|null|true|  
|null|False|False|null|  
|null|null|null|null|  

Notez que ces deux opérateurs ne suivent pas les règles décrites dans la section [Opérateurs](#operators) : le résultat d’une évaluation d’opérateur peut être non null même si l’un des opérandes est null.
  
## <a name="see-also"></a>Voir aussi

- [Types Nullable](index.md)  
- [Guide de programmation C#](../../programming-guide/index.md)  
- [Que signifie réellement « Lifted » ?](https://blogs.msdn.microsoft.com/ericlippert/2007/06/27/what-exactly-does-lifted-mean/)  
