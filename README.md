# FewRelDe :bow_and_arrow:
A German dataset for few-shot relation extraction.

## Data Source
The English [FewRel dataset](https://thunlp.github.io/1/fewrel1.html) is a benchmark for few-shot relation extraction.
FewRelDe is the German version of a subset from the training and validation set of FewRel.
The bootstrapping process via machine translation was first proposed by Markus Eberts in the master thesis ["Relation Extraction with Attention-Based Transfer Learning"](http://deepca.cs.hs-rm.de/files/deepca/19-thesis-eberts.pdf).
FewRelDe was created for the master thesis "Few-Shot Relation Extraction for German" by Anna Sauer.

## Translation Process
The English instances from FewRel have been automatically translated into German with the help of [DeepL Translator](https://www.deepl.com/translator).
Each translation has been reviewed by hand.

## Relation set
FewRelDe contains a subset of 19 relations from FewRel. Each relation is part of the Wikidata ontology. You can access more information about each relation by clicking on the Wikidata id in the following table:

| Wikidata id                                     | German name                     | English name                        |
|-------------------------------------------------|---------------------------------|-------------------------------------|
| [P6](https://www.wikidata.org/wiki/Property:P6) | Leiter:in der Regierung         | head of government                  | 
| [P22](https://www.wikidata.org/wiki/Property:P22) | Vater                           | father                              |
| [P25](https://www.wikidata.org/wiki/Property:P25) | Mutter                          | mother                              |
| [P26](https://www.wikidata.org/wiki/Property:P26) | Ehepartner:in                   | spouse                              |
| [P27](https://www.wikidata.org/wiki/Property:P27) | Land der Staatsangehörigkeit    | country of citizenship              |
| [P84](https://www.wikidata.org/wiki/Property:P84) | Architekt:in                    | architect                           |
| [P102](https://www.wikidata.org/wiki/Property:P102) | Parteizugehörigkeit             | member of political party           |
| [P118](https://www.wikidata.org/wiki/Property:P118) | Liga                            | league                              |
| [P177](https://www.wikidata.org/wiki/Property:P177) | Querung                         | crosses                             |
| [P206](https://www.wikidata.org/wiki/Property:P206) | liegt am or im Gewässer         | located in or next to body of water |
| [P466](https://www.wikidata.org/wiki/Property:P466) | Bewohner:in, Nutzer:in          | occupant                            |
| [P551](https://www.wikidata.org/wiki/Property:P551) | Wohnsitz                        | residence                           |
| [P740](https://www.wikidata.org/wiki/Property:P740) | Gründungsort                    | location of formation               |
| [P931](https://www.wikidata.org/wiki/Property:P931) | vom Verkehrsknotenpunkt bedient | place served by transport hub       |
| [P937](https://www.wikidata.org/wiki/Property:P937) | Wirkungsort                     | work location                       |
| [P974](https://www.wikidata.org/wiki/Property:P974) | Nebenfluss                      | tributary                           |
| [P1408](https://www.wikidata.org/wiki/Property:P1408) | Sendelizenz in                  | licensed to broadcast to            |
| [P3373](https://www.wikidata.org/wiki/Property:P3373) | Geschwister                     | sibling                             |
| [P4552](https://www.wikidata.org/wiki/Property:P4552) | Gebirgszug                      | mountain range                      |

FewRelDe also contains an OTHER relation for negative instances that do not belong to any of the other 19 relations. These negative instances were randomly selected from the remaining FewRel training and validation relations.

Each of the 20 relations in FewRelDe has 50 instances.
The total of labeled relation instances thus amounts to 1,000.


## Dataset Format
The format of the JSON file is modeled after the data format of the [FewRel benchmark](https://thunlp.github.io/1/fewrel1.html) for few-shot relation extraction.
Each file contains a dictionary whose keys are the names of the relations in the dataset.
For each relation key, the corresponding value is a list of the labeled instances of that relation.
This list contains a dictionary for each individual instance with
* "tokens": a list with the token string sequence in the sentence
* "h": information on the head entity in a list with
  * a string with the entity mention in lower case
  * a string with the Wikidata id of the entity (cf. wikidata.org). In WissenschaftsSTANDARD, this string is left empty because no entity linking between the head and tail entity and their Wikidata equivalent is performed.
  * a list with a nested list that contains the indices of the entity mention tokens in the sentence
* "t": information on the tail entity in a list with the same structure as "h"
* "ner": a list with information obtained from the task of named entity recognition (NER). The list contains the BIOES entity type tag for each token in the sentence. The BIOES tagging has been created using the German NER model in [Stanza](https://github.com/stanfordnlp/stanza) with the CoNLL 2003 tag set. This tag set contains the entity types PER (person), ORG (organisation) and LOC (location) (cf. https://stanfordnlp.github.io/stanza/available_models.html#available-ner-models).

Consider the following made-up example:
```json
{
  "tokens": ["Robin", "Hood", "lebt", "in", "Sherwood", "Forest", "."],
  "h": ["sherwood forest", "", [[4, 5]]],
  "t": ["robin hood", "", [[0, 1]]],
  "ner": ["B-PER", "E-PER", "O", "O", "B-PER", "E-PER", "O"]
}
```

## License
FewRel has been released under a [Creative Commons BY-SA 4.0 license](http://creativecommons.org/licenses/by-sa/4.0) (cf. https://thunlp.github.io/1/fewrel1.html).
Therefore, FewRelDe is also released under a [Creative Commons BY-SA 4.0 license](http://creativecommons.org/licenses/by-sa/4.0).
