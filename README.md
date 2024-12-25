java c
TELE4652   Lab   Manual
Experiment 4A    4B:   Digital   Modulation      Channel Coding
June   11,   2024
1.   IntroductionModern   wireless   communication   systems   involve   many   well-coordinated   steps   and   compo-   nents   to   deliver   a   message   from   a   transmitter   to   a   receiver.   A   simplified   system   diagram   of   such   a   wireless   communication   system   can   be   found   in   Figure. 1.1.On the transmitter side, the process   begins   with   the   information   source,   which   generates   the   data   to   be   transmitted.      This   data   is   converted   into   an   electrical   signal   by   the   input transducer.   The   base-band   processor   then   conditions   the   signal,   making   it   ready   for   encod-   ing.    The   encoder   applies   error   correction   codes,   and   the   modulator   combines   the   encoded   signal   with   a   carrier   frequency   for   transmission.      The   up   converter   shifts   this   modulated   signal   to   a   higher   frequency,   and   the   power   amplifier   boosts   its   strength.   Finally,   the   radio   transmitter   sends   the   amplified   signal   through   the   antenna   into   the   air.The   transmission   medium,   typically   air,   allows   the   electromagnetic   waves   to   travel   from   the transmitter to the receiver.    The receiver’s antenna captures these waves and passes   them   to   the   radio   receiver,   which   converts   them   into   a   form   suitable   for   further   processing.    The   down   converter   shifts   the   frequency   of   the   received   signal   to   a   lower   frequency,   making   it   ready   for   demodulation.    The   demodulator   extracts   the   base-band   signal   from   the   carrier,   effectively   reversing   the   modulation   process.    The   decoder   then   applies   error   correction   to   recover   the   original   data   format.On   the   receiver   side,    the   base-band   processor    conditions   the   decoded   signal   for   out-   put.       The   output   transducer   converts   this   processed   electrical   signal   back   into   a   human-   understandable   form,   such   as   sound   through   a   speaker   or   an   image   on   a   screen.   The   infor-   mation   receiver   presents   the   final   information   to   the   user,   completing   the   communication   process.    This   system   demonstrates   the   essential   components   and   steps   involved   in   modern   wireless   communication,   highlighting   the   transformation   of data   from   its   original   form   to   a   transmitted   signal   and   back   to   its   original   form   at   the   receiver’s   end.
This   lab   manual   is   designed   for   students   to   gain   hands-on   experience   with   different   digital   modulation   schemes   and   channel   coding   techniques   using   MATLAB.   By   performing
Figure   1.1:   A   simplified   system   diagram   of modern   wireless   communication   systems.
the   experiments   outlined   in   this   manual,   students   will:
•    Develop   an   understanding   of the   digital   modulation   techniques   such   as   Binary   Phase   Shift Keying   (BPSK) and Quadrature Amplitude Modulation   (QAM)   in   modern   wire-   less   communication   systems.
•    Learn to implement and analyse   the   performance   of   these   modulation   schemes   over   an   Additive   White   Gaussian   Noise   (AWGN)   channel.
•    Explore various channel coding techniques ranging   from   old-fashioned   Hamming   codes   to   state-of-the-art   codes.
•    Evaluate   the   effectiveness   of   these   techniques   with   the   well-known   metric   —   the   Bit   Error   Rate   (BER).
By   the   end   of this   lab,   students   should   be   able   to:
•   Understand   the   principles   and   applications   of   different   digital   modulation   and   channel coding   schemes.
•   Improve   the   MATLAB   skills   for   their   future   careers.
•   Improve   analytical   skills   and   critical   thinking   strategies.
2.      Crashcourse   on   MATLABMATLAB’s   user-friendly   interface   and   straightforward   syntax   make   it   an   excellent   choice   for you   while   learning   science   and   engineering   concepts   throughout   their   courses.      Specifically   for this course, MATLAB allows you to focus on understanding telecommunications concepts   without   getting   bogged   down   by   complex   programming   constructs   (such   as   C/C++).   This section   will   be   a   preliminary   for   MATLAB   programming,    but   you      are   welcome   to   seek   external sources if you wish to learn about this useful skill.    Besides, feel free to have a   look   at   the official tutorial about the fundamentals of MATLAB programming via this link: https:   //au.mathworks.com/help/matlab/language-fundamentals.html?s_tid=CRUX_lftnav.
2.1.   MATLAB   Environment
Familiarise   yourself with   the   MATLAB   desktop   environment,   which   includes:
•    Command   Window.   This   window   normally   sits   at   the   bottom   of   your   screen.   You   can type   in   any   commands/functions/scripts that you wish to   run   in   this   window.    This   is   where   you   can   search   the   documentation   of a   function   of your   interest.
•   Workspace.   It   is   at   the   right   side   of   your   screen.    Initially   it   is   empty   but   you   will   see   a list   of   variables   stored   in   the   memory   of   MATLAB.   You   can   double   click   the   variable of your interest to examine its value when the script. stops running   (i.e.   when the script   finishes,   paused   due   to   a   breakpoint   or   terminates   due   to   some   errors).
•    Current   Folder.   This   section   will   show   your   current   working   directory.
•   Editor.   The   place   to   write   your   MATLAB   script.   After   clicking   anywhere   in   the   editor,   the   menu   bar   at   the   top   automatically   changes   to   show   the   buttons   about   different   ways   of   running   the   current   script.      You   can   click   "Run"   to   run   the   whole   script   or   select   some   parts   of the   script   and   then   click   "Run   selection".
2.2.   MATLAB   Variables   and   Operations
Start   with   basic   commands   such   as   arithmetic   operations,    creating   variables,    and    using   built-in   functions.   For   example:
a    =      5;
b    =      10;
c    =      a      +   b;
disp(c);      %      This   will      display      the      result      of      a      +   bVariables   can   be   a   vector   or   a   matrix   and   you   can   apply   all   the   matrix   operations   to   these   variables.   However,   it   is your job to   make   sure the   dimensions   of your   operants   are   right   for   the   operation.   For   example,   you   can   add   2   vectors   with   the   same   dimension   together:
v      =      [1,      2,      3,      4];   M      =      [5,      6,      7,      8];
result      =   M      +      v      %   will      give      you      the      correct      result   .
However,   you   cannot   perform   matrix   multiplication   on   the   two   vectors   due   to   the   wrong dimensions   of v   and   M   :
v      =      [1,      2,      3,      4];   M      =      [5,      6,      7,      8];
result      =   M      *      v      %   will      give      you      an      error   .There   is   a   short-hand   syntax   in   MATLAB   if   you   wish   to   perform   element-to-element   oper-   ations   (mostly   multiplication   and   division)   by   add   a   "."   (period)   before   the   operation   you wish   to   perform.    For   example,   you   can   calculate   the   element-to-element   division   of   v    and   M   ,   you   can   do   the   following:
v      =      [1,      2,      3,      4];   M      =      [5,      6,      7,      8];
result      =   M    ./    v      %   will      give      you      the      correct      result   .
However,   if   you   miss   the   "."   in   the   front   of   "./",   it   means   that   you   are   trying   to   perform   the matrix   division,   which   will   give   you   an   error   in   the   last   example.
2.3.   The   “end”You   may   find   that   your   codes   stop   working   after   you   move   your   loops/if-else   branches   to   someplace   else.    If   this   happens,   the   first   thing   you   should   check   is   whether   you   move   the   correct   “end”   together   with   your   loops/if-else   branches.      The   MATLAB   keyword,   “end”,   marks   the   end   of a   code   block,   where the   code   block   could   be   your   loop   body   or your   if-else   statements,   just   like   the   close   curly   braces   ("}")   in   many   programming   languages   such   as   C/C++.
2.4.    Scripts   and   Functions
Code   Modularisation   is   always   a   good   practice   in   programming.    The   benefit   of the   modu-   larisation   may   lead   to   the   following   advantages:
•    Reuse   your   code.    Modularisation   allows   for   the   reuse   of   code   across   parts   of   scripts.   Once   a   module   is   created   and   tested,   it   can   be   reused   without   modification,   saving   time   and   reducing   the   likelihood   of   introducing   errors.   This   is   particularly   beneficial   in MATLAB, where   complex   algorithms   and   functions   can be encapsulated   into reusable   scripts   or   functions.
•    Easier   Testing   and   Debugging.       Testing    individual   functions   independently   is   more   straightforward   than   testing   a   length   MATLAB   script.    By   modularising   your   codes,   you   can   test   your   implementation   separately, which   will   significantly   help   you   identify and   fix   bugs   while   working   on   the   lab   tasks.Before   working   on   this   experiment,   you   are   recommended   to   read   through   the   tutorial   pages about defining and using your own functions in MATLAB via this link: https://au.   mathworks.com/help/matlab代 写TELE4652 Lab ManualC/C++
代做程序编程语言/functions.html?s_tid=CRUX_lftnav.Creating   your   own   function(s)   can   be   very   useful   when   you   are   required   to   complete   tasks   (e.g.      Task   2   of   Part   A)   from   scratch.      The   recommended   practice   is   to   define   your   own   function(s)   in   separate   files   and   call   your   defined   function(s)   wherever   you   need   them.   This   can   be   done   by   clicking   the   downward   triangle   under   the   button   “New”   and   selecting   “function”.   However,   there   are   a   few   things   to   keep   in   mind:
•    Keep   the   files   containing   your   own   functions   under   the   same   directory   of your   Lab   4   files.
•    Ensure that the name of your   function   is   exactly   the   same   as   the   name   of the   function   file.
For example, as shown below,   I   created   a   function   named   “addNumbers”   in   an   empty   .m   file:
%      Example      of      a      function
function      output      =      addNumbers(x,      y)   output      =      x      +      y;
end
When   I   save   this   file,   I   need   to   make   sure   that   the   saved   file   is   named   “addNumbers.m”.   Now,   if   I   would   like   to   call   this   “addNumbers”   function,   I   can   simply   do   the   following:
%      Example      of    calling      a      function   %       .   .   .   .   .      some    Matlab      codes
a      =      1;   b    =    2;
c      =    addNumbers(a,b);
%       .   .   .   .   .      some    Matlab      codes
2.5.   Debugging   in   MATLABDebugging is an essential part of the programming process.    Debugging your codes allows you   to understand how the codes   work   and   identify   the   source   of your   error.    Fortunately,   due to   its   own   feature,   MATLAB   will   always   run   your   code   until   an   error   is   generated.   MATLAB   provides   robust   (more   importantly,   easy-to-use)   debugging   tools   that   help   you   detect   and   correct   issues.   Here’s   a   brief example   of a   typical   debugging   workflow   in   MATLAB:
•    Set   a   Breakpoint:   Set   a   breakpoint   at the   beginning   of a   suspicious   code   section   by   clicking   the   line   number   in   the   Editor.
•   Run   the   Program:   Run   your   program.    MATLAB   will   pause   execution   at   the   break-   point,   allowing   you   to   inspect   the   program’s   current   state.   Now   it   is   time   to   examine   your   values   of all   the   variables   in   the   workspace.
•    Step   Through   Code:    Use   step-by-step   execution   commands   to   move   through   your   code,   examining   the   changes   in   the   variable   values   and   the   execution   flow   and   see   if   the   execution   matches   what   you   expect.
•   Analyze   Errors:    If   an   error   occurs,   read   the   error   message   carefully   to   understand   the nature of   the problem.   Use the information provided to make necessary corrections.
•    Modify   and   Continue:    Make   any   necessary   changes   to   your   code   and   restart   the   program.   Repeat   the   debugging   process   as   needed   until   all   issues   are   resolved.
Debugging   can   be   very   helpful   when   you   have   your   own   functions   defined.
2.6.   MATLAB   Tips
Some   additional   tips   might   be   useful   to   you:
•    Remove   the   semicolon   at   the   end   of   a   statement   to   show   you   the   execution   result   of   that   statement.    For   example,   in   the   codes   below,   the   value   of   d   will   be   shown   in   the   command   window,   but   the   value   of   c   will   be   hidden   from   you.    Note   that   both   c   and   d   are   executed.
%      Example      of    calling      a      function   %       .   .   .   .   .      some    Matlab      codesa      =      1;   b    =    2;   e    =    3;
c      =    addNumbers(a,b);   d    =    addNumbers(e,b)
%       .   .   .   .   .      some    Matlab      codes
•    Pause   the   execution   of   your   script   just   before   an   error   is   generated.       Clicking    the   downward   triangle   under   the   button   "Run"   will   show   you   additional   ways   of   running your   script.   By   selecting   "pause   on   error",   MATLAB   will   pause just   before   an   error   is   generated   and   enter   the   debugging   mode.   This   can   help   you   identify   where   your   code   will   go   wrong   and   make   it   easier   for   you   to   fix   it.
2.7.   Additional   Reading   on   Channel   codes   and   digital   modulation
in   MATLAB
With the MATLAB communication toolbox, you   can   simulate   all   the   critical   components   of   a   modern   communication   system.   Additional   reading   closely   related   to   Part   A   of   this   experi-ment can be found here: https://au.mathworks.com/help/comm/error-detection-and-correction.   html. For Part B, additional reading can be found here: https://au.mathworks.com/help/comm/modulation.html.
3.   Part   A:   Channel   CodesIn   this   part,   you   will   investigate   the   different   types   of channel   codes   and   observe   how   these   codes   can   improve   the   overall   performance   of   a   simulated   communication   system.    To   com-   plete this lab, you may use your own laptop   during the   lab   session   or   the   computers   provided   in   the   lab.   You   are   highly   recommended   to   install   and   use   MATLAB   Communication   Tool-   box   throughout   this   lab.
3.1.   Procedure
1.    Download the   Lab 4   package   from   TELE4652 pages   on   Moodle   and   extract the   down-   loaded   file   to   any   directory   you   prefer.
2.    Start   MATLAB   and   navigate   to   the   extracted   Lab   4   package.
3.    Go   through   the   file   "Lab4AcodesForStudents.m".
4.    Follow   the   instructions   in   this   file   and   complete   all   the   tasks   described.
5.    Once   you   complete   the   last   step   of the   procedure,   run   your   simulation   and   wait   until   it   finishes.
3.2.    Questions
1.    Briefly   introduce   the   channel   codes   that   you   used   in   your   simulation.
2.    Configure all the channel codes in   your   simulation   so   that   they   have   similar   code   rates.   Run   your   simulation   and   compare   their   BER   vs.      Eb   /No      performance.    Explain   your findings.
3.    Configure   all   the   channel   codes   in   your   simulation   to   a   different   code   rate   and   run   your   simulation   again.   How   did   your   codes   perform   compare   to   the   simulation   results   in   Question   2?
4.   What   will   you   observe   if your   channel   codes   cannot   correct   all   the   bit   errors?
5.    Time   the   encoding   and   decoding   process   separately   for   each   codes   in   your   simulation.   Do   you   think   the   encoding/decoding   time   is   a   critical   factor   to   consider   for   practical system?   Justify   your   answer   based   on   your   measured   processing   time.
6.    In   this   simulation,   we   essentially   transmitted   the   red,   green   and   blue   value   of   each   pixel   to   the   receiver.   Is   this   a   good   way   to   transmit   messages   such   as   pictures?
4.   Part   B:   ModulationIn this experiment, we will delve into the principles and practical applications of different dig-   ital modulation techniques.   We will mainly focus   on   several   key   digital   modulation   schemes,   including   Amplitude-based   modulatiom   and   Phase   Shift   Keying   (PSK).   These   techniques   are   fundamental to various   communication   systems,   from   cellular   networks to   satellite   com-   munications,   and   play   a   critical   role   in   ensuring   reliable   and   efficient   data   transmission.NOTE: You are   not required to   complete   Part   A   before   working   on   this   part.
4.1.   Procedure
1.    Download   the   Lab   4   package   from   the   TELE4652   pages   on   Moodle   and   extract   the   downloaded   file   to   any   directory   you   prefer.
2.    Start   MATLAB   and   navigate   to   the   extracted   Lab   4   package.
3.    Go   through   the   file   "Lab4BcodesForStudents.m".
4.    Follow   the   instructions   in   this   file   and   complete   all   the   tasks   described.
5.    Once   you   complete   the   last   step   of the   procedure,   run   your   simulation   and   wait   until   it   finishes.
4.2.    Questions
1.    Run   your   simulation   and   compare   the   BER   vs.    Eb   /No    performance   between   the   two   types   of the   modulation   with   the   following   parameters:
•   M-ary   PSK:   M   = 4,   Gray   labelling,   0   phase   shifts.
•   M-ary   QAM:   M   = 4,   Gray   labelling,   0   phase   shifts.
•   No   pulse-shaping   filter   applied.
2.    Change   the   Gray   labelling   to   natural   bit   labelling   in   the   configuration   in   Question   1   and   explain   whether   Gray   labelling   can   improve   the   overall   BER   performance.
3.    Explain how the eye diagram is   plotted.   What   information   we   can   obtain   from   the   eye   diagram?
4.   Why   pulse-shaping   filters   are   applied?      Apply   the   pulse-shaping   filter   while   keeping   the   rest   of   the   modulation   configuration   the   same   as   in   Q1.      Explain   your   findings,   particularly   in   the   eye   diagram.
5.   Why   a   fixed   phase   offset   can   be   introduced   for   PSK?   What   are   the   benefits   of   intro-   ducing   such   a   phase   offset?      Answer   this   question   by   setting   the   phase   shift   of   your PSK   modulation   function   to   π/4.
6.   Increase   the   value   of   M   to   16   and   then   64   for   both   PSK   modulation   and   QAM   while   keeping   other   parameters   the   same   as   in   Question    1.       Will   your    BER   performance   improve?

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
