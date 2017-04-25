Deblock me - casse tête-----------------------
Url     : http://codes-sources.commentcamarche.net/source/51883-deblock-me-casse-teteAuteur  : amrounixDate    : 13/08/2013
Licence :
=========

Ce document intitulé « Deblock me - casse tête » issu de CommentCaMarche
(codes-sources.commentcamarche.net) est mis à disposition sous les termes de
la licence Creative Commons. Vous pouvez copier, modifier des copies de cette
source, dans les conditions fixées par la licence, tant que cette note
apparaît clairement.

Description :
=============

casse t&ecirc;te o&ugrave; il faut sortir une pi&egrave;ce du jeu en coulisant l
es autres pi&egrave;ces
<br />
<br />derni&egrave;re version sur mon site :
<
br /><a href='http://www.crew.free.fr/' target='_blank'>http://www.crew.free.fr/
</a>
<br />
<br />amusez-vous bien !
<br /><a name='source-exemple'></a><h2> 
Source / Exemple : </h2>
<br /><pre class='code' data-mode='basic'>
&lt;html&
gt;
&lt;head&gt;
&lt;style&gt;

.scoring {
	background:#f0f0f0;
	width:250
px;
	height:50px;
	border:1px solid green;
	z-index:9999;
	text-align:center
;
	color:green;
	opacity: .9; filter: alpha(opacity=90); -ms-filter:&quot;prog
id:DXImageTransform.Microsoft.Alpha(Opacity=90)&quot;;
	}
.tableback {
	borde
r-top:1px #c0c0c0 dashed;
	border-left:1px #c0c0c0 dashed;
	}

.block0 {back
ground-color:#a0a0a0;border:2px black solid;}
.block1 {background-color:#a0a0a0
;border:2px black solid;}
.block2 {background-color:#a0a0a0;border:2px black so
lid;}
.block3 {background-color:#a0a0a0;border:2px black solid;}
.block4 {back
ground-color:#FFa0a0;border:2px black solid;}

.leveltable td {
border :1px s
olid green;
width:20px; text-align:center; color:green;
}

.finished {
back
ground:lightgreen;
}

&lt;/style&gt;

&lt;script language=&quot;javascript&
quot;&gt;
/*et oui ... mon programme est multilingue !*/
var fr ={&quot;stage_
clear&quot; : &quot;Niveau terminé&quot;,&quot;nb_move&quot;:&quot;nombre de mou
vement&quot;,&quot;score&quot;:&quot;score&quot;,&quot;nvx_grille&quot;:&quot;cr
éer une nouvelle grille&quot;}
var en ={&quot;stage_clear&quot; : &quot;Level c
lear&quot;,&quot;nb_move&quot;:&quot;number of movement&quot;,&quot;score&quot;:
&quot;score&quot;,&quot;nvx_grille&quot;:&quot;new puzzle&quot;}
var lang = fr;
 /*var lang = en ; //for english version*/
var diff = &quot;debutant&quot;;
va
r nivo =  {
&quot;nvx&quot; : {12:4}
};

function save_cok(p,diff) {
htm=&q
uot;&quot;; first = true;
for (e in nivo)
{
if (p[e])
{
htm+=&quot;c:&quot;
+e+&quot;,m:&quot;+p[e].mvt+&quot;,s:&quot;+p[e].score+&quot; &quot;;
}
}
   
   var expireDate = new Date();
      expireDate.setTime(expireDate.getTime() +
 365*24*3600*1000);
      document.cookie = &quot;sam_&quot;+diff+&quot;=&quot;
 + escape(htm)
         + &quot;;expires=&quot; + expireDate.toGMTString();
  
    }

function load_cok(diff) {

      var deb,fin, nom= &quot;sam_&quot;+d
iff;
      deb = document.cookie.indexOf(nom + &quot;=&quot;)
      if (deb &g
t;= 0) {
         deb += nom.length + 1
         fin = document.cookie.indexOf
(&quot;;&quot;,deb)
         if (fin &lt; 0) fin = document.cookie.length
    
     return unescape(document.cookie.substring(deb,fin))
         }
      retu
rn null;
      }

var modecreate = false; /*passer en mode creation*/
var sc
oretab = {}; /*liste des scores*/
var wx = 60,hx = 50,ss=null; /*piece selction
née*/
var cart=[]; /*tableau d'element*/
var level_x = 0;
var nbmove=0; 
var
 bougeMe = false;
var piece_x = 0;
var dxx = 0 , dyy = 0;

function _(x) /*a
ppel des objet + simple*/
	{return document.getElementById(x);}

function msg
(txt)
	{return lang[txt] ? lang[txt] : txt;}

	

function difficulte(niv_x)

{
diff = niv_x;
switch (diff)
{
case &quot;debutant&quot; : nivo = debutan
t; break;
case &quot;inter&quot; : nivo = inter; break;
case &quot;avance&quot
; : nivo = avance; break;
case &quot;expert&quot; : nivo = expert; break;
}
p
x_cok = load_cok(diff);
scoretab = {};
if ( px_cok != null)
{
px_cok.replace
(/c:([0-9]+),m:([0-9]+),s:([0-9]+) /g,function($1,$2,$3,$4){ scoretab[$2]={'mvt'
:parseInt($3,10), 'score': parseInt($4,10)};});
}
viewLevel();
/*recupère le 
1er niveau de la liste*/
for (level_x in nivo) {if (level_x!=&quot;nvx&quot;) b
reak;}
afficheBloc(level_x );
}

function viewLevel()
{
htm=&quot;&lt;div 
style='height:300px;overflow-y:scroll;padding-right:24px;overflow-x:hidden;'&gt;
&lt;table class='leveltable'&gt;&lt;tr&gt;&quot;;
w=0;
for (e in nivo)
{
if 
(e!=&quot;nvx&quot;)
{htm+=&quot;&lt;td &quot;;
if (scoretab[e])
{
htm+=&quo
t;class='finished' title='score : &quot;+scoretab[e].score+&quot;, mvt : &quot;+
scoretab[e].mvt+&quot;' &quot;;
}
htm+=&quot; onclick=changeLevel('&quot;+e+&q
uot;') &quot;
htm+=&quot; &gt;&lt;b&gt;&quot;+e+&quot;&lt;/b&gt;&lt;/td&gt;&quo
t;;

if ((w%10)==9) {htm+=&quot;&lt;/tr&gt;&lt;tr&gt;&quot;;w=0;} else w++;


}
}
if (w&gt;0) for (k=w;k&lt;9;k++)
htm+=&quot;&lt;td&gt;&amp;nbsp;&lt;/td&
gt;&quot;;
htm+=&quot;&lt;/tr&gt;&lt;table&gt;&lt;div&gt;&quot;;
_(&quot;level
&quot;).innerHTML = htm;
}

function changeLevel(xx)
{
level_x = xx;
affic
heBloc(xx);
}

function afficheBloc(level_x)
{

modecreate = (level_x==&qu
ot;nvx&quot;);
if (modecreate) 
{
htm=&quot;&lt;table border='1' &gt;&quot;;

htm+=&quot;&lt;tr&gt;&lt;td align='center' onclick='selpiece(0);'&gt;&lt;div cl
ass='block0' style='width:&quot;+(2*wx)+&quot;px;height:&quot;+(1*hx)+&quot;px;'
 &gt;&lt;/div&gt;&lt;/td&gt;&lt;/tr&gt;&quot;; /*onmousedown='choix(this,&quot;+
idx+&quot;,&quot;+type_+&quot;,event);return false;'*/
htm+=&quot;&lt;tr&gt;&lt
;td align='center' onclick='selpiece(1);'&gt;&lt;div class='block1' style='width
:&quot;+(1*wx)+&quot;px;height:&quot;+(2*hx)+&quot;px;' &gt;&lt;/div&gt;&lt;/td&
gt;&lt;/tr&gt;&quot;; /*onmousedown='choix(this,&quot;+idx+&quot;,&quot;+type_+&
quot;,event);return false;'*/
htm+=&quot;&lt;tr&gt;&lt;td align='center' onclic
k='selpiece(2);'&gt;&lt;div class='block2' style='width:&quot;+(3*wx)+&quot;px;h
eight:&quot;+(1*hx)+&quot;px;' &gt;&lt;/div&gt;&lt;/td&gt;&lt;/tr&gt;&quot;; /*o
nmousedown='choix(this,&quot;+idx+&quot;,&quot;+type_+&quot;,event);return false
;'*/
htm+=&quot;&lt;tr&gt;&lt;td align='center' onclick='selpiece(3);'&gt;&lt;d
iv class='block3' style='width:&quot;+(1*wx)+&quot;px;height:&quot;+(3*hx)+&quot
;px;' &gt;&lt;/div&gt;&lt;/td&gt;&lt;/tr&gt;&quot;; /*onmousedown='choix(this,&q
uot;+idx+&quot;,&quot;+type_+&quot;,event);return false;'*/
htm+=&quot;&lt;/tab
le&gt;&quot;;
_(&quot;level&quot;).innerHTML = htm;
}
dispo2html(nivo[level_x
],level_x);
}

function selpiece(piece)
{
if (modecreate)
{
piece_x = pie
ce;
switch (piece)
{
case 0 : _(&quot;mv&quot;).style.width = (2*wx)+&quot;px
&quot;;_(&quot;mv&quot;).style.height = (1*hx)+&quot;px&quot;; break;
case 1 : 
_(&quot;mv&quot;).style.width = (1*wx)+&quot;px&quot;;_(&quot;mv&quot;).style.he
ight = (2*hx)+&quot;px&quot;; break;
case 2 : _(&quot;mv&quot;).style.width = (
3*wx)+&quot;px&quot;;_(&quot;mv&quot;).style.height = (1*hx)+&quot;px&quot;; bre
ak;
case 3 : _(&quot;mv&quot;).style.width = (1*wx)+&quot;px&quot;;_(&quot;mv&q
uot;).style.height = (3*hx)+&quot;px&quot;; break;
}
}
}

function dispo2ht
ml(dd,level)
{
nbmove=0;
/*background du jeu*/
htmx=&quot;Niveau&lt;select o
nchange='difficulte(this.value)'&gt;&quot;;
niveau_jeu = {&quot;debutant&quot;:
&quot;debutant&quot;,&quot;inter&quot;:&quot;intermedaire&quot;,&quot;avance&quo
t;:&quot;avancé&quot;,&quot;expert&quot;:&quot;expert&quot;};
for (e in niveau_
jeu)
	htmx+=&quot;&lt;option &quot;+(e==diff ? &quot;selected&quot;:&quot;&quot
;)+&quot; value='&quot;+e+&quot;'&gt;&quot;+niveau_jeu[e]+&quot;&lt;/option&gt;&
quot;;
htmx+=&quot;&lt;/select&gt;&amp;nbsp;&amp;nbsp;&amp;nbsp;puzzle N°&lt;b&
gt;&quot;+level+&quot;&lt;/b&gt;&lt;br/&gt;&lt;br/&gt;&quot;;
htmx+=&quot;&lt;t
able id='tablo' cellspacing=0 cellpadding=0 class='tableback'&gt;&quot;;
for (y
=0;y&lt;6;y++)
{
	htmx+=&quot;&lt;tr&gt;&quot;;
	for (x=0;x&lt;6;x++)	
	{
	
	htmx+=&quot;&lt;td style='width:&quot;+(wx-1)+&quot;px;height:&quot;+(hx)+&quot
;px;border-right:1px #c0c0c0 dashed;border-bottom:1px #c0c0c0 dashed;'&gt;&amp;n
bsp;&lt;/td&gt;&quot;;
	}
	htmx+=&quot;&lt;/tr&gt;&quot;;
}
htmx+=&quot;&lt;
/table&gt;&quot;;
htmx+=&quot;&lt;b&gt;&quot;+msg('nb_move')+&quot;&lt;/b&gt;&l
t;input type=text id='nbmve' value='0' style='text-align:right;border:none;width
:40px;background:none;'&gt;&quot;;
_(&quot;tableau&quot;).innerHTML =htmx;
/*r
ecup position tableau -&gt; passer en relative*/
posxy_=posxy(_(&quot;tablo&quo
t;),dxx,dyy);

htmx=&quot;&quot;;
/*tableau de liaison de mouvement + piece*/

for (x=0;x&lt;6*6;x++)
{
cart[x]={c:0,h:(x&gt;=6)?x-6:-1,b:(x&lt;5*6)?x+6:-1
,g:(x%6==0)?-1:x-1,d:(x%6==5)?-1:x+1,m:x};
}

/*place les pièces*/
for (f in
 dd)
{
	if (/[0-9]+/.test(f))
	{
	p = parseInt(f,10);	idx=(p+1);
	type_=dd[
p]; /*type de pièce*/
	cart[p].c=idx;
	 switch(type_)
	 {
		case 0: w=2; h=1
;cart[p+1].c=idx; break;
		case 1: w=1; h=2;cart[p+6].c=idx; break;
		case 2: 
w=3; h=1;cart[p+1].c=idx;cart[p+2].c=idx; break;
		case 3: w=1; h=3;cart[p+6].c
=idx;cart[p+12].c=idx; break;
		case 4: w=2; h=1;cart[p+1].c=idx; break;		
	 }

	 var corr = window.Event ? 2 : 1; /*corrige la taille du tableau pr IE &amp; 
FF*/
	htmx+=&quot;&lt;div id='&quot;+&quot;p_&quot;+p+&quot;' class='block&quot
;+type_+&quot;' style='width:&quot;+((w*wx)-corr)+&quot;px;height:&quot;+((h*hx)
-corr)+&quot;px;left:&quot;+(posxy_.x+(p%6)*wx)+&quot;px;top:&quot;+(posxy_.y+(p
arseInt(p/6,10))*hx)+&quot;px;position : absolute;' onmousedown='choix(this,&quo
t;+idx+&quot;,&quot;+type_+&quot;,event);return false;'&gt;&lt;/div&gt;&quot;
 
   }
}
if (modecreate)
{
 htmx+=&quot;&lt;div id='mv' class='block0' style='
position:absolute;width:&quot;+(2*wx)+&quot;px;height:&quot;+(hx)+&quot;px;' onc
lick='posMe(event)'  &gt;&lt;/div&gt;&quot;;
}
/*affiche le tableau*/
_(&quot
;tableau&quot;).innerHTML += htmx;

if (modecreate)
{
  htm=&quot;&lt;br/&gt
;{&quot;;first=true;
 for (e in nivo[&quot;nvx&quot;]) {htm+=(first?&quot;&quot
;:&quot;,&quot;)+e+&quot;:&quot;+nivo[&quot;nvx&quot;][e];first=false;}
 htm+=&
quot;}&quot;;
_(&quot;deb_&quot;).innerHTML = htm;
}
/*************Info debug

htm=&quot;&lt;table&gt;&quot;; for(y=0;y&lt;6;y++){htm+=&quot;&lt;tr&gt;&quot;
;for (x=0;x&lt;6;x++){htm+=&quot;&lt;td&gt;&quot;+cart[y*6+x].c+&quot;&lt;/td&gt
;&quot;;}htm+=&quot;&lt;/tr&gt;&quot;;}
htm+=&quot;&lt;/table&gt;&quot;;_(&quot
;deb_&quot;).innerHTML=htm;*/
selpiece(piece_x);
bougeMe = true;
}

/*selec
tion d'une pièce (onclick)*/
function choix(src,p,type_,evt)
{
if (bougeMe)

{
  var x = document.all ? event.clientX : document.layers ? evt.x : evt.client
X;
  var y = document.all ? event.clientY : document.layers ? evt.y : evt.clien
tY;
ss={&quot;src&quot;:src,&quot;idx&quot;:p,&quot;sens&quot;:(type_==1 || typ
e_==3),&quot;cx&quot;:type_,&quot;ox&quot;:( parseInt(src.style.left,10)),&quot;
oy&quot;: (parseInt(src.style.top,10)),&quot;dx&quot;:x,&quot;dy&quot;: y};
}

}

function posMe(evt)
{
if (modecreate)
	{
	  var x = document.all ? even
t.clientX : document.layers ? evt.x : evt.clientX;
	  var y = document.all ? ev
ent.clientY : document.layers ? evt.y : evt.clientY;
	  var posxy_=posxy(_(&quo
t;tablo&quot;),dxx,dyy);	
	  var fx = Math.round((x-posxy_.x)/wx),fy = Math.rou
nd((y-posxy_.y)/hx);
	  var mx = [5,6,4,6], my = [6,5,6,4];
	  if (fx&gt;=0&am
p;&amp;fx&lt;mx[piece_x]&amp;&amp;fy&gt;=0&amp;&amp;fy&lt;my[piece_x]) 
	  { p 
= fy*6+fx; 
	    var test = cart[p].c == 0 ;
	    switch(piece_x)
		{
		case
 0: test&amp;=cart[p+1].c==0;  break;
		case 1: test&amp;=cart[p+6].c==0; break
;
		case 2: test&amp;=(cart[p+1].c==0)&amp;(cart[p+2].c==0); break;
		case 3: 
test&amp;=(cart[p+6].c==0)&amp;(cart[p+12].c==0); break;		
		}
		if (test) {ni
vo[&quot;nvx&quot;][p]=piece_x; afficheBloc(&quot;nvx&quot;) }
	  }
	}
}
/*d
eplacement de la pièce (onmouve)*/
function bouge(mx,my)
{
/*_(&quot;deb_&quo
t;).innerHTML=mx+&quot; - &quot;+my; //debug sur les corrdonnées de la souris*/

if (ss!=null) /*bouge si pièce sélectionné*/
{
if (ss.sens) /*deplacement hor
izontal ou vertical ?*/
  {
  /*deplacement vertical*/
  delta = (my-ss.dy); 
/*différence entre la souris et la position de départ*/
  if (!ss.miny) /*initi
alisation de l'amplitude du mouvement si pas encore calculé*/
  {
  slc = pars
eInt(ss.idx,10);
  /*recup la pièce*/
  x=0; while ((x&gt;6*6)|(cart[x].c!=slc
)) {x++;}
  /*recherche des zone vide avant &amp; après*/
  r=0;   f=parseInt(
cart[x].h,10);  while  (f!=-1 &amp;&amp; cart[f].c==0) {r++;  f=parseInt(cart[f]
.h,10);}
  ss.miny = -r*hx;
  r=0;  f=parseInt(cart[x].b,10);  while  (f!=-1 &
amp;&amp; ((cart[f].c==0) || (cart[f].c==slc)) ) {if (cart[f].c==0) {r++;}  f=pa
rseInt(cart[f].b,10); }
  ss.maxy = r*hx;
  }
      
  test = (delta&gt;ss.m
iny&amp;&amp;delta&lt;ss.maxy) ;
  if (test)   /*souris en dehors du mouvement 
?*/
	{
	ss.src.style.top = parseInt(my-ss.dy+ss.oy)+&quot;px&quot;;
	fy = Mat
h.round(delta / hx); /*coordonnée relative au tableau cart*/
	ss.fy = fy;

	}
 else
	{
	if (delta&lt;ss.miny) delta = ss.miny ; /*limite de déplacement*/
	
if (delta&gt;ss.maxy) delta = ss.maxy ;
	
	fy = parseInt(delta / hx,10);
	ss.
fy = fy;
	ss.src.style.top = parseInt(fy*hx + ss.oy)+&quot;px&quot;;
	//releas
e(null);
	}
  }
  else
  {
  /***************************/
  /*deplacement
 horizontal*/
  delta = (mx-ss.dx);
  if (!ss.minx) /*initialisation de l'ampl
itude du mouvement*/
  {
  /*pièce séctionnée*/
  slc = parseInt(ss.idx,10);

  x=0; while ((x&gt;6*6)|(cart[x].c!=slc)) {x++;}
  /*recherche zone vide avan
t &amp; aprés*/
  r=0;   f=parseInt(cart[x].g,10);  while  (f!=-1 &amp;&amp; ca
rt[f].c==0) {r++;  f=parseInt(cart[f].g,10);}
  ss.minx = -r*wx;
  r=0;  f=par
seInt(cart[x].d,10);  
  while  (f!=-1 &amp;&amp; ((cart[f].c==0) || (cart[f].c
==slc)) ) {if (cart[f].c==0) {r++;}  f=parseInt(cart[f].d,10); }
  ss.maxx = r*
wx;
  }
  /*test si souris en dehors de la zone*/
  test = (delta&gt;ss.minx&
amp;&amp;delta&lt;ss.maxx) ;
  if (test)
	{
	ss.src.style.left = parseInt(mx-
ss.dx+ss.ox)+&quot;px&quot;;
	fx = Math.round(delta / wx);
	ss.fx = fx;
	} el
se
	{
	if (delta&lt;ss.minx) delta = ss.minx;
	if (delta&gt;ss.maxx) delta = 
ss.maxx;
	
	fx = parseInt(delta / wx,10);
	ss.fx = fx;
	ss.src.style.left = 
parseInt(fx*wx + ss.ox)+&quot;px&quot;;
	//release(null);
	}
  }
}

visib 
= false;
if (modecreate &amp;&amp; ss==null)
{
  var posxy_=posxy(_(&quot;tab
lo&quot;),dxx,dyy);	
  var fx = Math.round((mx-posxy_.x)/wx),fy = Math.round((m
y-posxy_.y)/hx);
  var maxx = [5,6,4,6], maxy = [6,5,6,4];
  if (fx&gt;=0&amp;
&amp;fx&lt;maxx[piece_x]&amp;&amp;fy&gt;=0&amp;&amp;fy&lt;maxy[piece_x]) 
  {

    p=fy*6+fx;
	visib = cart[p].c == 0 ;
	switch(piece_x)
	{
	case 0: visib&
amp;=cart[p+1].c==0;  break;
	case 1: visib&amp;=cart[p+6].c==0; break;
	case 
2: visib&amp;=(cart[p+1].c==0)&amp;(cart[p+2].c==0); break;
	case 3: visib&amp;
=(cart[p+6].c==0)&amp;(cart[p+12].c==0); break;		
	}   
  }
}

if (visib)

{
_(&quot;mv&quot;).style.visibility=&quot;&quot;;
_(&quot;mv&quot;).style.lef
t = (mx-2)+&quot;px&quot;;
_(&quot;mv&quot;).style.top = (my-2)+&quot;px&quot;;

} else
{
if (modecreate)
 {_(&quot;mv&quot;).style.visibility=&quot;hidden&
quot;;}
}
}
/*relache la pièce (onmouseup)*/
function release(e)
{
if (ss!
=null)
{
  /*récupère la pièce*/
  x=0; while ((x&gt;6*6)|(cart[x].c!=ss.idx)
) {x++;}
  /*vide le tableau de sa position*/
  for (k=0;k&lt;6*6;k++) if (car
t[k].c==ss.idx) cart[k].c=0;
  /*replace la pièce dans les nouvelles coordonnée
s*/
  fx=0 ; fy = 0;   if (ss.fx != null) fx = ss.fx;  if (ss.fy != null) fy = 
ss.fy;
  if (fx!=0||fy!=0) {nbmove++;_(&quot;nbmve&quot;).value=nbmove;}
  p=x
+fx+fy*6;
  x=ss.idx;
  cart[p].c=x;
  type_ = nivo[level_x][x-1];
	 switch(
type_)
	 {
		case 0: cart[p+1].c=x; break;
		case 1: cart[p+6].c=x; break;
	
	case 2: cart[p+1].c=x;cart[p+2].c=x; break;
		case 3: cart[p+6].c=x;cart[p+12]
.c=x; break;
		case 4: cart[p+1].c=x; break;		
	 }
posxy_=posxy(_(&quot;tablo
&quot;),dxx,dyy);	 
ss.src.style.left = (posxy_.x+(p%6)*wx)+&quot;px&quot;;
ss
.src.style.top = (posxy_.y+(parseInt(p/6,10))*hx)+&quot;px&quot;;
/*si la pièce
 principale est positionnée sur la sortie*/
if (type_==4&amp;&amp;p==16&amp;&am
p;!modecreate) {clearLevel();bougeMe=false;}
if (modecreate) { 
//alert(type_)
;
var rc = {} ; 
for (e in nivo['nvx']) 
{ if (e!=(x-1)) rc[e]=nivo['nvx'][e]
;}
rc[p] = ss.cx ; 
nivo['nvx']=rc;
}
}
	ss=null;
}
/*fin du niveau - aff
iche le score*/
function clearLevel()
{
posxy_=posxy(_(&quot;tablo&quot;),dxx
,dyy);	 
var score = 2500-nbmove*40;
score = (score&lt;500) ? 500 : score;
ht
m = &quot;&lt;div class='scoring' style='position:absolute;left:&quot;+(posxy_.x
+50)+&quot;px;top:&quot;+(posxy_.y+50)+&quot;px;' &gt;&quot;;
htm+= &quot;&lt;b
&gt;&quot;+msg('stage_clear')+&quot;&lt;/b&gt;&lt;br/&gt;&quot;;
htm+= &quot;&l
t;b&gt;&quot;+msg('score')+&quot;&lt;/b&gt; : &quot;+score+&quot;&lt;br/&gt;&quo
t;;
//htm+= &quot;&lt;b&gt;&quot;+msg('nb_move')+&quot;&lt;/b&gt; : &quot;+nbmo
ve+&quot;&lt;br/&gt;&quot;;
htm+= &quot;&lt;/div&gt;&quot;;
_(&quot;tableau&qu
ot;).innerHTML += htm;
_(&quot;nbmve&quot;).value=nbmove;
scoretab[level_x]={&
quot;score&quot; : score , &quot;mvt&quot; : nbmove };
save_cok(scoretab,diff);

viewLevel();
}

/*déplacement de la souris (onmousemove)*/
function bouger
Souris (evt) {
  var x = document.all ? event.clientX : document.layers ? evt.x
 : evt.clientX;
  var y = document.all ? event.clientY : document.layers ? evt.
y : evt.clientY;
  bouge(x,y);
}

/*mouse move full compatible - capture des
 evenements*/
if (document.layers)  document.captureEvents(Event.MOUSEMOVE | Ev
ent.MOUSEUP );
if (document.layers || document.all)  
	{
	document.onmousemov
e = bougerSouris;
	document.onmouseup = release;
	}
if (document.addEventList
ener)   
	{
	document.addEventListener('mousemove', bougerSouris, true);
	doc
ument.addEventListener('mouseup', release, true);
	}
  
 /*init le programme 
au lancement*/
//window.onload = function() {load();}

/*retourne la position
 en {x,y} d'un element */
function posxy(rst,xx,yy) 
 { return rst ? posxy(rst
.offsetParent,xx+rst.offsetLeft,yy+rst.offsetTop): {&quot;x&quot;:xx,&quot;y&quo
t;:yy}; }
 
 
window.onload = function()
{
_(&quot;nvxGrille&quot;).value= 
msg('nvx_grille');
diff = &quot;debutant&quot;;
difficulte(diff);
} 

&lt;/
script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;br/&gt;&lt;br/&gt;
&lt;center&gt;&
lt;b&gt;Deblock Me V0.8&lt;/b&gt;&lt;br/&gt;&lt;br/&gt;&lt;input type=&quot;butt
on&quot; id=&quot;nvxGrille&quot; value=&quot;new&quot; onclick=&quot;afficheBlo
c('nvx');&quot; disabled &gt;&lt;br/&gt;&lt;br/&gt;

&lt;table&gt;&lt;tr&gt;&l
t;td&gt;&lt;div id=&quot;level&quot; style='margin:0px;'&gt;&lt;/div&gt;&lt;/td&
gt;&lt;td&gt;&lt;div id=&quot;tableau&quot; style='margin:0px;'&gt;&lt;i&gt;Load
ing...&lt;/i&gt;&lt;/div&gt;&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;
&lt;div id=&qu
ot;deb_&quot; style='margin:0px;'&gt;&lt;/div&gt;&lt;!--debug--&gt;
&lt;br/&gt;
&lt;br/&gt;&lt;br/&gt;
&lt;div style=&quot;font-family:Tahoma;font-size:9px&quo
t;&gt;dernière mise à jour sur mon site : &lt;a href=&quot;<a href='http://www.c
rew.free.fr' target='_blank'>http://www.crew.free.fr</a>&quot;&gt;<a href='http:
//www.crew.free.fr&lt;/a&gt;&lt;br&gt;powered' target='_blank'>http://www.crew.f
ree.fr&lt;/a&gt;&lt;br&gt;powered</a> by &lt;b&gt;AmRouNiX&lt;/b&gt; / &lt;b&gt;
MaSTeR-KiLLeR&lt;/b&gt; (&lt;i&gt;A. Selim&lt;/i&gt;) &lt;br&gt; Toutes copies a
utorisées !&lt;/div&gt;
&lt;script language=&quot;javascript&quot; src=&quot;js
/debutant.js&quot;&gt;&lt;/script&gt;
&lt;script language=&quot;javascript&quot
; src=&quot;js/intermediaire.js&quot;&gt;&lt;/script&gt;
&lt;script language=&q
uot;javascript&quot; src=&quot;js/avance.js&quot;&gt;&lt;/script&gt;
&lt;script
 language=&quot;javascript&quot; src=&quot;js/expert.js&quot;&gt;&lt;/script&gt;

&lt;script language=&quot;javascript&quot; src=&quot;js/extra.js&quot;&gt;&lt;
/script&gt;
&lt;/center&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
