# Prolog_A_Trial

### Prolog Syntax I Tried. (Basics)
 
 PROLOG is a Declarative Programming Language. Here, "LOGIC" is shown in the form of *facts* and *rules*. It is used for solving Queries about relationships in any given data.
 
Declarative statements are called Facts. These Facts are basically knowledge or Factbase of the system. We run Queries againsta the knowledge of this system. You will find the Queries and knowledge base quite similar to SQL or Databases and will perform something like this.
Let us Get into the Hands-on PROLOG (A Trial). And oh btw, it's fun not something you usually do in programming. So yeah kinda you can see it as a Break from usual Routine.

Before we Start,

Lemme Answer This:   Where can we write PROLOG?

1. You can Download GNU PROLOG from [here](http://www.gprolog.org/) according to your requirements. OR
2. Online Compiler like [Click me!](https://swish.swi-prolog.org/)

I used Online Compiler. Downloading and installing will properly make you use semicolons and write queries from strach I felt cause I tried it in College Lab-session.

  *Also One More Thing I ain't Teaching anyone here So this won't we me explaining sytax. I feel that comes naturally with observing and practice.*
  
So Let's Get Started,

        sisters(sarah,mary). /*sarah and mary are sisters*/
        singer(sarah). /*sarah is a singer */
        
 Asking Query
        
        ?- singer(sarah).
    
  Output would be True, Now Here you can Try out creative stuffs like,
   
        ?-singer(mary).
  
  Output would obviously ("LOGICALLY") be False. How experimental you can be while writing Queries I leave upto you.
  Cause It won't blast you computer or blow out your chemistry lab, So you can try and learn. We will move with other things forward.
  One thing I would like y'all to try 
        
        ?-sisters(mary,sarah).
        
  What output did you see ? **False**. Hmm...Although Mary and Sarah are sister but your knowledgebase knows that sarah is mary's sister and it cannot implies the converse to be true.
  Thus, Order of Evaluation in PROLOG goes from left to right.
    Now what I meant by not explainging syntax was, here for instance we used,
    
  1.Smallcase letters for denoting names of objects and relations.
  2.We separated objects by commas. 
  3.Ended with Fullstop. 
 
 #### Facts
 
     funny(Chandler).
     playful(Chandler).
  
 #### Rules
 
     not_boring(X):- funny(X),playful(X).
  
  Meaning, For All X, (variable in capital) X is not_boring if X is funny and playful.
  
  Now if you add,
    
    
       funny(man).
       funny(joey).
       playful(man).
       playful(joey).
       
  Ask A Query,
     
      ?- not_boring(X).
  
  There are two answers, in GNU compiler you need to put ; to see the other output until it becomes false.
  You will also Notice that man comes before joey since it was declared first.
  
  #### Unification
  
      eats(joey,pizza).
      
   How to Ask Compiler what joey eats
   
      ?- eats(joey,What). 
      
   Note, what isn't an object it's a variable and variable always starts which Capital letter.
     
 Now think how you will write this and query.
 
   * Men like joking.
   * Chandler is a men.
   
   And ask, 'Who likes joking'.
     
 I wrote it this way after trial and error(Got it right finally), if you find a better approach do lemme know !
    
      men(chandler).
      joking(X):- men(X).
      
  Query:
      
      ?- joking(X).
   This is called **Resolution**, basically here you are inferring from one statement to others.
   
   * If it is a nice day Sarah smiles
   * if Sarah smiles she is happy.
  
  Can be written as,
  
  Before coming to lists,
  let's try this interesting PROLOG Arithmetics. (Queries)
  
      ?- X= 2+4.
       
  Oops! You were expecting 6 right!?
  Well in PROLOG, we write.
  
      ? - X is 2+4.
      
   Congratulations ! You got 2+4 as 6 !
   
 Now, There are many arithmetic operations you can try, search on google 'Arithmetic operators in PROLOG' and you'll get tutorials point or some other websites answer popping.
 
 #### Define a Predicate
 
     add_5_and_triple(X,Y):- Y is (X+5) * 3.
     
   Query,
     
     ?- add_5_and_triple(1,X).
     
   Try,
    
    ?- add_5_and_triple(X,12).
    
  Error? Cause You cannot assign a constant to Y and make it calculate an unknown variable of X.
  
  #### Infix Operators (Special kind of relational Operators).
   ##### Equality and Inequality
         
          ?- 6+6=:=6*3-6.
          
          ?- sqrt(36)+14=:=5*11-35.
   Ineqality operator is donated by (=\=)
      
          ?- 15=\=7+3.
 #### Identical and Non-Identical Terms
 
         ?- eats(joey, pizza)==eats(joey,pizza).
         
         ?- eats(joey, pizza)==eats(chandler,pizza).
         
         ?- X is 25, val(X) == val(25).
         
   Non-Identical Terms are written as (\==)
        
        ?- eats(joey, pizza)\==eats(chandler,pizza).
        
  Try out different operators, it's fun.
  Now while looking at Execution Order of PROLOG it is similar as BODMAS. So no special rules here
    
Till now of This Tut, we haven't came accross terminology 'backward chaining', but we have already experienced it. Prolog was designed keeping backward chaining in mind for Clausal Execution to understand better.
         
  #### Imperitive Control Flow-Cut.
  Director says, CUT! yeah something similar here too. But make sure this is used carefully by only understanding what will Cut Do and not just experimenting and playing around.
  
        teaches(kumkum,stacks).
        teaches(kumkum,queues).
        teaches(kumkum,hashing).
        teaches(suneeta,sorting).

        studies(sarah,queues).
        studies(altaf,queues).
        studies(anas,hashing).
        studies(ninad,sorting).
        
   Query,
        
        ?- teaches(kumkum,Course), studies(Student,Course).
        
   Backtracking is not stopped in any way, shape or form over here.
   Course is in beginning bound to *Stacks* in the first fact, but there aren't any students so backtracking takes place and Course get bounds to *queues*, and next goal is tried and 2 answers are found. Here, suneeta and ninad are ignored by the way because the query makes it clear that only kumkum's courses are to be checked.
   Let's try with Cut,
   
       ?- teaches(kumkum,Course),!,studies(Student,Course).
       
  This time the course was bound to stacks, then the cut is executed and then  studies goal is tried and fails cause according to database noone studies stacks. Because of cut, we cannot backtrack to the teaches goal, so the whole query fails and returs False.Similarly, Try this and infer
  
       ?- teaches(kumkum,Course),studies(Student,Course),!.
       
  Here, the teaches goal is  tried as usual, and *Course* is bound to *stacks* as usual. Next the *studies* goal is tried and *fails* ( very ironic lol) so we don't get to the cut at the end of the query at this point, and backtracking can occur.
  Thus, the teached goal is re-tried, and *Course* is bound to *queues*. Then the studies goal is re-tried, and *succeeds*. After that cut is executed so no backtracking.
  
       ?- !, teaches(kumkum,Course),studies(Student,Course).
       
  Acts as if no *cut* was present. Because it is never necessary to backtrack past the cut to find the next solution, so backtracking is never inhibited.
  
       
  
      
     
