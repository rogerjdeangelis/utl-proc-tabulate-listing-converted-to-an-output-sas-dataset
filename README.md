# utl-proc-tabulate-listing-converted-to-an-output-sas-dataset
Proc Tabulate listing converted to an output sas dataset
    Proc Tabulate listing converted to an output sas dataset

    GitHub
    https://tinyurl.com/837se86e
    https://github.com/rogerjdeangelis/utl-proc-tabulate-listing-converted-to-an-output-sas-dataset


    * other ways to get a table from Report, Freq and Tabulate;
    https://github.com/rogerjdeangelis?tab=repositories&q=output+table+&type=&language=

    *                _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | '_ \| '__/ _ \| '_ \| |/ _ \ '_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    ;

    I want a SAS table that has the structure of tabulate output


     |Married|stats|Girl_momWgt|Girl_babyWgt|Boy_momWgt|Boy_babyWgt|

    ----------------------------------------------------------------------------------
    |                            |                     Baby Boy                      |
    |                            |---------------------------------------------------|
    |                            |            0            |            1            |
    |                            |-------------------------+-------------------------|
    |                            |  Mother's  |            |  Mother's  |            |
    |                            | Pregnancy  |Infant Birth| Pregnancy  |Infant Birth|
    |                            |Weight Gain |   Weight   |Weight Gain |   Weight   |
    |----------------------------+------------+------------+------------+------------|
    |Married Mother   |          |            |            |            |            |
    |-----------------+----------|            |            |            |            |
    |0                |Min       |      -30.00|      369.00|      -30.00|      284.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |P10       |      -17.00|     2551.00|      -16.00|     2636.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |Mean      |        0.39|     3178.52|        1.07|     3287.93|
    |                 |----------+------------+------------+------------+------------|
    |                 |P90       |       20.00|     3827.00|       20.00|     3969.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |Max       |       68.00|     6350.00|       68.00|     5330.00|
    |-----------------+----------+------------+------------+------------+------------|
    |1                |Min       |      -30.00|      240.00|      -30.00|      284.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |P10       |      -15.00|     2765.00|      -14.00|     2835.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |Mean      |        0.32|     3364.57|        1.05|     3482.69|
    |                 |----------+------------+------------+------------+------------|
    |                 |P90       |       15.00|     3985.00|       16.00|     4139.00|
    |                 |----------+------------+------------+------------+------------|
    |                 |Max       |       68.00|     5409.00|       68.00|     5970.00|
    ----------------------------------------------------------------------------------

    *                    _
    __      ____ _ _ __ | |_
    \ \ /\ / / _` | '_ \| __|
     \ V  V / (_| | | | | |_
      \_/\_/ \__,_|_| |_|\__|

    ;


    WORK.HAVMAP total obs=10

                                GIRL_     GIRL_      BOY_       BOY_
    Obs    MARRIED    STATS    MOMWGT    BABYWGT    MOMWGT    BABYWGT

      1       0       Min      -30.00     369.00    -30.00     284.00
      2       .       P10      -17.00    2551.00    -16.00    2636.00
      3       .       Mean       0.39    3178.52      1.07    3287.93
      4       .       P90       20.00    3827.00     20.00    3969.00
      5       .       Max       68.00    6350.00     68.00    5330.00
      6       1       Min      -30.00     240.00    -30.00     284.00
      7       .       P10      -15.00    2765.00    -14.00    2835.00
      8       .       Mean       0.32    3364.57      1.05    3482.69
      9       .       P90       15.00    3985.00     16.00    4139.00
     10       .       Max       68.00    5409.00     68.00    5970.00


     *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    options FORMCHAR='|----|+|---+=|-/\<>*';

    proc tabulate data=sashelp.bweight;
      title "|Married|stats|Girl_momWgt|Girl_babyWgt|Boy_momWgt|Boy_babyWgt|";
      class Married MomEdLevel Boy;
      var MomWtGain Weight;
      table Married  * (min p10 mean p90 max) , Boy * (MomWtGain Weight);
    run;

    * see problem;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    * macro on end or in Github;

    * incase you make changes to macro on end;
    %inc "c:/oto/utl_odstab.sas";

    proc datasets lib=work nolist;
       delete havMap;
    run;quit;

    %utl_odstab(setup);

    proc tabulate data=sashelp.bweight;

      * the title provides the column headings;

      title "|Married|stats|Girl_momWgt|Girl_babyWgt|Boy_momWgt|Boy_babyWgt|";
      class Married MomEdLevel Boy;
      var MomWtGain Weight;
      table Married  * (min p10 mean p90 max) , Boy * (MomWtGain Weight);

    run;quit;

    %utl_odstab(outdsn=havMap,datarow=7);

    * restore formchar;
    options FORMCHAR='|----|+|---+=|-/\<>*';

    * to get the data row value of 7
    * count the  number of lines to the first row of data in the input and diveid by 2

     1    |Married|stats|Girl_momWgt|Girl_babyWgt|Boy_momWgt|Boy_babyWgt|
     2
     3   ------------------------------
     4   |                            |
     5   |                            |
     6   |                            |
     7   |                            |
     8   |                            |
     9   |                            |
     10  |                            |
     11  |----------------------------+
     12  |Married Mother   |          |
     13  |-----------------+----------|
     14  |0                |Min       |  * data row


    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WORK.HAVMAP total obs=10

                                GIRL_     GIRL_      BOY_       BOY_
    Obs    MARRIED    STATS    MOMWGT    BABYWGT    MOMWGT    BABYWGT

      1       0       Min      -30.00     369.00    -30.00     284.00
      2       .       P10      -17.00    2551.00    -16.00    2636.00
      3       .       Mean       0.39    3178.52      1.07    3287.93
      4       .       P90       20.00    3827.00     20.00    3969.00
      5       .       Max       68.00    6350.00     68.00    5330.00
      6       1       Min      -30.00     240.00    -30.00     284.00
      7       .       P10      -15.00    2765.00    -14.00    2835.00
      8       .       Mean       0.32    3364.57      1.05    3482.69
      9       .       P90       15.00    3985.00     16.00    4139.00
     10       .       Max       68.00    5409.00     68.00    5970.00

    *
     _ __ ___   __ _  ___ _ __ ___
    | '_ ` _ \ / _` |/ __| '__/ _ \
    | | | | | | (_| | (__| | | (_) |
    |_| |_| |_|\__,_|\___|_|  \___/

    ;

    %macro utl_odstab(outdsn,datarow=1);

       %if %qupcase(&outdsn)=SETUP %then %do;

            filename _tmp1_ clear;  * just in case;

            %utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);

            filename _tmp1_ "%sysfunc(pathname(work))/_tmp1_.txt";

            %let _ps_= %sysfunc(getoption(ps));
            %let _fc_= %sysfunc(getoption(formchar));

            OPTIONS ls=max ps=32756  FORMCHAR='|'  nodate nocenter;

            title; footnote;

            proc printto print=_tmp1_;
            run;quit;

       %end;
       %else %do;

            /* %let outdsn=tst; %let datarow=3; */

            proc printto;
            run;quit;

            %utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

            *filename _tmp2_  "%sysfunc(pathname(work))/_tmp2_.txt";

            proc datasets lib=work nolist;  *just in case;
             delete &outdsn;
            run;quit;

            proc printto print="%sysfunc(pathname(work))/_tmp2_.txt";
            run;quit;

            data _null_;
              retain n 0;
              infile _tmp1_ length=l;
              input lyn $varying32756. l;
              if _n_=1 then do;
                  file print titles;
                  putlog lyn;
                  *put lyn;
              end;
              else do;
                 if countc(lyn,'|')>2;
                 n=n+1;
                 if n ge %eval(&datarow + 1) then do;
                    file print;
                    putlog lyn;
                    put lyn;
                 end;
              end;
            run;quit;

            proc printto;
            run;quit;

            proc import
               datafile="%sysfunc(pathname(work))/_tmp2_.txt"
               dbms=dlm
               out=&outdsn(drop=var:)
               replace;
               delimiter='|';
               getnames=yes;
            run;quit;

            filename _tmp1_ clear;
            filename _tmp2_ clear;

            %utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);
            %utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

       %end;

    %mend utl_odstab;
