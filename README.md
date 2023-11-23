# morning-cicada
![image](https://drive.google.com/uc?export=view&id=1cdWVLehoUuRAevVMhDhpSUMbow1FdYvJ)
## Overview 
A continuation of the unnamed fusion visual novel project, now built using C++/OpenGL. Previously a PoC was built using Lua/LOVE2D, seen [here](https://github.com/soyiu100/evening-cicada-engine).  
The purpose of this repository is to post monthly or bi-monthly updates on the progress of this project. If you are interested in a particular feature or in the software in general (either as an employer or a potential collaborator to the project), please feel free to reach out!    
**No code will be published to this repository in the interest of property.** Non-critical software versions and screenshots will be published as proof of process, but all rights are reserved; see LICENSE for details.   

---
![image](https://drive.google.com/uc?export=view&id=1cdWVLehoUuRAevVMhDhpSUMbow1FdYvJ)
## Progress Report
### November 2023
After cleaning and posting the archive for the evening-cicada project, I started following a tutorial for OpenGL/C++. Way back when, I followed a tutorial using GLUT/GLEW, but things did not go smoothly that time (leading to my segway into Lua). Thankfully, this tutorial using GLFW/GLAD (and MSVC abstracting out all the linkage underneath) worked out very smoothly! Very happy about that :D     

The result is a relatively standard tutorial app covering the basics: 
- shaders,
- textures, and
- the coordinate system.

I'm also aware that there's a whole advanced section of the OpenGL that I haven't covered, such as the camera concept, lighting, and modelling, but that isn't my priority right now. I do plan on visiting again, just not right now. :)  

Once I got a grasp on the basics of the tutorial, I started branching out into other stuff, like embedding resources in the executable, setting up a I/O (read-only currently), fonting (using FreeType).  

This week, I worked on cleaning up code and integrating Lua. Although the nature of LOVE2D made it good for fast development, there was a flaw on my part for not making it more flexible. Despite the story being the main function of the whole app, storyboarding was practically unintelligible to outsiders and mostly hard-coded into it. In addition, it was very cumbersome to test, limited to only the static files that needed to be modified in the app every time to test a change.  
In the new OpenGL app, the goal is to make Lua a bridge to gap those flaws, and at the very least, make it easier to test.  

Next steps from here are to have an on-screen console like I did in my LOVE2D app, and "hot-loading" features between the app and the script. Although I don't think I'll be able to debug *EVERYTHING* in the app, it'll definitely make things easier.  

For this month, I want to the feature the [end executable](https://drive.google.com/uc?export=view&id=1sAW-dk4grgnsJaoJC3mDmAiY5IiCYkh5) resulting from the work over the past month. To recap, it features:
- the parts of the tutorial I've covered,
- a bit of test text at the bottom, 
- the console outputs reading output from a file located at `src/resources/evil.txt` and
- the console outputs for testing the integration between a Lua script and the app.

MD5 Checksum: `d0f7641d60b2b1ecd0b3bb649bd9d356`  
