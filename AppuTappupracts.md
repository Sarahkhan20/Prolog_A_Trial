Code:- 

            elephant(appu).
            mammal(X):- elephant(X).
            vertebrate(X):- mammal(X).
            herbivore(X):- elephant(X).
            eats(X,grass):-herbivore(X).
            has(X,spinal_cord):-vertebrate(X).
            mascot_of_asian_games(appu).
            elephant(tappu).
            
 Queries:-
 
          has(tappu,spinal_cord).
          
          
          herbivore(Who).
          
          
          eats(appu,What).
          
          
          ertebrate(appu).
