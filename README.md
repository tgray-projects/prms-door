# prms-door
## Powell River Makerspace Door Project

RFID door lock for our Makerspace

### Usage:
#### To enter:
1.  scan card at door
1.  door unlocks
1.  enter; door relocks after 15 seconds

#### To exit:
1.  scan card at door
1.  door unlocks
1.  exit; door relocks after 15 seconds

#### To add a new member:
1.  ssh into the raspberry pi
1.  `cd prms-door`
1.  `./writeCard.py` to get a list of possible users
1.  `./writeCard.py -h` to get a list of options (to replace a card for a user)
1.  `./writeCard.py memberId` to write a member's id to a card; follow on-screen instructions
1.  test the new card

## Setup (big picture, details to come):
1.  Check out from git
1.  Install the pigpio library from abyz.co.uk/rpi/pigpio/
1.  Install any other missing modules.  Note that we include a modified MFRC522 library.
1.  Change to be executable:
    chmod a+x door.py
    chmod a+x fetchMembers.py
    chmod a+x writeCard.py
1.  Connect card reader as documented on the internet - we use a standard connection.
1.  Connect the servo to GPIO pin 14, 5v, and ground.
1.  Add cron entries via `sudo crontab -e`
    @reboot pigpiod
    @reboot sleep 30 && /home/pi/prms-door/door.py &
    @daily  sleep 30 && /home/pi/prms-door/fetchMembers.py &

Required features:
1.  current access control (keys) still work (needs testing)
1.  ~~members can scan an rfid card/key fob; door unlocks~~
1.  ~~the door can be unlocked from inside~~
1.  ~~new members are added by entering the key card id into the member database manually~~

Optional features:
1.  door can be unlocked from inside without a rfid key/card
1.  ~~list of members is updated from our website~~
  * ~~non-paying members are removed from the list automatically~~
1.  there's a way to scan new members into the system
1.  the door knows it's open 
  * and won't lock until closed
  * and will alarm if left open, until a card is swiped
1.  there's a camera connected
  * that takes video when the card is swiped?
  * that takes video when the door is opened?
  * that allows people to see if there's anybody in the Makerspace
  * that can be used for training machine learning to see if there's anybody in the space
