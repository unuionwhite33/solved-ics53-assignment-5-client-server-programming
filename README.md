Download Link: https://assignmentchef.com/product/solved-ics53-assignment-5-client-server-programming
<br>
You  will  write  a  networked  client/server  application  which  allows  a  client  program  to  query  a simple  database  which  is  managed  by  a  server  program.  For  this  assignment  we  selected  a

database  of  NFL  games  as  an  example.  The  client  program  sends  a  message  containing  the query  about  a  match  to  the  server  and  the  server  program  responds  back  a  message  containing the  requested  information.  Below,  we  will  describe  the  details  of  query  messages  and  the database.

<strong> </strong>

<h1>1.   Running  the  Client/Server</h1>

The  application  is  actually  two  different  programs,  the  client  program  and  the  server  program. These  two  programs  should  both  be  running  as  two  separate  processes  which  are  invoked  by the  user  in  a  shell.  These  two  programs  may  be  running  on  the  same  machine  but  they  may  be running  on  two  different  machines.  Since  the  client  and  server  are  communicating  using  TCP/IP, you  will  need  to  select  a  port  to  use  for  communication.  ICS  Computer  Support  has  advised  us that  ports  30000  –  60000  are  all  available  for  your  use,  so  you  can  use  any  one  of  those  ports.




For  the  purposes  of  this  explanation  we  will  refer  to  the  domain  name  of  the  server  machine  as “server.ics.uci.edu”.  Although  we  use  this  name  in  this  description,  your  program  should  operate correctly  for  any  domain  name.  We  will  also  assume  that  the  port  used  is  30000,  but  your program  should  be  able  to  communicate  on  any  port.




<h2>Database  as  a  .csv  file</h2>

For  this  assignment  we  use  a  comma-separated  values  or  csv  file  as  an  input  to  populate  our database.  This  file  will  have  the  following  fields  separated  by  commas  where  each  line  has information  regarding  one  match.  Assume  maximum  number  of  lines  is  200. The  1st  row  of  csv is  the  name  of  each  field  and  remains  unchanged.  It  won’t  be  read  into  the  database.  (The 1st  line  is  still  included  in  the  MAX_LINE_NUM,  200.)




<table width="624">

 <tbody>

  <tr>

   <td width="45">type</td>

   <td width="73">game_id</td>

   <td width="92">home_team</td>

   <td width="85">away_team</td>

   <td width="52">week</td>

   <td width="72">season</td>

   <td width="93">home_score</td>

   <td width="112">away_score</td>

  </tr>

 </tbody>

</table>




<ol>

 <li>type: specifies  if  this  match  was  a  regular  or  post s eason

  <ul>

   <li>Possible values:  [reg,  post]</li>

  </ul></li>

 <li>game_id: unique  identifier  for  a  specific

  <ul>

   <li>Example: 2018122400</li>

  </ul></li>

 <li>home_team: short  name  of  home  team  for  each m atch.

  <ul>

   <li>Examples: GB,  NYJ</li>

  </ul></li>

 <li>away_team: similar  to  home_team  but  specifying  the  away

  <ul>

   <li>Examples: LA,  KC</li>

  </ul></li>

 <li>week: week  number  in  the  season  that m atch  was

  <ul>

   <li>Possible values:  [1  to  20]</li>

  </ul></li>

 <li>season: year  that  match  belongs

  <ul>

   <li>Examples: 2005,  2006,  2019</li>

  </ul></li>

 <li>home_score: number  of  points  home t eam  scored  in  that  match

  <ul>

   <li>Possible values:  [0-1000]</li>

  </ul></li>

 <li>away_score: number  of  points  away  team  scored i n  that  match

  <ul>

   <li>Possible values:  [0-1000] Sample:</li>

  </ul></li>

</ol>







<h2>Starting  the  Server</h2>

If we       assume                that       the         name    of   the server’s                compiled           executable            is “server”          then      you        would   start     the  server  by  typing  the  following  at  a  linux p rompt,




“./server  data_base.csv  30000”.




When  the  server  is  started,  it  should  print  “server  started
”  and  then  wait  to  receive  messages from  a  client.  One  example  of  data_base.csv i s  provided  in  the  assignment  files.

<strong> </strong>

<h2>Starting  the  Client</h2>

If  we  assume  that  the  name  of  the  client’s  compiled  executable  is  “client”  then  you  would  start the  client  by  typing  the  following  at  a  linux p rompt:




“./client  server.ics.uci.edu  30000”.




Remember  server.ics.uci.edu  is  the  domain  name  of  the  machine  that  server  is  running  on.  In most  cases  if  you  run  both  client  and  server  on  the  same  machine,  you  can  use  “localhost” instead  to  loop  back  the  connection  between  client  and  server.  When  the  client  starts  it  should print  a  “&gt;”  prompt  on  the  screen  and  wait  for  input  from  the  user.  (Note:  “&gt;  “  is  one  &gt;  and  one space.)




<h1>2.   User  interface</h1>

<h2>User  Interface  of  the  Client</h2>

Requests  for  match  information  are  made  by  the  user  entering <em>game_id</em>  and <em>field</em>  info  at  the client’s  prompt.  When  this  information  is  entered  at  the  client’s  prompt,  the  client  will  send  a request  message  containing  the <em>game_id</em>  and <em>field</em>  to  the  server,  and  the  client  will  await  a

response  from  the  server.  The  server  will  send  a  response  message  containing  the corresponding  information  of  the <em>field</em>  for  the  match  with  that <em>game_id </em>.  The  client  will  print  the received  information  to  the  screen,  print  a  prompt  on  a  new  line,  and  wait  for  more  input  from the  user.  An  example  of  a  user  interaction  with  the  client  is  shown  below.  It  is  derived  from  the first  row  of  database  examples.










&gt;  2018090600  type reg

&gt;  2018090600  game_id

2018090600

&gt;  2018090600  home_team

PHI

&gt;  2018090600  away_team

ATL

&gt;  2018090600  week

1

&gt;  2018090600  season

2018

&gt;  2018090600  home_score

18

&gt;  2018090600  away_score

12

&gt;  whats  up? unknown

&gt;  2018090600  away_score

12

&gt;  quit

$ <em>←you</em> <em>  are  back  to  the  linux  prompt. </em>




The  client  will  continue  in  this  loop  until  the  user  enters  “quit”  which  will  cause  the client’s  process  to  exit. ( Note:  No  need  to  print  anything  after  quit  was  entered.)

<strong> </strong>

<h2>User  Interface  of  the  Server</h2>

Once  running,  the  server  will  only  accept r equests  sent  from  one  client  over  the network.  When  the  server  receives  a  request  from  a  client,  the  server  will  print  the<em> game_id</em>  and <em>field</em>         in  the  message  on  the  screen  on  a  new  line.  An  example  of  the  printed output  of  the  server  when  communicating  with  the  client  is  shown  below.




server  started

2018090600  game_id

2018090600  home_team

2018090600  away_team

2018090600  week

2018090600  season

2018090600  home_score

2018090600  away_score







The  server  will  continue  responding  to  requests  and  printing  the  associated  information  until  its process  is  killed  externally,  for  instance b y  a  ctrl-c  typed  at  the  keyboard.

<strong> </strong>

<h1>3.   Message  Format</h1>

Each  message  sent  between  the  client  and  the  server  must  contain  two  pieces  of  information,  a string,  and  the  length  of  the  string.  The  string  will  be  the <em>game_id </em>and<em>  field</em>  inside  a  request  sent from  the  client  to  the  server,  and  the  string  will  be  the  value  of  that  field  for  the  corresponding match  response  sent  from  the  server  to  the  client.  Each  message  must  be  shorter  than  256 bytes  long  and  must  be  formatted  as  follows:




<ul>

 <li>Byte 0:  Length  of  the  string</li>

 <li>Bytes 1  –  n:  Characters  of  the  string</li>

</ul>




<h1>4.   Implementation  Details</h1>

<ol>

 <li>If the <em>game_id</em>  or  the <em>field</em>  typed  into  the  client  is  not  in  the  database  which  is  known  to  the server,  just  return  “unknown”  and  continue  the</li>

 <li>Don’t worry  about  invalid  input  typed i nto  the    Everything  entered  into the  client  can  be  assumed  to  be  a  valid  input.</li>

</ol>

For  any  corner  cases,  you  can  use  “unknown”  for  commands  that  do  not  fit  the  description  of  the assignment  and  “unknown”  for  any  information  requested  that  do  not  exist.