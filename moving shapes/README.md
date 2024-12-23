# Assignment 1

## Program Specification

In this assignment you will be writing a C++/SFML program which will read descriptions of shapes from a configuration file, and then drawing those shapes to the screen. Each shape will have a name, position, speed, color, as well as properties unique to each shape type. For example, a Rectangle will have width and height, and a cicle will have a Radius. For this assignmentm the position of a shape refers to its SFML default of the upper-left corner of the shape.

You are also required to make these shapes "bounce" off the sides of the window which contains them. This means that if the shapes's left side hits the left side of the window, its X speed reverses. If the top of the shape hits the top of the window, its Y speed reverses. Similarly , if it hits the right side or bottom of the window. You can assume that all shapes will always be configured to start entirelyu within the window, and you don't have to worry about what happens if they start outside the window. Each shape's name should be drawn on the exact center of the shape in the given font size and color specified in the file. 

*Note: this may be the trickiest part of the assignment, you will not lose many marks if it's not he exact center*

You are also required to implement an ImGui user interface which is able to:
- List all of the shapes and select any one of them to edit their properties
- Toggle whether or not the selected shape will be drawn
- Change the scale of the shape (0 to 4)
- Change the x and y velocity of the shape (0 to 8)
- Change the color of the shape
- Change the name of the shape

**UI note:**

Do not worry if rapidly changing the scale parameter causes the shape to go outside the bounds of the rectangle. Assume that it will only be changed to remain within the rectangle. The newly scaled shape should properly bounce with its new size.

A sample configuration file is given to you in config.txt, however marking will be done with an unseen configuration file in order to test more completely. Be sure to add and remove your own shapes to this file to test if they all work correctly.

Each line fo teh configuration file specifies one of the config settings of the assignment program, with the first string in each line being the type of setting that the rest of the line specified. Lines in the config file can be one of the following types, and lines can appear in any order in the file.

Window W H
- This line declares that the SFML Window must be constructed with width W and height H, each of which will be integers

Font F S R G B 
- This lines defines the font which is to be used to draw test for this program. The format of the line is as follows:

|Meanin    |Label   | Data type                           |
|----------|--------|-------------------------------------|
|Font File |  F     | std::string (it will have no spaces)|
|Font Size |  S     | int                                 |
|RGB Color | RGB    | int, int, int                       |

Rectangle N X Y SX SY R G B W H
- Defines a Rectangle shape with:

|Meaning         |Label   | Data type   |
|----------------|--------|-------------|
|Shape Name      |  Name  | std::string |
|Initial Position| X,Y    | float,float |
|Initial Speed   | SX,XY  | float,float |
|RGB Color       | R,G,B  | int,int,int |
|Size            | W,H    | float,float |

Circle N X Y SX SY R G B R
- Defines a Circle shape with:

|Meaning         |Label   | Data type   |
|----------------|--------|-------------|
|Shape Name      |  Name  | std::string |
|Initial Position| X,Y    | float,float |
|Initial Speed   | SX,XY  | float,float |
|RGB Color       | R,G,B  | int,int,int |
|Radius          | R      | float       |


## Assignment Hints

- In order to store an arbitary number of shapes from the configuration file, you must store them in a container - std::vector is recommended.
- Consider creating a custom class or struct whihc stores all of the properties of a shape that are not stored within the sf::Shape class itself example: velocity, name, etc
- A shape will 'touch' the side of the winodw if its bounding box makes contact with it. Each shape's bounding rectangle can be obtained via:
    
    + shape.getLocalBounds(); // .top, .left, .width, .height
    + gives the LOCAL position of the (top, left) of the rectangle 
    + LOCAL pos means it is relative to shape.getPosition(), not the window
    + as well as the (width, height) size of the rectangle
    + shape.getGlobalBounds() will take into account any scale, translation, etc that has been applied to the shape. May be useful for the ui scaling

- Similarly, a sf::Text elements's bounding rectangle can also be retrieved via text.getLocalBounds(), which  you will need to use to center the text properly within a shape.
- Please use C++ file reading (std::ifstream makes this easy) rather than C-style FILE reading. You will lose makes for using older C functions!
