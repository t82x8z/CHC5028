java cCHC5028 Software Development with
C/C++
Coursework
Important Dates
Week 10 (an available day in that week): Class test.
Week 12 (16/12/2024-20/12/2024): Project demonstration and viva assessment. Source 
codes file submission.
Background
“Text adventures”, now called “interactive fiction”, were among the first type of computer
game ever produced. These games have no graphics; the player reads the story of the
game in text, and decides what their character will do by typing commands at a prompt.
Although less popular now, text adventures are still played and created, and developed
into the original online RPGs (MUDs). You can play some sample modern text
adventures here:
Discworld MUD, BatMUD, 
These are playable online via a web browser. It is advisable to try out the games to get
an understanding of how the games behave.
For this coursework, you will be creating a simple game engine for a text adventure.
You are not required to write an actual adventure, only the back-end program code that
would support one. You will need to add some material to the program in order to test it,
but this may just be simple test material. You may add interesting descriptions or stories
to your program if you want to, but there are no marks for doing so.
You are provided with a CLion project containing a very simple game harness which
supports only two commands: going north (north or n), and quitting (quit). Extend it
by doing the exercises below. Note that the later exercises are less explicitly described
than the earlier ones, meaning that you must solve more problems yourself. This is
intentional.
The coursework is written to be built using gcc through CMake and CLion. It is not
recommended that you attempt to build it using Visual Studio or XCode.
Important: If you are building the sample coursework on a platform other than Windows, or 
on a machine which does not have the Windows API installed, you may get an error in the
file wordwrap.c. This file calls a Windows specific function to find thewidth of the console. If 
you get this error, remove the #include  fromthe top of the file, and edit
the initWordWrap() function by deleting its contents andreplacing them with 
consoleWidth = 80; currentConsoleOffset = 0;. You can change 80 here to any
number that makes the output comfortably readable.
Task 1 (10% of the mark)
In the current system, you can only move North. Extend the engine to allow movement inall
four compass directions.
• Add properties to the Room class for storing east, south, and west exits. These
properties will need accessor methods.
• Add code to the gameLoop method to understand the commands east, south, andwest 
(and the abbreviations e, s and w) and to handle them in a similar way to north.
• Modify initRooms to create more rooms using the new exits to test yourcode.
• The rooms created should be constructed in a reasonable and logical relationship that 
makes the game playable and sensible.
Task 2 (15% of the mark)
A key part of most text adventure games is the ability to move objects around. Objects 
can be found in rooms and can be picked up and put down by the player. Add this 
capability to the game engine.
• Create a GameObject super class. It should contain at least a weight, and a
keyword (for the player to use when typing commands).
• Modify the Room class so that each Room includes a list of GameObjects in theroom.
• Create a derived class Weapon of GameOjbect class, the weight of each object of 
Weapon should be limited in a range of 5-10. It should contain a property named 
harm which should be limited in a range of 10-30. 
• Create a derived class Food of GameObject class, the weight of each object of Food
should be limited in a range of 1-5. It should contain a property named energy which 
should be limited in a range of 1-10. 
• Modify initRooms to create some GameObjects ((including food and weapon objects)
and put them in the rooms. Use this to test your program. (No marks are assigned 
specifically for this task, but without it, the ones following cannot be demonstrated.)
Task 3 (15% of the mark)
A key part of most text adventure games is the ability to fight with the NPC enemy. The 
NPC can be found in rooms and the player can fight with them. Add this capability to 
the game engine.
• Create a pure virtual EnemyObject class. It should contain at least a health, and a 
keyword (for the player to use when typing commands). It should contain a virtual 
method damage().
• Modify the Room class so that each Room includes a list of EnemyObject in theroom.
• Create a derived class Boss of EnemyObject class, the health of each object of 
Boss should be 100.
• Create a derived class Clowns of EnemyObject class, the health of each object of 
Clowns should be 30.
• Modify initRooms to create some EnemyObjects ((including boss and clowns 
objects) and put them in the rooms. Use this to test your program. (No marks are 
assigned specifically for this task, but without it, the ones following cannot be
demonstrated.)
• You need to consider different reasonable damage value for each different 
enemy objects’ damage() method.
Task 4 (5% of the mark)
• Modify the State class to include a representation of the player’s physical strength,
called strength, which is initiated as 100, and when strength goes to 0, the program 
shall be terminated. 
• Modify the Room::describe() method to print out the keywords of all theobjects in the 
room, formatted as nicely as possible.
Task 5 (30% of the mark)
• Modify the gameLoop method to pay attention to the second word of the commandthe
player enters, if there is one. The following commands can be used with the second 
word to search through a) objects in the current room,and b) objects in the inventory, for 
an object with a keyword matching the second word of the command the player typed. 
• Implement the player command get which, when typed with an object keyword, willmove 
that object from the current room list into the inventory. It should display appropriate 
errors if the object is not in the room, or the object is already in the inventory, or the 
object does not exist. 
• Implement the player command drop which, when typed with an object keyword, will 
move that object from the inventory into the current room list. It should display
appropriate errors if the object is not in the inventory or doesnot exist, etc. (5%)
• Implement the player command inventory which will print out the keywords ofall the
objects in the inventory. <代 写CHC5028、C/C++
代做程序编程语言br>• Implement the player command eat which, when typed with a food object
keyword, will print out the player’s strength after adding the energy of the food 
object to the player’s strength, which should not exceed 100.
• Implement the player’s command fight which, when typed with an enemy 
object keyword if the enemy object exists in the room, will print out the enemy’s 
health that subtracts from the sum of harm of weapons carried by the player.
• The harm is mutual, the player’s strength should reduce the damage of the 
enemy existing in the room and be printed out. You need to make the damage()
in the Boss and Clowns class can be applied when the fight command is 
working. 
• You need to make the printout of each command execution demonstrate the 
explicit status of all objects in the room.
Task 6 (25% of the mark)
Since most players will not want to play an entire game at one sitting, most games include
save and load (or restore) commands. Implement these commands. Theyshould ask the
user for a filename and then write or read the current game state, to orfrom that file.
Note that the layout and descriptions of rooms, and the list and descriptions of objects,are not 
part of the game state because they do not change during the game. These should not be
included in the save file and saving them will lose marks.
A simple file open, load, and save does not guarantee full marks and may notguarantee
“a good mark”.
To this end, some important points to consider:
• The “game state” may also include the locations of objects the player has dropped in
rooms. Would it be a good idea to restructure how object locations are stored?
• The “game state” may also include the status of the player and enemy objects. Would it 
be a good idea to restructure these objects to the original situation?
• The State object stores the current room, and objects, using pointers. Pointers cannot
safely be written to disk since addresses may be different when the programis reloaded.
How can you enable this data to be safely saved and reloaded?
• It is worth ensuring to some degree that the user cannot readily cheat, or spoil the game, 
by reading or changing a save file. While it is not necessary to implement actual 
authentication or encryption, at the same time, the file does not have to be just a text 
dump. This makes it harder to parse when loaded. So, for example, saving the required 
indexes into a static array of strings may be a better way than saving the strings 
themselves.
Marking scheme for this task:
• 5% for basic correct structure of I/O.
• 10% for the file format designed for storing the saved game.
• 10% for the code that performs the save and the load.
Assessment Rules( Very important )
Code will be assessed by a demonstration and viva in week 12. You will be asked to
demonstrate your code and to explain how it works. There is no hard division of 
marksbetween code and viva. The marks given are mainly based on your performance 
in answering the assessor's questions and the accuracy and correctness of the 
corresponding answers.
If you cannot explain your code sufficiently well to satisfy the assessor that it is your 
own work, they have the right to award 0 marks for that exercise, regardlessof the 
quality of the code.
The fact that your code works does not guarantee full marks. All code is expected to 
also be readable, maintainable, and efficient. You are not required to exactly follow the steps
in the exercises above. Alternative designs are also acceptable if they can bejustified in the 
viva. However, designs which substantially reduce efficiency or other desirable properties 
without corresponding benefits will lose marks.
• The deadline for submission of the coursework is Week 12.
• In Week 12 you will also be required to demonstrate the final version ofyour
work, and verbal feedback will be given.
In addition to final submission and viva in Week 12, there will be two counselling in
the week 10 and week 11 tutorial periods. You also can make appointments with the 
tutor during the whole semester to 
Notice on presentation and submission
You do not need to give a presentation nor submit a report for either section of the
coursework. This coursework’s focus is on the quality of your final code and on your ability to
understand it, not your software engineering process (which is not expected tobe standard 
when you are learning the language).
Standard rules on plagiarism apply to this coursework.
The Code should be your own work and must not be copied from the internet or any 
other source. If you have difficulty with the coursework, you should approach your practical 
tutor in the first instance. Posting questions about the coursework on Stack Overflow, Quora, 
or similar sites may be treated as an incitement to plagiarism. Posting parts of your answer to 
the coursework on the publicly available internet where other students may access it will be 
treated asan incitement to plagiarism. Soliciting or obtaining answers to the coursework in
exchange for money and any other consideration will be treated as serious academic
misconduct. Asking for coursework answers from any party outside of the University is itself
attempted plagiarism and you should not do it; if that third party commits any of theoffenses in 
this section on your behalf, you may be held responsible, even if you were not directly aware 
they would do so (because you should not have asked them in the first place).
Assignment Data
Contact person Leon Liang, leon@zy.cdut.edu.cn
Learning outcomes See below.
Formative deadline Week 10 (2/12/2024-6/12/2024):
Coursework Class Test
Formative feedback Week 10 (2/12/2024-6/12/2024):
Counselling
Week 11 (9/12/2023-13/12/2023):
 Counselling
Summative deadline Week 12 (16/12/2024-20/12/2024) 
Coursework project demonstration and viva
Summative feedback Week 12 (18/12/2023-22/12/2023)
Spoken interactive(viva)
Final marks after assessment committees
Assignment Weighting Coursework class test 20% of the module
Coursework project demonstration and viva 30% of the 
module
Learning Outcomes
• Understand the fundamental concepts of C and C++ programming for object
manipulation, data structuring and input/output control.
• Refine a problem specification into a collection of C++ classes.
• Create a software artefact specified in terms of C++ objects and their interrelations.
• Research the techniques for safe and efficient programming in C and C++.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
