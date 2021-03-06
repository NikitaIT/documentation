# RAP3

This section introduces the tool you will use during the course: [RAP3](http://ampersand.tarski.nl/RAP3). This tool stores Ampersand-scripts in which you can specify, analyze and build information systems. It runs in the cloud, so all you need is a browser and [click here](http://ampersand.tarski.nl/RAP3) to start using it.

## Identifying yourself

RAP3 keeps your work together under a student number. So you have to log in in the system under your own student number. The first time you have to register and leave your e-mail.

## Disclaimer

RAP3 is under development. You can expect to find teething problems \(kinderziektes\) in the software. Please notify us by [making an issue in our issue registration system](https://github.com/AmpersandTarski/RAP/issues). This way you can help improve Ampersand's tooling, for which the Ampersand-team is very grateful.

## Making your first Ampersand script

When you click on the blue plus-sign on the right side in the menu bar in your screen, you get to make a new script. It opens an editor screen in which you can type your very first Ampersand script. ![](/assets/your first Ampersand script.png)

## Assignment

* Copy and paste the script "[Hawaii.adl](https://github.com/AmpersandTarski/ampersand-models/blob/master/Hawaii/Hawaii.adl)" \(from GitHub\) and run it. If you have a tutor, she will undoubtedly show you which sequence of clicks will make it work. 
  * Scroll down to the bottom of the screen and try it out on your own by clicking the buttons. During the remainder of this course you will compile and run your own scripts in this way, so it pays to familiarize yourself with it.
* Let's add the possibility to register teachers in this system. The service code needs to be at the end, other information can be added anywhere above that:

  * Define a new concept with the keyword CONCEPT: `CONCEPT Teacher`
  * Define the relation between Subject and Teacher with the keyword RELATION:  
    `RELATION provided_by[Subject*Teacher]`  
    `MEANING "the course for a subject is provided by a teacher"`

  * You can define an initial set of teachers and relate them to a subject following the examples already available in the script. But you can also add the data later using the prototype. Adding initial data in the script is a lot of work. There is another method, using spreadsheets. This is the next topic in this tutorial.

  * Add a service for the teachers in the tab for Subjects, below the line for "students that passed":  
    `, "teachers" : provided_by  CRUD`

  * Save, compile and see the result.

  * Note that we have not defined any rules about teachers, so anything you fill in, is OK for this system.

* Try to understand what you see in the script by making other changes to the program. Compile and run your changes, to learn by doing. Try for instance to register a teacher for each course. Demonstrate your changes to your peers and discuss the results.

## What have you learned?

After finishing your assignment, you have learned:

* how to use RAP3 to write, save and compile code.
* the first basic keywords of Ampersand script and their effect on the prototype.



