pyrobot
=======


What is it?
-----------  

PyRobot is a lightweight, pure Python Windows automation library loosely modeled after Java's Robot Class. It can be used to drive applications that don't provide an API or any way of hooking into them programatically. Good for when you can't (or don't want to) install the great, but a bit hefty, pywin32 libraries.   

Installation
------------

PyRobot is a single Python file. So, you can either download it directly from this github page, or clone the repo: 

git clone https://github.com/chriskiehl/pyrobot  

Usage
------

Similar to Java, everything is controlled via a single class.

 ```python

# Import the robot class from the pyrobot module
from pyrobot import Robot

# create an instance of the class
robot = Robot()

# Launch a program
robot.start_program('program_name') 

# Do cool stuff
location_of_field = (340, 400)
expected_color = (255,255,255)

pixel = robot.get_pixel(location_of_field)
if pixel == (expected_color): 
	robot.set_mouse_pos(location_of_field)
	robot.click_mouse(button='left')
	robot.add_to_clipboard('Hello world! How are ya!')
	robot.paste()


# etc.. 

# If you need to take screengrabs, and have PIL Installed, 
# PyRobot extends the default behavior of PIL by 
# allowing the entire virtual screen to be targeted (rather 
# than just the primary). 

# returns a list of screen rects for all attached devices
monitors_coords = robot.get_display_monitors() 

# Takes a screenshot of the desktop and returns a PIL Image object
im = robot.take_screenshot(monitors_coords[-1]) # Coordinates of last monitor

# You can also do arbitrarily sized boxes
left = 100
top = 430
width = 1000
hright = 750

im = robot.take_screenshot((left, top, width, height))

# Save the PIL Image to disk
im.save('my_awesome_screenshot.png', 'png')

# and so on
 ```  

Doc  
---  


| Method                                | Summary                    |
| --------------------------------------|-----------------------------
| set_mouse_pos(x, y): | Moves mouse pointer to given screen coordinates. |
| get_mouse_pos() 		| Returns tuple of current mouse coordinates |
| get_pixel(x, y) 	| Returns the pixel color `tuple(R,G,B)` of the given screen coordinate|
| mouse_down(button) | Presses one mouse button.<br> button can be `'Left'`, `'right'`, or `'middle'` |
| mouse_up(button)	 | Releases mouse button.<br> button can be `'Left'`, `'right'`, or `'middle'` |
| click(button) 	| Simulates a full mouse click. One down event, one up event.<br> button can be `'Left'`, `'right'`, or `'middle'` |
| scroll_mouse_wheel(direction, clicks)  | Scrolls the mouse wheel either `'up'` or `'down'` X number of 'clicks'. |
| add_to_clipboard(string)  | Copy text into clip board for later pasting. |
| clear_clipboard() | Clear everything out of the clipboard |
| take_screenshot(bounds=None) | NOTE: REQUIRES PYTHON IMAGE LIBRARY<br>Takes a screenshot of the entire desktop and returns it as a PIL `Image` object.<br><br>Use with `get_display_monitors` to target a specific screen, or pass in a tuple consisting of (`left`, `top`, `width`, `height`).|
| key_press(key) | Presses a given key.<br>Input: `string`|
| key_release(key) | Releases a given key.<br>Input: `string` |
| type_string(input_string, delay=.005) | Convenience function for typing out strings.<br>delay = time between keystrokes |
| type_backwards(input_string, delay=.05) | Types right to left. Because why not! |
| start_program(full_path) | Launches a windows application. <br>Input type: `string`|  
| paste() | Pastes the contents of the clipboard |
| sleep(duration) | Pauses the robot for `duration` number of seconds. |
| get_display_monitors() | Enumerates and returns a list of virtual screen coordinates for the attached display devices<br>output = [<br>&nbsp;&nbsp;&nbsp;&nbsp;(left, top, right, bottom), # Monitor 1<br>&nbsp;&nbsp;&nbsp;&nbsp;(left, top, right, bottom)  # Monitor 2<br>&nbsp;&nbsp;&nbsp;&nbsp;# etc... <br>] |




Special take_snapshot Note
-----------------------  

Being that Python has no built in Image library (that I know of), it seemed of little use to include a snapshot method which simply saves the picture to disk. For 90% of program automation, I find that querying pixels works fairly well (e.g. `robot.get_pixel`). However, if you need to do more advanced display searching, or want to do template matching, you'll need an external library. So there is a method in there to contruct a PIL Image object. It just, of course, requires that PIL be installed. Other than that, dependency free! :-)  

TODO
----  

* Multi-monitor support for screen_grab functions
* Allow specific window/program targeting so that relative coordinates can be used while scripting. 


Contact
-------

Feature request? Bug? Hate it?  
Drop me a line at audionautic@gmail.com, or on Twitter @thechriskiehl 









 