# wrf-chem-chem-kpp-kpp2.1-..-gen_kpp.c
there is a mistake in official file gen_kpp.c, their gen_kpp.c 's function definition order is reserved! So when you make there is a report of error:implicit function: write_list_to_screen,screen_out,check_all 
官方很多WRF版本的chem下面的/chem/KPP/util/wkc/gen_kpp.c都是错的（直到2023.4.27最新版的WRF里面的这个都还是错的），因为他把函数顺序给放反了，把write_list_to_screen跟screen_out还有check_all都放在最下面了，而gen_kpp函数却放在最上面，所以就会导致报错函数没有定义，因此需要将原文件里面的函数顺序换一下，把write_list_to_screen等3个函数放到gen_kpp的上面，在我的这里是已经修改好的gen_kpp.c文件，下载后替换即可
error like this:
gcc -I../../../../inc  -c -g  gen_kpp.c
gen_kpp.c: In function ‘gen_kpp’:
gen_kpp.c:75:27: warning: implicit declaration of function ‘write_list_to_screen                                                     ’ [-Wimplicit-function-declaration]
   75 |        if ( DEBUGR == 2 ) write_list_to_screen( WRFC_packs ) ;
      |                           ^~~~~~~~~~~~~~~~~~~~
gen_kpp.c:115:6: warning: implicit declaration of function ‘screen_out’ [-Wimpli                                                     cit-function-declaration]
  115 |      screen_out( );
      |      ^~~~~~~~~~
gen_kpp.c:120:6: warning: implicit declaration of function ‘check_all’ [-Wimplic                                                     it-function-declaration]
  120 |      check_all ( kpp_dirname );
      |      ^~~~~~~~~

The /chem/KPP/util/wkc/gen_kpp.c under the chem of many official WRF versions is wrong (this is still wrong in the latest version of WRF until 2023.4.27), because the order of functions is reversed , put write_list_to_screen, screen_out and check_all at the bottom, but put the gen_kpp function at the top, so it will cause the error functions are implicit declaration, so you need to change the order of the functions in the original file, please put 'write_list_to_screen' 'screen_out','check_all' over top of gen_kpp. Here is the modified correct gen_kpp.c file in my github, you can use it.
