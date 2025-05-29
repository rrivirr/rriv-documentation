# Joplin Notes

We are trying out sharing a synced Joplin account as a way to more easily share loosely notes about topics we are exploring, building, and debugging. \
\
\## Setup

1. Install Joplin [https://joplinapp.org/help/install/](https://joplinapp.org/help/install/)
2. Get access to the S3 sync credentials (in Proton Pass)
3. Open Joplin, and from the file menu...
   1. Choose 'switch profile'
   2. Choose 'create new profile'
   3. Name your profile 'RRIV Notes'
4. Click 'Synchronize' in the lower left hand corner of the app
   1. A popup screen will appear
   2. At the bottom of the screen, there is text that mentions 'Self Hosting' and gives a link.
   3. Click this link ![](../../.gitbook/assets/image.png)
5. For 'Sychronization Target' select S3
6. Enter the credentials provided in (2)
7. Click 'Check sychronization settings'
8. Click 'Apply'
9. Go to Tools > Options > Encryption and enter the password (also in Proton Pass)
10. You are done, the shared notes should sync now.



In this case we are sharing a single Joplin notebook sychronization, which is different from the Joplin 'Shared Notebooks' feature, which requires a paid account.  The downside is that if you use Joplin for other notebooks, you can't view the RRIV Notes notebooks at the same time - because you have to be on the Joplin profile you created in (3c).   Joplin has a workaround for this inconvenience which is the unique 'Open Secondary App Instance' option in the File menu.   You can set up a profile in the 'secondary' app instance to sync the RRIV notes, while still using Joplin in your preferred way in the main instance. &#x20;



