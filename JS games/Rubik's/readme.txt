Jeu inspiré du rubik's cube---------------------------
Url     : http://codes-sources.commentcamarche.net/source/27816-jeu-inspire-du-rubik-s-cubeAuteur  : vbbreizhDate    : 07/08/2013
Licence :
=========

Ce document intitulé « Jeu inspiré du rubik's cube » issu de CommentCaMarche
(codes-sources.commentcamarche.net) est mis à disposition sous les termes de
la licence Creative Commons. Vous pouvez copier, modifier des copies de cette
source, dans les conditions fixées par la licence, tant que cette note
apparaît clairement.

Description :
=============

Jeu inspir&eacute; du Rubik's Cube utilisant des routines basiques et fonctionna
nt avec tous les navigateurs r&eacute;cents.
<br /><a name='source-exemple'></a
><h2> Source / Exemple : </h2>
<br /><pre class='code' data-mode='basic'>
&lt
;html&gt;&lt;head&gt;
&lt;title&gt;Rubiks&lt;/title&gt;
&lt;script language=&q
uot;JavaScript&quot;&gt;&lt;!--
//------------------chrono-----------------
va
r iHour = 0; var iMin = 0; var iSec = 0;
var iCount = 0; var iM=0; var iS=0;
f
unction startCount(){
             iCount++;
             iSec = iCount;
    
         if ( iSec&gt;59 ) { iMin= iMin+1 ;  iSec=0 ; iCount=0;}
             i
f (  iSec&lt;10 ) {  iS= &quot;0&quot; +iSec;} else {iS=iSec;}
             if 
( iMin&gt;59 ) { iHour= iHour+1 ; iMin=0;}
             if (  iMin&lt;10 ) {  i
M= &quot;0&quot; +iMin;} else {iM=iMin;}
var chrono=&quot;...&quot; +iHour+ &qu
ot;:&quot; +iM+ &quot;:&quot; +iS;
document.getElementById('clock').value=chron
o;
setTimeout(&quot;startCount()&quot;,1000);
}
//------------------game-----
------------
var colors= new Array('r','r','r','r','g','g','g','g','b','b','b',
'b','w','y','y','y');
//-----------------(images dans le zip)------------------
------
var pics= new Array('red.gif','green.gif','blue.gif','yellow.gif','pix.g
if');
var col=&quot;&quot;; var nr; 
var pos; var valid= false;
var size = co
lors.length;
function delete_element(array) {
   size = colors.length;
   var
 validNo = (nr != &quot;NaN&quot;);
   var inRange = ( (nr&gt;=0) &amp;&amp; (n
r&lt;size) );
   if (validNo &amp;&amp; inRange) {
       for (var i= 0; i&lt;
=size-1; i++) {
              colors[i] = ((i == nr) ? &quot;delete&quot; : col
ors[i]);}
       for (var j= nr; j&lt;size-1; j++) {
              if (j!= siz
e) {colors[j] = colors[j+1];}}
colors.length = size-1;
}}
function get_col(k)
 {
   nr= Math.floor(Math.random()*(size-1));
   if (colors[nr]=='r') {col=pic
s[0];}
   if (colors[nr]=='g') {col=pics[1];}
   if (colors[nr]=='b') {col=pic
s[2];}
   if (colors[nr]=='y') {col=pics[3];}
   if (colors[nr]=='w') {col=pic
s[4]; pos=k;}
delete_element(colors);
}
function mix_colors() {
    self.loc
ation.reload(true);
}
function check_validity(k) {
    var Ck=parseInt(k); 

    valid= false;
    if ((pos==(Ck-4)) || (pos==Ck+4)) {
          valid= tru
e;} 
    if ((pos==(Ck-1)) &amp;&amp; (pos!=3) &amp;&amp; (pos!=7) &amp;&amp; (
pos!=11)) {
          valid= true;}
    if ((pos==(Ck+1)) &amp;&amp; (pos!=4) 
&amp;&amp; (pos!=8) &amp;&amp; (pos!=12)) {
          valid= true;}
}
var tem
p = new Image();
function run_game(k) {
  check_validity(k);
  if (valid==tru
e) {
            temp.src= document.images[k].src; 
            document.image
s[k].src= document.images[pos].src; 
            document.images[pos].src= temp
.src;
            pos =k; valid= false;}
}
--&gt;&lt;/script&gt;&lt;/head&gt;

&lt;body&gt;
&lt;font size=2&gt;&lt;font color=black&gt;
Free JavaScript pro
vided by ©2004-&lt;a href=&quot;<a href='http://gilles.saunier.free.fr' target='
_blank'>http://gilles.saunier.free.fr</a>&quot;&gt;VB'Breizh&lt;/a&gt;&lt;br&gt;

inspired from the &lt;a href=&quot;<a href='http://dev.rubiks.com' target='_bl
ank'>http://dev.rubiks.com</a>&quot;&gt;Rubik's&lt;/a&gt; Cube game.&lt;br&gt;

cross browser compatibility (nntype/ietype/opera recent browsers).&lt;hr&gt;
&l
t;p&gt;
&lt;center&gt;&lt;script&gt;
     document.write('&lt;table style=&quo
t;cursor:pointer;&quot;&gt;&lt;tr&gt;');
     for (i=0; i&lt;16; i++) {
      
     get_col(i);
           if ((i==4) || (i==8) || (i==12)) {document.write('&
lt;/tr&gt;&lt;tr&gt;');};
           document.write('&lt;td&gt;&lt;img src=&quo
t;'+col+'&quot; name=&quot;'+i+'&quot; width=40px height=40px onmousedown=&quot;
run_game('+i+')&quot;&gt;&lt;/td&gt;');}
document.write('&lt;/tr&gt;&lt;/table&
gt;');
&lt;/script&gt;
&lt;img src=&quot;pix.gif&quot; width=1px height=200px 
border=0&gt;
&lt;p&gt;&lt;input type=button value=&quot;...mix...&quot; onclick
=&quot;mix_colors()&quot;&gt;&amp;nbsp;
&lt;input type=button id=&quot;clock&qu
ot; value=&quot;chrono&quot; size=6&gt;&lt;p&gt;&lt;font size=3&gt;
...Click on
 the color to move and align colors as fast as possible...&lt;/center&gt;
&lt;b
ody onload=&quot;startCount()&quot;&gt;
&lt;/body&gt;&lt;/html&gt;
</pre>
<br
 /><a name='conclusion'></a><h2> Conclusion : </h2>
<br />Pour avoir la derni&
egrave;re version, venez faire un tour sur <a href='http://gilles.saunier.free.f
r' target='_blank'>http://gilles.saunier.free.fr</a>&quot;
