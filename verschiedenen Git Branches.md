Ich möchte zwei branches parallel mit Änderungen versorgen. Im ``master`` ist die Version für Zikula 2.0.x enthalten und ein zweiter Branch enthält die Version für Zikula 1.5.x, hier ``zk1.5.x`` genannt.

Den folgenden Tipp habe ich erhalten und möchte ihn mir hier merken.


# A. Vorbereitung
Du musst Git einmal sagen, dass beide Branches auf dem selben Stand sind, trotz unterschiedlicher Codebase.

1. git checkout master
2. alle Dateien (2.x) irgendwo hin kopieren 
3. git merge zk1.5.x 
4. git checkout zk1.5.x
5. alle Dateien (1.5.x) löschen 
6. alle Dateien vom Backup (2.x) reinkopieren 
7. git commit -a (Merge-Commit sagt Git: Konflikte behoben) 
8. git push

# B. Wenn nun etwas in beiden Branches gemacht werden soll:

1. git checkout zk1.5.x
2. Änderungen durchführen
3. git commit -a -m "my super change"
4. git push
5. git checkout master
6. git merge zk1.5.x
7. git commit -a
8. git push

# C. Wenn nun etwas nur in 1.5.x gemacht werden soll:

1. git checkout zk1.5.x
2. Änderungen durchführen
3. git commit -a -m "my super change"
4. git push
5. git checkout master
6. git merge zk1.5.x
7. Änderungen zurücknehmen
8. git commit -a
9. git push

# D. Wenn nun etwas nur in 2.x gemacht werden soll:

1. git checkout master
2. Änderungen durchführen
3. git commit -a -m "my super change"
4. git push

# Git Console und VIM

Alle Befehle müssen auf der Git Console inegegeben werden. Startet dann einmal der VIM, kann man die Message für den Merge ändern. Raus kommt man mit ``:x``

