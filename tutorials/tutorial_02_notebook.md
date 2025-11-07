# Tutorial 2: Animation Magic and Advanced Module Usage (Notebook Edition) 🎬

**Time**: ~20 minutes  
**Goal**: Create dynamic animations and explore advanced module integration  
**Platform**: Online Jupyter Notebook Environment

The online Manim server times-out after a short time and so you will likely have to return to this below code to run it again to "fire-up" the Manim environment. Place this code at the top of your notebook and run it to ensure Manim is ready to go.

```python
import manim as mn
from manim import *

config.media_width = "75%"
config.verbosity = "WARNING"

print(mn.__version__)
```

## Part 1: Your First Dynamic Animation 🎭

Below are several pieces of code that demonstrate different animation techniques and module integrations in Manim. Follow along by creating new code cells in your Jupyter notebook and running the provided code snippets. Take note of how the modules work together to create complex animations. Later, you will trying your own creative animation using this code (or at least editing completed code to make something amazing happen!)

### The Text That Comes Alive

Create a new code cell in your notebook:

```python
%%manim -qm TextAnimation

from manim import *
import numpy as np  # External module integration!

class TextAnimation(Scene):
    """
    Tutorial 2, Part 1: Text animations with dynamic effects
    Demonstrates: Write, FadeIn, Transform animations with timing
    """
    
    def construct(self):
        # SECTION 1: ANIMATED TEXT CREATION
        
        # Create text objects
        title = Text("Welcome to Animation!", font_size=48)
        title.set_color(BLUE)
        
        subtitle = Text("Powered by Python Modules", font_size=32)
        subtitle.set_color(GREEN)
        subtitle.shift(DOWN)
        
        # SECTION 2: ANIMATION CLASSES IN ACTION
        # These classes come from manim.animation modules
        
        # Write text with a typing effect (from manim.animation.creation)
        self.play(Write(title), run_time=2)
        self.wait(0.5)
        
        # Fade in the subtitle (from manim.animation.fading)
        self.play(FadeIn(subtitle), run_time=1.5)
        self.wait(1)
        
        # Transform the title to something new (from manim.animation.transform)
        new_title = Text("Modules Make It Possible!", font_size=48)
        new_title.set_color(PURPLE)
        
        self.play(Transform(title, new_title), run_time=2)
        self.wait(1)
        
        # Fade everything out
        self.play(FadeOut(title), FadeOut(subtitle))
```

### Your Turn!

- Try changing the text content, colors, or font sizes.
- Try changing the title to something different that reflects your own interests!

**Animation Module Analysis**

**Key Differences from Tutorial 1:**
- `self.play()` instead of `self.add()` - creates movement over time
- `run_time` parameter controls animation speed
- `self.wait()` adds pauses between animations

**Animation Classes Used:**
- `Write()`: From manim.animation.creation - typing effect
- `FadeIn()`: From manim.animation.fading - gradual appearance  
- `Transform()`: From manim.animation.transform - morphs one object into another
- `FadeOut()`: From manim.animation.fading - gradual disappearance

**Module Cooperation:**
- Text objects from manim.mobject.text
- Animation classes from manim.animation.*
- Colors from manim.utils.color
- All coordinated by the Scene framework


## Part 2: Shape Transformations and Movement 🔄

### Geometric Animation Magic

```python
%%manim -qm ShapeAnimation

from manim import *

class ShapeAnimation(Scene):
    """
    Tutorial 2, Part 2: Geometric shape animations and transformations
    Demonstrates: Create, movement with .animate, VGroup, Rotate
    """
    
    def construct(self):
        # SECTION 3: CREATING AND ANIMATING SHAPES
        
        # Create shapes
        circle = Circle(radius=1)
        circle.set_color(RED)
        circle.set_fill(RED, opacity=0.3)
        
        square = Square(side_length=2)
        square.set_color(BLUE)  
        square.set_fill(BLUE, opacity=0.3)
        
        # Position them off-screen initially
        circle.shift(LEFT * 4)
        square.shift(RIGHT * 4)
        
        # Scene title
        title = Text("Shape Transformation Magic", font_size=36)
        title.shift(UP * 3)
        
        # SECTION 4: COMPLEX ANIMATION SEQUENCES
        
        # Start with title
        self.play(Write(title))
        
        # Create shapes with drawing effect
        self.play(Create(circle), Create(square))
        self.wait(0.5)
        
        # Move shapes to center using the .animate property
        self.play(
            circle.animate.shift(RIGHT * 4),  # Move circle right
            square.animate.shift(LEFT * 4),   # Move square left
            run_time=2
        )
        
        # Transform circle into square shape (while keeping circle object)
        self.play(Transform(circle, square.copy().set_color(RED)), run_time=2)
        self.wait(1)
        
        # Create a fun rotation effect using VGroup
        rotating_group = VGroup(circle, square)
        self.play(Rotate(rotating_group, angle=2*PI), run_time=3)
        
        # Fade out
        self.play(FadeOut(rotating_group), FadeOut(title))
```

### Your Turn!

- Try changing the shapes, colors, or adding new animations like scaling or changing opacity!
- Experiment with different arrangements and movements!

## Part 3: Mathematical Integration with NumPy 📊

### Plotting Mathematical Functions

```python
%%manim -qm MathPlotAnimation

from manim import *
import numpy as np

class MathPlotAnimation(Scene):
    """
    Tutorial 2, Part 3: Mathematical plotting with NumPy integration
    Demonstrates: Axes, plot functions, ValueTracker, updaters
    """
    
    def construct(self):
        # SECTION 5: MATHEMATICAL MODULES INTEGRATION
        
        # Create coordinate axes (from manim.mobject.coordinate_systems)
        axes = Axes(
            x_range=[-4, 4, 1],
            y_range=[-3, 3, 1], 
            axis_config={"color": WHITE}
        )
        
        # Create axis labels
        x_label = axes.get_x_axis_label("x")
        y_label = axes.get_y_axis_label("y")
        
        # SECTION 6: USING NUMPY MODULE WITH MANIM
        
        # Define a mathematical function using numpy
        def func(x):
            return np.sin(x) * np.exp(-x/3)
        
        # Create the function graph
        graph = axes.plot(func, color=YELLOW, x_range=[-4, 4])
        
        # Create equation text using MathTex
        equation = MathTex(r"f(x) = \sin(x) \cdot e^{-x/3}", font_size=36)
        equation.set_color(YELLOW)
        equation.shift(UP * 3)
        
        # SECTION 7: ADVANCED ANIMATION COORDINATION
        
        # Build the scene step by step
        self.play(Write(equation))
        self.wait(0.5)
        
        # Draw axes
        self.play(Create(axes), Write(x_label), Write(y_label))
        self.wait(0.5)
        
        # Animate the function drawing itself
        self.play(Create(graph), run_time=3)
        self.wait(1)
        
        # Add a moving dot that traces the curve
        dot = Dot(color=RED)
        dot.move_to(axes.c2p(-4, func(-4)))  # Convert coordinates to point
        
        # Create a value tracker for animation
        x_tracker = ValueTracker(-4)
        
        # Make dot follow the curve using updaters
        dot.add_updater(
            lambda m: m.move_to(
                axes.c2p(x_tracker.get_value(), func(x_tracker.get_value()))
            )
        )
        
        # Animate the dot moving along the curve
        self.add(dot)
        self.play(x_tracker.animate.set_value(4), run_time=4)
        
        # Clean up
        dot.clear_updaters()
        self.wait(1)
        
        # Final fade out
        self.play(
            FadeOut(VGroup(axes, x_label, y_label, graph, dot, equation))
        )
```

### Your Turn!

- Try changing the mathematical function being plotted!
- Try adjusting the axes ranges or adding more labels! 
- Experiment with different colors and styles for the graph.

### Analyze the Mathematical Integration

**Mathematical Module Integration Analysis**

**NumPy + Manim Cooperation:**

1. **NumPy provides**: `sin()`, `exp()`, mathematical constants
2. **Manim provides**: `Axes`, `plot()`, coordinate conversion
3. **Result**: Professional mathematical visualization

**Advanced Concepts Introduced:**

- `ValueTracker`: Animates numerical values over time
- `updaters`: Functions that run every frame to update objects
- `c2p()`: Coordinate conversion (mathematical → screen pixels)
- `VGroup`: Groups multiple objects for batch operations

**Why This Matters:**

- Shows how specialized modules work together
- Each module focuses on what it does best
- Complex visualizations become possible through module combinations
- Same pattern used in professional data science and research

## Part 4: Creative Animation Challenge 🌟

Now that you have seen several pieces of code, it is your turn to create something unique! Try combining different animation types, shapes, text, and mathematical elements to create your own animated scene. Remember *save* and then *download* your Jupyter notebook when you are done so that you can go back to your work later, if you want! You will also need the notebook for your submission.

### Your Animated Masterpiece

```python
%%manim -qm MyAnimatedCreation

from manim import *
import numpy as np

class MyAnimatedCreation(Scene):
    """
    Your creative challenge! Combine everything you've learned.
    
    Try incorporating:
    - Multiple animation types (Create, Transform, FadeIn/Out)
    - Text and mathematical elements  
    - NumPy for mathematical patterns
    - Coordinate movement and transformations
    """
    
    def construct(self):
        # YOUR CREATIVE CODE HERE!
        
        # Suggestions to try:
        # 1. Animated text introduction
        # 2. Shapes that move in mathematical patterns  
        # 3. Color changes over time
        # 4. Multiple objects moving in coordination
        # 5. Mathematical function visualization
        
        # Example starter - expand this!
        title = Text("My Animated Creation", font_size=42)
        title.set_color(GOLD)
        
        self.play(Write(title))
        self.play(title.animate.shift(UP * 3))
        
        # Add your creative animations below:
        
        
        
        self.wait(2)
```

---

**Excellent work!** You have gained fundamental skills that will serve you throughout your programming career. The ability to understand, use, and combine modules is what separates beginner programmers from professional developers.

**Next**: Complete your reflection questions and prepare for submission!
