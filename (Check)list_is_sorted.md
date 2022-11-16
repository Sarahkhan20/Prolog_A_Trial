/*To check if the elements in the list is sorted or not*/
/*recursive function*/

          is_sorted([]). /* Empty list*/
          is_sorted([_]). /* 1 element in a list*/
          is_sorted([X,Y|T]):-X=<Y,is_sorted([Y|T]).
       
QUERY:-
          
          ?- is_sorted([2,5,4,7]).

