# Tutorial 1: Basic Shapes and Module Fundamentals (Notebook Edition) 🎨

**Time**: ~20 minutes  
**Goal**: Learning Python Manim module Basics  
**Platform**: Online Jupyter Notebook Environment

## Part 1: Getting Started with Your First Manim Cell 🚀

We are going to use Jupyter notebooks to run Manim code interactively in the cloud. This allows you to write and execute code in small chunks (cells), see immediate results, and document your learning process all in one place.

### Complete the Tutorial By the Manim Community!

We will be using the online Manim tutorial to learn the basics of Manim modules and creating simple shapes. Please go to the following URL in your web browser and follow the tutorial. Please be sure to run your code to see what it produces but note, that since this is an online environment, rendering times may vary.

**Tutorial Website**: [https://www.manim.community/](https://www.manim.community/). Click on "Try Manim Online" to access the Jupyter notebook environment. Note: When you are working with a notebook, use "rename" to give the notebook the name, `Activity_08_Animation_Magic`. Then, from the "File" menu item, select "Save Notebook" to save your work. You will be submitting this notebook later with your activity work. To get your notebook, click "Download" from the "File" menu.

### Part 2: Your Own Code

You are now ready to start your own Manim Community Edition Jupyter notebook! Create a new notebook, or use the following URL [https://www.manim.community/](https://www.manim.community/) to open a blank Jupyter notebook. Find and click the "New" button in the top right corner and then select "Python 3" to begin.

IMPORTANT: Give this new notebook a name: Click on the title "Untitled" at the top and rename it to `Activity_08_Animation_Magic.ipynb`. You will be submitting this notebook later with your activity work.

#### First Thing's First: Import Manim Modules

Your first step is to ensure that the Jupyter notebook has access to the Manim modules. In the Jupyter notebook, create a new code cell and enter the following code to install the libraries, and to check the version of Manim (Community Edition) that is installed on the cloud notebook.

Note: The online Manim server times-out after a short time and so you will likely have to return to this below code to run it again to "fire-up" the Manim environment. Place this code at the top of your notebook and run it to ensure Manim is ready to go.

```python
import manim as mn
from manim import *

config.media_width = "75%"
config.verbosity = "WARNING"

print(mn.__version__)
```

Run the cell by clicking the "Run" button (the right-pointing triangle icon) in the toolbar above the cell. You should see the version number of Manim printed below the cell.

#### Step 1: Create Your First Animation Cell

**Remember: the `%%manim` magic command must be the very first line!**

```python
%%manim -qm BasicShapes

from manim import *

class BasicShapes(Scene):
    """
    Your first Manim scene! Creates basic geometric shapes.
    Notice how we import everything from the manim module.
    """
    
    def construct(self):
        # SECTION 1: CREATING BASIC SHAPES
        
        # Circle from manim.mobject.geometry
        circle = Circle(radius=1.5)
        circle.set_color(BLUE)  # Color from manim.utils.color
        circle.set_fill(BLUE, opacity=0.3)  # Semi-transparent fill
        
        # Square from the same geometry module  
        square = Square(side_length=2)
        square.set_color(RED)
        square.set_fill(RED, opacity=0.3)
        
        # Position them side by side
        circle.shift(LEFT * 3)   # Move left
        square.shift(RIGHT * 3)  # Move right
        
        # SECTION 2: ADDING TO THE SCENE
        # The Scene class provides self.add() method
        self.add(circle)
        self.add(square)
        
        # Alternative: Add multiple objects at once
        # self.add(circle, square)
```

**Run this cell (Shift + Enter) and watch the magic happen!**

#### Step 2: Understanding What Just Happened

Create a **markdown cell** (change cell type to "Markdown") and add your observations: What did you see? What modules were used? How did the code structure help organize the scene?

```markdown
**Questions to consider**

**What do the following pieces of code do?**

1. `from manim import *` 
2. `Circle()` and `Square()` 
3. `BLUE` and `RED` ]
4. `Scene` 
5. And how does a module have anything to do with these pieces of code?


#### Step 3: Experiment!

Now it's your turn! Modify the code to add some animation from Part 1 of this tutorial to play with this code. Try adding animations, new shapes, colors or arrangements to your work.

**Questions to consider**

1. What can you change in the code, and how will changes affect the output?
2. What new shapes or colors can you try?
3. What animations can you add and will they change the scene?

**Ready for Tutorial 2?** You'll learn about dynamic animations and even more advanced module integration!

---

**Next**: `tutorial_02_notebook.md` - Animation Magic and Advanced Module Usage
