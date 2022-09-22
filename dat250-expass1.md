The first steps of the Heroku guide started well, however when reaching the point of local postgres integration i slew of problems arose.
Firstly the psql command, and heroku pg:psql did not work. Apon further inspection i realised that the data folder of the postgres install folder was empty.
After reinstalling the problem was fixed. However now it asked for a password when the command psql was typed in the command prompt.
After typing in the password i got an error saying password authentication failed. After reinstalling again to reset the password for the second time it worked.
However when trying to create a new database postgres didnt seem to respond. After realising i can use the default database i struggled to figure out what the .env file was supposed to be, but after a while i managed to get that to work. After this everything went all right.

Note: The /hello, did for some reason not work as they described it, although i followed it step by step, but i just skipped fixing this.

The app is now deployed on Heroku. I was also able to deploy it locally, verifying it on localhost:5000.

Link https://polar-basin-20533.herokuapp.com/
