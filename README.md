# ACNR---Task-Quest1-reqruitment
Before ACNR started challenge recruitment there were only one task which now is called 
quest1 but before it was only this simple task without challenge. You have to decrypt 
encrypted message and doing next stuff like, decode base64, next scanning IP which was 
and finding magic port which is randomly generated every few minutes, next downloading with 
nc png file which we can check by simpy listening with nc. Another part png file is and qr 
code, thanks to it we have last task. Login to the website without creds. First the login we 
can find in code of website and there's a password part admin'or'1'='1. You can check this by 
executing exploit.py script or solution.py script.

The script have some additional libraries like: QR, webbrowser and maybe mechanize and requests(but for these
two I'm not sure) so without it you will not execute this script. Another thing:
you can use python below 3.x.x version.
https://raw.githubusercontent.com/WolfMan12333/ACNR---Task-Quest1-reqruitment/master/mail/2.jpeg



and last task screen:
https://raw.githubusercontent.com/WolfMan12333/ACNR---Task-Quest1-reqruitment/master/3.jpeg

Today with first part of challenge you have new part with flag, after decrypting:
//McKittrick leaderboard dot acnr dot se flag 09EbeMmIxhZetcAtMlghY9Pq


