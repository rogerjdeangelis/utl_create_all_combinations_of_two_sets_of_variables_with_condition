# utl_create_all_combinations_of_two_sets_of_variables_with_condition
Create all combinations of two sets of variables with condition. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Create all combinations of two sets of variables with condition

    Same result in SAS and WPS

    github
    https://tinyurl.com/y9vmq4ov
    https://github.com/rogerjdeangelis/utl_create_all_combinations_of_two_sets_of_variables_with_condition

    https://tinyurl.com/yaz8hpt8
    https://communities.sas.com/t5/SAS-Data-Management/How-to-count-the-number-of-each-combination-of-two-check-all/m-p/470698

    Novinosrin profile
    https://communities.sas.com/t5/user/viewprofilepage/user-id/138205


    INPUT

    WORK.HAVE total obs=3                        |  RULES  (All Combinations where A#=1 and B#=1)
                                                 |
      A1    A2    A3      B1    B2    B3    B4   |     A     B
                                                 |
       1     1     0       0     0     1     1   |    A1    B3
                                                 |    A1    B4
                                                 |    A2    B3
                                                 |    A2    B4
       0     1     1       0     0     1     0   |
       0     0     1       1     0     0     1   |

    EXAMPLE OUTPUT

     WORK.WANT total obs=8

      A     B

      A1    B3
      A1    B4

      A2    B3
      A2    B4

      A2    B3
      A3    B3
      A3    B1
      A3    B4


    PROCESS
    =======

    * compare all combinations of As with Bs and in the sum of A+B=1 then output;

    data want;
      retain A B;
      set have;
      array ab[*] a1--b4;
      do i=1 to dim(ab)-1;
         A=vname(ab[i]);
         do j=i+1 to dim(ab);
           B=vname(ab[j]);
           if first(vname(ab[i])) ne first(vname(ab[j])) and
              ab[i]+ab[j]=2 then output;
         end;
      end;
    keep A B;
    run;quit;


    OUTPUT
    ======

     WORK.WANT total obs=8

       A     B

       A1    B3
       A1    B4
       A2    B3
       A2    B4
       A2    B3
       A3    B3
       A3    B1
       A3    B4

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;
    data have;
       input A1-A3 B1-B4 $;
    datalines;
    1 1 0 0 0 1 1
    0 1 1 0 0 1 0
    0 0 1 1 0 0 1
    ;
    run;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    data wantwps;
      retain A B;
      set wrk.have;
      array ab[*] a1--b4;
      do i=1 to dim(ab)-1;
         A=vname(ab[i]);
         do j=i+1 to dim(ab);
           B=vname(ab[j]);
           if first(vname(ab[i])) ne first(vname(ab[j])) and
              ab[i]+ab[j]=2 then output;
         end;
      end;
    keep A B;
    run;quit;
    proc print;
    run;quit;
    ');

