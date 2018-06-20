# utl_select_a_sas_wps_dataset_from_windows_explorer_and_summarize_the_data
Select a sas wps dataset from windows explorer and summarize the data.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Select a SAS/WPS dataset from windows explorer and summarize the data

     Interactive file explorer window

      https://tinyurl.com/y9xwd8c9
      https://github.com/rogerjdeangelis/utl_select_a_sas_wps_dataset_from_windows_explorer_and_summarize_the_data/blob/master/
       utl_select_a_sas_wps_dataset_from_windows_explorer_and_summarize_the_data.png

      see
      https://tinyurl.com/y93knjoh
      https://github.com/rogerjdeangelis/utl_select_a_sas_wps_dataset_from_windows_explorer_and_summarize_the_data


      I tried to use WPS(proc python) but I suspect my python code may not work in Python 3.
      I suspect the same issue with SAS because it does not support 2.7.
      I find Python 2.7 to be much easier to use.


    INPUT
    =====

     * a drectory;

     %let path=d:/sd1

    +-------------------------+
    |  d:/sd1                 |
    +-------------------------+
    |                         |
    |    have.sas7bdat        | * summarize this table
    |                         |
    |    mtacolwps.sas7bdat   |
    |    mtaidxwps.sas7bdat   |
    |    mtatblwps.sas7bdat   |
    |    wantwps.sas7bdat     |
    |        |                |
    |                         |
    +-------------------------+

     SD1.HAVE total obs=19

      NAME       SEX    AGE    HEIGHT    WEIGHT

      Alfred      M      14     69.0      112.5
      Alice       F      13     56.5       84.0
      Barbara     F      13     65.3       98.0
      Carol       F      14     62.8      102.5
      Henry       M      14     63.5      102.5
      James       M      12     57.3       83.0
      Jane        F      12     59.8       84.5
      Janet       F      15     62.5      112.5
      Jeffrey     M      13     62.5       84.0
     ...


    PROCESS
    =======

    %symdel frompy /nowarn;

    %utl_submit_py64("
    import pyperclip;
    from Tkinter import *;
    import clipboard;
    import Tkinter, Tkconstants, tkFileDialog;
    root = Tk();
    root.filename=tkFileDialog.askopenfilename(initialdir='&path',
     title='Select file',filetypes=(('sas files','*.sas7bdat'),('all files','*.*')));
    print (root.filename);
    pyperclip.copy(root.filename);
    ",return=frompy);

    * click on the file with the data you want to summarize;

    proc freq data="&frompy";
    tables sex;
    run;quit;


    OUTPUT
    =====

                                    Cumulative    Cumulative
    SEX    Frequency     Percent     Frequency      Percent
    --------------------------------------------------------
    F             9       47.37             9        47.37
    M            10       52.63            19       100.00


    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    libname sd1 "d:/sd1";
    data sd1.have;
      set sashelp.class;
    run;quit;


    %let path=d:/sd1;

    %put &=path;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_py64('
    import pyperclip;
    import pandas as pd;
    from Tkinter import *;
    import clipboard;
    import Tkinter, Tkconstants, tkFileDialog;
    root = Tk();
    root.filename=tkFileDialog.askopenfilename(initialdir="&path.",title="Select file",filetypes=(("sas files","*.sas7bdat"),("all files","*.*")));
    print (root.filename);
    pyperclip.copy(root.filename);
    ',return=frpmpy);


    proc freq data="&frompy";
    tables sex;
    run;quit;

