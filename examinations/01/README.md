# Examination 1 - Understanding SSH and public key authentication

Connect to one of the virtual lab machines through SSH, i.e.

    $ ssh -i deploy_key -l deploy webserver

Study the `.ssh` folder in the home directory of the `deploy` user:

    $ ls -ld ~/.ssh

Look at the contents of the `~/.ssh` directory:

    $ ls -la ~/.ssh/

## QUESTION A

What are the permissions of the `~/.ssh` directory?

Why are the permissions set in such a way?

Svar: Bara skaparen av directoryn har permissions (drwx, directory, read, write och execute), alla andra har inga dvs.

## QUESTION B

What does the file `~/.ssh/authorized_keys` contain?

Svar: Den har alla nycklar för att kunna accessa ssh just nu är det bara deploy.

## QUESTION C

When logged into one of the VMs, how can you connect to the
other VM without a password?

Svar: Jag skapade en ny nyckel i cd .ssh ssh-keygen -t ed25519 -C newkeywithoutpassword. Lämnade lösenordsfältet tomt så det inte fanns ett. Sedan la jag in nyckeln i både webserver och db servers authorized keys. Därefter kunde jag med kommandot ssh deploy@ip gå in på dem utan ett lösenord. Gjorde en till nyckel för båda utan lösenord och gav varandra deras nya, efter det kunde jag byta mellan dem utan lösenord.


### Hints:

* man ssh-keygen(1)
* ssh-copy-id(1) or use a text editor

## BONUS QUESTION

Can you run a command on a remote host via SSH? How?

Svar: Ja det går, man använder ssh deploy@ip "kommandot du vill köra"

Exempel ssh deploy@192.168.121.117 "ls /.ssh"