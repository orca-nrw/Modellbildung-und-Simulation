---
redirect_from:
  - "/00-einleitung/usage"
interact_link: content/00_einleitung/usage.ipynb
kernel_name: octave
title: 'Verwendung des Buches'
prev_page:
  url: /00_einleitung/intro
  title: 'Einleitung'
next_page:
  url: /00_einleitung/matlab_00_first_steps
  title: 'Erste Schritte in Matlab'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Verwendung dieses Buches

Ganz einfach: Lesen. Es gibt aber ein paar zusätzliche Features, die hier erklärt werden. Es wird auch darauf eingegangen, welche Software für diese features verwendet wird. Das soll nur als Zusatzinformationen dienen und ist für die Verwendung des Online Buches nicht relevant.

Alle Seiten, die Codeblöcke enthalten haben oben in der Kopfzeile zwei Buttons, einen auf dem "Thebelab" steht, und einen auf dem "Interact" steht.

<img src="../images/usage_buttons.png" alt="Interact buttons" style="width: 250px;"/>

Beide Buttons bewirken auf unterschiedliche Weise, dass der Matlab-Code in den Code-Blöcken editierbar und ausführbar wird. Im Hintergrund wird in einer virtuellen Maschine ein Octave Kern gestartet. Octave ist ein freier Matlab-Klon, der weitestgehend mit Matlab kompatibel ist.

## Thebelab

Die einfachste Möglichkeit, den Code auf dieser Seite zu editieren und auszuführen ist über Thebelab. Per Klick auf die Taste "run", wird der Code ausgeführt, mit "restart" wird der im Hintergrund laufende Octave-Kernel neu gestartet.

<img src="../images/usage_thebe.png" alt="Binder Loading Page" style="width: 800px;"/>

## Interact

Der Nachteil von der "Interact"-Methode ist, dass man von dieser Seite weggeführt wird. Der Vorteil ist, dass man auf die Inhalte über [Jupyter Lab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) zugreifen kann, eine Art Entwicklungsumgebung die im Browser läuft. 

<img src="../images/usage_binder.png" alt="Jupyter Lab Screenshot" style="width: 1200px;"/>

<img src="../images/usage_binder_launcher.png" alt="Jupyter Lab Screenshot 2" style="width: 1200px;"/>


Sie können nicht nur die Code-Blöcke editieren und ausführen, sie können auch neue Dokumente, wie z.B. m-files, erstellen oder hochladen, Dokumente herunterladen und eine Linux-Konsole starten. Das ganze funktioniert über ein [Docker-Container](https://de.wikipedia.org/wiki/Docker_(Software)), der über den [Binder](https://mybinder.org/) Service geladen wird. 

<img src="../images/attention.svg" alt="" style="width: 25px; display: inline;" />    **Wichtig: Das bedeutet insbesondere, dass alle erstellten Dateien und Änderungen nur temporär sind und nicht über eine Session hinaus erhalten bleiben!** Laden Sie unbedingt erstellte Dateien runter, bevor sie das Fenster schließen, oder noch besser, erstellen Sie Dateien offline auf ihren Computer und laden Sie sie hoch, wenn Sie sie in einer interaktiven Session verwenden möchten.

## Dateien erstellen

In Jupyter Lab ("Interact" Button), lassen sich Dateien mit Hilfe des Launchers erstellen. Man kann aber auch Dateien mit der Thebelab Funktionalität erstellen. Wenn ein Code-Block mit der Zeile `%%file myfile.m` beginnt, wird der folgende Inhalt des Blocks in eine Datei `myfile.m` geschrieben. Dies ist insbesondere nützlich um Funktionen zu schreiben, da in Matlab Funktionen immer in eigenen Dateien gespeichert werden müssen, oder erst am Ende eines Skriptes stehen dürfen.



{:.input_area}
```matlab
%%file hello_world.m
function hello_world()
for i=1:5
    disp('Hello World, how is your day?')
end
```


{:.output .output_stream}
```
Created file '/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/hello_world.m'.

```



{:.input_area}
```matlab
run hello_world
```


{:.output .output_stream}
```
Hello World, how is your day?
Hello World, how is your day?
Hello World, how is your day?
Hello World, how is your day?
Hello World, how is your day?

```

<img src="../images/attention.svg" alt="" style="width: 25px; display: inline;" /> **Auch hier gilt, dass nur temporäre Dateien angelegt werden können, die die aktuelle Session nicht überleben.**

## Unit Testing

[*Unit Testing*](http://lmgtfy.com/?q=unit+testing) ist aus moderner Software-Entwicklung nicht mehr wegzudenken. Sobald ein Software-Paket etwas größer wird und aus einer Vielzahl von Modulen, Bibliotheken, Funktionen und Skripten besteht, sollte regelmäßig getestet werden, ob die Module noch so funktionieren wie erwartet. Unit Tests sind im wesentlichen kleine Programme, die diese Module auf ihrer Funktionsfähigkeit prüfen. Ein weit verbreitetes [Programmierparadigma](https://de.wikipedia.org/wiki/Testgetriebene_Entwicklung) besagt sogar, dass man erst die Unit Tests schreiben soll, bevor man das Modul erstellt. 

Auch Matlab und Octave bieten Möglichkeiten für Unit Tests an. Leider sind die jeweiligen Toolboxen von Octave und Matlab nicht kompatibel zu einander. Daher wird an dieser Stelle [MOxUnit](https://de.mathworks.com/matlabcentral/fileexchange/54417-moxunit) verwendet. MoXUnit ist ein freies open source unit testing framework, das sowohl mit Matlab als auch Octave funktioniert.

Für die meisten Übungsaufgaben auf dieser Seite müssen Matlabfunktionen erstellt werden. Auf dieser Seite werden für diese Übungsaufgaben bereits fertige Unit Tests zur Verfügung gestellt, mit der die eigens erstellten Funktionen auf ihre Richtigkeit überprüft werden können.

### Unit Tests auf dieser Seite ausführen

Wenn für eine Übungsaufgabe ein Unit Test zur Verfügung steht, dann wird das an der entsprechenden Stelle explizit erwähnt. Angenommen die Übungsaufgabe besteht darin, eine Funktion `fac` zu schreiben, die die Fakultät $n!$ einer Zahl $n$ berechnet. Der Einfachheit halber schreiben wir einen Wrapper für die von Matlab zur Verfügung gestellt Funktion `factorial`, ungeachtet dessen, dass es dem Zweck der Übungsaufgabe nicht so richtig gerecht wird:



{:.input_area}
```matlab
%%file fac.m
function r = fac(n)
% wrapper for Matlabs factorial function
    r = factorial(n);
```


{:.output .output_stream}
```
Created file '/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/fac.m'.

```

Die bereitgestellten Unit Tests befinden sich in der Datei `test_fac.m`. Diese Tests überprüfen ob die Funktion sich so verhält wie erwartet. Der Test wird mit folgendem Befehl ausgeführt:



{:.input_area}
```matlab
moxunit_runtests test_fac.m
```


{:.output .output_stream}
```
suite: 6 tests
......
--------------------------------------------------

OK (passed=6)
ans = 1

```

Aha, es gab also sechs Tests, und die werden alle von `fac`, bzw. der von Matlab zur Verfügung gestellten Funktion `factorial`, erfüllt. Super! 

Das war allerdings auch etwas geschummelt. Wir probieren eine etwas andere Implementierung der Funktion:



{:.input_area}
```matlab
%%file fac.m
function r = fac(n)
% calculates the factorial of the input n
    r = prod(1:n);
```


{:.output .output_stream}
```
Created file '/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/fac.m'.

```

Mal sehen, ob immer noch alle Tests durchlaufen:



{:.input_area}
```matlab
moxunit_runtests test_fac.m
```


{:.output .output_stream}
```
suite: 6 tests
...FFF
--------------------------------------------------

failure: No exception was raised
  assertExceptionThrown:84 (/home/jan/tools/MOxUnit/MOxUnit/assertExceptionThrown.m)
  test_fac>test_fac_exception_negative:31 (/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/test_fac.m)

failure: No exception was raised
  assertExceptionThrown:84 (/home/jan/tools/MOxUnit/MOxUnit/assertExceptionThrown.m)
  test_fac>test_fac_exception_noninteger:35 (/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/test_fac.m)

failure: inputs are not of the same size

First input: 1x1 double
1

Second input: 2x3 double
[1 1 2;6 24 120]
  assertEqual:70 (/home/jan/tools/MOxUnit/MOxUnit/assertEqual.m)
  test_fac>test_fac_array:39 (/data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/test_fac.m)

--------------------------------------------------

FAILED (passed=3, failure=3)
ans = 0

```

Ok, drei der Tests sind erfolgreich, drei schlagen fehl. Die Test Suite gibt Auskunft darüber, welche der Tests fehlschlagen. Die Ausgabe

```
suite: 6 tests
...FFF
--------------------------------------------------
```

bedeutet, dass die letzten drei Tests fehlgeschlagen sind. Zusätzlich gibt jeder fehlgeschlagene Tests Informationen darüber aus, welches Verhalten erwartet wurde und welches tatsächlich eingetroffen ist. Manchmal sind diese Ausgaben etwas kryptisch, und es lohnt sich einen Blick in die Implementierung der Tests zu werfen. Mit dem Befehl `type` lässt sich der Inhalt einer Datei in Matlab wiedergeben. Das können wir benutzen um uns die sechs Tests in `test_fac.m` genauer anzuschauen:



{:.input_area}
```matlab
type test_fac.m
```


{:.output .output_stream}
```
test_fac.m is the user-defined function defined from: /data/work/H_BRS/Modellbildung-und-Simulation/content/00_einleitung/test_fac.m

function test_suite=test_fac
% initialize unit tets
    try
        test_functions=localfunctions();
    catch
    end
    initTestSuite;

%%%%%%%%%%%%%%%%%%%%%%%
%     Basic tests     %
%%%%%%%%%%%%%%%%%%%%%%%
    
function test_fac_0
% test if fac(0)==1
    assertEqual(fac(0),1);

function test_fac_1
% test if fac(1)==1
    assertEqual(fac(1),1);
    
function test_fac_5
% test if fac(5)==120
    assertEqual(fac(5),120);
    
%%%%%%%%%%%%%%%%%%%%%%%
% More advanced tests %
%%%%%%%%%%%%%%%%%%%%%%%

function test_fac_exception_negative
% test if exceptions are thrown for negative values
    assertExceptionThrown(@()fac(-1));
    assertExceptionThrown(@()fac(1.5),'*');
    
function test_fac_exception_noninteger
% test if exceptions are thrown for noninteger values
    assertExceptionThrown(@()fac(1.5),'*');
    
function test_fac_array
% test if fac works on array inputs
    assertEqual(fac([0 1 2; 3 4 5]),[1 1 2; 6 24 120]);

```

Aha! Prinzipiell funktioniert die Funktion für nicht-negative ganzzahlige skalare Eingaben. Der Test erwartet aber zusätzlich, dass Fehler ausgegeben werden wenn die Eingabe negativ oder nicht ganzzahlig ist. Außerdem soll die Funktion für matrixwertige Eingaben funktionieren. Es wird erwartet, dass die Fakultät elementweise berechnet wird.

### Unit Tests offline ausführen.

* Installieren Sie [MOxUnit](https://de.mathworks.com/matlabcentral/fileexchange/54417-moxunit).
* Laden Sie sich den entsprechenden Unit Test von dieser Seite herunter. Wenn die Funktion die getestet werden soll `myFunction` heißt, ist der Unit Test in der Datei `test_myFunction.m` gespeichert. Sie können sich mit dem Befehl `type test_myFunction.m` den Inhalt der Datei wiedergeben lassen, oder mit dem "Interact"-Button eine interaktive Session starten und die Datei per Mausklick herunterladen.
* Führen Sie den Unit Test mit `moxunit_runtests test_myFunction.m` aus.

## Troubleshooting

Falls es Probleme oder Verbesserungsvorschläge gibt, freue ich mich über eine [Email](mailto:jan.kleinert@h-brs.de) oder noch besser, über einen Eintrag im [Issue tracker](https://github.com/joergbrech/Modellbildung-und-Simulation/issues) auf Github.

### Bekannte bzw. erwartete Probleme:

1. **Wenn ich auf `run` klicke, steht da nur `Waiting for kernel...` und nichts passiert.**

   <img src="../images/usage_waiting.png" alt="Drawing" style="width: 400px;"/>

   *Lösung:* Geduld. Wahrscheinlich wurden gerade Änderungen an diesem Buch vorgenommen und Sie sind die erste Person, die seitdem interaktive Inhalte nutzen wollen. Damit haben sie ein *rebuild des binder image getriggert*. Das kann schon mal eine Weile dauern. Dasselbe gilt für die "Interact" Funktion. Hier erhält man aber ausführlichere Informationen über eine Konsolenausgabe beim Start.
   
   <img src="../images/usage_binder_waiting.png" alt="Binder Loading Page" style="width: 1200px;"/>
   
1. **Wenn ich einen Code-Block starte, erhalte ich eine seltsame Fehlermeldung, die nicht nach Octave oder Matlab aussieht.**

   *Lösung:* Ab und zu wird der Code fälschlicherweise an einen *Python*-interpreter übergeben. In solchen Fällen hilft es, die Seite neu zuladen.
      
1. **Ich bin mir sicher, dass ich die Übungsaufgabe richtig bearbeitet habe, aber der Unit Test gibt Fehler aus.**

   *Lösung:* Möglicherweise wurde für die Bearbeitung der Übungsaufgabe Matlab-Code geschrieben, der nicht mit Octave kompatibel ist. In diesem Fall sollte es schon helfen, den Unit Test lokal in der eigenen Matlab Installation laufen zu lassen. 
