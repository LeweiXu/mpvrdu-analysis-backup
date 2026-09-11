## Turn 1 — document page 13 (rank 1 of 20)

Table 8: Filtering statistics of the entity dataset. [1st Wiki filtering]: removing ones without wiki page. [2nd Google filtering]: removing ones without enough images via google search API. [3rd Wiki filtering]: removing entity name with ambiguous wiki pages.

| Main category | Original Entity | 1st Wiki filtering | 2nd Google filtering | 3rd Wiki filtering |
|---------------|-----------------|--------------------|----------------------|--------------------|
| landmark      | 1595            | 1000               | 899                  | 753                |
| painting      | 1057            | 367                | 358                  | 288                |
| sculpture     | 300             | 164                | 164                  | 134                |
| food          | 883             | 338                | 337                  | 271                |
| fruit         | 361             | 236                | 233                  | 180                |
| vegetable     | 389             | 290                | 286                  | 214                |
| mammal        | 778             | 633                | 619                  | 434                |
| hibian        | 211             | 148                | 139                  | 124                |
| insect        | 366             | 179                | 176                  | 145                |
| fish          | 1089            | 1054               | 987                  | 722                |
| bird          | 739             | 546                | 545                  | 480                |
| reptile       | 279             | 232                | 231                  | 210                |
| celebrity     | 1514            | 1484               | 1466                 | 732                |
| instrument    | 477             | 375                | 368                  | 277                |
| plant         | 606             | 601                | 593                  | 489                |
| electronics   | 432             | 354                | 342                  | 269                |
| tool          | 801             | 213                | 209                  | 150                |
| transportation| 334             | 296                | 290                  | 227                |
| sport         | 694             | 478                | 464                  | 395                |
| book          | 1030            | 826                | 777                  | 645                |
| household     | 475             | 319                | 299                  | 221                |
| car           | 500             | 320                | 320                  | 208                |
| Summary       | 22              | 14910              | 10453                | 10102              |
|               |                 |                    |                      | 7568               |

Figure 6: Collecting images for building the evaluation dataset. Licenses: CC Publicdomain, CC Attribute, AA Sharealike, CC Noncommercial, or CC Nonderived licenses. Metadata: image URLs, source page URLs, renamed image names, and the corresponding Wikipedia page URL.

Knowledge retrieval via multi-source aggregation.

Semantic Region Extraction via Language-Guided Object Detection Due to the presence of entities within the image that occupy only a portion of the available space, employing a comprehensive image-level entity recognition approach may lead to a decrease in recognition performance. Instead, we opt to initially extract the image region containing the entity and utilize this specific region in subsequent recognition processes to enhance accuracy. During this phase, we leverage a language-guided object detection model, i.e., GLIP (Li et al., 2021), to extract meaningful regions from complex images. This approach helps precisely identify and extract image regions directly relevant to specific textual queries. It accomplishes this by understanding the context of the query and adjusting its object detection method to find the most

## Turn 2 — document page 3 (rank 2 of 20)

The current page confirms the total number of entities after the 3rd Wiki filtering is 7,568. It also states that the initial list contained 14,910 diverse entities. The page details the filtering process: first, entities without valid Wikipedia pages were removed (1st Wiki filtering), then those without sufficient images via Google Image Search were removed (2nd Google filtering), and finally, entities with ambiguous wiki pages were removed (3rd Wiki filtering). The final count after all filtering is explicitly stated as 7,568.

## Turn 3 — document page 12 (rank 3 of 20)

This page contains Figure 5, which illustrates the information collected from Wikipedia for each entity during dataset building (general introduction, toponym, location, etc.). It also references Table 8 for filtering details and introduces the dataset's question types and model methodology. However, it does not contain any new numerical data or direct information about the number of entities filtered out in the 1st or 3rd Wiki filtering steps. The page only reiterates that filtering details are in Table 8.

## Turn 4 — document page 11 (rank 4 of 20)

none

## Turn 5 — document page 10 (rank 5 of 20)

none

## Turn 6 — document page 4 (rank 6 of 20)

none
