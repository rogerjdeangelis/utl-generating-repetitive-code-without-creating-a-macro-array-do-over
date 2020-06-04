# utl-generating-repetitive-code-without-creating-a-macro-array-do-over
Generating repetitive code without creating a macro array do over 
    Generating repetitive code without creating a macro array do over                                                    
                                                                                                                         
    The op wants to be able to create just the code or generate the code inside a datastep                               
                                                                                                                         
        Two Solutions                                                                                                    
                                                                                                                         
           a  array and do_over                                                                                          
           b. generated the statements in the log then cut and paste from the log                                        
                                                                                                                         
    github                                                                                                               
    https://tinyurl.com/ybohe6vp                                                                                         
    https://github.com/rogerjdeangelis/utl-generating-repetitive-code-without-creating-a-macro-array-do-over             
                                                                                                                         
    SAS Forum                                                                                                            
    https://tinyurl.com/ybqxv67f                                                                                         
    https://communities.sas.com/t5/SAS-Programming/Shortcut-for-variable-names/m-p/653359                                
                                                                                                                         
    *_                   _                                                                                               
    (_)_ __  _ __  _   _| |_                                                                                             
    | | '_ \| '_ \| | | | __|                                                                                            
    | | | | | |_) | |_| | |_                                                                                             
    |_|_| |_| .__/ \__,_|\__|                                                                                            
            |_|                                                                                                          
    ;                                                                                                                    
                                                                                                                         
    data want ;                                                                                                          
                                                                                                                         
        array grossx[6]    gross_01-gross_06      (6*1);                                                                 
        array pensionx[6]  pension_01-pension_06  (6*1);                                                                 
        array nicx[6]      nic_01-nic_06          (6*1);                                                                 
                                                                                                                         
        pay_01= round(coalesce(gross_01,0) + coalesce(pension_01,0) + coalesce(nic_01,0) , 0.01) ;                       
        pay_02= round(coalesce(gross_02,0) + coalesce(pension_02,0) + coalesce(nic_02,0) , 0.01) ;                       
        pay_03= round(coalesce(gross_03,0) + coalesce(pension_03,0) + coalesce(nic_03,0) , 0.01) ;                       
        pay_04= round(coalesce(gross_04,0) + coalesce(pension_04,0) + coalesce(nic_04,0) , 0.01) ;                       
        pay_05= round(coalesce(gross_05,0) + coalesce(pension_05,0) + coalesce(nic_05,0) , 0.01) ;                       
        pay_06= round(coalesce(gross_06,0) + coalesce(pension_06,0) + coalesce(nic_06,0) , 0.01) ;                       
                                                                                                                         
        drop gro: pen: nic:;                                                                                             
                                                                                                                         
    run;quit;                                                                                                            
                                                                                                                         
    *          _       _   _                                                                                             
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                             
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                            
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                            
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                            
         _                                                                                                               
      __| | ___     _____   _____ _ __                                                                                   
     / _` |/ _ \   / _ \ \ / / _ \ '__|                                                                                  
    | (_| | (_) | | (_) \ V /  __/ |                                                                                     
     \__,_|\___/___\___/ \_/ \___|_|                                                                                     
              |_____|                                                                                                    
    ;                                                                                                                    
                                                                                                                         
    %array(ns,values=1-6);                                                                                               
                                                                                                                         
    data want ;                                                                                                          
                                                                                                                         
        array grossx[6]    gross_01-gross_06     (6*1);                                                                  
        array pensionx[6]  pension_01-pension_06  (6*1);                                                                 
        array nicx[6]      nic_01-nic_06          (6*1);                                                                 
                                                                                                                         
                                                                                                                         
        %do_over(ns,phrase=%str(                                                                                         
                                                                                                                         
          pay_0?= round(coalesce(gross_0?,0) + coalesce(pension_0?,0) + coalesce(nic_0?,0) , 0.0?);)                     
          );                                                                                                             
                                                                                                                         
        drop gro: pen: nic:;                                                                                             
                                                                                                                         
    run;quit;                                                                                                            
                                                                                                                         
                                                                                                                         
    WORK.WANT total obs=1                                                                                                
                                                                                                                         
      PAY_01    PAY_02    PAY_03    PAY_04    PAY_05    PAY_06                                                           
                                                                                                                         
         3         3         3         3         3         3                                                             
                                                                                                                         
    *                                 _                                                                                  
      __ _  ___ _ __     ___ ___   __| | ___                                                                             
     / _` |/ _ \ '_ \   / __/ _ \ / _` |/ _ \                                                                            
    | (_| |  __/ | | | | (_| (_) | (_| |  __/                                                                            
     \__, |\___|_| |_|  \___\___/ \__,_|\___|                                                                            
     |___/                                                                                                               
    ;                                                                                                                    
                                                                                                                         
    * may not need this;                                                                                                 
                                                                                                                         
    options nosymbolgen nomacrogen nomprint nomlogic;                                                                    
                                                                                                                         
    If you want the code;                                                                                                
                                                                                                                         
    data _null_;                                                                                                         
    %do_over(ns,phrase=%str(                                                                                             
       put "pay_0?= round(coalesce(gross_0?,0) + coalesce(pension_0?,0) + coalesce(nic_0?,0) , 0.0?)";)                  
      );                                                                                                                 
                                                                                                                         
    run;quit;                                                                                                            
                                                                                                                         
    Log  (cut and paste here)                                                                                            
                                                                                                                         
    pay_01= round(coalesce(gross_01,0) + coalesce(pension_01,0) + coalesce(nic_01,0) , 0.01) ;                           
    pay_02= round(coalesce(gross_02,0) + coalesce(pension_02,0) + coalesce(nic_02,0) , 0.01) ;                           
    pay_03= round(coalesce(gross_03,0) + coalesce(pension_03,0) + coalesce(nic_03,0) , 0.01) ;                           
    pay_04= round(coalesce(gross_04,0) + coalesce(pension_04,0) + coalesce(nic_04,0) , 0.01) ;                           
    pay_05= round(coalesce(gross_05,0) + coalesce(pension_05,0) + coalesce(nic_05,0) , 0.01) ;                           
    pay_06= round(coalesce(gross_06,0) + coalesce(pension_06,0) + coalesce(nic_06,0) , 0.01) ;                           
                                                                                                                         
                                                                                                                         
