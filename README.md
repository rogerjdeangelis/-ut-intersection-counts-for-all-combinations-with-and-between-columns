# utl-intersection-counts-for-all-combinations-with-and-between-columns
Intersection counts for all combinations with and between columns
    %let pgm=ut-intersection-counts-for-all-combinations-with-and-between-columns;

    Intersection counts for all combinations with and between columns

    github                                                                                                  
    https://tinyurl.com/2rwbjarc                                                                            
    https://github.com/rogerjdeangelis/utl-intersection-counts-for-all-combinations-with-and-between-columns

    related repos
    https://github.com/rogerjdeangelis/utl-how-to-find-intersection-between-all-possible-pairs-of-sets-in-a-two-column-table
    https://github.com/rogerjdeangelis/utl-intersection-key-counts-for-n-tables-five-table-example
    https://github.com/rogerjdeangelis/utl-intersection-of-words-in-two-lists
    https://github.com/rogerjdeangelis/utl_how_to_find_the_union_and_intersection_of_words_in_two_strings_nlp

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */
    /**************************************************************************************************************************/
    /*                          |                                         |                                                   */
    /*       INPUT              |       PROCESS ^ means intersect         |        OUTPUT                                     */
    /*                          |                                         |                                                   */
    /* Up to 40 obs WORK.HAVE   | VAR  NA1          NA2        NA3        | VAR  NA1   NA2   NA3                              */
    /*                          |                                         |                                                   */
    /*  A1   A2   A3            |  A1    7  A1^A1=7 3 A1^A2=3   3         |  A1    7     3     3                              */
    /*   1    .    .            |  A2    3          4           1         |  A2    3     4     1                              */
    /*   1    1    .            |  A3    3          1           4         |  A3    3     1     4                              */
    /*   1    .    1            |                                         |                                                   */
    /*   .    1    1            |  A1^A1 A1 A1   A1^A2 A1   A2            |                                                   */
    /*   1    1    .            |                                         |                                                   */
    /*   1    1    .            |         1  1          1    .            |                                                   */
    /*   1    .    1            |         1  1          1    1  x         |                                                   */
    /*   1    .    1            |         1  1          1    .            |                                                   */
    /*                          |         .  .          .    1            |                                                   */
    /*                          |         1  1          1    1  x         |                                                   */
    /*                          |         1  1          1    1  x         |                                                   */
    /*                          |         1  1          1    .            |                                                   */
    /*                          |         1  1          1    .            |                                                   */
    /*                          |                                         |                                                   */
    /*                          |   7 intersections    3 intersections    |                                                   */
    /*                          |                                         |                                                   */
    /*                          |  ods output pearsoncorr=                |                                                   */
    /*                          |    want(rename=variable=var             |                                                   */
    /*                          |     keep=variable n:) ;                 |                                                   */
    /*                          |  proc corr data=have ;                  |                                                   */
    /*                          |  var _numeric_;                         |                                                   */
    /*                          |  with _numeric_;                        |                                                   */
    /*                          |  run;quit;                              |                                                   */
    /*                          |                                         |                                                   */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    options validvarname=upcase;
    data have;
    input a1 a2 a3;
    cards4;
     1 . .
     1 1 .
     1 . 1
     . 1 1
     1 1 .
     1 1 .
     1 . 1
     1 . 1
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Up to 40 obs WORK.HAVE total obs=8                                                                                    */
    /*                                                                                                                        */
    /*  Obs    A1   A2   A3                                                                                                   */
    /*                                                                                                                        */
    /*   1      1    .    .                                                                                                   */
    /*   2      1    1    .                                                                                                   */
    /*   3      1    .    1                                                                                                   */
    /*   4      .    1    1                                                                                                   */
    /*   5      1    1    .                                                                                                   */
    /*   6      1    1    .                                                                                                   */
    /*   7      1    .    1                                                                                                   */
    /*   8      1    .    1                                                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    ods output pearsoncorr=
      want(rename=variable=var
       keep=variable n:) ;
    proc corr data=have ;
      var _numeric_;
      with _numeric_;
    run;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* WANT total obs=3                                                                                                       */
    /*                                                                                                                        */
    /*  VAR    N A1    NA2    NA3                                                                                             */
    /*                                                                                                                        */
    /*  A1      7      3      3                                                                                               */
    /*  A2      3      4      1                                                                                               */
    /*  A3      3      1      4                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
