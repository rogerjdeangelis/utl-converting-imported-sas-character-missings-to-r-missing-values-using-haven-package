# utl-converting-imported-sas-character-missings-to-r-missing-values-using-haven-package
    %let pgm=utl-converting-imported-sas-character-missings-to-r-missing-values-using-haven-package;

    %stop_submission;

    Converting imported sas character missings to r missing values using haven package

      CONTENTS

         1 ISSUE
         2 CORRECTION (using dplyr language)


    https://tinyurl.com/5cxkxfz2
    https://github.com/rogerjdeangelis/utl-converting-imported-sas-character-missings-to-r-missing-values-using-haven-package

    /*
    (_)___ ___ _   _  ___
    | / __/ __| | | |/ _ \
    | \__ \__ \ |_| |  __/
    |_|___/___/\__,_|\___|

    */

    /**************************************************************************************************************************/
    /*  PROBLEM: Haven imports sas character missing values as empty charcater string ""                                      */
    /*                                                                                                                        */
    /*  WORKING FIX:  mutate(across(where(is.character), ~na_if(.,"")))  (conver "" to <NA>                                   */
    /*                                                                                                                        */
    /*     INPUT                        |     PROCESS                             |         OUTPUT                            */
    /*     =====                        |     =======                             |         =======                           */
    /*                                  |                                         |                                           */
    /*  CHR    ISMISSING                | 1 ISSUE                                 |  R DOES NOT HONOR SAS MISSING             */
    /*                                  | =======                                 |                                           */
    /*   a         0                    |                                         |         SAS                               */
    /*             1                    | %utl_rbeginx;                           |    CHR  ISMISSING R_MISSING               */
    /*   b         0                    | parmcards4;                             |         ========= =========               */
    /*             1                    | library(haven)                          |  1 "a"      0     FALSE                   */
    /*                                  | library(dplyr)                          |  2 ""       1     FALSE WRONG             */
    /* options validvarname=upcase;     | have<-read_sas("d:/sd1/have.sas7bdat")  |  3 "b"      0     FALSE                   */
    /* libname sd1 "d:/sd1";            | have$R_MISSING<-is.na(have$CHR)         |  4 ""       1     FALSE WRONG             */
    /* data sd1.have ;                  | print(have)                             |                                           */
    /* input  chr $1.;                  | str(have)                               |                                           */
    /* ismissing=missing(chr);          | ;;;;                                    |                                           */
    /* cards4;                          | %utl_rendx;                             |                                           */
    /* a                                |                                         |                                           */
    /* .                                |-------------------------------------------------------------------------------------*/
    /* b                                |                                         |        SAS                                */
    /* .                                | 2 CORRECTION                            |  CHR   ISMISSING R_MISSING                */
    /* ;;;;                             | ============                            |        ========= =========                */
    /* run;quit;                        |                                         |  a         0     FALSE                    */
    /*                                  | %utl_rbeginx;                           |  <NA>      1     TRUE  CORRECTED          */
    /*                                  | parmcards4;                             |  b         0     FALSE                    */
    /*                                  | library(haven)                          |  <NA>      1     TRUE  CORRECTED          */
    /*                                  | library(dplyr)                          |                                           */
    /*                                  | have<-read_sas("d:/sd1/have.sas7bdat")  |                                           */
    /*                                  |   %>% mutate(across(where(is.character) |                                           */
    /*                                  |   ,~na_if(.,"")))                       |                                           */
    /*                                  | have$R_MISSING<-is.na(have$CHR)         |                                           */
    /*                                  | print(have)                             |                                           */
    /*                                  | str(have)                               |                                           */
    /*                                  | ;;;;                                    |                                           */
    /*                                  | %utl_rendx;                             |                                           */
    /****************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
