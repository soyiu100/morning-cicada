# morning-cicada
![image](https://drive.google.com/uc?export=view&id=1cdWVLehoUuRAevVMhDhpSUMbow1FdYvJ)
## Overview 
A continuation of the unnamed fusion visual novel project, now built using C++/OpenGL. Previously a PoC was built using Lua/LOVE2D, seen [here](https://github.com/soyiu100/evening-cicada-engine).  
The purpose of this repository is to post monthly or bi-monthly updates on the progress of this project. If you are interested in a particular feature or in the software in general (either as an employer or a potential collaborator to the project), please feel free to reach out!    
**No code will be published to this repository in the interest of property.** Non-critical software versions and screenshots will be published as proof of process, but all rights are reserved; see LICENSE for details.   

---
![image](https://drive.google.com/uc?export=view&id=1cdWVLehoUuRAevVMhDhpSUMbow1FdYvJ)
## Progress Report
### January 2024
There are a lot of small and fast updates here and there, as I'm getting the grip of how I want my project to be structured.  
I went back to the tutorial to learn about instancing, and then modify my internal graphics controllers to account for it.  
It's already being used for laying out an specialized Q&A data type that I can't quite reveal yet.  

Here are some rectangles and lines that use instancing to draw over the mess of my tutorial page.  
![instancing](https://github.com/soyiu100/morning-cicada/assets/31663498/7f7463e9-d10f-47ba-aa28-6551b1b10bd5)

----

Other than this, it's been mostly backend changes and some visual things, like 
- a basic Q&A hub for questions,
- text coloring,
- text size,
- text speed,
- text interruption,
- and miscellaneous visual bug fixes.

I also demo a re-done boolean evaluator that, I must admit, was very scuffed in my original Lua implementation.  
See video below.    

https://github.com/soyiu100/morning-cicada/assets/31663498/d4369dc0-29ed-4927-81ab-98ab905f4b84

At this point, I'd have to say my project is about 66% of the way to where it was in Lua :D  
Also, speaking of instancing, those buttons for the Q&A hub are not instanced. They need to move and react dynamically, and I'll need to modify my shaders to take in uniform variables instead of binding it.  

----

Finally - and I promise it's related to this same project - I've been working on getting real-time eye detection to work in C++. It uses vanilla OpenCV2 with the default Haars cascades, which surprisingly is not all that bad. I think I'm fine with just this for now.   

In the coming months, I plan to work on optimizing scanning, and methods of detecting eye movement. I anticipate it's going to wildly inaccurate, considering there is nothing precise, like pupil detection specifically or gaze direction, but it's better than nothing.    

I did scour the internet for other advanced CV solutions before deciding on this.  
dlib refuses to work with the base MSVC and needs to use CMake. That would mean needing to redo my entire compile setup for my other dependencies like Boost, OpenGL, and so on...so that was a hard pass for me.  
Tensorflow always seems to be incompatible with Windows somehow, even back when I was messing around with it in college. It was no different this around trying to link Tensorflow Lite to C++. I did find pre-compiled libraries for it on Github, but using it ended up with my app crashing :)  
So, with the little documentation available on it, I decided to pass on it as well. I do suspect that that it's something similar to its incompability to the base MSVC compiler.  
![har har har](https://github.com/soyiu100/morning-cicada/assets/31663498/573a3042-093a-4375-8ce5-73d41d21bb47)

### December 2023
Hello! Here's a quick update before the year ends. So far at a high level summary, it's been a lot of bringing over code from my Lua project, refactoring it, and then making it all work. Also, a lot of tweaking/usuability updates to the graphics methods I have set up from the tutorial days.  
Even then, there are a lot of unique updates, so perhaps a video summarizing all of the changes would be more appropriate:

https://github.com/soyiu100/morning-cicada/assets/31663498/1f2ffd0f-f6f3-4800-b80d-5d4e901b7c31

In the video shown, you can see debug command at the bottom of the screen, and on enter, the responses back from it. I test out the lua file from last month that I've refactored into a command for sanity check purposes.  
Around the 30 second mark, I use the `/set` command, which can switch between modes. `/set 3` sets to the view to the end executable from last month.  
`/set 2` switches to a view where I was messing around with font size, color, transparency. I also went back to the tutorial for OpenGL for framebuffers, which was essential for my new and improved implementation for the text window on `/set 1`, the main mode.  
To segway, there are a few improvements to text rendering. The old method used to render every line, then throw it away if it went off-screen. Now it uses framebuffers to render only the current line, and saves previous lines to a framebuffer.  
In addition, in hangul rendering, there used to be a little visual bug where the jongsong did not render individually. For example, in '닭', 'ㄹ' and 'ㄱ' typed out as one 'jamo',  when actually it's two 'jamos'. In the video, if you slow it down, it should render one by one.  
In the ending part of the video, like I promised, I used the Lua bridge to "hot-load" lines from a Lua script. The `/dodo ps` debug command line reads from the Lua file, pushes it to the story module internally, and I am able read through it and advance. `/dodo rl` does the same thing, except clear the current story context first, then reload with the potentially new lines the Lua file has.  
The "Unknown ID " spam cascading up and above the lines is due to the name label feature from my Lua project not being completely implemented visually or internally.  

----

Not shown in the video is an underlying encode/decode system. In my Lua PoC, I borrowed a json encoder/decoder. While json is nice and common, it's much too bulky and it doesn't work very well with a strictly typed language like C++. I did think of: 
- msgpack,
- cereal,
- implementing my own.

After some days of experimenting with all of those, I opted to go for cereal to encode/decode save files. There aren't any particular advantages to it in terms of performance or space, but it's a lot more documented than msgpack is.  

All that being said, I think the next immediate steps are just continuing to implement all the other features (e.g. name label feature, choices, etc.) and flesh out the schema for lines. What made my story progression unique is currently not all here yet, and is just a generic version of what it was in the Lua project.  

To anyone seeing this, hope you have a happy new year, and all best in 2024 if you're already in it!

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
