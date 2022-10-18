# double-chess960-fairness
Analysis of engine evaluations of randomized chess starting positions and how to improve fairness. Some positions are already winning/losing for White.
Analysis for an [answer on StackExchange][6].

**Summary of results regarding DFRC fairness:**
=================================================================

If White's position is randomly assigned and Black is allowed to adapt his battle line-up to counter White's attack, **Black is almost always better, even though White gets the first move advantage.**
The markedness was very surprising, see the **centipawn evaluation summary statistics** for yourself: 

 - **mean**:    -109 
 - **min** :    -243
 - **25%**  :   -139 
 - **50%**   :  -110 
 - **75%**    : -77 
 - **max**     : 23

On average, Black can get an advantage of -1. If White is fortunate, he can get one of two positions, where he has a guaranteed first-move advantage comparable to standard chess, no matter Black's setup (about 20 centipawns).
In the worst case, White is losing from the start. 
The harmonious-looking standard chess setup isn't very robust for White. Black has multiple setups that give him an advantage of about -100 centipawns, e.g. [this one][3]:

       [FEN "bbnrqkrn/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"]

For seeing more examples and the best and worst setups, [check the analysis][1]. 

**The best setup for White**, i.e. most robust w.r.t. Black's possibilities is [the following][4]:

     [FEN "bbrqnnkr/pppppppp/8/8/8/8/PPPPPPPP/BQRBNNKR w KQkq - 0 1"]

The only other setup where White has a guaranteed first-move advantage is this very setup, mirrored. There seems to be something particularly good about this piece coordination for White (even though the castling would differ). If Black isn't careful with his setup, he can quickly find himself losing from the start (337 centipawns). Interestingly, the engine likes 1. a4 as an opening (more on best opening moves later).

**I further investigated, how large the advantage for White would be if both sides can influence the setups:** 

1) White advantage when Black decides on White's setup first and White decides on Black's setup: White always has a sizeable advantage
2) White advantage when White decides on Black's setup first and Black decides on Whites's setup: Black almost always has an advantage (the first move advantage helps White to not always be worse)

Therefore, it is beneficial to have the last word, even if the opponent can try to mess up your own position however they like. There are no setups that are so bad that the opponent couldn't find a setup for you that is pretty bad against what he chose for you.

Furthermore, I analyzed the **importance of undefended pawns in the starting position** on its fairness. At first glance, it doesn't seem to have a large impact on the evaluations, even if only one side had weaknesses.
If that was the case, however, it had an impact on the best opening moves for White.

**Best opening moves for White**

> Seize the centah! (*IM Andras Toth*)

It's comforting to see, that the opening principles still generally apply. The most frequent best moves: 

**Chess960** : number of occurrences (number of occurrences if neither side has weaknesses):

 - **e4**   :    168 (89)
 - **d4**   :    149 (77)
 - **f4**    :   132 (43)
 - **c4**     :  121 (48)

**Double Fischer Random** : number of occurrences (number of occurrences if neither side has weaknesses)

 - **e4**   :    117246 (23491)
 - **f4**    :   115029 (16425)
 - **d4**   :    102330 (20973)
 - **b3**     :  92310 (9288)
 - **g3**   :    90390 (8734)
 - **c4**     :  88084 (13381)
 
**Double Fischer Random** : number of occurrences, only Black has weaknesses

 - **e4**   :    32346
 - **f4**    :   27672
 - **d4**   :    27415
 - **c4**     :  22421


**Double Fischer Random**: number of occurrences, only White has weaknesses

 - **f4**   :    27931
 - **b4**    :   26486
 - **g3**   :    25791
 - **e4**     :  24821
 - **d4**   :    22836
 - **c4**     :  20522

**e4 is generally the best first move for White** (just like in regular chess). Most often, the best first move is to control the center with a pawn (at least from the side). 
The pawn that is the best one to move depends on its impact on piece development. If neither side has weaknesses, the ranking of best first moves is e4, d4, f4, and c4. 
If the own position has weaknesses, it seems we need to be more careful in the opening, with modest moves such as b3 and g3 being good (probably activating a bishop or queen) and controlling the center with pieces. 


**Limitations:**
All of the analysis is based on the [data provided by TCEC][5] with engine evaluations of depth 20. The evaluations can change with increasing depth.
Some of the evaluations differ from those on my local machine. The evaluations are also dependent on engine configuration.
The general findings should however be valid.

  [1]: https://github.com/Arminius4/double-chess960-fairness/blob/main/Fairness%20analysis%20of%20Double%20Chess960%20(DFRC).ipynb
  [2]: https://nbbqrnkr/pppppppp/8/8/8/8/PPPPPPPP/BQRNNKRB%20w%20KQkq%20-%200%201
  [3]: https://lichess.org/analysis/standard/bbnrqkrn/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR_w_KQkq_-_0_1#0
  [4]: https://lichess.org/analysis/standard/bbrqnnkr/pppppppp/8/8/8/8/PPPPPPPP/BQRBNNKR
  [5]: https://tcec-chess.com/misc/dfrc/DFRC_depth20.csv.xz
  [6]: https://chess.stackexchange.com/questions/40800/chess960-can-black-profit-by-being-allowed-to-choose-a-custom-setup/
