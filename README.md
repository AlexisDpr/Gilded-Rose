
Projets : Gilded Rose

Gilded Rose
1. Introduction

Bonjour à toi, et bienvenue pour ce célèbre exercice des Gilded Rose.
Dans les 2 prochains jours tu vas apprendre à déchiffrer du code absolument horrible et tu vas également écrire tes premiers tests unitaires !

Pour ceci tu vas reprendre l'exercice de Gilded Roses, notamment la partie JavaScript - Jasmine
2. Les règles
Spécification de la Rose dorée (Gilded Rose)

Bonjour et bienvenue dans l'équipe de la Rose dorée.

Comme vous le savez, notre petite taverne située à proximité d'une cité importante est dirigée par l'amicale aubergiste Allison.

Nous achetons et vendons uniquement les meilleurs produits.
Malheureusement, la qualité de nos marchandises se dégrade constamment à l'approche de leur date de péremption.

Un système a été mis en place pour mettre à jour notre inventaire.
Il a été développé par Leeroy, une personne pleine de bon sens qui est partie pour de nouvelles aventures.

Votre mission est d'ajouter une nouvelle fonctionnalité à notre système pour que nous puissions commencer à vendre un nouveau type de produit.

Mais d'abord, laissez-moi vous présenter notre système :

    Tous les éléments ont une valeur sellIn qui désigne le nombre de jours restant pour vendre l'article.
    Tous les articles ont une valeur quality qui dénote combien l'article est précieux.
    A la fin de chaque journée, notre système diminue ces deux valeurs pour chaque produit.

Plutôt simple, non ?

Attendez, ça devient intéressant :

    Une fois que la date de péremption est passée, la qualité se dégrade deux fois plus rapidement.
    La qualité (quality) d'un produit ne peut jamais être négative.
    "Aged Brie" augmente sa qualité (quality) plus le temps passe, mais la qualité tombe à 0 après le concert.
    La qualité d'un produit n'est jamais de plus de 50.
    "Sulfuras", étant un objet légendaire, n'a pas de date de péremption et ne perd jamais en qualité (quality)
    "Backstage passes" augmente sa qualité (quality) plus le temps passe (sellIn) : La qualité augmente de 2 quand il reste 10 jours ou moins et de 3 quand il reste 5 jours ou moins, mais la qualité tombe à 0 après le concert (jour 0).

Nous avons récemment signé un partenariat avec un fournisseur de produit invoqué ("Conjured").
Cela nécessite une mise à jour de notre système :

    les éléments "Conjured" voient leur qualité se dégrader deux fois plus vite que les objets normaux.
    "Conjured" est un préfixe au nom des éléments cela signifie que tu dois identifier quels éléments en sont (exemple: "Conjured Dark Blade", "Conjured Magic Stick")

3. Les tests

Tu as pu remarquer qu'un dossier spec était disponible, à quoi peut-il bien servir ?
À l'intérieur, tu trouveras deux fichiers JS, ce nommant texttest_fixture.js et gilded_rose_spec.js. Dans le fichier texttest_fixture.js, tu trouveras un test qui permet de tester si ton programme répond aux attentes des différentes règles :

    La qualité baisse bien de 1
    La qualité augmente bien de 1 pour les items dont c'est le cas
    ...

Pour commencer il te faut déplacer le test présent dans le fichier JS se nommant texttest_fixture.js qui se trouve dans le dossier spec dans ton fichier JS se nommant gilded_rose_spec.js. Le fichier gilded_rose_spec.js devrait donc ressembler à cela :

const {Shop, Item} = require('../src/gilded_rose.js');

describe("Gilded Rose", function() {

  it("full test", () => {
    const items = [
      new Item("+5 Dexterity Vest", 10, 20),
      new Item("Aged Brie", 2, 0),
      new Item("Elixir of the Mongoose", 5, 7),
      new Item("Sulfuras, Hand of Ragnaros", 0, 80),
      new Item("Sulfuras, Hand of Ragnaros", -1, 80),
      new Item("Backstage passes to a TAFKAL80ETC concert", 15, 20),
      new Item("Backstage passes to a TAFKAL80ETC concert", 10, 49),
      new Item("Backstage passes to a TAFKAL80ETC concert", 5, 39),

      // This Conjured item does not work properly yet
      new Item("Conjured Mana Cake", 3, 6),
    ];

    const days = Number(process.argv[2]) || 2;;
    const gildedRose = new Shop(items);

    for (let day = 0; day < days; day++) {
      console.log(`\n-------- day ${day} --------`);
      console.log("name, sellIn, quality");
      items.forEach(item => console.log(`${item.name}, ${item.sellIn}, ${item.quality}`));
      gildedRose.updateQuality();
    }
  });

  it("should foo", function() {
    const gildedRose = new Shop([new Item("foo", 0, 0)]);
    const items = gildedRose.updateQuality();
    expect(items[0].name).toBe("fixme");
  });
});

Comme tu peux le constater, ce test répond à quasiment toutes les règles, mais celui-ci est incomplet pour fonctionner correctement, on te demandera donc de compléter ce "full test" et de créer des tests individuels avec le expect pour chacune des règles dans le fichier JS gilded_rose_spec.js ! Nous avons compté 9 règles qu'il faut tester. Nous te donnons 2 règles à tester, à toi de trouver les restantes :

    Tester si la qualité augmente par 3 quand il reste 5 jours ou moins (Backstage passes)
    Tester si la qualité de Sulfuras ne se modifie pas

Il est préférable d'ajouter plusieurs items pour chaque test afin d'être plus fiable.

Pour lancer la batterie de test, fais un pnpm install à la racine du dossier pour installer les différentes dépendances, puis lance le script pnpm test.
N'hésite surtout pas à rajouter d'autres tests si l'envie t'en prend !
4. Travail attendu

Comme tu peux le voir, la fonction updateQuality est presque incompréhensible, on a donc également besoin de toi (en plus de rajouter les éléments "Conjured") pour rendre tout ce code plus joli !
Tu peux faire les changements que tu veux à la classe Shop et ajouter autant de code que tu veux, tant que tout fonctionne correctement.
Cependant, nous devons te prévenir, tu ne dois modifier en aucun cas la classe Item ou ses propriétés car cette classe appartient au gobelin maléfique et il rentrera dans une rage instantanée et te tuera sans délai : il ne croit pas dans le partage du code.
(Tu peux ajouter une méthode updateQuality et des propriétés statiques dans la classe Item si tu veux, nous te couvrirons).
Pense à bien utiliser les nouveautés ES6 que tu as appris au début de la formation.

Juste une précision, un produit ne peut jamais voir sa qualité augmenter au-dessus de 50, cependant "Sulfuras" est un objet légendaire et comme tel sa qualité est de 80 et il ne change jamais.