# Android notes

---

view = element (button,..)
layout= page/interface
activité = composant (ensemble des elements)

findviewbyid always before setContextView ...
order is highly important

concatination : do not use +
%1$s : variable 1 of String TYPE
%2$f : variable 2 of float TYPE

toast == notification (temporel msg)
	toast.LENGTH_LONG (takes up to 2.5 SECONDS)
	toast.LENGTH_SHORT (takes up to 1.5 SECONDS)

callback function: related to an event listner, and called when an event is executed

---

### life cycle:

onStart() : display only without the ability to interact
onResume() : activate interaction with layout/view...
onPause() : mise en veille l'activité 
onStop() : arreter l'activité, 
onDestroy() : depiler l'activité, end processus 

in Manifest file:  
	- display first activity "main activity" : the one that the app start with.

---

intend == routing to an activity
	intend (explecit) == change to an activity of the same app
	intend (implecit) == change to an activity of another app  
	